+++
title = "JuliaでGIFアニメーションを作る"
hascode = true
date = Date(2022, 6, 4)
rss = "JuliaでPlotsのGIFアニメーションを作るときの覚え書き。"
tags = ["misc"]
+++

# JuliaでGIFアニメーションを作る

JuliaでPlotsのGIFアニメーションを作るときの覚え書き。

## ソースコード

1次元移流問題

$$
\frac{\partial q}{\partial t} + c \frac{\partial q}{\partial x} = 0 \qquad (c>0)
$$

のGIFアニメーションを作る例。
ソースコードは[こちら](https://github.com/kofujii1812/PythonCFD/blob/main/chapter2-2%5B2%5D-FTCS.ipynb)を参考にした。

```Julia
using Plots

c = 1.0
dt = 0.05
dx = 0.1
jmax = 21
nmax = 6

x = zeros(Float64,jmax)
q = zeros(Float64,jmax)
qold = zeros(Float64,jmax)

for j=1:jmax
    x[j] = dx * (j - 1)
    if x[j] < 1
        q[j] = 1
    else
        q[j] = 0
    end
end

anim = @animate for n=1:nmax
    qold = q
    for j=2:jmax-1
        q[j] = qold[j] - dt * c * (qold[j+1] - qold[j-1]) / (2.0 * dx)
    end
    plt = plot(x, q, label="FTCS",
               linestyle=:solid, color=:black,
               marker=:circle, markercolor=:blue,
               title="n=$n", xlabel="x", ylabel="q", ylim=(0,2.0))
    # display(plt) # check
end

gif(anim, "FTCS.gif", fps=2)
```

最終行よりGIFアニメーションのファイルが出力される。

![](/pages/img/20220604133533.gif)

- 時間発展のfor文の前に`anim = @animate`を置く。ループ中で`plot`関数を呼んでおいて、ループ終了後に`gif`関数を呼ぶことで動画を生成できる。
  - `gif`関数のファイル名と`fps`の値はお好みで設定する。
- ループ中で呼んだ`plt = plot()`の後に`display(plt)`すれば、おのおののフレームの静止画を取得できる。
- `plot()`について（[参考](https://docs.juliaplots.org/latest/generated/attributes_series/)）
  - `label`でその要素の凡例を表示。
  - `linestyle`で線分の種類を設定。破線 (`:dash`) などにもできる。`color`で線の色を設定。
  - `marker`でマーカーの形状を設定。四角 (`:rect`) などにもできる。`markercolor`でマーカーの色を設定。
  - `title`でグラフ上部のタイトルを設定。ステップ数を表示する例（変数を簡単に含められる）: `title="n=$n"`
  - `xlabel (ylabel)`で軸のタイトルを設定。
  - `ylim=(0,2.0)`の要領で軸の上下限値を設定。
- ループ中で`plt = plot!()`とすれば別要素の重ね書きもできる。（解析解を重ね書きしようと思ったがやめた）

アニメーションで見てわかる通り、時間発展にともなって不連続面に振動が生じている。
"一般的な流体問題を対象とする場合、このような計算法は不安定な計算法と理解できます。(p. 27)" [^1]
これは残念。

[^1]: 藤井, 立川. Pythonで学ぶ流体力学の数値計算法. Ohmsha, 2020.

追記: アニメーションを取得するステップ間隔を変えたい場合、ループ内で`plot()`を呼ぶ回数を制御するのではなく、for文に付随する`every`で制御する。

例えば10ステップおきにしたい場合、

```julia
anim = @animate for n=1:nmax

    ...

    if n % 10 == 0
        plt = plot(x, q, label="FTCS",
                   linestyle=:solid, color=:black,
                   marker=:circle, markercolor=:blue,
                   title="n=$n", xlabel="x", ylabel="q", ylim=(0,2.0))
        # display(plt) # check
    end
end
```

ではなく、

```julia
anim = @animate for n=1:nmax

    ...

    plt = plot(x, q, label="FTCS",
               linestyle=:solid, color=:black,
               marker=:circle, markercolor=:blue,
               title="n=$n", xlabel="x", ylabel="q", ylim=(0,2.0))
    # display(plt) # check
end every 10
```

とする。（[参考](https://docs.juliaplots.org/latest/animations/)）
