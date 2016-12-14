---
title: Go言語インストール
date: 2016-12-12 00:00:00
tags:
- "Go"
- "プログラミング"
category: Go
---
## Go入門
仕事でGoを使う必要があったので、今更ながらGoを勉強してみたいと思います。
<!-- More -->

## はじめに
環境はMacです。自分の為の備忘録ですので悪しからず。

## gvmインストール
gvmでGoの管理をしたいと思います。
gvmのインストールには以下を実行します。

```
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```

インストールが終わったらコンソールの指示に従って以下を実行します。

```
source ~/.gvm/scripts/gvm 
```

ちゃんと動くか確認します。

```
$ gvm version
Go Version Manager v1.0.22 installed at /Users/hoge/.gvm
```

大丈夫そうですね。

## Goのインストール
インストールできるバージョンの一覧を確認します。


```
gvm listall
   go1
   go1.0.1
   go1.0.2
   go1.0.3
   go1.1
   go1.1.1
   ...
```

今回は1.7.4をインストールしてみたいと思います。

```
gvm install go1.7.4
```

と、途中でエラーが出てしまいました。

```
$ gvm install go1.7.4
Downloading Go source...
Installing go1.7.4...
 * Compiling...
ERROR: Failed to compile. Check the logs at /Users/hoge/.gvm/logs/go-go1.7.4-compile.log
ERROR: Failed to use installed version
```

エラーログの中身を確認するとgoの1.4がないって怒られている様子。
なので先に1.4.3をインストールしてみます。

```
gvm install go1.4.3
```

go1.4.3は素直にインストールができました。

```
gvm use go1.4.3
```

バージョンを1.4.3に切り替えて再度1.7.4をインストールしてみるとソースのダウンロードに結構時間がかかりましたが、無事にインストールが終わりました。

```
$ gvm list

=> go1.4.3
   go1.7.4
   system
```

ちゃんとインストールされていますね。
このままだと1.4.3になっているので1.7.3に切り替えます。


```
gvm use go1.7.4 --default
```

ちゃんと切り替わっていますね。

```
$ gvm list

   go1.4.3
=> go1.7.4
   system
```

無事Goのインストールができました。
この後、少しGoで遊んでみました。

## Goのimportの書き方
Goを書き始めてまず気になったimportの書き方についてです。
Githubからパッケージをそのままインポートできたりしてすごく便利なんですが、結構色々な書き方があるみたいなので調べてみました。

### ファイルからの相対パスで指定

```
import "./model"
```

### GOPATHからの絶対パスで指定

```
import "shorturl/model"
```

### グループ化して複数指定

```
import (
    "fmt"
    "string"
)
```

### ドットをパッケージの前に書く

```
import (
    . "fmt"
    "string"
)
```

**fmt.Println("hello world")**と書くところをドットをつけると**Println("hello world")**とパッケージ名を省略することができます。

### エイリアスを付ける

```
import (
    f "fmt"
)
```

パッケージ名の前にエイリアスを指定することで、**fmt.Println("hello world")**と書くところ**f.Println("hello world")**と書くことができます。
パッケージ名が同じ他のパッケージを使用したい場合などにエイリアスを指定して別名を付けてあげる場合などに使用します。


### アンダースコアをパッケージの前に書く

```
import (
    "database"
    _ "github.com/go-sql-driver/mysql"
)
```

対象のパッケージのinit関数だけ実行されます。
これはブランク識別子というもので、importした対象のパッケージと依存関係のある他のパッケージをimportするときに指定します。


Goについても今後少しづつ勉強していこうと思います。
終わり。


