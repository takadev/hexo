---
title: jpegtran使ってみた
date: 2016-12-25 00:00:00
tags:
- "jpegtran"
- "フロント"
- "最適化"
category: フロント
---
## 画像最適化してみた
今回も少し短いですが、jpgの画像最適化をやってみました。
最適化ツールとしてはjpegtranとjpegoptimがありますが、jpegtranを使用してみました。
<!-- More -->

## はじめに
環境はmacでOSはEl Capitanです。
自分用のメモなので悪しからず。

## jpegtranのインストール
まずはインストールしてみます。と思ったらデフォルトでインストールされていました。
ただHomebrewで一発なので簡単です。

```
brew install jpeg
```

インストールできたか確認してみましょう。

```
jpegtran -v
```

無事インストールできたみたいですね。

## 最適化
最適化してみましょう。以下のようなコマンドで行います。

```
jpegtran -copy none -optimize -outfile hoge.jpg base.jpg
```

オプションの意味はこんな感じです。

* -copy none
  - JPEG ファイルのメタデータをすべて削除する。
* -optimize
  - ハフマンテーブルを最適化する。
* -outfile
  - ファイルの出力先の指定


## まとめて最適化
1ファイルづつはめんどくさいのでディレクトリ内のjpgをまとめて最適化してみます。
以下のようなコマンドで一発で最適化できます。

```
find /path/to/image/ -name "*.jpg" -type f -exec jpegtran -copy none -optimize -outfile {} {} \;
```

楽チンですね。

## PNGの場合
pngの場合はOptiPNGやPNGOUTなどのツールがありますので、機会があれば試してみたいと思います。

終わり。