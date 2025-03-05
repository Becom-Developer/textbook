# GUI アプリケーションの準備

2025-03-05 更新

インストールの流れはすべてダウンロードページからパッケージをダウンロードしてきて、`sudo apt install` コマンドでインストール、ファイルの拡張子が `.deb` のものを使うこと。

例: google chorme の場合

```bash
cd ~/ダウンロード
sudo apt install ./google-chrome-stable_current_amd64.deb
```

インストール完了後は、画面左下の「アプリケーションを表示する」からアイコンの存在確認ができるので、アイコンを右クリックして「お気に入りに追加」しておく

## web ブラウザ

google chorme

- 公式ページからインストール
  - <https://www.google.co.jp/intl/ja/chrome/>

起動して既存の web ブラウザに設定、必要なら自身のアカウントでログインしておく

## テキストエディタ

vscode

- 公式ページからインストール
  - <https://azure.microsoft.com/ja-jp/products/visual-studio-code/>

### 初期設定

#### プラグイン

日本語表示にするプラグインを導入

Japanese Language Pack for Visual Studio Code

- 手順
  - 上部のメニューから
  - View -> Extensions
  - 検索フォームからプラグイン名を入力すると表示されるのでインストールする
  - インストールが完了するとアプリの再起動を促すボタンが表示されるので再起動すると使える

#### ワークスペース

事前に必要なディレクトリやファイルを用意しておく

```bash
echo '# draft' > ~/tmp/draft.md
```

ワークスペースを用意

- フォルダを追加
  - ファイル -> フォルダをワークスペースに追加 -> `tmp`フォルダを選択
- ワークスペースの名前をつける
  - ファイル -> 名前をつけてワークスペースを保存 ->
  - 今回は ~/etc ディレクトリに my.code-workspace という名前で保存
- ワークスペースを終了
  - ファイル -> ワークスペースを閉じる
- 閉じたワークスペースを始める
  - ファイル -> ファイルでワークスペースを開く -> `my.code-workspace` を開く
- さらに設定ファイルのディレクトリをワークスペースに追加
  - ファイル -> フォルダをワークスペースに追加 -> `etc`フォルダを選択

次回から vscode を起動するときはコマンドラインで `code ~/etc/my.code-workspace` を実行するとワークスペースが立ち上がる

#### 設定ファイル

vscode の設定ファイルをつくる

- etc -> my.code-workspace をクリックして開く
- 下記のような設定値をくわえて保存する。

```json
{
  "folders": [
    {
      "path": "../tmp"
    },
    {
      "path": "."
    }
  ],
  "settings": {
    "editor.fontFamily": "Ubuntu Mono",
    "editor.fontSize": 16,
    "editor.minimap.enabled": false,
    "editor.renderWhitespace": "all",
    "files.trimTrailingWhitespace": true,
    "explorer.autoReveal": false,
    "editor.rulers": [78],
    "editor.quickSuggestions": {
      "comments": "on",
      "strings": "on",
      "other": "on"
    },
    "editor.copyWithSyntaxHighlighting": false
  }
}
```

## 開発支援

GitHub Desktop

- 公式ページからインストール
  - <https://github.com/shiftkey/desktop/releases>

## コミュニケーションツール

slack

- 公式ページからインストール
  - <https://slack.com/intl/ja-jp/downloads/linux>

## データ保存

Dropbox

- 公式ページからインストール
  - <https://www.dropbox.com/ja/install-linux>
