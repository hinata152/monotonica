+++
title = "縁起物の式年遷宮"
hascode = true
date = Date(2022, 1, 22)
rss = "Engimonoのノート移行先として、FranklinとGitHub Pagesによる静的サイトを作成したメモ。"
tags = ["misc"]
+++

# 縁起物の式年遷宮

Engimonoのノート移行先として、[Franklin](https://franklinjl.org/)と[GitHub Pages](https://pages.github.com/)による静的サイトを作成したメモ。

\toc

## 背景

CSとCAEの論文読みPodcastである[Engimono](https://hinata152.github.io/engimono/)では、エピソードの収録に先立つ形で論文読みノートを作っている。
[Engimonoエピソード0](https://hinata152.github.io/engimono/episode/0)で話したように、このノートはPodcastサイトのドメインの下に作成できると収まりが良い。
げんにいくつかのPodcast（たとえば[Researchat.fm](https://researchat.fm), [Interaxion Podcast](https://interaxion-podcast.github.io)）ではドメインの下にブログ等の読み物が置いてある構成を見かける。
しかし僕はRubyに明るくなく、そのため[Jekyll](https://jekyllrb.com/)の使い方、狭義には[Yattecast](https://r7kamura.github.io/yattecast/)のカスタマイズの仕方がわからなかった。
そこでやむなく手元にあったはてなブログに論文読みノートを書いていくことにした。

はてなブログのよい点はMarkdown記法に対応していることで、このおかげもあって今でも書き物の置き場所として使い続けている。
ただし以下の点で改善したいという思いが出てきた：

- 仮住まいで論文読みの技術系記事を書き続けてきたものの、お気持ち表明の記事とはやっぱり分けて書きたい（本とゲームについてまた何か書きたい）
- ブログテーマとして使っている[MonoTsuduri](https://blog.hatena.ne.jp/-/store/theme/17680117126988535567)はとても好きなので使い続けたいけれど、コードブロックでシンタックスハイライトが効かない
  - そもそもの用途が違うだろうから効かないことそれ自体が問題ではなく、（前の項目でも書いたように）技術系の記事はそれにふさわしいところに書くべき、ということ。
- 技術系の記事はMarkdown + Gitで管理したい
  - （まとまった時間が取れなくとも）incrementalに書き続ける、ということをやりたい

Markdown記法で記事を書き、かつGitで管理できるとなると、候補に挙がるのはやはり[Jekyll](https://jekyllrb.com/)などの静的サイトジェネレーターになるのだろう。けれど僕はRubyに明るくないので、どうするか。

## 技術選定

静的サイトジェネレーターといえば[Jekyll](https://jekyllrb.com/)が一般的、というのはこれまでの観測範囲（[Yattecast](https://r7kamura.github.io/yattecast/)もしくはこれまで見てきたブログ[^1][^2] ）、あるいは[Setting up a GitHub Pages site with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll)といったGitHubによる記事から受ける印象としてあった。

しかし調べてみると[Julia](https://julialang.org/)にも静的サイトジェネレーターの[Franklin](https://franklinjl.org/)があることがわかり、これはよかろうということで使うことにした。
静的サイトを作る目的であれば別のJuliaパッケージである[Documenter](https://juliadocs.github.io/Documenter.jl/stable/)も良さそうだったが（げんにいくつかの実装例[^3][^4] も見つかる）、生成されるサイトの構成はやはりマニュアル用途であって、ブログを書いていくのはちょっと難しそうという印象を受けた。

## 構築と運用

公式サイトにある[Quick start](https://franklinjl.org/#quick_start)の手順通りに初期サイトを生成した。
また構築作業の全体を通じて[先人の資料](https://terasakisatoshi.github.io/MathSeminar.jl/slideshow/franklin/build/#1)に助けられた。

- `using Franklin`からの`serve()`することでlocalhostにウェブページを表示できる。ページの様子を確認しつつ、テキストファイルを更新するとウェブページも自動更新されるのでとても楽だった。
- [Working with Franklin](https://franklinjl.org/workflow/)でフォルダ構造を確認し、ブログ記事のテキストファイルは`pages`フォルダに置くことに。
- [Franklin themes](https://tlienart.github.io/FranklinTemplates.jl/)よりいい感じのtemplateとして[Lanyon](https://tlienart.github.io/FranklinTemplates.jl/templates/lanyon/index.html)を選択した。
  - サイドバーは`_layout/sidebar.html`で編集できる。タグ用のページを別に作るか、サイドバーにタグを表示してしまうかは、タグの運用も含めて今後の検討。（はてなブログ時代はタグのやる気がなかった）

GitHub Pagesへのデプロイはやはり公式サイトの[Deploying on GitHub](https://franklinjl.org/workflow/deploy/#deploying_on_github)を参考にした。GitHub Pagesでウェブページが見られるようになる仕組みはこれまで知らなかったけど、今回の一連の構築作業を通してなんとなく理解できた。

- Engimonoと対になるURLを持たせたかったので、**personal (or org) website**ではなく**project website**として作成した。説明にも出てくる[basic project webpage](https://github.com/tlienart2/myWebsite)のリポジトリがとても参考になったのでありがたい。

将来的にFranklin本家のパッケージが更新されたらどうするか？　手元で改めて`newsite()`して更新分を差し替える感じになるのか、今後の検討。

追記：Gitで手元ではドラフト稿をバージョン管理しつつ、mainブランチには成果物だけをコミットしたい。一旦`git checkout -b dev`で開発ブランチを作成したあとで、このブランチでドラフト稿をcommitしていく。公開できるだけの完成版になったら`git checkout main`からの`git merge --squash dev`とすることで、完成版までに加えた変更は1コミットにまとめられる。（[参考](https://stackoverflow.com/questions/5308816/how-can-i-merge-multiple-commits-onto-another-branch-as-a-single-squashed-commit)）その後`git push origin main`でmainブランチをpushする。この追記部分と本文が1コミットになって見えていればOK。

追記2：
上で書いた追記のやり方を使って記事ごとにブランチを作ると、しばらく作業していなかったブランチでは他記事の公開状況が反映されないまま、当該ブランチで書こうとしている記事を書いていくことになる。
これは公開済の記事を引用したい場合には不便な状態だ。
このようなときには`git rebase`を使って、「ブランチがどこから分岐したか」を変更してやる。
`git rebase main dev`とすることで、devブランチの分岐元をmainブランチの先頭コミット（＝公開済の記事が存在する状態）へと変更することができる。
`git rebase`については[Gitポケットリファレンス](https://gihyo.jp/book/2017/978-4-7741-8593-4)も参考になる。

## 結果

- 記事執筆のはじめから終わりまでをMarkdown形式のテキストファイルで完結させられるようになった。
  - 反面、はてなブログでは出来ていたリンクの埋め込みができなくなったので、視覚的なインパクトは小さくなったかもしれない。
- このサイトのURLをTwitterなどにを貼り付けたときにサムネイルが表示されない。調べてみるとこの仕組みは[Open Graph protocol](https://ogp.me/) (OGP) と呼ばれるもののようで（[参考](https://e-words.jp/w/OGP.html)）、Franklinでは[open issue](https://github.com/tlienart/Franklin.jl/issues/669)になっていて未実装の様子。静かにやっていくことにする。
- コードブロックにシンタックスハイライトが効くようになった。[以前の記事](https://tl.hateblo.jp/entry/2021/10/03/143211)でのコード引用部分は以下のように表示される（ただしFortranではハイライトされない。残念）：

```Julia
n,m = 3*2^6,2^7
center,radius = m/2,m/6
body = AutoBody((x,t)->√sum(abs2,x .- center) - radius)
sim = Simulation((n+2,m+2), [1.,0.], radius; ν=ν, body=body)
sim_step!(sim,10)

# plot the vorcity ω=curl(u) scaled by the body length L and flow speed U
function plot_vorticity(sim)
  @inside sim.flow.σ[I] = WaterLily.curl(3,I,sim.flow.u)*sim.L/sim.U
  contourf(sim.flow.σ',
    color=palette(:BuGn), clims=(-10,10),linewidth=0,
    aspect_ratio=:equal,legend=false,border=:none)
end

# make a gif over a swimming cycle
@gif for t ∈ sim_time(sim) .+ range(0.0, stop=20.0, step=0.25)
  sim_step!(sim,t)
  plot_vorticity(sim)
end
```

## 参考文献

[^1]: [https://karino2.github.io/](https://karino2.github.io/)

[^2]: [https://nhiroki.jp/](https://nhiroki.jp/)

[^3]: [https://hyrodium.github.io/en/](https://hyrodium.github.io/en/)（[Zenn解説記事](https://zenn.dev/hyrodium/articles/dea67b9a233356)）

[^4]: [https://mizutokadowaki0312.github.io/Documenter_website/build/](https://mizutokadowaki0312.github.io/Documenter_website/build/)（[Zenn解説記事](https://zenn.dev/mizuto/articles/adcb28db0e427c)）
