---
title: Docker基本コマンド
date: 2016-11-30 00:00:00
tags: Docker
category: Docker
---
## Dockerを使うときのメモ
先人からDockerの環境を引き継ぐこととなりDockerほぼ使ったことなかったので
色々調べたことをメモしておきます。
<!-- More -->

## Dockerイメージの検索
DockerイメージをDocker Hub上から検索できます。

```
docker search [イメージ名]
```

## Dcokerイメージをダウンロード
Docker Hub上からイメージをダウンロードします

```
docker pull [イメージ名]
```

## 取得したDockerイメージの確認
pullしてきたイメージの一覧を確認できる

```
docker images
```

## 起動中のコンテナの一覧を確認

`-a`を付けると停止中のコンテナも取得できる

```
docker ps -a
```

## DockerfileからDockerイメージを構築

```
docker build
```

## Dockerイメージからコンテナを作成

```
docker create [イメージ名]
```

## Dockerコンテナをスタート

```
docker start [コンテナ名]
```

## Dockerコンテナのストップ

```
docker stop [コンテナ名]
```

## Dcokerコンテナの削除

```
docker rm [コンテナ名]
```

## Dockerビルド時の履歴を確認

```
docker history [IMAGE]
```

## Dockerのコンテナで動作中のシェルへの接続方法
動作中のDockerにシェルでつないで色々いじりたいとき

```
docker exec -it [コンテナ名] /bin/bash
```

## Dockerコンテナのログを確認

```
docker logs [コンテナ名]
```

## Dockerイメージの削除

```
docker rmi [IMAGE]
```

