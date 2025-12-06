---
title: "SlackにGitHubリポジトリのリリースを通知する方法"
emoji: "📌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["GitHub", "Slack"]
published: true
---
## 1. はじめに
OSS（Open Source Software）をセルフホストしている方の中には、アップデートに気が付けずに便利な機能を利用しそびれていた経験をした方もいると思います。

この記事では、OSSがGitHubで公開されている想定で、新しいリリース（アップデート）があった場合にSlackに通知する方法を紹介します。これによって、アップデートがあった場合にすぐに気が付けるようになります。

## 2. 導入方法
公式のドキュメントはこちらです。
https://github.com/integrations/slack

以降では、かいつまんで導入方法を説明します。

1. SlackワークスペースにGitHubを導入する
**[slack.github.com](https://slack.github.com/)** にアクセスして流れに従えばOK
2. GitHubアカウントとSlackを連携する
GitHubアプリのチャネルで **`/github signin`** を送信すると以下のようなメッセージが返ってくるので「**Connect GitHub account**」をクリックして流れに従えばOK
![](/images/20251206-github-release-slack-notification/pic1.png)
3. リリース通知を受信したいチャネルで **`/github subscribe owner/repo releases`** を送信する
**`owner/repo`** の部分は、リリース通知を受信したい特定のGitHubリポジトリを設定

## 3. 試した結果
ノーコードでAIアプリ開発ができる [Dify](https://dify.ai/jp) のGitHubリポジトリを使います。
https://github.com/langgenius/dify

**`/github subscribe langgenius/dify releases`** を送信するだけでリリース通知を受信する設定ができます。新しいリリースがあると同じチャネルに通知がありました。
![](/images/20251206-github-release-slack-notification/pic2.png)

同じチャネルに複数のGitHubリポジトリを設定できます。**`/github subscribe owner/repo`** とすれば、 `releases` だけではなく、`issues`, `pulls`, `commits`, `deployments` でも通知を受信するようになります。
![](/images/20251206-github-release-slack-notification/pic3.png)

通知設定しているリポジトリと機能を確認する場合は、 **`/github subscribe list features`** を送信すればOKです。
![](/images/20251206-github-release-slack-notification/pic4.png)

特定のリポジトリの通知設定を解除する場合は、 **`/github unsubscribe owner/repo`** を送信すればOKです。
![](/images/20251206-github-release-slack-notification/pic5.png)

## 4. おわりに
この記事ではGitHubリポジトリのリリースをSlackに通知する方法を紹介しました。
今後も業務効率化を実現する方法を発信し、同じ課題を持つ方のお役に立てれば幸いです。

## 5. 参考
https://github.com/integrations/slack