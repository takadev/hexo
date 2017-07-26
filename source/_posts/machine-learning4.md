---
title: 機械学習用語3
date: 2017-01-17 00:00:00
tags:
- "機械学習"
- "用語集"
category: 機械学習
---
引き続き
「[イラストで学ぶ　人工知能概論](http://amzn.to/2jE6IKp)」を読んでいます。
半分程度読み終わりました。月1冊の目標は余裕で達成できそうですね。もう1冊ぐらい頑張って読んでみようと思います。
本の自体の内容は分かり易いですし、ストーリー仕立ての話もすごく面白いんでこのままサクッと読んでしまおうと思います。
<!-- More -->

今回も本の中に出てくる用語を忘れないように&復習用にメモしておこうと思います。

## 多段決定問題
ある時点tの状態Stで選択した行動atが利得rt+1(もしくはコスト)をもたらし、次の時点の状態St+1を決め、時点t+1での行動at+1が時点t+2での状態St+2を決める。このようなときに時刻Tまでにかかるコストの和を最小化、もしくは得られる利得の和を最大化する計画問題のこと。

## 動的計画法
多段決定問題に対して効率的に解を求める方法

## 編集距離
文字列と文字列の距離を測る尺度のこと。文字列と文字列の異なり具合を測る尺度とも言える。ハミング距離が文字の挿入や削除に対応できないのに対して、文字の挿入や削除も1つの異なりとしてカウントして距離を算出することができる。どの文字とどの文字が対応するかをずらしながら解かないといけないため、簡単には計算できないストリングマッチング問題がある。動的計画法を用いることで効率的に解ける。

## ハミング距離
編集距離より簡単な文字列と文字列の距離の定義方法。文字列に含まれる文字を一つずつ照合していき、いくつ異なっているかを返す距離関数である。"TANIGUCHI"と"TANIMACHI"であれば2を返す。
ハミング距離では文字の挿入や削除に対応できないので、ハミング距離では直感的な文字の近さは表現できない。

## マルコフ性
ある変数が1ステップ前の変数のみに影響お受けて確率的に変化していく性質を持つ場合、その系列をマルコフ性を持つという。マルコフ性を持つ状態遷移モデルをマルコフモデルともいう。

## 強化学習
試行錯誤を通して報酬を得ることで徐々に行動パターンを学習していく過程をモデル化し、この過程を数学的に表現した理論が強化学習理論である。この得られる報酬を最大化するために、何をするべきかを学習させる手法のこと。

## マルコフ決定過程(Markov Decision Process; MDP)
> 状態遷移が確率的に生じる動的システム（確率システム）の確率モデルであり、状態遷移がマルコフ性を満たすものをいう。 MDPは不確実性を伴う意思決定のモデリングにおける数学的枠組みとして、強化学習など動的計画法が適用される幅広い最適化問題の研究に活用されている。

[wiki引用](https://ja.wikipedia.org/wiki/%E3%83%9E%E3%83%AB%E3%82%B3%E3%83%95%E6%B1%BA%E5%AE%9A%E9%81%8E%E7%A8%8B)


## 割引累積報酬
基本的には将来に渡って得られる報酬の和になっているが、遠い未来であればあるほど割引換算されるようになっている。正味現在価値とも言われる。

## 割引率
将来の報酬をどれほど評価に加味するかを変化させる定数。割引率によって同じ報酬を得ていても割引累積報酬の視点から評価は異なってくる。

## 価値関数
割引累積報酬の期待値を価値関数という。その状態における行動の価値を見積もる関数。方策πの評価は価値関数によって行えば良い。価値関数の値を高める方策が良い方策といえる。

## 状態価値関数
方策πに従った際に、その状態sからスタートして将来どれだけ割引累積報酬が得られるかという値を表している。

## 行動価値関数
状態sにおいて行動aをとった後に方策πに従う場合に得られる割引累積報酬の期待値。

## Q学習（Q-learning）
或る環境状態sの下で、行動aを選択する価値（行動の価値）Q(s,a)を学習する方法となる。

## モンテカルロ法
サンプルを用いて何らかの値を見積もる方法。ここでいうサンプルとは事象に対する結果を乱数で表したもの。例えばサイコロがを10回振った際のそれぞれの目の出た回数。モンテカルロは期待値の評価などに使用される。

終わり

{% iframe //rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=tassoc121-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B00TPL99ZW&linkId=296468de44ed2927abe212a964d48b09 120px 240px %}