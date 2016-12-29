---
title: スクレイピングしてみた
date: 2016-12-25 00:00:00
tags:
- "Scrapy"
- "python"
- "スクレイピング"
category: python
---
## Pythonでスクレイピングしてみた
今後、機械学習で必要になると思うのでスクレイピングをしてみました。
<!-- More -->

## はじめに
Pythonの環境は[こちらの記事](http://devlog.site/tensorflow/tensorflow1/)で作っています。
Ptyhonのバージョンは3.5.1を使用します。個人の備忘録なので結構雑です。悪しからず。

今回はこちらのサイトを参考にさせて頂きました。
[Scrapy + Scrapy Cloudで快適Pythonクロール+スクレイピングライフを送る](http://data.gunosy.io/entry/python-scrapy-scraping)

## スクレイピングとは
スクレイピングとはWebページのHTMLデータを収集して、特定のデータを抽出、整形し直すことです。

## Scrapyのインストール
Pythonでスクレイピングを簡単に行うためにScrapyをインストールします。Scrapyはクローラーを実装するためのフレームワークです。
詳しくは[公式サイト](https://doc.scrapy.org/en/latest/index.html)を参照下さい。

インストールはpipコマンドを使用します。

```
pip install scrapy
```

インストールできたか確認してみましょう。

```
scrapy version
Scrapy 1.3.0
```

無事インストールできたみたいですね。


## プロジェクトの作成
インストールが終わったので早速スクレイピングしてみたいと思います。
まずはプロジェクトを作成します。

```
scrapy startproject gunosynews
```

コマンドを実行すると以下のようなディレクトリ構成で雛型が作成されます。

```
|--gunosynews
|  |--__init__.py
|  |--__pycache__
|  |--items.py
|  |--middlewares.py
|  |--pipelines.py
|  |--settings.py
|  |--spiders
|  |  |--__init__.py
|  |  |--__pycache__
|--scrapy.cfg
```

プロジェクトが作成できたらまずは**settings.py**を編集します。
**DOWNLOAD_DELAY**項目がコメントアウトされていますので、コメントアウトを外します。

```
DOWNLOAD_DELAY = 3
```

これはクローラーを動かす際の収集間隔です。対象のサイトに間隔をきちんと空けてアクセスするようにします。

次にitems.pyを以下のように編集してwebサイトから取得してくるタイトル、URL、サブカテゴリーのコードを追加します。

```python
import scrapy

class GunosynewsItem(scrapy.Item):
    title = scrapy.Field()
    url = scrapy.Field()
    subcategory = scrapy.Field()
```

items.pyの編集が終わったら次に、スパイダーを自動生成します。
スパイダーとはウェブを巡回しデータを抽出するファイルのことです。巡回開始のアドレスと、巡回条件、データ抽出条件などを指定します。

以下のコマンドでスパイダーが作成できます。

```
scrapy genspider gunosy gunosy.com
```

これでスパイダーが作成できました。**gunosynews/spiders/gunosy.py**が生成されたファイルになります。
これを参考のサイト同様に修正を行います。

```python
# -*- coding: utf-8 -*-
import scrapy

from gunosynews.items import GunosynewsItem


class GunosynewsSpider(scrapy.Spider):
    name = "gunosy"
    allowed_domains = ["gunosy.com"]

    start_urls = (
        'https://gunosy.com/categories/1',  # エンタメ
        'https://gunosy.com/categories/2',  # スポーツ
        'https://gunosy.com/categories/3',  # おもしろ
        'https://gunosy.com/categories/4',  # 国内
        'https://gunosy.com/categories/5',  # 海外
        'https://gunosy.com/categories/6',  # コラム
        'https://gunosy.com/categories/7',  # IT・科学
        'https://gunosy.com/categories/8',  # グルメ
    )

    def parse(self, response):
        for sel in response.css("div.list_content"):
            article = GunosynewsItem()
            article['title'] = sel.css("div.list_title > a::text").extract_first()
            article['url'] = sel.css("div.list_title > a::attr('href')").extract_first()
            article['subcategory'] = sel.css("div.list_text > a::text").extract_first()
            yield article

        next_page = response.css("div.page-link-option > a::attr('href')")
        if next_page:
            url = response.urljoin(next_page[0].extract())
            yield scrapy.Request(url, callback=self.parse)
```

まるまる参考にさせて頂いてますが、これでちゃんと動きます。
各種処理の内容は参考サイトに詳しく説明されています。

## 実際に動かしてみる
以下のコマンドで実行することができるので、早速試してみましょう。

```
scrapy crawl gunosy
```

コンソールに取得したかったタイトル、URL、サブカテゴリーがずらずらっと出力されたかと思います。
スクレイピングが無事に出来ていますね。

参考にさせていただいたサイトではこの後にScrapy Cloudを使用してデータを保存していますが、今回はここまでにします。
今後は機械学習で大量のデータが必要になると思うのでscrapyを使って色々なデータをスクレイピングしてみたいと思います。

終わり。

