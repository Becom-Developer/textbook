# NAME

docker_dev - Docker を活用したwebアプリ開発環境について

# SYNOPSIS

## DOCKER

Docker のインストール

docker のインストールには Docker Hub のアカウント登録が必要

インストールの案内に従いインストールを実行し、そのあと Docker アプリを立ち上げる

```
(docker コマンドが使えることを確認)
$ docker --version
Docker version 18.09.2, build 6247962

(クイックスタートの案内に従ってdockerを使ってみる)
(最後までおわると自分の Docker Hub アカウントに自分がつくったコンテナがアップされている)
(docker コマンドをためす)
$ docker container run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
...

Hello from Docker!
...

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

(途中で Hello form Docker! と表示するだけ)
(現在と過去に起動させたコンテナの一覧コマンド)
$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
410b275df5d4        hello-world         "/hello"            About a minute ago   Exited (0) About a minute ago                       musing_euclid

(停止したコンテナ削除、コンテナ名は毎回変更される)
$ docker container rm musing_euclid
musing_euclid

(削除されたことの確認)
$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

## PHP

```
(Docker をつかったphpを試してみる)
(任意の作業ディレクトリを用意)
$ mkdir -p ~/tmp/php-book && cd ~/tmp/php-book

$ docker container run -d --name php-book -v $(pwd):/var/www/html -p 80:80 php:7.2-apache
Unable to find image 'php:7.2-apache' locally
...
Status: Downloaded newer image for php:7.2-apache
ab79ec3f19c1755018dc7cb42a4492b3cf85ccefc7882655d5f56a194993f03c

(コンテナのなかに入る)
$ docker container exec -it php-book bash

(なかに入った)
root@ab79ec3f19c1:/var/www/html# echo '<?php phpinfo();' > index.php

(web ブラウザで下記にアクセスするとphpinfoが表示される)
http://localhost/

(いちどぬける)
root@ab79ec3f19c1:/var/www/html# exit

(デーモン化されてつねに動いたままになっている)
$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
ab79ec3f19c1        php:7.2-apache      "docker-php-entrypoi…"   9 minutes ago       Up 9 minutes        0.0.0.0:80->80/tcp   php-book

(~/tmp/php-book の中のファイルは Dockerコンテナの中の /var/www/html の中に存在するような状態になっている)

(もう一度コンテナのなかに入ってみる)
$ docker container exec -it php-book bash

(vim が使えるか確認するが vim は使えない)
root@064aa59d626a:/var/www/html# which vim
root@064aa59d626a:/var/www/html# exit

(Docker file を作成して vim を使えるようにする)
$ cat ~/tmp/php-book/Dockerfile
FROM php:7.2-apache

RUN apt-get update

RUN apt-get install -y vim

(ビルド)
$ docker image build -t php-book:ver1 .
Sending build context to Docker daemon  3.072kB
Step 1/3 : FROM php:7.2-apache
...

 (コンテナ起動)
$ docker container run -d --name php-book-vim php-book:ver1
30ba2d1db066be40f74eebb93c9d59e64bf1f36318b026f75de7ac4003496b63

(コンテナの中に入る)
yk-iMac2017:php-book yk$ docker container exec -it php-book-vim bash

(vim コマンド確認)
root@30ba2d1db066:/var/www/html# which vim
/usr/bin/vim

(vim のバージョン)
root@30ba2d1db066:/var/www/html# vim --version
VIM - Vi IMproved 8.0 (2016 Sep 12, compiled Jun 21 2019 04:10:35)
...
root@30ba2d1db066:/var/www/html# exit

(このような状態になる)
$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
30ba2d1db066        php-book:ver1       "docker-php-entrypoi…"   3 minutes ago       Up 3 minutes        80/tcp               php-book-vim
064aa59d626a        php:7.2-apache      "docker-php-entrypoi…"   29 minutes ago      Up 29 minutes       0.0.0.0:80->80/tcp   php-book

(稼働中のものを確認)
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
30ba2d1db066        php-book:ver1       "docker-php-entrypoi…"   13 hours ago        Up 13 hours         80/tcp                 php-book-vim
064aa59d626a        php:7.2-apache      "docker-php-entrypoi…"   14 hours ago        Up 14 hours         0.0.0.0:80->80/tcp     php-book
(php-book-vim を停止)
$ docker stop php-book-vim
php-book-vim

(停止されている確認)
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
fd670c821c2c        php-book-app_web    "docker-php-entrypoi…"   11 hours ago        Up 11 hours         0.0.0.0:5000->80/tcp   php-book-app-web
064aa59d626a        php:7.2-apache      "docker-php-entrypoi…"   14 hours ago        Up 14 hours         0.0.0.0:80->80/tcp     php-book

