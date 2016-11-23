---
title: TensorFlowで四則演算をやってみた
date: 2016-11-23 00:00:00
tags:
- "TensorFlow"
- "python"
- "機械学習"
category: tensorflow
---
# TensorFlowで四則演算をやってみた
前回環境を整えたので、今回はTensorFlowで四則演算を行ってみました。

## はじめに
TensorFlow全くの初心者ですので、右も左もわかってません。間違ったこともたくさん書いてると思います。基本的に自分の為にメモしておく程度なのであしからずです。

## 四則演算
まずはTensorFlowで四則演算を行ってみたいと思います。
こんな感じのコードになります。

```
import tensorflow as tf

# 定数宣言
const1 = tf.constant(2)
const2 = tf.constant(3)

# 足し算オペレーション
add_op = tf.add(const1, const2)

# セッションオブジェクト
sess = tf.Session()

result = sess.run(add_op)
print(result)

# 引き算オペレーション
sub_op = tf.sub(const1, const2)
result = sess.run(sub_op)
print(result)

# 掛け算オペレーション
mul_op = tf.mul(const1, const2)
result = sess.run(mul_op)
print(result)

# 割り算オペレーション
div_op = tf.div(const1, const2)
result = sess.run(div_op)
print(result)
```

これを適当な名前\(今回はmath.py\)で保存して実行すると

```
python math.py
5
-1
6
0
```

と出力されます。普通の四則演算のコードと全然違いますよね。
1つずつ解説していきましょう。

1行目

```
import tensorflow as tf
```

これはtensorflow moduleをインポートして、それをtfとして使用するということです。

4行目

```
const1 = tf.constant(2)
```

const1という定数を宣言し、その定数に2を設定しています。

8行目

```
add_op = tf.add(const1, const2)
```

const1とconst2を足し算するオペーレションadd_opを設定

11行目

```
sess = tf.Session()
```

セッションの作成

13行目

```
result = sess.run(add_op)
```

定義したオペレーションの実行

足し算以降の引き算、掛け算、割り算はやってることは同じです。
とこのように、TensorFlowでは最初に演算するオペレーションを定義し、その後でセッションを使用してその演算を行うという流れになります。
基本的な概念は一旦置いておいて、ざっとこんな感じのようです。

ところで気になった方もいるかもしれませんが、割り算の結果が0になってしまっていますね。
2 / 3 なので0.666...になるはず？ですよね。いえ、これは間違いではなく、正しい結果です。
tf.divはリファレンスを見てみると
> テンソルの数値型がint等の浮動小数でない型である場合、小数点以下切り捨て
となっているので小数点以下が切り捨てられてしまって0になっているんですね。

小数点以下を切り捨てたくない場合はtf.truedivを使用してます。

```
div_op = tf.truediv(const1, const2)
result = sess.run(div_op)
print(result)
```

こうすることで正しく0.666...が出力されます。

次回は基礎的な概念を少し学んでみたいと思います。
