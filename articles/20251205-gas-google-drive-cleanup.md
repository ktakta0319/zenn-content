---
title: "Google Drive内のファイルを定期的に自動削除する方法"
emoji: "⚙️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ['GAS']
published: true
---
## 1. はじめに
生成AIの業務への導入によって、スライドのたたき台や定期的なレポーティング資料を作成するケースが増えたのではないかと思います。ファイルの定期削除を導入することによって、面倒な手動削除をせずに、フォルダの容量の圧迫や古いファイルによるセキュリティ上のリスクを避けることができます。

この記事では、Google Apps Script (GAS)を使って、Google Driveの特定のフォルダにあるファイル（ドキュメント/スプレッドシート/スライド）を定期的に自動削除する方法を紹介します。
## 2. 仕組みの全体像
GASのトリガー機能を使って、スクリプトを定期実行して対象のファイルを自動削除（ゴミ箱へ移動）します。
1. 削除対象とするファイルを事前に設定
    - どのフォルダ内のファイルを削除対象とするか（1つのフォルダのみ）
    - どのファイルを削除対象外とするか（複数のファイルを設定可能）
    - 最終更新から何日経過したファイルを削除対象とするか
    - どの種別のファイルを削除対象とするか
        - Googleスライド
        - スプレッドシート
        - Googleドキュメント
2. フォルダ内のファイルを1つずつチェック
3. 条件に当てはまるファイルをゴミ箱へ移動
4. 実行ログを残す
## 3. 導入方法
1. Apps Scriptプロジェクトを作成し、下記リポジトリの`google-drive-cleanup.gs`を貼り付ける

https://github.com/ktakta0319/work-automation/tree/main/gas/google-drive-cleanup

2. スクリプトを編集し、削除対象とするファイルを設定する

https://github.com/ktakta0319/work-automation/blob/main/gas/google-drive-cleanup/google-drive-cleanup.gs#L9-L17

3. トリガー機能を設定する
![](/images/20251205-gas-google-drive-cleanup/pic1.png)
## 4. 試した結果
1. 下記のようにファイルを用意する
![](/images/20251205-gas-google-drive-cleanup/pic2.png)
2. 削除対象とするファイルを以下のように設定する（「削除対象スプレッドシート」と「削除対象スライド」のみが削除される想定）
```javascript
  // ===== 設定値 =====
  const TARGET_FOLDER_ID = '1omJ9Ff-ZFrqTk-6FbG1iei1qAOPZ9KUj'; // 削除対象のフォルダID
  const EXCLUDED_FILE_IDS = ['1ThIvMQiuioOk497qvi6Amreti4q5sJqdF3VKqYovmes', '1lxf6c485l5Prjez831IEsDkltKaV5ILIuQ63so_eVW0']; // 削除対象外のファイルID
  const RETENTION_DAYS = 30; // この日数より前に作成されたファイルを削除対象とする

  // 削除対象とするファイル種別（true にしたものだけを削除）
  const DELETE_SLIDES = true;   // Google スライド
  const DELETE_SHEETS = true;   // スプレッドシート
  const DELETE_DOCS   = false;  // Google ドキュメント

  // ===== 削除ロジック =====
  // 削除対象のMIMEタイプの配列を作成

  // ......

  // const cutoff = new Date(now.getTime() - RETENTION_DAYS * 24 * 60 * 60 * 1000);
  const cutoff = new Date(now.getTime() - 60 * 1000); // テスト用に作成から1分経過したファイルを削除対象に
```
3. トリガーが起動して以下のように想定通りのファイルが削除されたことが確認できる
![](/images/20251205-gas-google-drive-cleanup/pic3.png)
4. スクリプトの実行ログで削除されたファイルが確認できる
![](/images/20251205-gas-google-drive-cleanup/pic4.png)
## 5. おわりに
この記事ではGASを使って、Google Driveの特定のフォルダにあるファイルを定期的に自動削除する方法を紹介しました。
今後も業務効率化を実現する方法を発信し、同じ課題を持つ方のお役に立てれば幸いです。
## 6. 参考
https://github.com/ktakta0319/work-automation/tree/main/gas/google-drive-cleanup