(もう一つも停止)
$ docker stop php-book
php-book

(停止されている確認)
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES

(もう一度使いたい時)
$ docker start php-book
php-book
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
064aa59d626a        php:7.2-apache      "docker-php-entrypoi…"   14 hours ago        Up 2 seconds        0.0.0.0:80->80/tcp     php-book
```

php のサンプルコードを書く場所をきめる

```
(お手元のmacで作業場所を作る)
$ mkdir -p ~/tmp/php-book && cd ~/tmp/php-book

(docker が使えることの確認)
$ docker info

(よけいなイメージなどがないか確認、まっさらではじめたい)
$ docker images

$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
0e6820334c51        nginx               "nginx -g 'daemon of…"   4 hours ago         Up About an hour    0.0.0.0:8181->80/tcp   nginx-container

(削除する場合、起動中であれば停止)
$ docker stop 0e6820334c51

$ docker stop 0e6820334c51
0e6820334c51

$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
0e6820334c51        nginx               "nginx -g 'daemon of…"   4 hours ago         Exited (0) 15 seconds ago                       nginx-container
$ docker rm 0e6820334c51
(イメージ削除は docker rmi 最後に -f をつけると紐づくものも削除)

(docker composer を使った起動をおこなう)
$ cat docker-compose.yml
version: '3'
services:
  web:
    container_name: php-book
    build:
      context: .
      dockerfile: ./Dockerfile
    volumes:
      - .:/var/www/html:cached
    ports:
      - "80:80"

$ cat Dockerfile
FROM php:7.2-apache
(デーモン化されて起動、イメージがないので明示的に --build)
$ docker-compose up -d --build
Building web
...
Creating php-book ... done

(状態を確認)
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
c11c5c12d1a4        php-book_web        "docker-php-entrypoi…"   53 seconds ago      Up 53 seconds       0.0.0.0:80->80/tcp   php-book
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
php-book_web        latest              705b23f384d9        2 days ago          381MB
php                 7.2-apache          705b23f384d9        2 days ago          381MB

(この時点でwebブラウザにアクセスwebブラウザに下記のような文字がでればサーバーは動いている)
(アクセス: http://localhost/)

Forbidden
You don't have permission to access / on this server.
Apache/2.4.25 (Debian) Server at localhost Port 80

(停止と開始)
$ docker-compose stop
$ docker-compose up -d

(compose を停止 compose で作られたイメージも削除)
$ docker-compose down --rmi all

(コンテナの中に入る)
$ docker container exec -it php-book bash
```

```
(PHP の具体的なコーディングについて)
(PHP-FIG という団体が昨今のPHPのコーティング方法全般の指南をしている)
(推奨しているコーディングルールは PSR 「PHP Standards Recomendation」を参照)

(phpの拡張モジュールについて)

PHP おいては拡張ライブラリという表現をつかう
拡張ライブラリのインストール方法は過去においては 「PEAR」 が使われたが現在は 「Composer」

Composer はプロジェクトごとの依存パッケージ管理ができるようになっている

Composer の使い方は Packagist サイトを参考にするとよい

Docker で Composer コマンドを使いたい場合はすでにイメージが存在するので活用する
```

```
Docker のなかで Composer コマンドを使えるようにする

先ほどの Docker ファイルに下記を追記

laravel インストールにはlinuxのパッケージをいくつか追加

$ echo 'RUN apt-get update && apt-get install -y zip unzip' >> ./Dockerfile
$ echo 'ENV COMPOSER_ALLOW_SUPERUSER 1' >> ./Dockerfile
$ echo 'COPY --from=composer:1.7 /usr/bin/composer /usr/bin/composer' >> ./Dockerfile

Docker ファイルを書き換えたので、コンテナを再度ビルドしなおす

$ docker-compose down --rmi all
$ docker-compose up -d --build

コンテナの中に入ってイントールする

(laravel インストールは laravel 公式ページ参照)
$ docker container exec -it php-book bash
# composer create-project --prefer-dist --no-interaction laravel/laravel ./testphp
Installing laravel/laravel (v5.8.17)
  - Installing laravel/laravel (v5.8.17): Downloading (100%)
Created project in ./testphp
...
Application key set successfully.
#
```

# SEE ALSO

- <https://www.php.net/> - PHP 公式ページ
- <https://laravel.com/> - web フレームワーク Laravel 公式
- <https://www.docker.com/> - docker 公式
- <https://github.com/php-book/php-qa-plaza> - はじめての PHP プロフェッショナル開発
- <https://knowledge.sakura.ad.jp/13265/> - Docker入門
- <https://www.php-fig.org/> - PHP FIG 公式
- <https://packagist.org/> - Packagist (Composer のメインレポジトリサービス)
