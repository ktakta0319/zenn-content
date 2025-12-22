---
title: "DifyでLangfuseプラグインを使ってプロンプトを管理する方法"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Dify", "Langfuse"]
published: true
---
## 1. はじめに
Difyのワークフロー/チャットフローを開発するうえで、プロンプト・エンジニアリングは重要です。しかし、プロンプトを適切に管理できていない場合、「少し前のバージョンのプロンプトを使いたいけど消してしまった...」なんて事態が起こりかねません。

この記事では、Difyのワークフロー開発においてプロンプトのべた書きを避け、Langfuseを使ってプロンプトを管理する方法を紹介します。Langfuseを使うことによって、**プロンプトのバージョン管理**が可能になり、効率的なワークフロー開発に繋がるのではないかと思います。また、**ワークフローは変更せず、プロンプトだけを更新**できるようになります。

## 2. Langfuseプラグインの導入方法
0. Langfuseアカウントを作成
まだ[Langfuse](https://langfuse.com/)のアカウントがない場合は作成します。今回はクラウド版を使用します。

1. Langfuse APIキーを取得
以下の手順に従って、APIキーを作成します。APIキーは1度しか表示されないため控えておきます。
![](/images/20251222-dify-langfuse-plugin/pic1.png)
![](/images/20251222-dify-langfuse-plugin/pic2.png)
![](/images/20251222-dify-langfuse-plugin/pic3.png)

2. DifyにLangfuseプラグインをインストール
Difyのプラグイン画面に移動し、GitHub ( https://github.com/gao-ai-com/dify-plugin-langfuse )からインストールします。プラグインのバージョンは最新の **v0.0.3** を選択します（2025/12/22時点）。
![](/images/20251222-dify-langfuse-plugin/pic4.png)
![](/images/20251222-dify-langfuse-plugin/pic5.png)
![](/images/20251222-dify-langfuse-plugin/pic6.png)
![](/images/20251222-dify-langfuse-plugin/pic7.png)
![](/images/20251222-dify-langfuse-plugin/pic8.png)

3. LangfuseプラグインのAPIキー認証設定
ワークフローでLangfuseプラグインを選択できるようになりますが、はじめにAPIキー認証設定が必要になります。控えておいたLangfuse秘密鍵（`LANGFUSE_SECRET_KEY`）、Langfuse公開鍵（`LANGFUSE_PUBLIC_KEY`）、Langfuse Host（`LANGFUSE_BASE_URL`）を入力します。
![](/images/20251222-dify-langfuse-plugin/pic9.png)
![](/images/20251222-dify-langfuse-plugin/pic10.png)

## 3. Langfuseにプロンプトを用意
会社名と日付を入力すると、その日の株価を出力するワークフローを作成する前提でプロンプトを用意します。はじめて作成されるプロンプトには自動で**Production**ラベルが付与されます。
- Name： `テスト/株価検索プロンプト`
    :::message
    スラッシュ（`/`）で区切るとフォルダを作成できます。今回は意図的にフォルダを作成してテストします。
    :::
- Prompt： `{{target_date}}の{{company_name}}の株価を教えて`
    :::message
    プロンプト内の`{{変数名}}`は、Difyワークフロー内でユーザーが入力した会社名と日付に置換できます。利用可能な変数は青枠部分に表示されます。
    :::
![](/images/20251222-dify-langfuse-plugin/pic11.png)
![](/images/20251222-dify-langfuse-plugin/pic12.png)

実際に使うプロンプトとは別に、同じ階層に新しいバージョンのプロンプトを作成します。新しいバージョンであっても**Production**ラベルが付与されていないと使われないことを確認するために意図的に用意しました。
![](/images/20251222-dify-langfuse-plugin/pic13.png)
:::message
新しいバージョンであっても**Production**ラベルに変更するためには明示的に設定する必要があります。自動的に本番環境に適用されないような安全設計になっています。
![](/images/20251222-dify-langfuse-plugin/pic14.png)
:::

## 4. Difyワークフローの概要
ワークフローの全体像はこちらです。
![](/images/20251222-dify-langfuse-plugin/pic15.png)

### ユーザー入力
- 入力フィールド①
    - フィールドタイプ： 短文
    - 変数名： `target_date`
    - ラベル名： `target_date`
    - 最大長： 48
    - デフォルト値： `現在`
    - 必須
- 入力フィールド②
    - フィールドタイプ： 短文
    - 変数名： `company_name`
    - ラベル名： `company_name`
    - 最大長： 48
    - デフォルト値： 空欄
    - 必須

### プロンプト取得（Langfuseプラグイン）
- プロンプト名： `テスト/株価検索プロンプト`
- バージョン： 空欄
    :::message
    バージョン欄を空欄にしておくと、**Production**ラベルのプロンプトが取得されます。
    :::
- ラベル： 空欄
    :::message
    Langfuseでは任意のラベル名を設定できます。バージョンの代わりに、そのラベル名を指定してプロンプトを取得することも可能です。
    :::
- 変数：
    ```
    {"target_date" : "ユーザー入力/target_date", "company_name": "ユーザー入力/company_name"}
    ```
    :::message
    JSON文字列の値（value）もダブルクオーテーション（`"`）で括る必要があります。そうしないとエラーになってしまいます。
    ![](/images/20251222-dify-langfuse-plugin/pic16.png)
    :::

### Tavily Search
- Query： `プロンプト取得/text`
- Country： `Japan`
- Include Answer： `True`
- その他の設定： デフォルトのまま

### Answer取得（テンプレート）
- 入力変数
    - 変数名： `json`
    - 変数： `Tavily Search/json`
- コード： `{{ json[0].answer }}`

### 出力
- 出力変数
    - 変数名： `output`
    - 変数： `Answer取得/output`

## 5. 試した結果
ワークフローを実行すると、2025年12月19日のソフトバンクの終値が取得されました。
![](/images/20251222-dify-langfuse-plugin/pic17.png)

ログを見ると、下記のプロンプトが使われていることも確認できました。
```
2025年12月19日のソフトバンクの株価を教えて
```

## 6. おわりに
Difyのワークフロー開発において、Langfuseを使ってプロンプトを管理する方法を紹介しました。特に複数人で1つのワークフローを編集する場合、プロンプトを誤って削除してしまうことを避け、結果的に効率的な開発に繋がりそうだなと思いました。

## 7. 参考
https://langfuse.com/
https://github.com/gao-ai-com/dify-plugin-langfuse
https://www.gao-ai.com/post/dify-plugin-langfuse