# NAME

win_dev - Windows を活用したwebアプリ開発環境について

## INTRODUCTION

```text
2020年時点でweb系のシステム開発は Mac で行う人が多いと思われるが、様々な事情につき
Windows マシンで構築することなった場合のために資料を残しておく
昨今のMicrosoftは随分とエンジニアに寄り添う姿勢をとっているようで公式ドキュメントも随分と充実している様子であるが
Mac から移行する場合理解がむつかしいところも多く、何かのお役に立てれば幸いと思う。
```

## CHAPTER1

開発用のPC自体の準備

ハードウェアについて

コスパでいくなら `Lenove ThinkPad x260` が良いと思う

```text
Mac と違い Win はハードウェアを自由に選べるため良くも悪く自由な選択肢が用意されている
web 系の開発に活用するなら昨今は docker を使う場面が多いので docker が使えるマシンのスペックを選ぶ
docker の公式ドキュメントによれば Windows 10, 64bit, メモリ4G, 以上と記されている、
実際にはメモリは余裕があったほうがいいので 8G 以上を目安にするとよい
デスクトップタイプは持ち運びが出来ないので、現実的な選択肢はノートブックで軽めの物が使い勝手はよいと思う。
Win の良いところは中古市場の選択肢が豊富というところなので今回は中古の Lenove ThinkPad x260 を選択した
```

メモリの増設について

x260 はメモリ 16G に増設しておく

```text
x260 についてはメモリカードが１枚しかさせない構造になっている、中古で購入する場合注意したいのは最初に搭載されているメモリの容量。
メモリ8G以上のものは購入に１万円くらい余裕を見たほうがよいので、中古で4G搭載の安いものを購入してあとから
16Gにつけかえるか、8G以上の中古を狙うのかはそのときの市場の品揃えでバランスを考えて購入するとよい
x260 シリーズのメモリ増設方法はネット上にもたくさん記事が存在するのでそれほど難しくはない
メモリに限らず ThinkPad シリーズは個別の部品、部品交換がやりやすいように作られている。
```

オペレーションシステムについて

Windows 10 Pro にしておき常に最新の状態にしておく

```text
Windows 10 においても定期的にバージョンアップをしており、初期の Win10 と最近の Win10 では仮想マシンの仕組みなど
改良されている、実際に初期の Win10 においては docker が正常に起動しない。
Windows update のやり方などはネット上にたくさんわかりやすい記事が存在するので参考にするとよい
間違いない情報としては Microsoft の公式ドキュメントで確認をする
```

Microsoft Store について

アカウントは作っておき、常にアップデートしておく

```text
Mac でいうところの AppleID のような位置づけで Microsoft Store というものが使えるようになっている
基本的にインストールされいるアプリはこちらの Store を経由して管理するような状態になっているので
アカウントはつくっておき、こちらもアップデートできるものはすべて行っておく
```

Power Shell について

`Windows Power Shell ISE` ではなく `Windows Power Shell` をつかう

```text
昔の Win はコマンドラインの操作はコマンドプロンプトをつかっていたが、今は Power Shell を使うようになっている
注意しないといけないのは Power Shell が４種類存在する
Power Shell, Power Shell(x86), Power Shell ISE, Power Shell ISE(x86)
ISE は簡易的なテキストエディタと統合環境になっており、フォントなど充実しているが使ってみると挙動が怪しい時がある
ISE で実行すると謎のエラーメッセージが出現するが Power Shell だと普通に動くものがあるので ISE を使うのはおすすめしない
ちなみに現時点では Power Shell を立ち上げると PowerShell Core を紹介しているサイトへのリンクが出現する
PowerShell Core についてはインストールがひと手間かかるので今回は活用を見送っておく
```

Web ブラウザについて

google chrome をインストールしておく

```text
Win10 においては Microsoft Edge が標準の Web ブラウザになっているが開発においての確認は
chorme を使うほうがよい、最終的に Edge での挙動も確認したい場合は Edge をつかう
chorme の使い方についてもネット上にたくさん資料が存在するので基本的な使い方は把握しておく
```

Windows 10 全般について

操作方法を一通り把握しておく

```text
今でも Win ユーザーは日本にはおおいので基本的な操作方法の資料はたくさん用意されている
最近はネット上で無料で提供されているのであえて高額な書籍などの購入の必要はないとおもわれる
快適に作業をすすめるにはショートカットキーを活用することが大事なので自分の操作の癖に応じて
ショートカットキーの自分用のチートシートなどを作っておくとよい
```

## CHAPTER2

ミドルウェアの準備

docker について

```text
昨今は開発環境の構築の手間を軽減するために docker を活用する場合がおおいため
Windows 用の Docker Desktop for Windows をインストールする
こちらが問題なくインストールできない場合は開発マシンとしてはいろいろと厳しい状況になっていくので
docker のインストール作業がうまくいかない場合は別のマシンを検討するときの良い目安になる
インストールは公式ページからおこない、別途 windows の場合の注意事項はネット上に様々な記事があるので
それらを参考にしてインストールをおこなう
```

docker の基本的な使い方

docker インストール完了後、 Power Shell で下記を試してみる

```console
(docker と docker-compose コマンドが使えること確認)
> docker --version
Docker version 19.03.5, build 633a0ea
> docker-compose --version
docker-compose version 1.25.4, build 8d51620a

(コンテナに正常にアクセスできることを確認)
> docker info
Client:
 Debug Mode: false
...

```

## CHAPTER3

## CHAPTER4

## CHAPTER5

## CHAPTER6

## CHAPTER7

## CHAPTER8

## CHAPTER9

## SEE ALSO

- 開発用のPC自体の準備
  - <https://www.be-stock.com/shop/> - ThinkPad 専門店 Be-Stock
  - <https://docs.microsoft.com/ja-jp/> - Microsoft Docs
  - <https://www.google.com/intl/ja_jp/chrome/> - Google Chrome
  - <https://www.windows10info.net/index.html>
  - <https://pc-karuma.net/windows10/>
- ミドルウェアの準備
  - <https://www.docker.com/> - Docker 公式
  - <https://docs.docker.com/docker-for-windows/install/> - docker ダウンロード
  - <https://lab.sonicmoov.com/development/install-docker-windows/> - docker インストール参考記事
