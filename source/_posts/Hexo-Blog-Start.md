---
title: Hexoでブログをはじめてみた前編
date: 2016-11-19 21:54:03
tags:
- "ブログ"
- "nvm"
- "git"
category: hexo
---

自身の勉強と草を生やす為にHexoとGithub Pagesを使ってブログを書くことにしました。
早速、ブログの立ち上げ方をブログに書きたいと思います。
まずはローカルでHexoのビルトインサーバの立ち上げまでを行います。

<!-- more -->

## はじめに
必要なものとして
- Git
- Githubアカウント
- Github Pages

上記は既に持っている前提です。

## Hexoの導入

### nvmインストール
HexoはNode.jsなので、まずはNodeのインストールを行います。
Nodeのバージョン管理に便利なnvmを先にインストールします。

```
⋊> ~ git clone git://github.com/creationix/nvm.git ~/.nvm/  
```

クローンが終わったら

```
⋊> ~ source ~/.nvm/nvm.sh  
```

bashで叩かないとエラーが出るかもしれません。普段使ってるfishだとエラーが出ました。

### Nodeのインストール

インストールできるNodeのバージョンを確認をします。

```
nvm ls-remote
v0.1.14
v0.1.15
v0.1.16
v0.1.17
v0.1.18
v0.1.19
...
```

私はこの当時最新だった4.6.2をインストールしました。

```
nvm install 4.6.2
```

無事インストールが終わりました。

```
node -v
v4.6.2
```

### Hexoのインストール

```
npm install -g hexo
```

Hexoのインストールはこれで終了です。簡単！


## Hexoでブログを作ってみる

Hexoのインストールができたらブログを立ち上げてみましょう
今回はmyBlogという名前でブログを作成しました。

```
hexo init myBlog
```

これで新規作成できました。
その後はディレクトリを移動し初期化を行います。

```
cd myBlog
npm install
```

そしてローカルでサーバを立ち上げてみると

```
hexo s
```

http://localhost:4000 にアクセスすると、Hexoブログが表示されていることが確認できると思います。
ここまででHexoブログの立ち上げ方
