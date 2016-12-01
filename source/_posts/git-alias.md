---
title: gitエイリアス
date: 2016-12-01 00:00:00
tags:
- "git"
- "alias"
category: git
---
## gitエイリアス

gitはたくさんのコマンドがあってオプションも盛りだくさんなので毎度忘れてしまうし、いちいち打つのが大変なのでそんな時はgitエイリアスが便利です。

## .gitconfigファイルで指定
.gitconfigファイルに以下のようにaliasセクションに`短縮形 = 展開形`というふうに書きます。

<!-- More -->

```
[alias]
    ai = add -i
```

こんな感じで書きます。

## 設定しているエイリアス

私が設定しているエイリアスですが、ちゃんと見返すと全然使ってないものも結構ありましたw

```
ai	 => add -i
al	 => !git config --get-regexp '^alias\.' | sed 's/alias\.\([^ ]*\) \(.*\)/\1\	 => \2/' | sort
br	 => branch
ch	 => checkout
cl	 => clean
co	 => commit
cp	 => cherry-pick
d1	 => diff HEAD~
d2	 => diff HEAD~2
d3	 => diff HEAD~3
dc	 => diff --cached
dn	 => diff --name-only
fi	 => !git ls-files | grep -i
fa	 => fetch --all --prune
fe	 => fetch
gr	 => log --graph --all --date=short --pretty=format:'%Cgreen%h %cd %Cblue%cn %Creset%s %Cred%d%Creset'
ll	 => log --name-status --pretty=oneline
rs	 => reset
re   => rebase
sh	 => show
sl	 => stash list
sp	 => stash pop
ss	 => stash save
st	 => status
sts	 => status -s
```

この機会に少し見直してみようと思います。

## どんなエイリアス設定したか忘れてしまったとき
色々なエイリアスを設定しているとたまにしか使わないのは忘れがちになってしまうのでそんなときに役に立つのがこれ

```
al  => !git config --get-regexp '^alias\.' | sed 's/alias\.\([^ ]*\) \(.*\)/\1\ => \2/' | sort
```

エイリアスの一覧を表示してくれるエイリアス。.gitconfigをいちいち確認しなくていいので便利です。

その他にもたくさん便利な使い方があるのでエイリアスはどんどん設定して効率化していきたいですね。
