# NAME

vscode - テキストエディタ vscode について

## SYNOPSIS

```text
2020年時点で初心者向けにおすすめのテキストエディタといえば vs code という意見がおおい
mac, windows, linux とおもなプラットフォームで動作して無料で提供しているので
テキストエディタ選びで迷っている方にはおすすめの選択肢である。
記事の最後の SEEALSO に参考リンクをまとめておいたので、詳細な情報はそこから入手するのがよい
```

## INSTALL

インストールについて

```text
vscode 公式ページからインストールと手順を参考にする
```

インストール終了後、ターミナルから code コマンドがつかえることを確認

```console
$ which code
/usr/local/bin/code

(こちらで起動も出来る)
$ code

(.vscode というディレクトリの中に設定ファイルなどが保存される)
$ ls -al ~/
...
drwxr-xr-x    4 yk    staff      128  2 16 15:32 .vscode
...

(コマンドの使い方詳細はこちら)
$ code --help
Visual Studio Code 1.42.1
...
```

## VIEW

表示の仕方について

```text
vs code はインストール直後はメニューなどが英語表記になっている
日本語表示にしたほうが使い勝手はよいので変更しておく
```

- 日本語表示にするプラグインを導入
  - Japanese Language Pack for Visual Studio Code

手順

- 上部のメニューから
  - View -> Extensions
    - 検索フォームからプラグイン名を入力すると表示されるのでインストールする
    - インストールが完了するとアプリの再起動を促すボタンが表示されるので再起動すると使える

## WORKSPACE

ワークスペースをについて

```text
最近のテキストエディタはワークスペースという考え方がある
vs code もワークスペースを作成するところからはじめる
```

詳細は、公式ページワークスペースの設定を参照

具体例: github という名前のワークスペースを用意する場合

- フォルダを追加
  - ファイル -> フォルダをワークスペースに追加 -> 任意のフォルダを選択
- ワークスペースの名前をつける
  - ファイル -> 名前をつけてワークスペースを保存 ->
    - 今回は ~/etc ディレクトリに github.code-workspace という名前で保存
- ワークスペースを終了
  - ファイル -> ワークスペースを閉じる
- 閉じたワークスペースを始める
  - ファイル -> ワークスペースを始める

ワークスペースをしてして始める場合ターミナルを使うやり方もある

```console
(ワークスペースをしてして起動)
$ code ~/etc/github.code-workspace

(コマンドで textbook というフォルダをワークスペースに追加する場合)
$ code ~/github/textbook
```

## SETTING

設定について

```text
アプリケーションの実行に対しての設定ファイルの適用のしかたはいろいろ存在するが
vs code の場合はアプリ本来の設定に対して段階をおって設定できるようになっている
どこの層にどの設定をくわえるのかは好みの問題もあるが
わかりやすさを考えると workspace に対して設定をするのがわかりやすい
vs code 設定の考え方は下記の図を参考にするとイメージしやすい
```

概念図

```text
        +------+
        | view |
        +------+
      +----------+
      |  folder  |
      +----------+
    +--------------+
    |  workspace   |
    +--------------+
  +------------------+
  |       user       |
  +------------------+
+----------------------+
|   vscode (default)   |
+----------------------+
```

設定ファイルの場所

- 設定ファイルは共通して `settings.json` という名前
  - folder -> 任意の場所、フォルダの中に `.vscode` ディレクトリを作成
  - workspace -> 任意の場所 今回 (`~/etc/github.code-workspace` ファイルの中)
  - user -> mac の場合 `$HOME/Library/Application Support/Code/User/settings.json`
  - vscode (default) -> 触れない

今回は user と folder に対しての設定は何もせず workspace に対して設定を紹介

設定の仕方は 2 つある

1. code -> 基本設定 -> 設定 -> ワークスペース -> 各項目を編集
1. `~/etc/github.code-workspace` に直接記述

さきほどワークスペースをつくったので `~/etc/github.code-workspace` に下記のように直接記述するのが早い

`~/etc/github.code-workspace` (パスは各環境で読み替えてください)

```json
{
  "folders": [
    {
      "path": "/Users/yk/github"
    }
  ],
  "settings": {
    "editor.fontFamily": "Ricty Diminished",
    "editor.fontSize": 16
  }
}
```

`Ricty Diminished` については別途追加でフォントをインストールしないと使えない

---

```text
新しく設定を増やす場合の事例も書いておく
メモ書き用のマークダウンファイルのためのワークスペース設定をつくる場合
```

ワークスペースファイル自体を直接新しく作る

```console
touch ~/etc/memo.code-workspace
```

`~/etc/memo.code-workspace` (ミニマップを表示しないように追加の設定をくわえた)

```json
{
  "folders": [
    {
      "path": "/Users/yk/Dropbox/home/tmp/draft"
    }
  ],
  "settings": {
    "editor.fontFamily": "Ricty Diminished",
    "editor.fontSize": 16,
    "editor.minimap.enabled": false
  }
}
```

