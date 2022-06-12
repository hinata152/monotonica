+++
title = "音速、無次元化、状態方程式"
hascode = true
date = Date(2022, 6, 9)
rss = "支配方程式とともに並ぶ数式を眺めていると、どれが独立したものでどれが従属的に求まるものなのかが時々わからなくなる。"
tags = ["tech"]
+++

# 音速、無次元化、状態方程式

支配方程式とともに並ぶ数式を眺めていると、どれが独立したものでどれが従属的に求まるものなのかが時々わからなくなる。

\toc

## 音速

文献 [^1] のp. 297には $a_0 = \sqrt{\gamma R T_0}$ という式が天下り的に出てきていて、これより前のページを見ても説明がされている様子はない（見落としてるだけかも）。

調べると別の文献 [^2] が音速と流体の圧縮率の関係式を与えていた。

$$
a^2 = (\frac{\partial p}{\partial \rho})_s
$$

また理想気体の場合に成立する式

$$
p = const \cdot \rho^\gamma
$$

これより（等エントロピー流れを仮定の下で）見慣れた音速の式が得られる。

$$
a^2 = \frac{\partial p}{\partial \rho} = \frac{\partial}{\partial \rho} (const \cdot \rho^\gamma) \\
= const \cdot \gamma \rho^{\gamma - 1} = \frac{\gamma (const \cdot \rho^{\gamma})}{\rho} \\
= \frac{\gamma p}{\rho}
$$

上式は理想気体の状態方程式 $p = \rho R T$ より以下のように書き換えることができる:

$$
a^2 = \frac{\gamma p}{\rho} = \gamma R T
$$

基準状態に対して以下の式が成立する。

$$
a_0^2 = \frac{\gamma p_0}{\rho_0} = \gamma R T_0
$$

話を文献 [^1] に戻すと、p. 313の式 (7.76) に音速を求める式が出てくる:

$$
M = \frac{V}{\sqrt{T}}
$$

ここで $V$, $T$ はいずれも無次元化された値である。
この式についても天下り的に出てきて詳細が書かれていないが、マッハ数の定義式より以下のように導出することができる。

$$
M = \frac{V}{a} = \frac{V/a_0}{a / a_0} = \frac{V'}{\frac{\sqrt{\gamma R T}}{\sqrt{\gamma R T_0}}} = \frac{V'}{\sqrt{T'}}
$$


## 無次元化

式 (5) を変形すると

$$
p_0 = \frac{1}{\gamma} \rho_0 a_0^2
$$

いま圧力を $\rho_0 a_0^2$ で無次元化するとして

$$
p' = p / \rho_0 a_0^2
$$

すると無次元化した基準圧力の値は$1/\gamma$になる。

$$
p_0' = p_0 / \rho_0 a_0^2 = (\frac{1}{\gamma} \rho_0 a_0^2) / \rho_0 a_0^2 = \frac{1}{\gamma}
$$

一方、圧力を基準圧力 $p_0$ で無次元化した場合には状態方程式は以下のようになる:

$$
(p' p_0) = (\rho' \rho_0) R (T' T_0)
$$

これを変形して

$$
p' = \frac{\rho_0 R T_0}{p_0} \rho' T' = \rho' T' \qquad \because p_0 = \rho_0 R T_0
$$

したがって、基準圧力で無次元化した場合には圧力は密度と温度の無次元量の積で与えられる。
これはこれで便利。

## 状態方程式

理想気体の状態方程式

$$
p = \rho R T
$$

見慣れたこの式ではなく、以下のようないつもと異なる形で出てくることがある（1次元での表記）:

$$
p = (\gamma - 1)(e - \frac{1}{2} \rho u^2)
$$

定圧比熱 $c_p$ と定積比熱 $c_v$ の間に成り立つ関係式

$$
c_p - c_v = R
$$

$$
\gamma \equiv \frac{c_p}{c_v}
$$

上2式より $c_v = \frac{1}{\gamma - 1}R$ を得る。
これを変形した $R = (\gamma - 1) c_v$ を状態方程式に代入すると

$$
p = \rho R T = \rho (\gamma - 1) c_v T = \rho (\gamma - 1) \epsilon \\
\qquad \because \epsilon = c_v T
$$

$\epsilon$ は単位**質量**あたりの内部エネルギーであり、$\rho \epsilon$ で単位**体積**あたりの内部エネルギーになる。単位**体積**あたりの全エネルギーを$e$とすると、内部エネルギーとは全エネルギーから運動エネルギーを差し引いたものに等しい。すなわち:

$$
p = (\gamma - 1) \rho \epsilon = (\gamma - 1) (e - \frac{1}{2} \rho u^2)
$$

ここの議論は文献 [^3] を参考にした。


[^1]: John D. Anderson, "Computational Fluid Dynamics: The Basics With Applications," McGraw-Hill Inc. (1995)
[^2]: リープマン, ロシュコ著, 玉田珖訳, "気体力学," 吉岡書店 (1956)
[^3]: 日本航空宇宙学会編, "圧縮性流体力学," 丸善出版 (2015)
