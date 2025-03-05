# ubuntu での開発環境

2025-03-05 更新

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

- 個別の開発環境は docker を構築で対応
- 開発しているシステムに直接依存しないようなテキストエディタや web ブラウザなどは公式ページからパッケージを入手

#### ubuntu でのアプリケーションのインストール方法の基本知識

- インストール方法の種類
  1. ソースコードをダウンロードしてきてコンパイル
  1. `.deb` 形式のパッケージをダウンロードして apt コマンドでインストール
  1. パッケージ名を指定して `sudo apt install ...` のようにインストール
  1. GUI、アプリセンター(snap)を使ってインストール
- アプリケーションは依存関係の問題があるので基本はパッケージ名を指定してのインストールにする
- .deb 形式のパッケージはまれに品質に問題があるものが存在するので注意
- 信頼性の高い提供場所
  - ubuntu が公式に提供しているもの (パッケージ検索ページから検索できる)
  - アプリケーションの公式サイトが提供しているもの
- `lsb_release -a` このコマンドから ubuntu バージョンとコードネームが確認できる

参考になりそうな記事

- apt とリポジトリの意味
  - <https://weblabo.oscasierra.net/ubuntu-apt/>
  - <https://pc.watch.impress.co.jp/docs/column/ubuntu/1417585.html>
  - <https://qiita.com/kon_yu/items/8ac350f3951f8534c931>
- パッケージの検索
  - <https://packages.ubuntu.com/ja/>

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
