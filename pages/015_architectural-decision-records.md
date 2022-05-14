+++
title = "monotonicaの物書き"
hascode = true
date = Date(2022, 5, 14)
rss = "monotonicaでの書き物はArchitectural Decision Records (ADR) を意識して書いている。"
tags = ["misc"]
+++

# monotonicaの物書き

monotonicaでの書き物はArchitectural Decision Records (ADR) を意識して書いている。

ADRをどこで知ったかは定かではないけれども、かつて[Rebuild.fmのエピソード300](https://rebuild.fm/300/)（**omoさんゲスト回**）で聴いたことを覚えている。
僕が参考にしていたのは、おそらく検索でヒットしたであろうMichael Nygardによる[ブログ記事](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions.html)だった。
この記事によればADRは以下の要素からなる：

- **Title** These documents have names that are short noun phrases. For example, "ADR 1: Deployment on Ruby on Rails 3.0.10" or "ADR 9: LDAP for Multitenant Integration"
- **Context** This section describes the forces at play, including technological, political, social, and project local. These forces are probably in tension, and should be called out as such. The language in this section is value-neutral. It is simply describing facts.
- **Decision** This section describes our response to these forces. It is stated in full sentences, with active voice. "We will …"
- **Status** A decision may be "proposed" if the project stakeholders haven't agreed with it yet, or "accepted" once it is agreed. If a later ADR changes or reverses a decision, it may be marked as "deprecated" or "superseded" with a reference to its replacement.
- **Consequences** This section describes the resulting context, after applying the decision. All consequences should be listed here, not just the "positive" ones. A particular decision may have positive, negative, and neutral consequences, but all of them affect the team and project in the future.

これら要素をすべて厳密に含めているわけではないけれども、1つの記事には困りごとの背景情報、技術選定の過程（Decision Recordsなのでなぜその決定をしたのかを記録しておきたい）、導入の結果を含めるように心がけている。

その他、意識していることとして：

- **context**の要素で書かれている通り、"The language in this section is value-neutral. It is simply describing facts." なるべく事実を淡々と記す（お気持ち表明はブログでやる）
- "Bullets are acceptable only for visual style, not as an excuse for writing sentence fragments." ということで箇条書きを使わない [^1]

その後、<https://adr.github.io/>というADRのまとめサイトを見つけた。
ADRとそれに類するもののやり方、フォーマットはひとつではなく、各人が種々の様式を試していることがわかる。

[^1]: 箇条書きにしてしまった
