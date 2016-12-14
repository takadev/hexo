---
title: Docker入門
date: 2016-12-08 00:00:00
tags:
- "Docker"
- "mysql"
category: Docker
---
## Dockerを使ってみた
業務でDocker環境を引き継いだもののDcokerはさっぱりわからないので、まずは使える環境をローカルにも作ってみました。
<!-- More -->

## はじめに
Homebrewでもインストールできるみたいですが、今回はDocker for Macを公式サイトの手順に従ってインストールして行いたいと思います。

## インストール
[公式サイト](https://docs.docker.com/docker-for-mac/)からインストーラをダウンロードします。
インストーラを起動させた際にDocker Toolboxを使用していた場合、設定などをコピーしますかと聞かれます。
自分はDocker Toolboxをちょろっと試したことがあったのでダイアログが出ましたが、コピーする必要はないのでNoで進めました。

## 起動
インストール後Docker.appをアプリケーションから起動します。
起動の際にVirtualBoxのバージョンが古いとアップグレードしてください。と注意されます。もし注意されたらVirtualBoxのバージョンを上げましょう。
起動するとメニューバーにDockerのアイコンが表示されます。

メニューバーのアイコンからはPreferenceの設定などができます。

## 試してみる
無事に起動できたみたいなのでターミナルからコマンドを叩いてみたいと思います。

```
⋊> ~ docker version                                                     14:20:49
Client:
 Version:      1.12.3
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   6b644ec
 Built:        Wed Oct 26 23:26:11 2016
 OS/Arch:      darwin/amd64

Server:
 Version:      1.12.3
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   6b644ec
 Built:        Wed Oct 26 23:26:11 2016
 OS/Arch:      linux/amd64
```

これでDockerが使えるようになりましたね。

## Dockerイメージをsave/loadしてみる
Docekrイメージを別環境へ移動するやり方は調べるといくつかあるみたいですが、
元の環境でsaveしてからインポートしたい環境でloadするやり方を試してみたいと思います。

まずDockerが動いてる環境でsaveをしてtar.gzにします。
imagesで一覧を確認します。


```
$ docker images
REPOSITORY           TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
mysql                latest              e571f0e3f4a6        9 months ago        385.5 MB

```

次にsaveでイメージをtar.gzします。

```
$ docker save e571f0e3f4a6 > image.tar
```

移動したい環境へ作成したtarをscpなどで移動して、loadを実行します。

```
$ docker load < image.tar
```

loadが終わったらimagesで確認してみましょう。

```
$ docker images
REPOSITORY           TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
mysql                latest              e571f0e3f4a6        9 months ago        385.5 MB
```

ちゃんとimagesの一覧に出てきましたね。これで移動ができました。
ちなみにexport/importというコマンドもあり、save/loadとの違いは、exportはDockerイメージのファイルシステムをまるっとtarで固めただけで、saveは親子関係やメタデータも含めて固めてくれるようです。

## mysqlコンテナを立ち上げてみる


次にmysqlコンテナを立ち上げてみたいと思います。

```
docker run --name mysqld -e MYSQL_DATABASE= -e MYSQL_USER=root -e MYSQL_PASSWORD=secret  -e MYSQL_ROOT_PASSWORD=verysecret -d mysql
```

mysqlの環境変数を**-e**で指定できるのでユーザやデータベースを指定して起動することができます。
ローカルからmysqlへ繋ぎにいけるか確認してみます。

```
$ docker exec -it mysqld mysql -u user -pパスワード
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 6
Server version: 5.7.15 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

無事に接続できましたね。
ちなみにローカルのmysqlコマンドを使用してもコンテナのIPを指定すれば繋ぎに行くこともできます。

```
mysql -hコンテナIP -u user -pパスワード
```

コンテナのIPアドレスは以下のコマンドで確認できます。

```
docker inspect --format '{{ .NetworkSettings.IPAddress }}' コンテナIDまたはコンテナ名
```

## データの永続化
最後に気をつけないといけないのがmysqlに保存しているデータについてです。
コンテナ内にデータを保存する場合、コンテナ作成時に**-vオプション**を指定する必要があります。

```
docker run --name mysqld -v /var/lib/mysql -d mysql
```

こんな感じで、**-v**の後に保存先のパスを指定してあげます。(-eオプションは省略してます。)
ただし、mysqlコンテナにデータ自体も保存してしまうとDockerの長所であるポータビリティが失われてしまいます。
そこでデータのみを格納するコンテナを別に作成することで、データ自体のポータビリティを保ちます。
適当にストレージとなるコンテナを作成します。

```
docker run -it -v /var/lib/mysql --name strage image
```

作成したストレージコンテナを指定してmysqlコンテナを作成しなおします。


```
docker run --volumes-from strage --name mysqld -d mysql
```

これでデータを格納するコンテナとmysqlのコンテナを切り離すことができました。
こうしておけばデータだけを移したいときに便利ですね。


今後は趣味で色々と試してみたいと思います。