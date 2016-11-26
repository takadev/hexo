---
title: TensorFlowの基礎
date: 2016-11-24 00:00:00
tags:
- "TensorFlow"
- "python"
- "機械学習"
category: tensorflow
---
# TensorFlow基礎

今回はTensorFlowの計算処理の流れを見ていきたいと思います。

## TensorFlowの計算処理の流れ

[前回のTensorFlowで四則演算をやってみた](http://devlog.site/tensorflow/tensorflow2/)でも少しだけ書きましたが、
ざっくりオペレーションを先に定義し、セッションを使用してそれを実行するという流れになります。
このオペレーションやセッションとはどんなものなんでしょうか？
<!-- more -->

もう少し詳しく調べてみると、TensorFlowでは計算処理にグラフを用いるとのことです。
グラフというのはエクセルとかでよく見る折れ線グラフや円グラフのことではなく、
[こちらのwikiのグラフ理論](https://ja.wikipedia.org/wiki/%E3%82%B0%E3%83%A9%E3%83%95%E7%90%86%E8%AB%96)のことらしいです。

グラフはノードとエッジから構成されるデータ構造のことです。またTensorFlowにおいてのノードはop\(オペレーション\)と呼ばれ、どうやら一つの計算処理に対応しているとのこと。
オペレーションというのは簡単に言うと何かしらの計算処理を行う一つの処理ブロックということのようです。

このopはTensor\(テンソル\)と呼ばれる行列形式のデータを受け取り、何かしらの計算処理を行い、結果を次のopへ渡していきます。
次のopでも受け取った行列形式のデータを使用し、同じように計算処理を行いさらに次のopへ結果を渡します。
このように次々にopにデータを受け渡し計算処理を行うことで、最終的な結果を得ることができるという流れです。

次に先ほど出てきたエッジについてです。
エッジはノードとノードを繋ぐものでデータをどのノードからどのノードへ受け渡すかを決めるものです。
単純にノードで処理した結果を次にどのノードで処理されるかというだけのようですね。

最後にセッションについてです。
TensorFlowでは各opごとにCPUコアやGPUコアのリソースをどの程度割り当てるかを指定することができます。
パワーを必要とする計算処理には多くのリソースを割り当て、簡単な処理には少ないリソースで済ませるという割り振りができるようでうす。
この割り当てを担うのがセッションのようです。そしてセッションは各opの実行も行います。

簡単なコードを見てみましょう。

```python
import tensorflow as tf

# 定数の定義
const  = tf.constant(2)
const1 = tf.constant(3)
const2 = tf.constant(4)

# add_opノード(op)を定義
add_op  = tf.add(const, const1)
# add_op1ノード(op)を定義、同時にadd_opの結果をadd_op1へ受け渡すエッジ
add_op1 = tf.add(add_op, const2)

# セッション
sess = tf.Session()
# add_opの実行
sess.run(add_op)
# add_op1の実行、結果をresultへ格納
result = sess.run(add_op1)

print(result)
```

足し算を2回行うだけの処理です。実行すると9が出力されると思います。
コメントでコード中に注釈を入れているのでわかると思いますが、
それぞれがノード(op)、エッジ、セッションになります。

これをtensorboardでグラフ出力してみるとこんな感じになります。

オペレーションAddとAdd_1がエッジで繋がれ、AddにはConst、Const_1が、Add_1にはConst_2が入力として渡されているのがわかりますね。
なんとなくTensorFlowの計算処理の流れがわかった気がします！

## TensorBoardについて
先ほど出てきたTensorBoardとは何かというと、TensorFlowに搭載されている可視化ツールのことです。
TensorBoardを使用することでグラフを可視化でき、ブラウザで確認することができます。

TensorBoardでグラフ出力するには以下のコードを追加します。

```python
tf.train.SummaryWriter('./', sess.graph)
```

追記したファイルを実行するとTensorBoard用のファイルが生成されます。
TensorBoard用のファイルが生成されたら、次のコマンドを実行します。


```python
tensorboard --logdir=[TensorBoard用のファイルがあるディレクトリ]
```

ブラウザでlocalhost:6006にアクセスするとTensorBoardが立ち上がっていることが確認できると思います。
TensorBoardは便利な使い方が色々あるみたいなので今後もっと詳しく調べてみたいと思います。

今回はここまでです。
次回はTensorFlowを使う上でもっと基本的な機械学習とは何かについて学んでいこうと思います。
