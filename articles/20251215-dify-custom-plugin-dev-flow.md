---
title: "Difyのカスタムプラグインを開発する流れ"
emoji: "🛠"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Dify", "Python"]
published: true
---
## 1. はじめに
普段ちょこちょことDifyを使っているのですが、ふと自分でもプラグインを作ってみたいなと思いました。しかし、調べてみても自分の環境に合った開発方法がまとめられているサイトを見つけられませんでした。

この記事では、WSL2環境（Ubuntu）にpyenvを使って仮想環境を用意し、カスタムプラグインを開発する流れを紹介します。あくまで流れを紹介するだけなので、プラグインの内容に踏み込むことはしません。

## 2. カスタムプラグインとは
Difyには、追加の機能を簡単に導入できるように、[マーケットプレイス](https://marketplace.dify.ai/)にさまざまなプラグインが公開されています。プラグインをインストールすることでワークフローやチャットフローで活用できます。

![](/images/20251215-dify-custom-plugin-dev-flow/pic1.png)

プラグインは利用するだけでなく、自作することが可能です。これが「**カスタムプラグイン**」です。カスタムプラグインは、非公開にして自分のワークフローだけで使うことも、マーケットプレイスに公開して他のユーザに使ってもらうこともできます。

## 3. プラグイン開発の流れ
前提として、以下の環境は準備できている想定で説明します。
- Ubuntu： インストール済み
- pyenv： Ubuntu上で利用可能
- Git： Ubuntu上で利用可能
- GitHub： Gitコマンドを使ってGitHubリポジトリの操作可能

### 開発環境のセットアップ
1. プラグイン開発用のディレクトリを作成
今回は`dify-plugin`を開発用のディレクトリとします。このディレクトリ内で複数のプラグインを開発する想定です。
```bash
mkdir dify-plugin
cd dify-plugin
```

2. Python 3.12系のインストール
`dify-plugin`ディレクトリでPython 3.12系の最新バージョンをインストールし、仮想環境を有効化します。ドキュメントには前提条件として「**Pythonバージョン ≥ 3.12**」と記載されていますが、私が試した限り、3.13系・3.14系では後ほど紹介する `python -m main` を実行するとエラーになりました（2025/12/14時点）。
```bash
pyenv install --list | grep 3.12 # pyenvでインストール可能なPython 3.12系のバージョンを一覧表示
pyenv install 3.12.12 # 3.12.12（この時点の最新版）をインストール
pyenv local 3.12.12 # dify-pluginディレクトリで使うPythonバージョンを3.12.12に設定
python -m venv .venv # dify-pluginディレクトリに仮想環境「.venv」を作成
source .venv/bin/activate # 仮想環境を有効化
```

3. Dify CLIのインストール
プラグインのひな型プロジェクトを自動で作れるように公式のスキャフォールディングツール（`dify`コマンド）をインストールします。
```bash
wget https://github.com/langgenius/dify-plugin-daemon/releases/download/0.5.1/dify-plugin-linux-amd64 # dify-plugin-daemonのLinux用バイナリをGitHubからダウンロード
chmod +x dify-plugin-linux-amd64 # ダウンロードしたファイルに実行権限を付与
mv dify-plugin-linux-amd64 dify # ファイル名を短く「dify」に変更（コマンドとして使いやすくするため）
sudo mv dify /usr/local/bin/ # システムのPATHにある/usr/local/binに移動させ、どこからでも実行できるようにする
dify version # バージョンが表示されれば成功（この時点ではv0.5.1）
```

4. プラグインプロジェクトの初期化
プロジェクトの初期化コマンドを入力し、プロジェクト名を`hello_world`、プラグインタイプを`tool`とします。今回はシンプルなプラグインにするため、デフォルト設定から変更しません。
```bash
dify plugin init # 実行後に「hello_world」というディレクトリが作成される
cd hello_world
```
![](/images/20251215-dify-custom-plugin-dev-flow/pic2.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic3.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic4.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic5.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic6.png)

### プラグインの開発
1. プラグインの編集
今回は単純に出力結果に`result2`を追加します。
```python:./tools/hello_world.py
class HelloWorldTool(Tool):
    def _invoke(self, tool_parameters: dict[str, Any]) -> Generator[ToolInvokeMessage]:
        yield self.create_json_message({
            "result": "Hello, world!",
            "result2": "Hello, world! 2",
        })
```

2. デバッグ環境のセットアップ
`.env.example`をコピーして`.env`を作成し、Difyのプラグイン設定画面から取得したURLを`REMOTE_INSTALL_URL`に、Keyを`REMOTE_INSTALL_KEY`に上書きします。
```bash
cp .env.example .env
```
![](/images/20251215-dify-custom-plugin-dev-flow/pic7.png)
*Difyのプラグイン画面*

3. 依存関係のインストール
```bash
pip install -r requirements.txt
```

4. デバッグの実行
Difyにプラグインをインストールする前にデバッグモードで実行して確認できます。下記のコマンド実行中は、プラグイン画面に`hello_world`プラグインが表示され、ワークフローやチャットフローでも使用できます。
```bash
python -m main
```
![](/images/20251215-dify-custom-plugin-dev-flow/pic8.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic9.png)
*Difyのプラグイン画面*
![](/images/20251215-dify-custom-plugin-dev-flow/pic10.png)
*Difyのワークフロー*

### プラグインのインストール
プラグインをDifyにインストールするためには、下記のコマンドによってパッケージ化する（`.difypkg`ファイルを作成する）必要があります。
```bash
dify plugin package ../hello_world
```

`.difypkg`ファイル（カスタムプラグイン）をインストールするには2つの方法があります。
![](/images/20251215-dify-custom-plugin-dev-flow/pic11.png)
*Difyのプラグイン画面*

1. GitHubリポジトリを指定する
パブリックリポジトリのリリースに添付された`.difypkg`ファイルを読み取ってインストールします。プラグインをパブリックリポジトリで管理しても問題ない場合に適しています。
![](/images/20251215-dify-custom-plugin-dev-flow/pic12.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic13.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic14.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic15.png)

2. ローカルファイルをアップロードする
ローカル環境からアップロードするため、プラグインを外部に公開せずに利用したい場合に適しています。
![](/images/20251215-dify-custom-plugin-dev-flow/pic16.png)
![](/images/20251215-dify-custom-plugin-dev-flow/pic17.png)

カスタムプラグインのインストール後は、マーケットプレイスから取得したプラグインと同様に、ワークフローやチャットフローで使えるようになります。

## 4. おわりに
この記事では、カスタムプラグインのための開発環境の構築からDifyにインストールするまでの流れを紹介しました。1つのリポジトリで複数のプラグインを管理する設計にしていますが、他のユーザに公開する場合には「1リポジトリ＝1プラグイン」にした方が分かりやすいかもしれません。

便利なプラグインを思いついた際には実際に作ってみたいなと思います。

## 5. 参考
https://docs.dify.ai/ja/use-dify/workspace/plugins
https://docs.dify.ai/ja/develop-plugin/getting-started
https://github.com/ktakta0319/dify-plugin