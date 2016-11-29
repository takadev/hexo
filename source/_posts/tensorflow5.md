---
title: TensorFlowの基本的なAPI1
date: 2016-11-29 00:00:00
tags:
- "TensorFlow"
- "python"
- "機械学習"
category: tensorflow
---
## TensorFlowのリファレンスを確認してみた

ネットにはTensorFlowのサンプルコードが山ほどあるので読んで勉強したい！と思ったのですが、APIをまだ全然理解していないので今回は基礎的なAPIのリファレンスを確認してみました。
公式のリファレンスは[こちら](https://www.tensorflow.org/api_docs/python/index.html)

Pythonの対話モードでAPIを実行してみました。

```
python
>>> import tensorflow as tf
>>> sess = tf.Session()
```

<!-- More -->

## zeros

```
>>> sess.run(tf.zeros(3))
array([ 0.,  0.,  0.], dtype=float32)

>>> sess.run(tf.zeros([3,3]))
array([[ 0.,  0.,  0.],
       [ 0.,  0.,  0.],
       [ 0.,  0.,  0.]], dtype=float32)

>>> sess.run(tf.zeros([3,3,3]))
array([[[ 0.,  0.,  0.],
        [ 0.,  0.,  0.],
        [ 0.,  0.,  0.]],

       [[ 0.,  0.,  0.],
        [ 0.,  0.,  0.],
        [ 0.,  0.,  0.]],

       [[ 0.,  0.,  0.],
        [ 0.,  0.,  0.],
        [ 0.,  0.,  0.]]], dtype=float32)

>>> sess.run(tf.zeros([3,3], dtype=tf.int32))
array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]], dtype=int32)

>>> sess.run(tf.zeros([3,3], "int32"))
array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]], dtype=int32)
```

0埋めされたTensorを作成してくれるAPIですね。
第二引数でdtype=の後にデータタイプを指定できるようです。
dtype=ではなく文字列として"int32"としてもいいみたいです。
指定しないとデフォルトでtf.float32データタイプになるようです。

## zeros_like

```
>>> sess.run(tf.zeros_like(0))
0

>>> sess.run(tf.zeros_like([1]))
array([0], dtype=int32)

>>> sess.run(tf.zeros_like([1,2]))
array([0, 0], dtype=int32)

>>> sess.run(tf.zeros_like([[1,2],[3,4]]))
array([[0, 0],
       [0, 0]], dtype=int32)

>>> sess.run(tf.zeros_like([[1,2],[3,4],[5,6]]))
array([[0, 0],
       [0, 0],
       [0, 0]], dtype=int32)

>>> sess.run(tf.zeros_like([[1,2],[3,4]], "float32"))
array([[ 0.,  0.],
       [ 0.,  0.]], dtype=float32)
```

zeros_likeは第一引数と同じ要素数のTensorを0埋めして作成してくるようです。
zerosと同様にデータタイプの指定もできますね。ただzerosの場合はデフォルトでtf.float32だったのが、
zeros_likeはデフォルトはtf.int32になっていますね。なんでだろう？？

## ones

```
>>> sess.run(tf.ones([3]))
array([ 1.,  1.,  1.], dtype=float32)

>>> sess.run(tf.ones([3,3]))
array([[ 1.,  1.,  1.],
       [ 1.,  1.,  1.],
       [ 1.,  1.,  1.]], dtype=float32)
```

基本的にzerosと同様ですね。
zerosが0に対してonesは1埋めされたTensorを作成してくるAPIですね。
データタイプの指定も前述のAPIと同様のようですね。

## ones_like

```
>>> sess.run(tf.ones_like(0))
1

>>> sess.run(tf.ones_like([1]))
array([1], dtype=int32)

>>> sess.run(tf.ones_like([1,2], "float32"))
array([ 1.,  1.], dtype=float32)
```

こちらもzeros_likeと同様で要素が0でなく1で埋められているだけの違いですね。

## fill

```
>>> sess.run(tf.fill([],3))
3

>>> sess.run(tf.fill([3],3))
array([3, 3, 3], dtype=int32)

>>> sess.run(tf.fill([3,3],3))
array([[3, 3, 3],
       [3, 3, 3],
       [3, 3, 3]], dtype=int32)

>>> sess.run(tf.fill([3], 3.5))
array([ 3.5,  3.5,  3.5], dtype=float32)
```

fillは第一引数で指定した要素数のTensorを第二引数で指定した値で埋めて返してくれるAPIのようです。


## constant
```
>>> sess.run(tf.constant(1.5))
1.5

>>> sess.run(tf.constant([1]))
array([1], dtype=int32)

>>> sess.run(tf.constant([1.5, 2]))
array([ 1.5,  2. ], dtype=float32)

>>> sess.run(tf.constant([[1.5, 2],[3, 4]], "float32"))
array([[ 1.5,  2. ],
       [ 3. ,  4. ]], dtype=float32)
       
>>> sess.run(tf.constant(1.5, "float32",[2,2]))
array([[ 1.5,  1.5],
       [ 1.5,  1.5]], dtype=float32)
```

定数のTensorを生成するAPIのようですね。
第三引数にSharpを指定することも出来ます。

極々基礎的なAPIを確認してみました。今後も使っていてわからないものや気になったAPIをチェックしていきたいと思います。