コマンドで直接ワークスペースファイルを起動させるやり方もある

```console
code ~/etc/memo.code-workspace
```

---

あとは必要に応じて設定ファイルごとにワークスペースを用意していく

設定ファイルの書き方の詳細は公式ページの「公式ページワークスペースの設定」を参照

## PLUGIN

機能拡張について

```text
vs code は機能拡張が充実しているので他のテキストエディタユーザーからの乗り換えに対しても
柔軟に対応できるプラグインがある
```

vscode の機能拡張については公式ページのマーケットプレイスから探す

どのプラグインを使うかは好みだがいくつかを紹介

- 操作性向上
  - Center Editor Window - カーソルを画面の中央に移動させる
  - Japanese Language Pack for Visual Studio Code - 日本語表示にする
  - line-jumper - 10 行ごとにカーソルが移動する
  - Markdown Preview Github Styling - マークダウンのプレビュー機能を github 風に表示する
  - Material Icon Theme - アイコンの表示の仕方を充実させる
  - Sublime Text Keymap and Settings Importer - サブライムテキストの使い勝手を再現
- コード整形
  - markdownlint - 一貫性のあるマークダウンの書き方を強要する
  - EditorConfig for VS Code - テキストエディタ共通の設定
  - ESLint - おもにjsのシンタックスエラーをチェック
  - Prettier - おもにjsのコード整形
- perl
  - Mojolicious - Mojolicious の書き方のシンタックス表示
  - perltidy - Perl コードを整形
- 動作確認
  - Debugger for Chrome - chrome を使った動作確認
  - Vetur - vue.js 動作確認

## SHORTCUTS

ショートカットキーについて

```text
vscode が初期設定としているショートカットキーとプラグインを入れることによって変わってしまうショートカットキーがある
よく使い動きは大抵ショートカットキーが用意されているので事前に調べておくとよい
```

設定はこちらから確認できる

- 例: たとえば「カーソルを行の始めに移動する」のショートカットキーの設定を調べる
  - Code -> 基本設定 -> キーボードショートカット
    - 検索フォームに `ctrl+a`
- 検索事例
  - 「コピーをする」の場合 -> 検索フォームに `cmd+c`
  - 「行を下にコピー」の場合 -> 検索フォームに `cmd+shift+d`
  - 「折りたたみ」の場合 -> 検索フォームに `cmd+alt+[`
  - 「展開」の場合 -> 検索フォームに `cmd+alt+]`

## FORMATTING

書式設定について

```text
vscode は最初からソースコードを整形するしくみが入っている
```

例: HTML の場合

- 詳細は公式ページの HTML in Visual Studio Code を参照
- html ファイルについては最初から整形する仕組みが入っている
  - `alt+shift+f` のショートカットキーで自動整形する
  - 設定を確認したい場合
    - code -> 基本設定 -> 設定 -> 拡張機能 -> HTML (もしくは設定の検索から `html.format` と入力する )

例: javascript (node.js) の場合

- 詳細は公式ページの JavaScript in Visual Studio Code を参照
- js ファイルについては最初からコード整形だけでなくたくさんの仕組みが入っている
  - `alt+shift+f` のショートカットキーで自動整形
  - 設定を確認したい場合
    - code -> 基本設定 -> 設定 -> 拡張機能 -> TypeScript (もしくは設定の検索から `javascript.format` と入力する )

## LINT

書式設定を共有したい場合

```text
2020年現在の node.js ベースの開発ではソースコードの書き方をチェックするために ESLint を使い
ソースコードの整形には prettier を使うというのが流れとなっている vscode での具体的な使い方をまとめておく
```

### ESLint

シンタックスエラーを確認

```text
vscode の ESLint プラグインは npm 配布ライブラリの ESLint に依存しているので
npm からの ESLint インストールが必須になる
もともとの ESLint の動きを確認して vscode 上での動きもみていく
```

1. 有効化するためのプロジェクトフォルダを作成
1. vs code プラグイン ESLint をインストールする
1. npm より ESLint ライブラリをインストールする
1. 使えるようになるための設定

プロジェクトフォルダを作成

```console
(ESLint ライブラリを試すためのプロジェクトフォルダを用意)
$ mkdir -p ~/tmp/node_sample/test_eslint && cd ~/tmp/node_sample/test_eslint

(サンプルコードのためのファイルを準備)
$ touch hello.js

(vscode のフォルダ用設定ファイルを設定)
$ mkdir -p ~/tmp/node_sample/test_eslint/.vscode && \
touch ~/tmp/node_sample/test_eslint/.vscode/settings.json
```

`hello.js` (推奨されない書き方をしておく)

```js
// セミコロンが２つ! 動くには動くが普通はやらない書き方
console.log("hello----!");;
```

