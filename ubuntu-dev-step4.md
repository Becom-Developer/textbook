# CLI アプリケーションの準備

2022 年 10 月 27 日時点

コマンドラインアプリケーションは開発支援をするものが多くミドルウェアアプリケーションとよばれることもある。

ubuntu インストール時に入っていなかったもので利用する可能性が高いものを選出して連続でインストールする

## インストール実行

- make (インストール関係)
- gcc (インストール関係)
- git (ソースコード管理)
- curl (ネットワーク)
- sqlite3 (データベース)
- nkf (文字コード変換)
- unar (圧縮ファイル文字コード対策)
- docker.io (仮想空間、ubuntu パッケージ名は .io がつく)
- docker-compose (docker のコマンド)

```bash
sudo apt install make gcc git curl sqlite3 nkf unar docker.io docker-compose
```

## インストール後の調整

### docker

sudo なしでつかえるようにしておく

```bash
sudo usermod -aG docker $USER
```

上記のコマンドはログインまわりの調整になるので実行後に PC 自体の電源をおとして再び PC を立ち上げる

下記のコマンドを実行して正常に動作すればよし

```bash
docker run hello-world
```

### git

最低限度の設定をしておく

git の設定ファイルは `~/.gitconfig` にできる、git のユーザー名を設定 -> `MYNAME` 任意の名前

```bash
git config --global user.name "MYNAME"
```

### ssh

この pc 用の秘密鍵と公開鍵を用意しておく

下記、鍵の生成にいろいろ聞かれるがすべてリターン -> `PCNAME` pc のユーザー名
`(rat, ox, tiger, rabbit, dragon, snake, horse, sheep, monkey, rooster, dog, pig)`

```bash
ssh-keygen -t rsa -C 'PCNAME'
```

下記コマンドで `.ssh` フォルダ内に鍵ファイルができたことが確認できる (id_rsa -> 秘密鍵 id_rsa.pub -> 公開鍵)

```bash
ls -a ~/.ssh/
```
