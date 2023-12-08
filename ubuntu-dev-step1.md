# OS の準備

2022 年 10 月 27 日時点

## ubuntu OS の準備

linux OS はネット上で無償で提供されているので OS をダウンロードしてインストールするためのインストールメディアを作成する。

```text
ひと昔前はインストール用のインストールメディアは CD や DVD ディスクで供給していたが、
最近の PC はディスクを再生する装置がないものが多くなってきたので
USB メモリをつかってインストールメディアを作成。
```

### usb メモリについて

os のイメージが 3GB 程度あるので 4GB 以上のものを用意、今回は 16GB を使用

### linux OS 入手先について

os を配布しているサイトからダウンロード

- ubuntu の os は大きく分けて二つある
  - 公式ページが配布しているも
  - japan team が配布している「日本語 Remix」

~~今回は「公式ページ」の Ubuntu 22.04.01 LTS を選択する~~

2023-12-08 時点では `Ubuntu 22.04.03 LTS` が公開されているようなので `22.04.03` に読み替えてください

### ダウンロード手順

- 公式ページの場合 <- `今回はこちらの手順を採用`
  - ダウンロードページ
    - url: <https://jp.ubuntu.com/download>
    - ~~「Ubuntu Desktop 22.04.1 LTS」をクリック~~
    - 「Ubuntu Desktop 22.04.3 LTS」をクリック
    - ダウンロードがはじまるのでダウンロードのフォルダに保存をする
- 日本語 Remix の場合
  - ダウンロードページ
    - url: <https://www.ubuntulinux.jp/download>
    - 「日本語 Remix イメージのダウンロード」をクリック
    - Ubuntu Desktop 日本語 Remix のダウンロード
    - url: <https://www.ubuntulinux.jp/products/JA-Localized/download>
    - Ubuntu 22.04 LTS - 2027 年 4 月までサポートをクリック
    - Index of /releases/22.04
    - url: <http://cdimage.ubuntulinux.jp/releases/22.04/>
    - ubuntu-ja-22.04-desktop-amd64.iso をクリックしてダウンロード

### インストールメディアの作成

`linux pc`, `mac`, `windows` どの OS 上でもインストールメディアを作成することは可能

OS をダウンロードするところまではどの端末上でも同じだがメディアを作成する手順は異なるので注意

windows pc を使ってインストールメディアを作るやり方を紹介

#### windows pc の場合の書き込み手順

ダウンロードしたファイルをそのまま usb メモリにコピーしても使えないので usb で起動できる状態にする

usb メモリにインストールメディアの状態にするためのアプリを活用

- windouws 用で無料で使える Rufus を使う
  - Rufus 公式サイトからダウンロード
    - url: <https://rufus.ie/ja/>
    - 使い方などは公式ページの解説を参考
    - 他、参考になりそうなページはこちら
    - url: <https://onoredekaiketsu.com/rufus-if-booting-from-usb/>
    - usb メモリをさす場所には注意したほうがいいかもしれない、認識しない場合は usb メモリをさす場所を変えるとうまくいくかもしれない。

#### linux(Ubuntu) pc の場合の書き込み手順

#### Mac pc の場合の書き込み手順
