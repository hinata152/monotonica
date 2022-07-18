+++
title = "VisItでの可視化メモ"
hascode = false
date = Date(2022, 7, 18)
rss = "解析結果をVisItで可視化するときのメモ。"
tags = ["tech"]
+++

# VisItでの可視化メモ

解析結果をVisItで可視化するときのメモ。

\toc

## 背景

これまでの準1次元ノズルフロー問題では、結果を確認するのにおもにx-yグラフでのプロットを用いてきた。
準1次元流れを扱っているうちはこれで良いのだけど、将来的により複雑な流れを取り扱うさいには流れの2次元性を考慮してそれをプロットしてやる必要がある。

準1次元でない流れ場の一例として、文献 [^1] に近い問題設定がされた[2次元版のコード](https://www.jsass.or.jp/publications/733/)では、2次元の流れ場データをTecplot形式で出力するようになっている。
このファイルを手元で可視化できるようにすることを考える。なお当然ながらTecplotを使うのがストレートなやり方であるものの、ここでは取り扱わない。

## 技術選定

（ゆくゆくは3次元場を扱うかもしれないが）まずは2次元場で考えると、手頃に使えそうなJuliaパッケージとして[Makie](https://makie.juliaplots.org/stable/)があるものの、[contour](https://makie.juliaplots.org/stable/examples/plotting_functions/contour/)の[Examples](https://makie.juliaplots.org/stable/examples/plotting_functions/contour/#examples)を見るに直交座標系が前提となっている様子だった。
[Plots](https://docs.juliaplots.org/latest/)パッケージの[Contours](https://docs.juliaplots.org/latest/gallery/gr/generated/gr-ref22/#gr_demo_22)も同様に直交座標系が前提の様子だった。

そのほかに[Dash](https://dash.plotly.com/julia/vtk/intro)というパッケージを見つけて、これは3次元での可視化ができそうな様子だったが、今やりたいこととは少しずれているような気がしたので見送り。

Juliaで直接可視化するのは一旦は諦めて、Juliaから出力したファイルを別のソフトで可視化する方針を探ることにした。（これだとFortranでやっていることと変わらなくなってしまうので少し残念）

[2次元版のコード](https://www.jsass.or.jp/publications/733/)提供元が用意した[注意書き](https://www.jsass.or.jp/wp-content/uploads/2018/11/ReadMeFirst-LavalNozzle.pdf)によれば、結果の可視化において**フリーソフトではVisItの利用実績があります**とある。

[VisItの公式サイト](https://visit-dav.github.io/visit-website/)を見ると種々の可視化事例とともに、GitHubでソースコード管理がなされていることがわかった。また[過去のブログ記事](https://visit-dav.github.io/visit-website/admin/VisIt-20yrs-ctr/)を読むと、新しい技術を積極的に導入しつつ開発が進められている様子もわかった。こうした姿勢に賛同できたこと、また技術のスジの良さが感じられたことから、今回はVisItを使わせてもらうことにした。

## 導入と結果

VisItをインストールして、[2次元版のコード](https://www.jsass.or.jp/publications/733/)のうちノズル内流れの解析より得られたTecplot形式の出力データ`tec-ln.plt`を読み込ませたところ、それらしき可視化図を表示させることができた。

![](/pages/img/2022-07-18-17-14-15.png)

- いくつかの変数のうちマッハ数を可視化している。流入部分で亜音速の流れがスロート部に向けて加速し、スロート部でマッハ数1をとったあと、スロート以降の拡大管部分で更に加速している。
  - contourではなくてPseudocolorにすることで2次元場に色が付いた。細かい設定はまだよくわからない。
- 可視化はできたけれども、さらに複雑な後処理までVisIt上でこなせるかどうかは要確認。

[^1]: John D. Anderson, "Computational Fluid Dynamics: The Basics With Applications," McGraw-Hill Inc. (1995)
