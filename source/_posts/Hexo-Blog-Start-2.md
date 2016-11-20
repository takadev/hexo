---
title: Hexoでブログをはじめてみた中編
date: 2016-11-20 00:00:00
tags:Hexo
---

[Hexoでブログをはじめてみた-前編](http://devlog.site/2016/11/19/Hexo-Blog-Start/)の続きです。

ビルトインサーバでブログを立ち上げることができたと思います。
次にGithub Pagesへブログを公開してみましょう。

### 設定ファイルの修正とプラグインのインストール

Github Pagesへの公開には設定ファイルの修正が必要です。
_config.ymlファイルを修正します。

```
vim _config.yml

deploy:
  type: git
  repo: git@github.com:<アカウント名>/<アカウント名>gituhub.io.git
  branch: master
```

設定ファイルの修正が終わったらGithubデプロイ用のプラグインをインストールします。

```
npm install hexo-deployer-git --save
```

## Github Pagesに公開
ここまで終わったらあとはデプロイするだけです。

```
hexo d -g
```

このコマンドを叩くと1発でGithub Pagesに公開することができます。

## テーマの変更
Github Pagesへの公開はできましたが、このままだとHexoデフォルトのテーマのままなので変更してみたいと思います。
今回はGithubに公開せれている[hexo-theme-icarus](https://github.com/ppoffice/hexo-theme-icarus)を使用してみました。
テーマはGithubに公開されているもの多いので気に入ったもので試してみて下さい。

まずGitからcloneしてきます。

```
git clone git@github.com:ppoffice/hexo-theme-icarus.git theme/icarus
```

clone後、icarus内の設定ファイルをリネイムします。

```
cd theme/icarus
mv _config.yml.example _config.yml
```

次にHexoの設定ファイルを編集します。
設定ファイルのthemeを書き換えます。

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: icarus
```

themeをデフォルトのlandscapeからicarusへ変更します。
ここまで終わったら1度Githubへデプロイします。

```
hexo d -g
```

これでテーマが変わっていることが確認できると思います。
今回はここまでで、次回は記事の作成とテーマのカスタマイズを行います。
