+++
title = "Juliaでの配列のコピー"
hascode = true
date = Date(2022, 6, 12)
rss = "shallow copyとdeep copyの違いについて。"
tags = ["misc"]
+++

# Juliaでの配列のコピー

shallow copyとdeep copyの違いについて。

文献 [^1] を読んでいたら気になる記述を見つけた。
コードブロックのところだけ引用。

```julia
A = [1, 2, 3] # 列ベクトルを作る
B = A         # いわゆる shallow copy になる　(ポインタだけ複製する)
A[1] = 5
```

手元の環境 (Julia Version 1.7.2 (2022-02-06)) で試すとたしかにこうなる。
これには気付いていなかった。

[1次元ノズルフローを解いた](/pages/018_quasi1d-nozzle-flow1/)手元のソースコードでは、1ステップ前の値を保存する際にFortranライクに以下のケース1のように書いていたが、これは適切ではない。
意図した結果を得るためにはケース2もしくは3のようにする必要がある。

```julia
# case1
rold = r

# case2
rold[:] = r[:]

# case3
for j=1:N
    rold[j] = r[j]
end
```

先ほどの文献 [^1] でもdeep copyとする例が示されている。

```julia
B = A[:]         # ベクトルのすべての要素をコピー
B = deepcopy(A)  # shallow copy に対して deep copy
```

ところで計算に必要な配列をどのように確保し・どのように計算ルーチンに渡せばよいかの知見はまだない。
今のところは配列をすべて `global` で宣言する雑なやり方で対応しているけど、もっと良いやり方に変えていきたい。

[^1]: 富永, "Juliaでふつうの統計解析（第二版）" (2021)
