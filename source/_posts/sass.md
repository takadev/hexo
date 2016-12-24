---
title: Sassを使ってみた
date: 2016-12-19 00:00:00
tags:
- "Sass"
- "CSS"
- "フロント"
category: Sass
---
## はじめに
環境はmacです。OSはEl Capitanです。
rubyのインストールは[以前の記事](http://devlog.site/anyenv/anyenv/)を参照してください。
<!-- More -->

## Sassとは？
SASSとは、CSSを拡張するメタ言語のことです。CSSでは使えなかった変数やネスト、ループなんかもできて非常に便利です。**Syntactically Awesome Style Sheets**の頭文字でSassのようです。

## Sassインストール
早速インストールしてみます。

```
gem install sass
```

gemコマンドで一発でインストールできます。

```
sass -v
Sass 3.4.22 (Selective Steve)
```

簡単ですね。

## Sass使ってみる
簡単なコードを書いてみたいと思います。

### 変数の定義
Sassでは変数が使えます。
$colorが変数で**#00ccff**を指定して宣言しています。

```
$color: #00ccff;

button {
  color: $color;
}
p {
  color: $color;
}
```

### ネスト
CSSではいちいちセレクタを全て指定する必要がありましたが、Sassの場合ネストすることができるので省略できます。

```
.article {
  width: 700px;
  margin: 10 auto;
  background-color: #069fff;
  background-image: url("../img/background.png")
  
  .title {
    color: #ffffff;
  }
  .text .name {
    color: #000000;
  }
}
```

コーディングする時も楽ですしすごく読みやすいですね。

### for文/if文
Sassではfor文やif文もかけます。制御構文の頭には**@for**や**@if**のように**@**をつけます。

```
@for $i from 1 through 10 {
  .sample#{$i} {
    margin: {
      @if $i <= 5 {
        bottom: 10px;
      }
      @else {
        bottom: 20px;
      }
    }
  }
}
```

もっとたくさん便利な機能がありますが、一旦ここまでで、style.scssとしてファイルを保存しておきます。

## コンパイルする
先ほど保存したstyle.scssファイルをコンパイルしてcssへ変換してみます。
Sassのコンパイルの仕方は手動コンパルと自動コンパイルがあります。
まず手動コンパイルをしてみたいと思います。

```
sass style.scss:style.css
```

コンパイルするとstyle.cssファイルが生成されていることがわかると思います。
この状態だとsassを修正するたびにコマンドを発行する必要がありますが、
自動コンパイルを指定しておくとsassを修正すると自動的にコンパイルされcssが更新されます。

```
sass --watch style.scss:style.css
```

**--watch**オプションを指定するとstyle.scssが更新されるたびに自動的にコンパイルしてくれます。
またファイルのみではなくディレクトリを指定することができ、ディレクトリ内のscssファイルを監視してくれます。

終わり。