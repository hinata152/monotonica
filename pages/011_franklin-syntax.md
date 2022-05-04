+++
title = "Franklinの構文メモ"
hascode = true
date = Date(2022, 5, 4)
rss = "Franklinでどのような構文が使えるかをおさらいする。（随時アップデートするかも）"
tags = ["misc"]
+++

# Franklinの構文メモ

[Franklin](https://franklinjl.org/)でどのような構文が使えるかをおさらいする。（随時アップデートするかも）

\toc

## References

- [Franklinの公式ページ](https://franklinjl.org/)
  - [Markdown syntax](https://franklinjl.org/syntax/markdown/)
- [Franklinで作られたデモサイト](https://tlienart.github.io/FranklinTemplates.jl/templates/lanyon/)

## Markdown

- 基本的にはMarkdownで書ける
  - **強調**
  - *斜体*
  - ~~打ち消し線は出ないみたい~~
- [リンク](https://hinata152.github.io/monotonica/)
  - 画像の場合は先頭に！マーク: `![alt text](link)`
- 脚注 [^1] はこんなふうに
  - 脚注が連続する場合 [^2] [^3] の書き方に注意
- \$を書くときには前にエスケープ記号を置く

## 数式

数式が書ける。ありがたい。

### 文中の数式

文中に数式を入れる場合 $Re = 1.2 \times 10^6$ のようにする。

### 独立した数式

数式を一行に独立させる場合（式番号が自動で付与される）

$$ \label{ma} Ma = 3.4 $$

### 偏微分方程式

分数には`\dfrac{}{}`、偏微分記号には`\partial`を使う。例えばクエット流れ [^4] の式は以下の通り：

$$ \dfrac{\partial^2 u}{\partial y^2} = 0 $$

この方程式の解は積分定数 $c_1$、$c_2$ を使って以下のように書ける：

$$ u = c_1y+c_2 $$

### 式の参照

マッハ数の式 $\ref{ma}$ を参照しているつもり。 [^5]

式番号が自動で付与されるので番号で式を参照したいが、できない様子。

[^1]: ここに脚注を書く
[^2]: 脚注その2
[^3]: 脚注その3
[^4]: [FORmula-TRANslation Translation into Julia (1)](/pages/012_formula-translation-translation-into-julia1)
[^5]: [LaTeX 入門 4 -式番号を参照する-](https://mashiroyuya.hatenablog.com/entry/tutorial4labelcomment)
