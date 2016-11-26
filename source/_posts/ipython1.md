---
title: IPython使ってみた
date: 2016-11-26 00:00:00
tags:
- "python"
- "TensorFlow"
category: python
---
## IPython使ってみた

TensorFlowを勉強してて出てきたIPythonという言葉...なんかだよく分からなかったので調べてみました。

## IPythonとは？
「あいぱいそん」って読むらしいです。
Wikiを見てみると
<!-- More -->

>IPython (あいぱいそん) はPythonを対話的に実行するためのシェルである。オリジナルのPythonに比較して、型推定を強化し、対話的実行のための文法を追加してあり、コード・ハイライティングおよびタブによる補完が行える。

とあります。要するに、IPythonは対話的に実行できてタブ補完とかしてくれて色とかついて見やすい便利なやつってことっぽいです。
まぁ使ってみた方が早そうですねw

## インストール
私の環境はmacでOS X El Capitanです。
pythonのバージョンは2.7.11です。

```
python -V
Python 2.7.11
```

インストールにはpipコマンドを使用します。

```
pip install ipython
```

## 起動してみる
インストールが終わったら早速起動してみましょう。

```
ipython
```

起動したら`import t`と入力してTABキーを押してみましょう。
すると

```
In [1]: import t
   tabnanny        terminalcommand this            tkColorChooser  tkSimpleDialog  traceback        
   tarfile         termios         thread          tkCommonDialog  toaiff          traitlets        
   telnetlib       test            threading       tkFileDialog    token           ttk             >
   tempfile        tests           time            tkFont          tokenize        tty              
   tensorflow      textwrap        timeit          tkMessageBox    trace           turtle           
```

こんな感じで候補の一覧が出てきます！これは便利！
ちゃんとインポートしたモジュールの中も補完してくれます。

```
In [2]: tf.ze
              tf.zeros             tf.zeros_like                                           
              tf.zeros_initializer tf.zeta                   
```

今まではpythonコマンドで対話的に実行してたんですが、これは便利ですね。

## 便利な機能

### イントロスペクション

オブジェクトに?をつけてやると対象の情報が表示されます。

```
In [1]: ipython = "Great!"
In [2]: ipython?
Type:        str
String form: Great!
Length:      6
Docstring:  
str(object='') -> string

Return a nice string representation of the object.
If the argument is a string, the return value is the same object.
```

また関数に??をつけるとソースコードも表示されるようです。

```
In [1]: get_ipython??
Signature: get_ipython()
Source:   
    def get_ipython(self):
        """Return the currently running IPython instance."""
        return self
File:      ~/.pyenv/versions/2.7.11/envs/tensorflow0.10/lib/python2.7/site-packages/IPython/core/interactiveshell.py
Type:      instancemethod
```

### マジックコマンド
マジックコマンドはIPythonの用の便利コマンドで頭に%がつくものです。
公式のドキュメントは[こちら](http://ipython.readthedocs.io/en/stable/interactive/magics.html)

便利そうなコマンドがたくさんありますね。

|コマンド|	説明|
|:------|:--------|
|%lsmagic|	利用できるマジックコマンドを表示する|
|%hist |または %history	コマンドの履歴を表示する|
|%paste|	クリップボードのコードをペーストして実行する|
|%run	|ファイルに保存されているスクリプトを実行する|
|%time	|単一ステートメントの実行時間を測定し表示する|
|%timeit|	ステートメントを複数回実行して平均実行時間を表示する|
|%save	|コマンドの実行履歴をファイルに保存する|
|%reset|	変数や名前空間などをクリアする|

特に%saveは良さそうですね。IPythonでああでもない、こうでもないって適当に試した履歴をファイルに保存しておきたいってことは多そうです。

```
In [21]: %save save.py 1-20
```

こんな感じでファイルに保存できるようです。


## 終了
終了するときはexitで抜けられます。

```
In [1]: exit
```

## TensorFlowのInteractiveSession
今後IPythonをTensorFlowの勉強に使いたいと思いますが、そんな時に便利なのが、InteractiveSessionです。
TensorFlowはまずグラフを作り、Sessionを実行するという流れですが、対話的に作業する際にはグラフを作り終えない状態で、Sessionで実行してみたい場合があります。
そこでInteractiveSessionを使うと途中で色々と確認しながら作業を進められるということですね。
