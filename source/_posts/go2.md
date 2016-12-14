---
title: Revelフレームワークpart1
date: 2016-12-13 00:00:00
tags:
- "Go"
- "Revel"
- "プログラミング"
category: Go
---
## Revelフレームワークを試してみた
RevelはgoのフルスタックのWebフレームワークです。Dockerと一緒にこのRevelでできたWebアプリも引き継ぐことになったので今回は勉強の為、ローカルでチュートリアルを試してみようと思います。
<!-- More -->

## はじめに
goのインストールはすでに終わっています。
[前回](http://devlog.site/Go/go1/)、gvmでインストールしてますので、気になる方は見てみてください。


## インストール
go getによりリポジトリからrevelをインストールします。

```
go get github.com/robfig/revel
```

次にコマンドラインツールをインストールします。

```
go get github.com/revel/cmd/revel
```

インストールできているか確認します。

```
$ revel version                                                                                                  
~
~ revel! http://revel.github.io
~
Version(s):
   Revel v0.13.1 (2016-06-06)
   go1.7 darwin/amd64
```

バージョンの確認ができましたね。これでインストールは終わりです。

## Revelコマンド
Revelには6つのコマンドがあります。
1つ1つ見ていきましょう。

```
revel new
```
アプリケーションのスケルトンを作成します。

```
revel run
```

テスト用にアプリケーションを起動します。

```
revel build
```

アプリケーションをビルドします。

```
revel package
```

アプリケーションをデプロイ用パッケージを作成します。

```
revel clean
```

一時ファイルを削除します。

```
revel test
```

テストを実行します。

## サンプルアプリを作ってみる

revelがインストールできたら早速アプリを作ってみたいと思います。
revelコマンドから新しくサンプルアプリを作成します。

```
revel new myapp
```

$GOPATH/src/myapp にアプリケーションのスケルトンが作成されます。
myapp以下のディレクトリ構造はこんな感じです。

```
|--.gitignore
|--README.md
|--app
|  |--controllers
|  |  |--app.go
|  |--init.go
|  |--routes
|  |  |--routes.go
|  |--tmp
|  |  |--main.go
|  |--views
|  |  |--App
|  |  |  |--Index.html
|  |  |--debug.html
|  |  |--errors
|  |  |  |--404.html
|  |  |  |--500.html
|  |  |--flash.html
|  |  |--footer.html
|  |  |--header.html
|--conf
|  |--app.conf
|  |--routes
|--messages
|  |--sample.en
|--public
|  |--css
|  |  |--bootstrap-3.3.6.min.css
|  |--fonts
|  |  |--glyphicons-halflings-regular.ttf
|  |  |--glyphicons-halflings-regular.woff
|  |  |--glyphicons-halflings-regular.woff2
|  |--img
|  |  |--favicon.png
|  |--js
|  |  |--bootstrap-3.3.6.min.js
|  |  |--jquery-2.2.4.min.js
|--tests
|  |--apptest.go
```

実際にアプリケーションを起動してみましょう。

```
revel run myapp
```

revelのビルトインサーバーが立ち上がるのでlocalhost:9000にアクセスしてみましょう。
アプリの画面が表示されると思います。

終わり。