---
title: ディープラーニング用語
date: 2016-12-17 00:00:00
tags:
- "機械学習"
- "ディープラーニング"
category: ディープラーニング
---
## わからない用語調べてみた
先日、「ゼロから作るディープラーニング」をやっとこ読み終えました。
かなり面白くて勉強になりました！ディープラーニングを始めてみようって人にはめちゃめちゃオススメです。理解が浅買った箇所をもう一度読み直してみようと思ってます。
そんな中、分からなかった用語を調べたのでメモしておこうと思います。
<!-- More -->

## 特徴量
4章辺りで特徴量という言葉が出てきます。最初一瞬わからなかったんですが、前後の流れでなんとくこんな意味かなぁと思ってたらその通りでした。
これは文字通り特徴の量のことで、よく画像認識なんかを扱う文脈で出てきます。
「特徴量を記述する」とかっていう文章をたまに見かけますね。

## 特徴点
特徴量と似ていますが、こちらも画像認識の文脈で使われ、言葉通り画像内のどこに特徴があるかを点で表したものです。

## OpenCV
OpneCV自体は本の中には多分出てこなかったと思いますが、画像認識周りでこの用語も出てくるので、前提知識として調べてみました。

> OpenCV（オープンシーヴィ、英語: Open Source Computer Vision Library）とはインテルが開発・公開したオープンソースのコンピュータビジョン向けライブラリ

[wiki引用](https://ja.wikipedia.org/wiki/OpenCV)

画像を扱う便利なオープンソースのライブラリですね。まぁこれもなんとなく想像はできますよね。


## SIFT
**Scale-Invariant Feature Transform**の頭文字を取ってSIFTです。
SIFTは画像認識のためのアルゴリズムの一つで、特徴点の検出や特徴量の記述を行います。
SIFTは画像の照明の変化や回転、スケール変化などに対して不変な特徴量を記述することができます。
その分処理コストがかなり高いそうです。多分シフトって読むと思います。

## SURF
**Speed-Up Robust Features**の頭文字を取ってSURFです。
SURFは処理コストが高かったSIFTの改良版で、精度はSIFTに劣りますが高速にマッチングすることが可能です。
SIFTでは特徴点を検出する方法として、DoG画像生成や勾配ヒストグラム生成などのコストの高い計算をしていましたが、SURFは積分画像を利用することにより約10倍の高速化しています。
多分サーフって読むと思います。

## HOG
**Histograms of Oriented Gradients**の頭文字を取ってHOGです。
HOGは画像を細かいグリッドに分割して、1つ1つのセルごとに方向つき輝度勾配のヒストグラムを連結したものです。メリットとしては、勾配情報をもとにしているため、異なるサイズの画像を対象としても同じサイズにリサイズすることで比較することが可能です。
多分ホグって読むと思います。

## 回帰
普通の日本語ですが、よく出てくるので正確に理解しておきたいと思い調べました。

>回帰（かいき）とは一般にはもとの位置または状態に戻ること、あるいはそれを繰り返すこと。

[wiki引用](https://ja.wikipedia.org/wiki/%E5%9B%9E%E5%B8%B0)

この回帰がつく用語としてよくロジスティック回帰分析という言葉を見かけますね。

## ロジスティック回帰分析
これはよく統計学やマーケティング関連の文脈で出てくる言葉で、YesかNoの二択のどちらかになるかを分析するための分析方法です。もっと言えば0か1、TrueかFalseのように2値をとる場合に有効です。線形回帰分析は量的変数を予測しますが、ロジスティック回帰分析は発生確率を予測する手法ということです。

## SVM
**Support Vector Machine**の頭文字を取ってSVM(サポートベクターマシン)です。

>サポートベクターマシン（英: support vector machine, SVM）は、教師あり学習を用いるパターン認識モデルの一つである。分類や回帰へ適用できる。

[wiki引用](https://ja.wikipedia.org/wiki/%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%83%99%E3%82%AF%E3%82%BF%E3%83%BC%E3%83%9E%E3%82%B7%E3%83%B3)

## KNN
**k-nearest neighbor algorithm**の頭文字を取ってKNNです。
日本語ではk近傍法(ケイきんぼうほう)というようです。某姉貴ではない。

> 基づいた分類の手法であり、パターン認識でよく使われる。最近傍探索問題の一つ。k近傍法は、インスタンスに基づく学習の一種であり、怠惰学習 (lazy learning) の一種である。その関数は局所的な近似に過ぎず、全ての計算は分類時まで後回しにされる。また、回帰分析にも使われる。

[wiki引用](https://ja.wikipedia.org/wiki/K%E8%BF%91%E5%82%8D%E6%B3%95)

## ソフトマックス関数
ソフトマックス関数は活性化関数の一種で、分類問題解く場合に、出力層で用いられる関数です。一般的に分類問題を解く場合はこのソフトマックス関数が用いられるようです。


## 教師データ
機械学習を行う際の訓練用のデータのことです。単に訓練データという時もあるようです。
まんまですね。一応調べたので書きました。

## 損失関数
機械学習のモデルがどれだけ性能が悪いかを表す関数です。現在、教師データとどれだけ適合していないかをこの関数を通して判断することができます。有名なものに2乗和誤差や交差エントロピー誤差などがあります。

まだまだ調べないといけない用語がたくさんありますが、調べごとばかりしていると奥さんに怒られるので今回はこの辺で。
終わり。

