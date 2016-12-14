---
title: matplotlibを少しだけ
date: 2016-12-03 00:00:00
tags:
- "matplotlib"
- "python"
- "プログラミング"
category: python
---
## matplotlibについて調べてみた
引き続き「ゼロから作るディープラーニング」を読んでいます。
まだまだ序盤ですが、そこで出てきたのがmatplotlib。どんなものか調べてみました。
自分の為の簡単なメモですのであしからず。
<!-- More -->

## matplotlibとは
Pythonでグラフを描画するときに便利なライブラリです。
NumPyなどと組み合わせてデータの可視化に使われます。Pythonで機械学習やる場合は必須なライブラリみたいです。

[公式のギャラリー](http://matplotlib.org/gallery.html)を見ると色々できる見たいですね。

## 試してみた
早速試してみた。[前回](http://devlog.site/python/numpy/)ディープラーニングの勉強の為に環境は作ってあるので既にインストールは終わっています。

簡単なsin関数をグラフに描画してみました。

```
In [1]: import numpy as np
In [2]: import matplotlib.py
matplotlib.pylab      matplotlib.pyparsing  matplotlib.pyplot     
In [2]: import matplotlib.pyplot as plt
In [3]: x = np.arange(0, 6, 1)
In [4]: y = np.sin(x)
In [5]: plt.plot(x, y)
Out[5]: [<matplotlib.lines.Line2D at 0x110738e10>]
In [6]: plt.show()
```

`show()`を実行するとグラフが描画されます。

次に線グラフではなくプロットにしてみましょう。
`plot()`の第三引数にオプションを指定できるみたいで、`"o"`とすることでプロットのグラフになります。

```
In [3]: x = np.random.randn(30)
In [4]: y = np.sin(x) + np.random.randn(30)
In [5]: plt.plot(x, y, "o")
Out[5]: [<matplotlib.lines.Line2D at 0x110709e48>]
In [6]: plt.show()
```

簡単にグラフが描画できましたね。

## タイトルや軸にラベルをつけてみた
グラフにタイトルや軸の名前をつけることもできるみたいです。

```
In [1]: import numpy as np
In [3]: import matplotlib.pyplot as plt
In [4]: x = np.arange(0, 6, 0.1)
In [5]: y1 = np.sin(x)
In [6]: y2 = np.cos(x)
In [7]: plt.plot(x, y1, label="sin")
Out[7]: [<matplotlib.lines.Line2D at 0x110723160>]
In [8]: plt.plot(x, y2, linestyle="--", label="cos")
Out[8]: [<matplotlib.lines.Line2D at 0x110723cf8>]
In [9]: plt.xlabel("x")
Out[9]: <matplotlib.text.Text at 0x10a2be0b8>
In [10]: plt.ylabel("y")
Out[10]: <matplotlib.text.Text at 0x1106e2780>
In [11]: plt.title('sin & cos')
Out[11]: <matplotlib.text.Text at 0x1106f95c0>
In [12]: plt.legend()
Out[12]: <matplotlib.legend.Legend at 0x110723c18>
In [13]: plt.show()
```

`plt.savefig("イメージ名.png")`とすることでファイルとして保存することもできるみたいです。

## 画像の読み込み
matplotlibのimageモジュールを使用することで画像を読み込むこともできるようです。
先ほど保存した画像を読み込んでみたいと思います。

```
In [29]: from matplotlib.image import imread
In [30]: img = imread("イメージ名.png")
In [31]: plt.imshow(img)
Out[31]: <matplotlib.image.AxesImage at 0x1115d0b38>
In [32]: plt.show()
```

もっと複雑なことが色々できるみたいですが、一旦この辺りで終わり。


