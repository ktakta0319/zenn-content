---
title: "SlackにRSSフィードを追加してセキュリティ情報を通知する方法"
emoji: "📢"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Slack", "RSS"]
published: true
---

## 1. はじめに
現代の企業活動においてITは不可欠な存在となっており、セキュリティ情報を迅速に把握し、必要な対応を講じる必要があります。その一方で、情報セキュリティ部門を持っていない企業は日々の業務に集中し、セキュリティ情報へのアンテナは低くなりがちだと思います。

この記事では、SlackにRSSフィードを追加して、セキュリティ情報を自動で通知する方法を紹介します。導入は非常に簡単です。

:::message
**RSSフィード**とは、ウェブサイトの最新記事のタイトルや概要、リンク先などの情報を構造化してまとめたファイル（XML形式）のことです。ブログやニュースサイトが更新されると、このファイルが自動で更新されます。

今回の目的である「**SlackにRSSフィードを追加する**」というのは、セキュリティ機関（IPAなど）が更新するこのファイルをSlackに定期的に読み込ませるということです。これにより、手動でサイトを見に行かなくても、新しい情報がSlackチャンネルに自動で通知されるようになります。
:::

## 2. 導入方法
0. Slackに通知用のチャネルを追加する（必要があれば）
既存のチャネルを使わない場合、セキュリティ情報通知用のチャネルを新しく作成します。今回は「**security-alert-notification**」というチャネルを作成しました。

1. SlackにRSSアプリを追加する
[Slackマーケットプレイス](https://slack.com/marketplace)から「**RSS**」を検索し、Slackワークスペースに追加
![](/images/20251209-slack-rss-security-notification/pic1.png)

2. RSSフィードURLを取得する
今回は次の3つのサイトのRSSフィードURLを取得します。それぞれのサイト画面の赤枠の部分のリンクです。
    - IPA セキュリティ情報
        - RSSフィードURL： https://www.ipa.go.jp/security/alert-rss.rdf
        - サイトURL： https://www.ipa.go.jp/security/security-alert/
        ![](/images/20251209-slack-rss-security-notification/pic2.png)
    - JPCERT/CC 発表情報
        - RSSフィードURL： https://www.jpcert.or.jp/rss/jpcert.rdf
        - サイトURL： https://www.jpcert.or.jp/rss/
        ![](/images/20251209-slack-rss-security-notification/pic3.png)
    - JVN 脆弱性対策情報
        - RSSフィードURL： https://jvn.jp/rss/jvn.rdf
        - サイトURL： https://jvn.jp/
        ![](/images/20251209-slack-rss-security-notification/pic4.png)

3. SlackにRSSフィードを設定する
SlackワークスペースにRSSフィードを1つずつ追加します。次のとおり入力して「**Subscribe to this feed**」をクリックします。
    - Feed URL： RSSフィードURL
    - Post to Channel： **security-alert-notification**
    ![](/images/20251209-slack-rss-security-notification/pic5.png)

最終的にこちらの画面のとおりになれば完了です。
![](/images/20251209-slack-rss-security-notification/pic6.png)

## 3. 試した結果
各サイト（RSSフィード）が更新されると、**security-alert-notification**に通知されます。
![](/images/20251209-slack-rss-security-notification/pic7.png)

このチャネルで`/feed list`を送信すると、通知設定されているRSSフィードを確認できます。
![](/images/20251209-slack-rss-security-notification/pic8.png)

通知設定を解除したいRSSフィードがある場合は、`/feed remove ID`（JVN 脆弱性対策情報を削除する場合は`ID`を`10070375266484`に置換）を送信するか、RSSアプリの画面で削除ボタンをクリックします。
![](/images/20251209-slack-rss-security-notification/pic9.png)
![](/images/20251209-slack-rss-security-notification/pic10.png)

## 4. おわりに
この記事では、SlackにRSSフィードを追加してセキュリティ情報を通知する方法を紹介しました。セキュリティ情報に限らず、RSSフィードを提供している他のサイトでも応用できます。
今後も業務効率化を実現する方法を発信し、同じ課題を持つ方のお役に立てれば幸いです。