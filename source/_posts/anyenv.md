---
title: anyenvについて
date: 2016-12-18 00:00:00
tags:
- "anyenv"
- "ruby"
- "環境"
category: anyenv
---
## anyenvを入れてみた
仕事でRailsを使って簡単なWebアプリを作ることになり、rubyは昔書いてたことがある為なし崩しに自分がやることになりました。rbenvを使ってrubyの管理を行おうと思いましたが、pyenvやndenv、rbenvと~envが増えてきたのでそれを一括管理するanyenvというのを今回使ってみました。
<!-- More -->

##　はじめに
環境はMacでまだEl Capitanです。
簡単な備忘録なんで悪しからず。

## anyenvのインストール
まずはgitでクローンしてきます。

```
git clone https://github.com/riywo/anyenv ~/.anyenv 
```

自分はbashがデフォルトなので.bash_profileを編集します。

```
$ echo 'export PATH="$HOME/.anyenv/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(anyenv init -)"' >> ~/.bash_profile
$ exec $SHELL -l
```

これでインストールは終了です。簡単ですね。

## rbenvをインストールしてみる
インストールできるenv系の一覧をまずチェックしてみましょう

```
nyenv install -l
Available **envs:
  Renv
  crenv
  denv
  erlenv
  exenv
  goenv
  hsenv
  jenv
  luaenv
  ndenv
  nenv
  nodenv
  phpenv
  plenv
  pyenv
  rbenv
  sbtenv
  scalaenv
  swiftenv
```

こんなにたくさんあるんですね。知らなかった。
rbenvももちろんいますね。ではrbenvをanyenvを使ってインストールしてみます。

```
anyenv install rbenv
```

インストールが終わるとシェルを再起動してくれと出ます。

```
exec $SHELL -l
```

これでrbenvのインストールが終わります。

## rbenvでrubyをインストール
rbenvが無事インストールできたので続いてRubyをインストールしてみます。
インストールできるバージョンを確認してみます。

```
rbenv install -l
Available versions:
  1.8.5-p113
  1.8.5-p114
  1.8.5-p115
  1.8.5-p231
  ...
```

今回はRuby2.3.3をインストールしてみます。

```
rbenv install 2.3.3
```

インストールができたか確認してみます。

```
rbenv versions
* system (set by /Users/hoge/.rbenv/version)
  2.3.3
```

2.3.3が入ってますね。このままだとデフォルトのrubyなのでバージョンを切り替えてみましょう。

```
rbenv global 2.3.3
rbenv versions
  system (set by /Users/hoge/.rbenv/version)
* 2.3.3
```

これでバージョンが切り替わりました。

```
ruby -v
ruby 2.3.3p222 (2016-11-21 revision 56859) [x86_64-darwin15]
```

無事切り替わってますね。これでrubyのインストールは終了です。

この際env系で統一してもいいかなと思いました。
終わり。
