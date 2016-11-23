---
title: TensorFlowの環境を作ってみた
date: 2016-11-22 00:00:00
tags:
- "TensorFlow"
- "python"
- "機械学習"
category: tensorflow
---
# TensorFlowの環境を作ってみた

機械学習の勉強を始めようと思い、今回はTensorFlowの環境を作成してみました。

## 前提
私の環境はmacでOS X El Capitanです。まだmacOS Sierraにはあげてません...
TensorFlowのバージョンは0.10を使用します。
HomeBrewを使用しますので予めインストールしておいて下さい。

## pythonのインストール
TensorFlowではpythonを使用するので事前にインストールしておきます。
macには一応デフォルトでpythonがインストールされえていますが、TensorFlow用に別バージョンのpythonを使用したいと思います。
インストールにはバージョン管理が便利なpyenvを使用しますので先にこちらをインストールしておきます。

```
brew install pyenv
```

~/.bash_profileに以下を追加します。

```
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
```

pyenvのインストールが終わったら現在使用されているpythonを確認してみましょう

```
pyenv versions
* system (set by /Users/hoge/.pyenv/version)
```

macのデフォルトのpythonになっていますね。
それではpythonをインストールしてみましょう。今回は2.7.11と3.5.1をインストールしてみます。

```
pyenv install 2.7.11
pyenv install 3.5.1
```

インストールが終わったら、対象のバージョンが追加されているか確認してみましょう。

```
pyenv versions
* system (set by /Users/hoge/.pyenv/version)
  2.7.11
  3.5.1
```

2.7.11と3.5.1が追加されていることがわかりますね。
ただしこのままだとmacにデフォルトで入っているpythonを使用する設定になっていますのでバージョンの切り替えを行います。

```
pyenv global 2.7.11
pyenv versions
  system
* 2.7.11 (set by /Users/hoge/.pyenv/version)
  3.5.1
```

globalでバージョンの切り替えを行うことができます。systemに付いていた✳︎マークが2.7.11のところに付いているのがわかると思います。これで2.7.11へ切り替わりました。

## pyenv-virtualenvのインストール
今回はTensorFlow用の仮想環境を作成してその上でTensorFlowを動かしてみたいと思います。
仮想環境作成に便利なpyenv-virtualenvを使用します。まずはインストールから。

```
brew install pyenv-virtualenv
```

インストールはbrewコマンドで1発で済みます。楽チンですね。

## 仮想環境の作成
pyenv-virtualenvのインストールが終わったら早速、仮想環境を作成してみたいと思います。

```
pyenv virtualenv [pyenvのバージョン] [仮想環境名]
```

このコマンドで仮想環境が作れます。
今回はTensorFlowのバージョン0.10を使用するので仮想環境名はtensorflow0.10として作成してみます。

```
pyenv virtualenv 2.7.11 tensorflow0.10
```

作成が終わったらpyenv versionsコマンドをた実行してみましょう

```
pyenv versions
  system
* 2.7.11 (set by /Users/hoge/.pyenv/version)
  2.7.11/envs/tensorflow0.10
  3.5.1
  tensorflow0.10
```

2.7.11/envs/tensorflow0.10とtensorflow0.10が追加されていることがわかりますね。pyenv globalコマンドでバージョンを切り替えましょう

```
pyenv global tensorflow0.10
```

ここまでで仮想環境の作成が終了です。
仮想環境へ入るにはアクティベートコマンドを実行します。

```
pyenv activate
```

これで仮想環境へ入ることができます。仮想環境から出る場合は以下のコマンドを実行します。

```
pyenv deactivate
```

## TensorFlowのインストール
ここからは先ほど作成した仮装環境上で行って下さい。
TensorFlowのインストールにはPyPIを使用します。PyPIはPythonのパッケージ管理ツールで、今回使用するpython2.7.11にはデフォルトでインストールされています。
コマンドはpipになります。

```
pip -V
pip 9.0.1 from /Users/hoge/.pyenv/versions/2.7.11/envs/tensorflow0.10/lib/python2.7/site-packages (python 2.7)
```

PyPIを使用してTensorFlowをインストールするのですが、TensorFlowはPyPIのパッケージには登録されていないのでURLを指定してインストールを行います。

またTensorFlowにはPC環境に応じたバージョンがいくつかあり、ご自身のPC環境に応じたバージョンを使用して下さい。
[TensorFlow Pip installation](https://www.tensorflow.org/versions/r0.10/get_started/os_setup.html#pip-installation)こちらから確認できます。

PC環境の違いはGPUがあるかないか、OSはLinuxかMacか、pythonは2.7か3.4もしくは3.5
かといった違いです。
私の場合はGPUなし、Mac、python2.7になりますので以下のようにインストールを行いました。

```
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-0.10.0-py2-none-any.whl
pip install --upgrade $TF_BINARY_URL
```

これでTensorFlowのインストールは終了です。

##  TensorFlowの動作確認
動作確認は[公式サイト](https://www.tensorflow.org/versions/r0.10/get_started/os_setup.html#test-the-tensorflow-installation)にもあるようにコマンドラインからpythonコマンドで行います。

```
$ python
...
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print(sess.run(a + b))
42
>>>
```

これで無事にTensorFlowが動作していることが確認できました。
今後はこのTensorFlowで遊んでみたいと思います。
