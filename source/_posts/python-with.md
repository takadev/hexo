---
title: Pythonのwith構文について調べてみた
date: 2016-11-27 00:00:00
tags:
- "python"
- "プログラムミング"
category: python
---
## with構文について
TensorFlowでpython書いてるとよく見かけるwith構文ですが、きちんと理解していなかったのでこの機会に調べてみました。
簡単なメモです。
<!-- More -->

## with構文とは？
with構文はファイルの読み書きなど後処理が必要なものに対して安全にその処理を行える機能です。
簡単なファイルを開くコードを見てみましょう。

まずはwith構文を使っていないコード

```python
text = None
try:
  text = open("text.txt", 'w')
  try:
    text.write("Hello, world!")
  except:
    raise
finally:
  if text:
    text.close()
```

厳密に書こうとすると結構大変ですよね。
次にwithを使った書き方についてですが、

```python
with ファイル読み込み as 変数:
    ...
```

こんな感じの構文になります。
先ほどのファイルを開くコードを書き換えると

```python
with open("text.txt", 'w') as text:
    text.write("Hello, world!")
```

すっきりしましたね。これだけでwithを抜けた際にファイルを自動的に閉じてくれます。

## withが使えるオブジェクト
with構文はコードをスッキリ簡潔にしてくれるのでいろんなところで使いたいですが、
使える場合とそうでない場合があります。

withが使えるのは__enter__メソッドと__exit__メソッドの両方が定義されているオブジェクトの場合です。
例えばこんなコードを実行してみます。

```python
class Test():

    def __init__(self):
        print '__init__'

    def __enter__(self):
        print '__enter__'
        return self

    def __exit__(self, *args, **kwargs):
        print '__exit__'

    def __del__(self):
        print '__del__'

    def say(self):
        print 'hello'

with Test() as obj:
    obj.say()

print 'end'
```

結果は次のようになります。

```
__init__
__enter__
hello
__exit__
end
__del__
```

withを使うと__enter__メソッドと__exit__メソッドが呼び出されているのがわかると思います。
withを使いたい時は__enter__メソッドと__exit__メソッドをきちんと定義してあげましょう。

## TensorFlowでよく使うwith
ファイルを開く際に安全にcloseしてくれるwith構文ですが、TensorFlowではよくセッションを使用する際に使われていますね。
ということはSessionを安全に閉じてくれてるってことです。

なんでwith構文が使われているんだろうなぁと思っていましたが、そういった理由があったんですね。
TensorFlowのリファレンスを見てみるとSessionクラスには確かに__enter__メソッドと__exit__メソッドが定義されています。

> tf.Session.\__enter\__()
> tf.Session.\__exit\__(exec_type, exec_value, exec_tb)

## withのネスト
withはネストも出来るみたいです。

```python
with A() as a:
    with B() as b:
```

このようにネストして書くこともでき、またカンマで繋げても同じ意味になるようです。

```python
with A() as a, B() as b:
```

終わり
