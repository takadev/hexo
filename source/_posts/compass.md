---
title: Compassを使ってみた
date: 2016-12-20 20:50:51
tags:
- "Sass"
- "Compass"
- "フロント"
category: Compass
---
## Compassについて
[前回](http://devlog.site/Sass/sass/)Sassをインストールしてみたので今回はCompassをインストールしてみたいと思います。
<!-- More -->

## はじめに
環境はMacでEl Capitanです。
自分の為の備忘録なので悪しからず。

## Compassとは
Compassとは、オープンソースのCSSフレームワークです。Sassを使ってCSSを書く場合はCompassを併用することが一般的になっています。

## Compassのインストール
Sass同様にgemでインストールできます。

```
$ gem install compass
```

インストールが正常に終わったら、compassコマンドが使用できるようになっているはずです。

```
$ compass -v
Compass 1.0.3 (Polaris)
Copyright (c) 2008-2016 Chris Eppstein
Released under the MIT License.
Compass is charityware.
Please make a tax deductable donation for a worthy cause: http://umdf.org/compass
```

問題なさそうですね。

## Compass使ってみる
早速Compassを使ってみたいと思います。
まずは以下のコマンドを発行するとCompass用のディレクトリや設定ファイルが作成されます。

```
$ compass create
```

こんな感じでディレクトリとファイルが作成されるかと思います。

```
|--config.rb
|--sass
|  |--ie.scss
|  |--print.scss
|  |--screen.scss
|--stylesheets
|  |--ie.css
|  |--print.css
|  |--screen.css
```

sassはsassファイルを格納するディレクトリです。コンパイルされたcssファイルはstylesheetsディレクトリに生成されます。config.rbはCompassの設定ファイルになります。

## Sassファイルの作成
ではsassディレクトリ配下にsassファイルを作成してみましょう。
以下のようにCompassを使用する場合は**@import "compass";**とインポート文を最初に書きます。


```scss
@import "compass";
 
a {
     text-decoration: none;
     &:hover {
          text-decoration: underline;
     }
}
```

次にこのsassをコンパイルしてます。
前回はsassコマンドでコンパイルを行いましたが、今回はcompassコマンドを使用して自動でコンパイルしてみたいと思います。

## Compassの起動
以下のコマンドを発行するとsassコマンドのwatchオプションを指定した挙動と同じように自動でsassファイルを監視し、変更があるたびにコンパイルを行ってくれます。

```
$ compass watch
>>> Compass is watching for changes. Press Ctrl-C to Stop.
DEPRECATION WARNING on line 87 of /Users/hoge/.rbenv/versions/2.3.3/lib/ruby/gems/2.3.0/gems/compass-core-1.0.3/stylesheets/compass/css3/_deprecated-support.scss: #{} interpolation near operators will be simplified
in a future version of Sass. To preserve the current behavior, use quotes:
....
```

これで起動状態となり、scssファイルを更新すると自動でコンパイルが走ります。

## Mixinを利用してみる
ここまでではSassと特に変わらないので便利さがいまいちわからないと思います。
CompassにはMixinがたくさんあり、様々な機能を提供してくれていますのでそれを使わない手はありません。

## Mixinとは
そもそもMixinとは何かというと、MixinとはScss全体で再利用することができる様々なスタイルのことです。また制御構文などで動的にスタイルの構成を変えることができるものです。

Mixinは**@include**を使って次のように指定することができます。

```
div{
@include opacity(.5);
}
```

これは透過を指定するopacity()というMixinです。
コンパイルされたcssを見てみると

```
div {
  filter: progid:DXImageTransform.Microsoft.Alpha(Opacity=50);
  opacity: 0.5;
}
```

各種ブラウザの差異を気にしなくて済みますね。非常に便利です。
これは機能の一部ですので、詳しくは[公式サイト](http://compass-style.org/reference/compass/css3/)をご覧ください。

終わり。