---
title: Dockerで開発環境
date: 2016-12-26 00:00:00
tags:
- "Docker"
- "php"
- "mysql"
- "nginx"
category: Docker
---
## Dockerで開発環境構築
今回はDockerで開発環境を作成してみたいと思います。
<!-- More -->

## はじめに
仕事で必要になったのでNginx + PHP(Phalcon) + MySQL + Redisの環境を作ってみます。
Docker自体は[以前の記事](http://devlog.site/docker/docker2/)で環境は整えてあります。

## 各種サービスのコンテナ作成
それぞれのサービス用コンテナを作成していこうと思いますが、その前に今回はDocker Composeを使用したいと思います。
Docker composeとは、複数のコンテナから成るサービスを構築・実行する手順を自動で行うことができ、また管理することができるものです。Docker composeを使用することで1回のコマンド実行で、すべてのコンテナサービスを起動することができたりなんかしちゃいます。すごく便利ですね。Docker compose自体はDocker for Macに入っているので以下のコマンドで確認してみましょう。

```
docker-compose -v
```

バージョンが確認できましたね。
docker-composeはYAMLファイルで各コンテナを管理することができます。YAMLファイルの書式はほぼdocker runのオプションと対応していますので、書き方などはそこまで難しくないと思います。

それでは次に各種サービスのコンテナを作成したいと思います。docker hubからイメージを取得してきます。まずはnginxとphalconのイメージです。

```
docker pull alfonso/nginx-phalcon
```

次にmysqlのイメージです。

```
docker pull mysql
```

最後にRedisです。

```
docker pull redis
```

確認してみましょう。

```
docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
redis                   latest              d59dc9e6d0bf        11 days ago         182.9 MB
mysql                   latest              594dc21de8de        12 days ago         400.2 MB
alfonso/nginx-phalcon   latest              6a69953541cf        2 years ago         540.5 MB
```

イメージがダウンロードされていますね。
あとは各種イメージのコンテナを作成しましょう。
まずはredisのコンテナを立ち上げます。

```
docker run --name redis -p 6379:6379 -d redis redis-server --appendonly yes
```

次にmysqlのコンテナです。

```
docker run --name ban_mysql -p 3306:3306 --volumes-from ban_data -e MYSQL_ROOT_PASSWORD=hoge -d mysql
```

最後にnginx-phalconです。
**-v**オプションではコードのパスを指定します。

```
docker run --name php -p 8888:80 -d -v="/path/code":"/var/www" alfonso/nginx-phalcon
```

これでコンテナが作成されました。確認してみましょう。

```
docker ps -a
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS                  PORTS                    NAMES
1cc31121475c        alfonso/nginx-phalcon   "/bin/sh -c 'service "   15 seconds ago      Up 15 seconds           0.0.0.0:8888->80/tcp     php
d0919a3a1bd6        mysql                   "docker-entrypoint.sh"   1 minutes ago       Up 1 minutes            0.0.0.0:3306->3306/tcp   mysql
7198ba879cf6        redis                   "docker-entrypoint.sh"   1 minutes ago       Up 1 minutes            0.0.0.0:6379->6379/tcp   redis
```

無事に作成されていますね。
サービスのコンテナ作成はここまでです。

## テータコンテナの作成
最後に今回はデータの永続化を行いたいと思うので、BusyBoxを使ってみます。
BusyBoxとは標準UNIXコマンドの主要コマンドをまとめて1つの実行ファイル化したものです。BusyBoxは主要なコマンドとシェルを備えているので、これだけで基本的なLinux環境を整えることができます。

実際にBusyBoxを使ってみましょう。以下のコマンドでイメージのダウンロードからコンテナの作成まで行い、コンテナへアタッチすることができます。**--rm**オプションを指定しているのでコンテナから出ると自動でコンテナが削除されます。

```
docker run -it --rm busybox
```

簡易Linux環境って感じですね。
しかしDocker便利ですね。では、実際にデータコンテナのどこにデータを保存するかを指定してコンテナを立ち上げてみましょう。以下のコマンドで**/data**ディレクトリ以下がデータの保存先になります。**-v**オプションを指定したディレクトリが保存先となります。

```
docker run -it -v /data --name data busybox /bin/sh
```

ログイン後に**/data**ディレクトリ配下に適当にファイルを作成してみましょう。

```
/ # echo "TEST!!!" >> /data/test.txt
```

次にこのデータコンテナのデータを使用するコンテナを立ち上げてみましょう。
本来は先ほどダウンロードしてきたmysqlイメージのコンテナを使うところですが、mysqlのデータがまだないので確認のためにCentOSのイメージを使用したいと思います。
以下のように**--volumes-from**オプションでbusyboxコンテナの名前を指定することでデータコンテナへマウントすることができます。

```
docker run -it --volumes-from data --name tmp_os centos /bin/bash
```

ログイン後**/data**配下に先ほど作成した**test.txt**ファイルがあることがわかると思います。

```
[root@3fcdf68d7070 /]# cat /data/test.txt 
TEST!!!
```

ちゃんとマウントされていることがわかりますね。無事にデータの永続化ができました。

## docker-compose.ymlの作成
ここまでで一つ一つコンテナを作成してきましたが、冒頭でも書きましたがDocker Compseを使ってそれぞれのコンテナを自動で構築することができるんです。
そのためには**docker-compse.yml**ファイルを作成します。
以下のようなファイルを作成してください。詳しい構文などは[公式サイト](https://docs.docker.com/compose/compose-file/#/version-2)を参照してください。

```
version: '2'
services:
  php:
    image: alfonso/nginx-phalcon
    ports:
      - "8000:80"
    volumes:
      - ./project_name:/var/www
    depends_on:
      - db
      - redis
    container_name: php
  busybox:
    image: busybox
    volumes:
          - /data:/var/lib/mysql
    command: /bin/sh
    stdin_open: true
    container_name: data 
  mysql:
    image: mysql
    volumes_from:
      - busybox
    environment:
      MYSQL_ROOT_PASSWORD: 'hoge'
      MYSQL_USER: 'bar'
      MYSQL_PASSWORD: 'fuga'
      MYSQL_DATABASE: 'piyo'
    ports:
      - '3306:3306'
    container_name: mysql
  redis:
    image: redis
    ports:
      - '6379:6379'
    container_name: redis
```

docker-compse.ymlファイルはPhalconのプロジェクトのディレクトリと同階層に配置してある想定です。

## アプリケーションを立ち上げる
**docker-compse.yml**ファイルを作成が終わったら実際にアプリを立ち上げてみましょう。
以下のコマンドで立ち上がります。

```
docker-compose up
```

実行するとコンソールにログが一気に流れてコンテナが立ち上がるのがわかると思います。
ただしデータコンテナだけ起動しないと思います。データコンテナはデータの保持だけが目的なのでコンテナとして起動している必要がありませんので問題ありません。

```
docker-compose up -d {コンテナー名}
```

**-d**オプションをつけるバックグラウンドで実行できます。
またコンテナ名を指定することで個別に起動することもできます。

これでdockerでの環境構築は終わりです。他のマシーンに同じ環境を作る際はデータコンテナをロードすればそのままデータも同じものが使えるのでかなり便利ですね。

終わり。