---
title: 久々にPHPやってみた
date: 2017-01-12 00:00:00
tags:
- "PHP"
- "プログラミング"
category: プログラミング
---
## PHPのお勉強
折角PHPを書く機会ができたので少し勉強してみようと思います。
ソースコードを読んでてわからなかったところや気になったところ、知らなかったライブラリなど取り留めないですが、色々と調べてみました。
<!-- More -->

## HybridAuth(ハイブリッドオース)
作ってるアプリがOAuth認証のライブラリにこのHybridAuthというのを使っていて、知らなかったので調べました。
HybridAuthは、PHPのOAuthのライブラリでFacebookとかTwitterからMySpaceやLinkedInといった多くのプロバイダに対応してるみたいです。GPL/MITライセンスのオープンソース・ソフトウェアで結構有名みたいです。知らなくってすいません...

公式サイトは[こちら](http://hybridauth.sourceforge.net/index.html)になります。
詳細は公式サイトを見てみて下さい。

ついでにいつも忘れちゃうAuthenticationとAuthorizationの違いについても調べました。
日本語で言うと認証と認可の違いですね。
[このスライド](http://www.slideshare.net/matake/id-openid-technight-vol13?ref=http://oauth.jp/blog/2016/02/25/oauth-authentication/)がすごくわかりやすかったので参考にさせて頂きました。

### Authentication
認証のことです。認証とは正当性を検証することで、例えばユーザ名とパスワードを使って、サイト利用者きちんとその権利があるかどうかや、その人が本人かどうかを確認することですね。
先ほどのスライドから引用させていただくと、

> ブラウザの前のにいるEntityがサービス側が認識するどのIdentityと紐付いているかの確証を得ること。
> 「あの時お越しいただいたお客様ですね」と確証を持って言えればOK。

これがAuthenticationです。

### Authorization
認可のことです。認可とは、ある特定の条件に対しリソースアクセスの権限を与えることやまたはその条件のことを言います。
こちらも先ほどのスライドから引用させていただくと

> リソースにアクセスするための条件を定めること。
> 「20歳以上」とか「社長限定」とか。
> ユーザーの属性がそのリソースにアクセスするに足りるかをチェックすること。

これがAuthorizationです。


## AMF
AMFという単語が出てきて何のことだかわからなかったので調べてみました。
AMFは**Action Message Format**の略でどうやらクライアントとサーバ間で通信する際に使用されるフォーマットのようです。Flexで使用されるバイナリフォーマットのことみたいですね。
このフォーマットを使用することにより軽量で高速にFlexとサーバ間の通信をおこなうことができ、結果としてWebアプリケーションのパフォーマンスを上げることができるとのことです。

PHPではAMFPHPというライブラリがZendFrameworkでサポートされているようで、結構古くから存在して実績もあるようです。

## サブクラス自信をnewする場合
打って変わってPHPの構文についてです。PHPは昔少し書いてたことがありましたが、サブクラス自信をnewする際の構文を今まで全然知らなかったです。お恥ずかしい。

[こちらのQiitaのエントリ](http://qiita.com/armorik83/items/9fc7cfd59abc05bab49a)を参考に実験的に以下のようなコードを書いてみました。

```
class A {
    public static function get_self() {
        return new self();
    }

    public static function get_static() {
        return new static();
    }
}

class B extends A {}

echo get_class(B::get_self());   // A
echo get_class(B::get_static()); // B
echo get_class(A::get_static()); // A
```

サブクラスから**new self()**を行うとサブクラスではなくスーパークラスが帰ってきてしますので、サブクラス自信をnewしたい時は**new static()**という構文を使わないといけないようですね。

## php_uname関数
PHPが稼動しているOSに関する情報を返す関数です。
構文はこんな感じです。

```
string php_uname ([ string $mode = "a" ] )
```

引数によって取得できる情報が違うようです。
詳しくは[こちらのマニュアル](http://php.net/manual/ja/function.php-uname.php)を参照してください。

終わり