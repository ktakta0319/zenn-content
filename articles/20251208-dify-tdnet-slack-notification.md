---
title: "Difyを使ってTDnetの適時開示書類をSlackに自動通知する方法"
emoji: "📢"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Dify", "Slack"]
published: true
---
## 1. はじめに
クライアントワークにおいて、クライアントのことを知っておくことは重要です。クライアントが上場企業の場合、即座に重要な情報を知る手段のひとつが適時開示書類だと思います。

この記事では、Difyワークフローを使って、1時間おきにTDnet（適時開示情報伝達システム）のページを取得し、指定した証券コードの会社が直近1時間のうちに公開した適時開示書類を要約してSlackに通知する仕組みを紹介します。
## 2. 事前準備
Difyワークフローを作成する事前準備として次の2点を完了しておきます。

1. DifyにSlack Webhookツール（プラグイン）をインストール・設定する

https://marketplace.dify.ai/plugins/langgenius/slack

2. DifyにLLMプロバイダを追加・設定する
今回は無料でAPIを使用できる**GroqCloud**を選択しました。

https://marketplace.dify.ai/plugins/langgenius/groq

## 3. Difyワークフローの作成方法
Difyワークフローの全体像はこちらです。
![](/images/20251208-dify-tdnet-slack-notification/pic1.png)

このワークフローのDSLファイルは下記のリポジトリから入手できます。DSLファイルをインポートするとすぐにワークフローを使い始められます。

https://github.com/ktakta0319/work-automation/tree/main/dify/dify-tdnet-slack-notification

以降では、各ブロックの種類や設定方法を説明します。
なお、環境変数に `slack_incoming_webhook_url` という変数名で Slack Incoming Webhook URL を設定します。

### スケジュールトリガー
スケジュールをCron式で設定します。ほとんどのケースで平日に公開されることを踏まえて、以下のように記載します。
```cron
5 8-19 * * 1-5
```
| フィールド | 数値または範囲 | 意味 |
| ---- | ---- | ---- |
| 1番目 | 5 | 毎時5分に実行 |
| 2番目 | 8-19 | 8時から19時の間に実行 |
| 3番目 | * | 毎日実行 |
| 4番目 | * | 毎月実行 |
| 5番目 | 1-5 | 月曜日(1)から金曜日(5)に実行 |
:::message
トリガー機能は **v1.10.0** 以降でのみ利用できます
:::

### TDnet URL生成（コード実行）
- コード
```python
from datetime import datetime

def main():
    # 実行日を yyyymmdd 形式に変換
    today_str = datetime.now().strftime("%Y%m%d")

    # URL生成
    url = f"https://www.release.tdnet.info/inbs/I_list_001_{today_str}.html"

    return {
        "result": url
        # "result": "https://www.release.tdnet.info/inbs/I_list_001_20251205.html" # テスト用
    }
```
- 出力変数
    - 変数名： `result`
    - データ型： `String`

### TDnetページ取得（HTMLリクエスト）
- API
    - メソッド： `GET`
    - URL: **TDnet URL生成**ノードで出力された`result`

### HTMLパース（コード実行）
- 入力変数
    - 変数名： `html`
    - 変数： **TDnetページ取得**ノードで出力された`body`
- コード
```python
import re
from urllib.parse import urljoin
from typing import List, Dict
from datetime import datetime, timedelta


def main(html: str) -> dict:
    """
    直前1時間の投稿のみ取得
    （例: 19:05 に実行 → 18:01〜19:00 のみ）
    """

    base_url = "https://www.release.tdnet.info/inbs/"
    results: List[Dict[str, str]] = []

    # 監視したい証券コード
    target_codes = [
        "22690", # 【テスト用】明治HD
        "63900", # 【テスト用】加藤製造所
        "245A0", # 【テスト用】INGS
    ]

    now = datetime.now()

    # 本番用（「直前1時間」を動的に判定）
    end_time = now.replace(minute=0, second=0, microsecond=0)

    # テスト用（手動で設定）
    # end_time = now.replace(hour=17, minute=0, second=0, microsecond=0)

    # end_timeの1時間前
    start_time = end_time - timedelta(hours=1)

    # <tr> ごとに抽出
    tr_pattern = re.compile(r"<tr>\s*(.*?)\s*</tr>", re.DOTALL)

    for tr_match in tr_pattern.finditer(html):
        tr_html = tr_match.group(1)

        # 証券コード抽出
        code_match = re.search(
            r'class="[^"]*kjCode[^"]*"[^>]*>(.*?)</td>',
            tr_html
        )
        if not code_match:
            continue

        code = code_match.group(1).strip()

        # 対象コード以外はスキップ
        if code not in target_codes:
            continue

        # 時刻取得（例: "17:00"）
        time_match = re.search(
            r'class="[^"]*kjTime[^"]*"[^>]*>(.*?)</td>',
            tr_html
        )
        if not time_match:
            continue

        time_str = time_match.group(1).strip()

        try:
            # "HH:MM" → time オブジェクト
            t = datetime.strptime(time_str, "%H:%M").time()
            # 今日の日付 + 時刻（秒・マイクロ秒は 0）
            row_time = datetime.combine(now.date(), t)
        except ValueError:
            # パースできない時刻は無視
            continue

        # 直前1時間のみ（start_time は含まず、end_time は含む）
        if not (start_time < row_time <= end_time):
            continue

        # PDF とタイトル
        title_match = re.search(
            r'class="[^"]*kjTitle[^"]*"[^>]*>.*?<a[^>]*href="([^"]+)"[^>]*>(.*?)</a>',
            tr_html,
            re.DOTALL
        )
        if not title_match:
            continue

        pdf_path = title_match.group(1).strip()
        # 改行や余計なスペースをまとめる
        title = re.sub(r"\s+", " ", title_match.group(2)).strip()
        pdf_url = urljoin(base_url, pdf_path)

        # 会社名
        name_match = re.search(
            r'class="[^"]*kjName[^"]*"[^>]*>(.*?)</td>',
            tr_html
        )
        company = name_match.group(1).strip() if name_match else ""

        results.append(
            {
                "time": time_str,
                "code": code,
                "company": company,
                "title": title,
                "pdf_path": pdf_path,
                "pdf_url": pdf_url,
            }
        )

    return {"results": results}
```
- 出力変数
    - 変数名： `results`
    - データ型： `Array[Object]`

