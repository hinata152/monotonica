+++
title = "ひとりでディスコード"
hascode = false
date = Date(2022, 3, 21)
rss = "Discordのひとり運用記録。（随時アップデート）"
tags = ["misc"]
+++

# ひとりでディスコード

[Discord](https://discord.com/)のひとり運用記録。（随時アップデート）

\toc

## 背景

昨年12月末の[Researchat.fm Lightning Talk Vol.02](https://researchat.fm/blog/11/)がきっかけで[Discord](https://discord.com/)を使うようになった。
[Slack](https://slack.com/intl/ja-jp/)みたく情報収集に活用できることがわかって、その後3ヶ月ほど使い続けて運用が固まってきたので、このあたりで一度まとめておく。

## 運用の所見

テキストチャンネルはinbox、断片の記録、スレッド専用チャンネル、本とゲームとポッドキャストの記録用チャンネルの4つ。

1. inboxは見つけたものを取りあえず入れる。
1. 断片の記録にはちょっとしたことを記録しておく（[参考](https://anemone.dodgson.org/2019/04/18/fragments-1/)）。
1. スレッド専用チャンネルは考えをまとめる用。inboxからの切り貼りと考えごとでスレッドを伸ばす。
1. 記録用チャンネルには、本は[ブクログ](https://booklog.jp/)の書籍URLを貼っておく。ポッドキャストは[Overcast](https://overcast.fm/)の共有リンクを貼っておく。ゲームは運用が定まっていない（定まるほどの流入量が今のところない）

[Discord](https://discord.com/)で投稿のエクスポートが出来るのかどうか調べてみたけど判然としなかった。
それもあって最終的にはMarkdownのテキストファイルにまとめていく（この記事のように）。

ボイスチャンネルは使っていない。

## 運用の試行錯誤

- [IFTTT](https://ifttt.com/)との連携でRSSフィードを自動投稿するチャンネルを作ったものの、投稿が入ってくるばかりでチェックが追いつかないので止めた。
  - あとは[Google Alerts](https://www.google.com/alerts)で良質なRSSをいまいち生成できなかった。[Google Scholar](https://scholar.google.com/)のアラートをRSSにできれば良かったけど、こちらはアラートの方法としてメールを送る以外のやり方がよくわからなかった。
- 記録用チャンネルは、当初は本とゲームとポッドキャストでそれぞれ分けていたが、前述の通りゲームの流入量が少なかったので一元化した。
- 人との対話ログ専用チャンネルを作っていたが、断片の記録もしくはスレッド専用チャンネルで十分だったので廃止した。

## Discord Nitro

[Discord](https://discord.com/)には課金システムとして[Discord Nitro](https://support.discord.com/hc/ja/articles/115000435108-Discord-Nitro-Classic-Nitro)がある。
Nitroに加入することで[サーバーブースト](https://support.discord.com/hc/ja/articles/360028038352-%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%83%96%E3%83%BC%E3%82%B9%E3%83%88-)レベル1をアンロックでき [^1] 、以下の特典が得られる [^2] 。

~~~
<blockquote>
<b>Level 1 Perks</b>
<ul>
    <li>+50 Emoji Slots (for a total of 100 emojis)</li>
    <li>128 Kbps Audio Quality</li>
    <li>Go Live streams boosted to 720P 60FPS</li>
    <li>Custom Server Invite Background</li>
    <li>Animated Server Icon</li>
    <li>15 custom sticker slots</li>
    <li>3 day archive option from last activity for th</li>
</ul>
</blockquote>
~~~

このうち最後の項目 "**3 day archive option from last activity for threads**" の機能がどうしても欲しかったので課金しているのだけど、それ以外の機能は使っていないので、正直なところ割に合わない。
Nitroは月額1050円のサブスクリプションであり、仮に一年間使い続けたとすると（いま自分が使っている）[Evernote Personal](https://evernote.com/compare-plans)の年額プランの倍ほどの出費になる。
しかしそれを逆手に取って、元を取ろうという気持ちで情報収集と思考の記録ができれば良いと考えた。
そんな吝嗇駆動な情報収集とアウトプットが今のところはうまく働いている。

## 参考：価格の比較

- [Scrapbox](https://scrapbox.io/pricing?lang=ja) 個人利用については無料プランあり
- [Notion](https://www.notion.so/ja-jp/pricing) 個人利用については無料プランあり
- [Evernote Personal](https://evernote.com/compare-plans) 680 JPY/month or 5800 JPY/year (= 483 JPY/month)
- [Discord Nitro](https://support.discord.com/hc/ja/articles/115000435108-Discord-Nitro-Classic-Nitro) 1050 JPY/month
- [Roam Research](https://roamresearch.com/) \$15/month
  - [Rebuild.fmのエピソード300](https://rebuild.fm/300/)（**omoさんゲスト回**）でも言及されていたBeliever Planは \$500/5years (= \$8.33/month)

月額でいえば[Roam Research](https://roamresearch.com/)よりも[Discord Nitro](https://support.discord.com/hc/ja/articles/115000435108-Discord-Nitro-Classic-Nitro)のほうがお手頃価格であり、かつゲーマーとしての矜持も満たされる。

[^1]: Nitroへの加入でサーバーブーストが2つ手に入る。手に入れたサーバーブースト2つをレベルなしのサーバーに使うことでレベル1にできる。なおレベルに応じて必要なサーバーブーストの数は増えていく（レベル2になるにはサーバーブースト7つ、レベル3になるにはサーバーブースト14つ）。課金との相談で現状ではレベル1にとどめている。
[^2]: [Server Boosting FAQ 💨 | Discord](https://support.discord.com/hc/en-us/articles/360028038352)