- 作ったプロジェクトフォルダを今使っているワークスペースに追加する
  - ファイル -> フォルダーをワークスペースに追加 -> `test_eslint` 追加

vs code プラグイン ESLint

```console
(node.js は事前にインストールしておく)
(コマンドラインでプラグインがインストールできることがわかる)
$ code --help
...
Extensions Management
...
  --install-extension <extension-id | path-to-vsix> Installs or updates the extension. Use `--force` argument to avoid prompts.

(マーケットプレイスの URL itemName のところが extension-id になっている)
$ code --install-extension dbaeumer.vscode-eslint

(インストールできたことを確認)
$ code --list-extensions
...
dbaeumer.vscode-eslint
...

(プラグインをいれたときはアプリを再起動しなくてはいけないことに注意)
```

- vscode 側
  - 表示 -> 機能拡張 -> 有効から ESLint が有効になっていることを確認
  - `hello.js` をひらいてみてなにも警告がでていないことを確認

```console
(問題なく実行できる)
$ node hello.js
hello----!
```

npm より ESLint ライブラリ

```console
(今回は npm コマンドで作業場でのみ有効な設定をする)
(初期化、おためしなので、値をおまかせ)
$ npm init -y

(開発時のみ有効なインストール)
$ npm install eslint --save-dev

(初期設定をする、おためしのなので下記のような条件にしておく)
$ ./node_modules/.bin/eslint --init
? How would you like to use ESLint? To check syntax and find problems
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? None of these
? Does your project use TypeScript? No
? Where does your code run? Browser
? What format do you want your config file to be in? JavaScript
Successfully created .eslintrc.js file in /Users/yk/tmp/node_sample/test_eslint
$
(インストールがおわると .eslintrc.js という設定ファイルができる)

(問題なく実行できる)
$ node hello.js
hello----!

(eslint で書き方チェック、エラーがでる)
$ ./node_modules/.bin/eslint hello.js
...
✖ 1 problem (1 error, 0 warnings)
  1 error and 0 warnings potentially fixable with the `--fix` option.
...
```

`hello.js` をひらいてみてなにも警告がでている、プラグインが有効になった

ESLint の設定はたくさんある

```text
js というのは本来の(昔の)書き方、ES2015 以降の書き方、React や Vue などのフレームワークでの書き方など
様々な状況によって推奨される書き方というのが多様に存在するのですべてをおいかけることは現実味がない
ここでは挙動を確認するためなので初期値の通りに設定したが、各フレームワークごとに ESLint の設定はかえていかなくてはいけない
```

`setting.json`

```js
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

こちらをくわえると保存のタイミングでコードの整形もおこなってくれる

### prettier

ソースコードを整形

```text
prettier については vscode のプラグイン単体でもうごかすことができるが、
大抵は npm 経由で prettier のライブラリもインストールする
prettier のライブラリを使うことで違うテキストエディタの環境でもコードの整形を共有できる
```

1. vs code プラグイン prettier をインストールする
1. vs code での設定
1. npm より prettier ライブラリをインストールする
1. 使えるようになるための設定

vs code プラグイン prettier をインストールする

```console
(prettier の名前で複数あるので注意)
$ code --install-extension esbenp.prettier-vscode

(インストールできたことを確認)
$ code --list-extensions
...
esbenp.prettier-vscode
...

(プラグインをいれたときはアプリを再起動しなくてはいけないことに注意)
```

vs code での設定

`setting.json` を下記のように変更

```js
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

`hello.js` (問題ない書き方に変更する)

```js
// 文字の囲みをシングルクォートにする
console.log('hello----!');
```

- vscode 側
  - 表示 -> 機能拡張 -> 有効から prettier が有効になっていることを確認
  - `hello.js` をひらいて `alt+shift+f` をおして整形を実行する
  - シングルクォートがダブルクォートに変更される

npm より prettier ライブラリをインストールする

```console
(開発用にインストール)
$ npm install prettier --save-dev

(このように実行するとファイルが整形されたものに上書き)
$ ./node_modules/.bin/prettier --write hello.js
```

使えるようになるための設定

```console
(シングルクォートはそのままで使いたいので設定ファイルを設置)
$ touch .prettierrc
```

`.prettierrc`

```js
{
    "singleQuote": true
}
```

## SEEALSO

- <https://code.visualstudio.com/> - vscode 公式ページ
  - <https://code.visualstudio.com/docs/setup/mac> - インストールあとの設定(mac)
  - <https://code.visualstudio.com/docs/getstarted/settings> - 公式ページワークスペースの設定
  - <https://code.visualstudio.com/docs/getstarted/keybindings> - キーバインディングのページ
  - <https://marketplace.visualstudio.com/VSCode> - マーケットプレイス(機能拡張)
  - <https://code.visualstudio.com/docs/languages/html> - HTML in Visual Studio Code
  - <https://code.visualstudio.com/docs/languages/javascript> - JavaScript in Visual Studio Code
