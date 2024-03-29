# ubuntu での開発環境

2022 年 10 月 27 日時点

## ubuntu OS の準備

- 下記のリンク先記事を参考に進める
  - [ubuntu-dev-step1](ubuntu-dev-step1.md) - OS の準備

## インストールする PC の準備からインストールまで

- 下記のリンク先記事を参考に進める
  - [ubuntu-dev-step2](ubuntu-dev-step2.md) - PC の準備

## ディレクトリについて

- Becom 仕様の ubuntu pc 設定では下記のディレクトリを追加したい (`USER` はそれぞれのユーザー名に読み替えて)
  - `/home/USER/etc/` -> 設定ファイルの類を保管 (vscode の設定ファイルなど)
  - `/home/USER/tmp/` -> 暫定的に作成したファイルなどを保管 (draft.md のようなメモ書きのためのファイルなど)
  - `/home/USER/bin/` -> オリジナルで作った実行スクリプトを保管 (別途パスの設定などは必要)

```bash
mkdir ~/etc ~/tmp ~/bin
```

## アプリケーションのインストール方針

- 最初に「ソフトウェアの更新」の機能でできるところまでアップデートをしておく

### アプリケーションのインストールについて

- snap というアプリのインストール管理の機能「Ubuntu Softwave」が存在するがこちらは挙動がまだ不安定
- アプリなどのインストールは基本的にコンソール画面の apt コマンドをつかってインストールすることにしておく。

#### ubuntu でのアプリケーションのインストール方法の基本

- インストール方法は以下の２つの方法がある
  - ソースコードをダウンロードしてきてコンパイルする方法
  - .deb 形式のパッケージをダウンロードして apt コマンドでインストールする方法

よほど特殊な状況出ない限りは apt コマンドでインストールする方法を使う

インストールしたいアプリのパッケージ提供場所

.deb 形式のパッケージは様々なところで提供されているがごくまれに品質に問題があるものが存在するので信頼性の高い提供場所から入手したい。

- 信頼性の高い提供場所
  - ubuntu が公式に提供しているもの
  - アプリケーションの公式サイトが提供しているもの

参考になりそうな記事

- apt とリポジトリの意味
  - <https://weblabo.oscasierra.net/ubuntu-apt/>
  - <https://pc.watch.impress.co.jp/docs/column/ubuntu/1417585.html>
  - <https://qiita.com/kon_yu/items/8ac350f3951f8534c931>
- パッケージの検索
  - <https://packages.ubuntu.com/ja/>

アプリのバージョンの問題について

```text
上記のパッケージの検索からみると ubuntu22 は mysql8 を提供している、
mysql5.7 をインストールしたい場合 ubuntu18 のころのリポジトリを使うことになりそうだが、
すんなりインストールできるかどうかはやってみないとわからない。

アプリというのは他のアプリを依存していることがあるのでイントールにつまづくことになる可能性が高い。
かといって ubuntu18 をいまさら設定するのもやらないほうがよさそうだ。

公式に提供しているバッケージ以外のバージョンをインストールするのはいろいろはハマりポイントがありそうだ。

新しいバーションのアプリをイントールするための様々な依存関係のアプリのアップデートはまだよいが、
古いバージョンをいれるための他のアプリのダウングレードはやらないほうが良い。

もしすんなり mysql5.7 を入れれたとして、その環境に mysql8 を使いたくなったとき同居ができるかどうか、
mysql8 のアップデートが正確に反映されるのかなどアプリの依存関係というのはとてもややこしい。

基本方針としては docker を活用して開発環境を構築することにしたい。

開発しているシステムに直接依存しないようなテキストエディタや web ブラウザなどは
公式ページからパッケージを入手して、
開発システムに直接依存するものは docker の二本立てのアプリケーションのインストール方針にしておく。
```

## インストール手順

- GUI アプリケーションについては下記のリンク先記事を参考に進める
  - [ubuntu-dev-step3](ubuntu-dev-step3.md) - GUI アプリケーションの準備
- CLI アプリケーションについては下記のリンク先記事を参考に進める
  - [ubuntu-dev-step4](ubuntu-dev-step4.md) - CLI アプリケーションの準備

## お気に入りの調整

左側の Dock の調整

よく使うものだけを表示しておき使わないものはお気に入りから削除しておく

- お気に入りに残すもの
  - ファイル
  - 端末
  - web ブラウザ -> google
  - テキストエディタ -> vscode
  - Github Desktop
  - slack
  - 設定
  - ソフトウェアの更新
  - ヘルプ

設定の調整

設定 -> 外観 -> Dock -> Dock を自動的に隠すを有効

## 参考のリンク

- ubuntu japan team: <https://www.ubuntulinux.jp/>
- ubuntu 公式ページ: <https://ubuntu.com/>
- git 公式: <https://git-scm.com/>
- git チートシート: <https://training.github.com/downloads/ja/github-git-cheat-sheet/>