### イテレーション
- 入力： **HTMLパース**ノードで出力された`results`
- 出力： **Slack通知文面作成**ノードで出力された`result`

##### PDF URL抽出（テンプレート）
- 入力変数
    - 変数名： `item`
    - 変数： **イテレーション**の`item`
- コード： `{{ item.pdf_url }}`

##### PDF取得（HTMLリクエスト）
- API
    - メソッド： `GET`
    - URL: **PDF URL抽出**ノードで出力された`output`

##### テキスト抽出
- 入力変数： **PDF取得**ノードで出力された`files`

##### テキスト文字列化（テンプレート）
- 入力変数
    - 変数名： `text`
    - 変数： **テキスト抽出**ノードで出力された`text`
- コード： `{{ text[0] }}`
:::message
**テキスト抽出**ノードの出力結果は`Array[String]`である。LLMブロックのコンテキストには`String`として渡す必要があるため、この**テキスト文字列化**ノードを挟んで`String`に変換している。
:::

##### PDF要約（LLM）
- AIモデル： Llama-3.1-8b-instant
- コンテキスト
    - 変数： **テキスト文字列化**ノードで出力された`output`
    - SYSTEM：
        ```
        PDFの内容を300文字程度に要約してください。
        ```
    - USER：
        ```
        ## PDFの内容
        {{#context#}}
        ```

##### Slack通知文面作成
- 入力変数
    - 変数1
        - 変数名： `item`
        - 変数： **イテレーション**の`item`
    - 変数2
        - 変数名： `summary`
        - 変数： **PDF要約**ノードで出力された`text`
- コード
```python
def main(item, summary):

    company = item.get("company", "")
    code = item.get("code", "")
    url = item.get("pdf_url")
    title = item.get("title", "")

    # Slack通知文面
    text = f"*{company}（{code}）*\n*{title}*\n{url}\n\n{summary}"

    return {"result": text}
```

##### Incoming Webhook to send message
- 入力変数
    - content： **Slack通知文面作成**ノードで出力された`result`
- 設定
    - Slack Incoming Webhook url： 環境変数の`slack_incoming_webhook_url`

### 出力
- 出力変数
    - 変数名： output
    - 変数： **イテレーション**の`output`

## 4. 試した結果
ワークフローの作成が上手くいったことをすぐに確認するため、テスト用に次のとおり設定を変更します。

- スケジュールトリガーを**ユーザー入力**（元の開始ノード）に変更する
- **TDnet URL生成**ノードのコードをテスト用に変更する
    ```python
    return {
        # "result": url
        "result": "https://www.release.tdnet.info/inbs/I_list_001_20251205.html" # テスト用
    }
    ```
- **HTMLパース**ノードのコードをテスト用に変更する
    ```python
    # 本番用（「直前1時間」を動的に判定）
    # end_time = now.replace(minute=0, second=0, microsecond=0)

    # テスト用（手動で設定）
    end_time = now.replace(hour=17, minute=0, second=0, microsecond=0)
    ```
このテストでは、[こちら](https://www.release.tdnet.info/inbs/I_list_001_20251205.html)のTDnetページを取得して、**HTMLパース**ノードのコードで指定されている3社が16:01～17:00に公開した書類の要約をSlackに通知する、というのが正しい挙動となります。
```python
    # 監視したい証券コード
    target_codes = [
        "22690", # 【テスト用】明治HD
        "63900", # 【テスト用】加藤製造所
        "245A0", # 【テスト用】INGS
    ]
```



つまり、下記の画像のうち、赤枠の3件が通知され、青枠の1件は通知されないことが求められます。

![](/images/20251208-dify-tdnet-slack-notification/pic2.png)

変更後のワークフローを実行した結果、下記のように3件の適時開示書類の要約が通知されました。

![](/images/20251208-dify-tdnet-slack-notification/pic3.png)

![](/images/20251208-dify-tdnet-slack-notification/pic4.png)

## 5. おわりに
この記事では、Difyワークフローを使って、指定した証券コードの会社が直近1時間のうちに公開した適時開示書類の要約をSlackに通知する仕組みを紹介しました。
今後も業務効率化を実現する方法を発信し、同じ課題を持つ方のお役に立てれば幸いです。

## 6. 参考

https://docs.dify.ai/ja/

https://www.release.tdnet.info/inbs/I_main_00.html

