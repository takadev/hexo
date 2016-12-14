---
title: Revelフレームワークpart2
date: 2016-12-14 00:00:00
tags:
- "Go"
- "Revel"
- "プログラミング"
category: Go
---
## Revel入門
折角Revelフレームワークでサンプルアプリを作ったので、もう少し勉強してみようと思います。
フレームワークのインストールは[前回の記事](http://devlog.site/Go/go2/)を参照して下さい。
<!-- More -->

## テンプレートをいじってみる
まずは見た目を少しいじってみたいと思います。

```
myapp/app/views/App/Index.html
```

viewのファイルの拡張子は.htmlなんですね。
中身を見てみると

```html
{{set . "title" "Home"}}
{{template "header.html" .}}

<header class="jumbotron" style="background-color:#A9F16C">
  <div class="container">
    <div class="row">
      <h1>It works!</h1>
      <p></p>
    </div>
  </div>
</header>

<div class="container">
  <div class="row">
    <div class="span6">
      {{template "flash.html" .}}
    </div>
  </div>
</div>

{{template "footer.html" .}}
```

こんな感じになってるんですね。テンプレートエンジンはちょっとクセがありそうに見えるけどどうなんでしょう。中身を見てみましょう。

## テンプレート関数
Index.htmlの1行目に

```
{{set . "title" "Home"}}
```

とありますが、これはRevelのテンプレート関数であるset関数を呼び出す構文になります。
これはtitleに"Home"という文字列をアサインするという意味です。
ただtitleはIndex.html内には見当たりません。
どこにあるかというと別のファイルの

```
myapp/app/views/header.html
```

になります。
header.htmlを見てみると`\{\{.title\}\}`と埋め込まれる箇所が用意されているのがわかりますね。

```html
<title>{{.title}}</title>
```

この`\{\{.title\}\}`にset関数で指定した"Home"がアサインされます。
ブラウザから確認するとタイトルがHomeになっていることが分かるかと思います。

2行目は別ファイルを読み込む処理になります。

```
{{template "header.html" .}}
```

こちらもテンプレート関数であるtemplate関数を呼び出す構文です。ここではheader.htmlを読み込んでいますね。こうすることでいろんなページで共通のヘッダーやフッターを1つにまとめて読み込むことができますね。

このようにテンプレート側からも関数を呼び出すことで色々な処理が書けそうです。
どんな関数があるかは[こちらの公式](https://revel.github.io/manual/templates.html)から確認することができます。

## Viewに変数をアサインしてみる
テンプレート内からのアサインはset関数できますが、コントローラーからのアサインはどのようにやるのか調べてみました。
修正するファイルはTOPページのコントローラである

```
myapp/app/controllers/app.go
```

こちらのファイルになります。
app.goファイルを以下のように編集しました。

```go
func (c App) Index() revel.Result {
	hello := "Hello"
	return c.Render(hello)
}
```

これでコントローラ内からViewにhelloという変数がアサインできました。次にView側でそれを表示してみたいと思います。
Index.htmlに`\{\{.hello\}\}`を追加します。

```html
<h1>{{.hello}}</h1>
```

ブラウザで確認するときちんとHelloと表示されていることがわかりますね。

終わり。