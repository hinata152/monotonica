+++
title = "monotonicaのフォント設定"
hascode = false
date = Date(2022, 3, 13)
rss = "このブログのフォントを変更した記録。"
tags = ["misc"]
+++

# monotonicaのフォント設定

このブログのフォントを変更した記録。

\toc

## 背景

[monotonica](https://hinata152.github.io/monotonica/)では[Lanyon](https://lanyon.getpoole.com/)というテーマを使っていて、これは紹介ページにあるようにアルファベットの表示を前提としている。
そのせいか、このテーマで日本語を表示するとまったく衒いのない明朝体のフォントになってしまうので、少し工夫したいなという思いがあった。

## フォント選定

素敵なフォント使いのひとつの理想形 [^1] を数年前に見かけていたものの、よく調べてみると有料フォントのようだった。
まずは無料の基本プレイからはじめることにして、一旦は保留。

自分がこのブログを閲覧する環境として、OSではWindowsとiOS (iPadOS) がある。
互換性の観点からはWebフォントを使うのが良さそうだ。
普段のWindowsでは[BIZ UDゴシック](https://www.morisawa.co.jp/products/fonts/bizplus/lineup/)をよく使っているけど、これはWebフォントとしては利用できないようだった。（[参考](https://support.bizplus.typesquare.com/hc/ja/articles/360004820071-Web%E3%83%95%E3%82%A9%E3%83%B3%E3%83%88%E3%81%A8%E3%81%97%E3%81%A6%E5%88%A9%E7%94%A8%E5%8F%AF%E8%83%BD%E3%81%A7%E3%81%99%E3%81%8B-)）
代わりに[Google Fonts](https://fonts.google.com/)が無料で使えるWebフォントを提供してくれているので、その中から探してみることにする。

- やわらかめのフォントとして[M PLUS 1p](https://fonts.google.com/specimen/M+PLUS+1p)は良かったけど、実際に文章を表示させてみたら丸まりすぎるのが少しだけ気になった。
- [Noto Sans Japanese](https://fonts.google.com/noto/specimen/Noto+Sans+JP)も良かったけど、今度は逆に直線的なのが少しだけ気になった。もうちょっとやさしい感じが欲しかった。
  - ただし、ブログのタイトルつながりでこのフォントを選ぶのもありだったかもしれない。
- 最終的に[Zen Kaku Gothic New](https://fonts.google.com/specimen/Zen+Kaku+Gothic+New)に落ち着いた。
  - Styleを**Regular 400**にするか**Medium 500**にするか悩んだけど、視認性の良さから**Medium 500**を選択した。

## HTMLとCSSに適用

リポジトリの`_layout`にあるhtmlファイルと、`_css`にあるcssファイルのそれらしきところを書き換えた。

- htmlには[Google Fonts](https://fonts.google.com/)のガイドに従って、ヘッダ部分にコードスニペットを追記した。
- cssは試行錯誤しながらフォント指定の場所を変更した。以下の2つの変更を施したと認識している：
  - グローバルでの`font-family`を指定（指定方法は[Google Fonts](https://fonts.google.com/)のガイドに従った）
  - ローカルでの`font-family`指定を削除

## 結果

- 表示されるフォントを変えることができた。
  - ページの読み込みにオーバーヘッドが発生するかと心配したけれど、体感としてはほとんど気にならない程度。
- Medium 500のスタイルだと行間がやや密になりすぎたので、行高さのパラメータ`line-height`も併せて微調整している。
- 本文のフォントは変わった一方、コードブロックのフォントがまだ変わっていない。普段のコード書きには[JetBrains Mono](https://www.jetbrains.com/lp/mono/)を使っていて、調べたら[Google FontsでWebフォントが提供されていた](https://fonts.google.com/specimen/JetBrains+Mono)のでありがたい。追って適用する。
- [Zen Kaku Gothic New](https://fonts.google.com/specimen/Zen+Kaku+Gothic+New)には[GitHubリポジトリ](https://github.com/googlefonts/zen-kakugothic)があって、[SIL Open Font Licenseの下で公開されている](https://github.com/googlefonts/zen-kakugothic/blob/main/OFL.txt)。ありがたく使わせていただいた。SIL Open Font Licenseについては記事 [^2] が参考になった。

[^1]: [このブログのフォントの話 | 愛のらくがき帳](https://blog.ishotihadus.com/archives/24)
[^2]: [「SILオープンフォントライセンス」って何？という方のためのざっくり解説 | たぬきフォント](https://tanukifont.com/sil/)
