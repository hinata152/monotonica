+++
title = "monotonicaの運用メモ"
hascode = true
date = Date(2022, 5, 6)
rss = "monotonicaのカテゴリ分けを変更したメモ。"
tags = ["misc"]
+++

# monotonicaの運用メモ

monotonicaのカテゴリ分けを変更したメモ。

\toc

## 背景

monotonicaのサイドバーにはResearchという項目を用意していて、これはGitHubのリポジトリとは別に外部公開しない研究のコンテンツをフォルダに置きながら、ローカルホストで使うことを想定していた。

けれど外部公開するものとそうでないものの関係を考えたとき、まずは公開を前提としない自分の考えなり記録があって、そこから外部公開できる部分を切り出してきて記事にする、という流れが（自分にとっては）自然であった。
言い換えると、monotonicaが外部公開を前提としたコンテンツ群なのに対して、こうした自分の考えや記録の全体をかりに*Gardenia* [^1] と呼ぶとすれば、包含関係としては $ monotonica \in Gardenia $ ということになる。
Franklinでこうしたサイト構成が実現できないかを検討した。

## 実装

前述のような多重化した構成での運用はFranklinでは想定されていないだろうとは思いつつ、以下のようなフォルダ構成とした。

```
gardenia
│
│  .gitignore
│  ...
│  config.md
│  ...
│
├─monotonica
│   │
│   │ ...
│   │
│   ├─...
│   │
│   ├─pages
│   │
│   ...
│
├─notes
│
├─references
│
├─_assets
│
├─_css
│
├─_layout
│
├─_libs
│
├─_rss
│
└─__site
    │
    ├─...
    │
    ├─pages（シンボリックリンク）
    │
    ...
```

gardeniaとmonotonicaはそれぞれFranklinの`newsite()`で作成したもの。
親にあたるgardeniaの側で以下の設定を行った。

- .gitignoreには、monotonicaフォルダ以下をバージョン管理から無視する設定を追加
- config.mdではmonotonica下の不要なフォルダ群を`__site`以下に作らないよう、変数ignoreに追記

```
ignore = [..., "monotonica/node_modules/", "monotonica/_assets/", "monotonica/_css/", "monotonica/_layout/", "monotonica/_libs/", "monotonica/_rss/"]
```

- `__site`フォルダにmonotonica/pageへのシンボリックリンクを作成（「管理者として実行」で起動したコマンドプロンプトにて以下のコマンドを実行）
  - シンボリックリンクを置くことで、特別にパスを修正することなく表示させることができる。
  - 副作用として、親側での記事を入れるフォルダ名に`pages`が使えないので、`notes`と`references`で代用した。フォルダでなくファイル単位でシンボリックリンクを作成すれば回避できるのかもしれないが、さすがに手間だと考えてやめた。

```
> cd __site
> mklink /D pages （途中までのパス）\monotonica\pages
pages <<===>> （途中までのパス）\monotonica\pages のシンボリック リンクが作成されました
```

- (optional) サイドバーの設定ファイル `_layout/sidebar.html` において以下を`class="sidebar-nav-item` の並びに追記

```
<a class="sidebar-nav-item {{ispage monotonica/*}}active{{end}}" href="/monotonica/">monotonica</a>
```

- (optional) `_css/franklin.css`と`_css/poole_lanyon.css`でフォントの設定
  - ローカルホストでしか動かさないので、Webフォントは使わずに直接指定した。

## 結果

親にあたるgardeniaの下で`serve()`した場合、サイドバーにmonotonicaへのリンクが表示され、ここをクリックすることでコンテンツにアクセスできるようになった。

![monotonica-in-gardenia](/pages/img/20220505113825.png)

一方、子にあたるmonotonicaの下で`serve()`した場合にはこれまで通りに（このサイトで表示されている通りに）表示できる。

monotonicaのサイドバーにあったResearchカテゴリは使う見込みがなくなったので、削除した。

## 参考

- [縁起物の式年遷宮](/pages/001_engimono-migration/)
- [monotonicaのフォント設定](/pages/008_changing-font-in-monotonica/)

[^1]: 梔子（くちなし）。学名 *Gardenia jasminoides*
