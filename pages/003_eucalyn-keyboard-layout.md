+++
title = "Eucalyn配列への乗り換え記録"
hascode = false
date = Date(2022, 3, 6)
rss = "キーボードレイアウトをQWERTY配列からEucalyn配列に乗り換えて適応するまでの記録。（随時アップデート）"
tags = ["misc"]
+++

# Eucalyn配列への乗り換え記録

キーボードレイアウトをQWERTY配列からEucalyn配列に乗り換えて適応するまでの記録。（随時アップデート）

\toc

## 背景

普段のPCの入力デバイス（キーボード）にはMistelの[BAROCCO MD770](https://archisite.co.jp/products/mistel/barocco-md770-rgb-bt/)を使っている。
このキーボードの配列は、世の中のほとんどのキーボードがそうであるようにQWERTY配列になっているけれども、この配列を使い続ける理由は自分自身の慣れ以外には特に見当たらない。

BAROCCO MD770では初期設定（とキーボードの印字）であるQWERTY配列のほか、ソフトウェア的にColemak配列とDvorak配列が使えるようになっている。
加えて、キーボードのマクロプログラミング機能を使えば任意のキーボード配列を再現することも可能である [^1] （[参考](https://archisite.co.jp/wp-content/uploads/2020/10/Mistel-MD770RGB-BT-Manual-web.pdf)）。
このことを受けて、改めてQWERTY以外の配列を検討してみることにした。

## 配列の選定

少し調べてみた結果、Eucalyn配列が良さそうという結論に達した。

[Eucalyn配列について | ゆかりメモ](https://eucalyn.hatenadiary.jp/entry/about-eucalyn-layout)

このサイトでも紹介があるように、特長は以下の通り：

- **ローマ字入力特化**
  - 引用元の書き出しにも「**日本語を入力する機会は多いと思います。**」とある。最近では日本語しか打ち込まない生活が続いていて、また今後もしばらくこの生活が続くことが予想されるので、より良い配列に乗り換えるのも一つの選択肢と考えた。
- **よく使うショートカットはそのまま**
  - `ZXCVQWP`の配置がQWERTY配列から維持されているので、これらのキーを使ったショートカットを引き続き使うことができる。
- **HJKLの配置**
  - カーソルキー代わりの`HJKL`の並びが維持されている。横並びではなく逆T字になっているけど、MD770ではレイヤーに初期設定されているカーソルキーの並びが逆T字になっているので、特に違和感はない。

配列の選定にあたっては、このほかにも以下のサイトを参考にした：

- [Eucalyn配列の紹介と一年使ってみた感想](https://speakerdeck.com/hyuyukun/introduction-of-the-eucalyn-layout-and-my-impressions-after-one-year-of-use)
  - Eucalyn配列の特徴が図で解説されている。
- [キー配列頂上決戦！さいつよなレイアウトはどれだ！ | 遊舎工房](https://yushakobo.jp/blog/pluis9/2017/12/thinkkeylayout/)
  - 世の中にはQWERTY以外にもいろいろな配列があることがわかる。定量的な検証としてEucalyn配列のスコアが高いこともわかる。
- [Dvorakのその先へ（その1） | Qiita](https://qiita.com/miyaoka/items/e9118f01f924beb56b1d) / [Dvorakのその先へ（その2） | Qiita](https://qiita.com/miyaoka/items/4f363059e831bd003775)
  - 書き手のmiyaokaさんは[soussune](https://soussune.com/) (Podcast) の中の人。その1に出てくるErgoDoxは、[Rebuild.fmのエピソード206](https://rebuild.fm/206/)（**omoさんゲスト回**）のスポンサーとして紹介されている。
- [Self-Made Keyboards in Japan | Scrapbox](https://scrapbox.io/self-made-kbds-ja/)
  - READMEに出てくるBiacco42さんは[それはそう](https://biacco-radio.tumblr.com/) (Podcast) の中の人。聴き直すまで気づいていなかったけど、番組のいくつかのエピソードではEucalyn配列の作者の方も登場している。


## 経過（随時アップデート）

### 2022-01-25

正確な日付を覚えていないものの、記録によればこの日あたりからEucalyn配列を試し始めている。

配列自体は1日2日で覚えた。何となく元素の周期表を暗記している感覚があった。
QWERTY配列と比べると`H`と`M`の上下が逆転している。
Eucalynでは`H`が下段、`M`が上段にある一方、QWERTYでは`H`が中段、`M`が下段にある。

キーの並びを覚えることと実際に指が動くことは別物である、ということを理解した。
慣れない状態での自分のキーボード入力方法を再認識したのが面白かった。
文字列を一度ローマ字に脳内変換して（こんにちは→KONNNITIHA）、Kのキーはどこだっけと考えて、対応する右手中指を動かす、ということをやっている。
この処理に脳内のメモリを体感で2~3割ほど取られた状態で入力するので、入力中はただ文字列を打ち込むことしかできず、考えを巡らせられないのが大きなストレスだった。

他方では、仕事では定型文を使う場面がほとんどだということもわかった。
一度入力してしまえば、あとは最初の数文字を入れると予測変換が効くので、必要な文章は文節毎に予測変換していくことでわりとなんとかなった。

### 2022-02-12

2週間くらい続けると脳内変換のメモリ専有量が体感で1~2割くらいに下がって、だいぶ入力がしやすくなった。
とはいえ以前のQWERTY配列ほど早くは打てない。
この時点で、[e-typing](https://www.e-typing.ne.jp/)のスコアでいうと120pt、WPMが150くらい。

普段は問題なくても、緊張する場面ではキーのマッピングをど忘れして入力できない。
一方でQWERTY配列に戻すのにも労力がいる（戻してしばらくの間はミスタイプを多発する）ので、どっち付かずになった。
バイリンガルでいけるという先人の記録もあるけれど、自分の場合はそうはならなかった。

### 2022-02-26

1ヶ月くらい続けると指が慣れてきて、打つことを考えずに打てるようになった。
この時点で、[e-typing](https://www.e-typing.ne.jp/)のスコアでいうと200pt、WPMが220くらい。
全国平均データがスコア217pt、WPMが241ということで、全国平均の9割ほどは出るようになった。
QWERTYのときのスコアを取っておかなかったので、以前と比べてどれくらい速く（or 遅く）打てているのかが比較できないけれど、指の動きは楽になったように思う。

ローマ字入力はいいけれど、アルファベットの入力はまだ慣れない。
コマンドの`ls`や`cd`など、あるいはこれに限らず英単語の入力は指の動きで覚えていたということがよくわかる。
最近ではこのブログの更新のためにGitをはじめとするコマンドを打っているので、多少は入力への慣れが進んでいる。

### 2022-04-07

乗り換えてから2ヶ月とちょっとが経つと、タイピングのスコアがようやく全国平均に追いつくようになった。
[e-typing](https://www.e-typing.ne.jp/)のスコアが219pt、WPMが247くらい。
正確率は全国平均とほぼ同じで、ミス入力数は全国平均が12に対して14ある。
擬音語や擬態語のように、同じ文字の並びを2回繰り返す入力が苦手でミスしているという自覚がある。
`ls`や`cd`あるいは`git`といったコマンド、英単語の入力にはようやく慣れてきて、意識せずに指を動かせるようになってきている。

### 2022-06-18

乗り換えてから5ヶ月が経とうとしていて、直近の[e-typing](https://www.e-typing.ne.jp/)の最高スコアは258pt、WPMが262くらい。
なんとなくこのあたりに成長の限界を感じつつある。
最近では`f`と`b`が入れ替わる入力ミスが多いので注意したい。
英単語の入力は以前よりはスムーズになったけどまだ時間がかかっている。英単語を日常的に入力するようになれれば多少は改善するかも。

久しぶりに[溶鉄のマルフーシャ](https://store.steampowered.com/app/1456820/_/)を起動したら、自キャラがうまく動かせないことに気付いた。
このゲームはADキーで左右移動、Rキーでリロードを行うけど、Eucalyn配列ではこれらのキーの配置が左手から外れている。
Eucalyn配列を設定したレイヤーからデフォルトのレイヤー（QWERTY配列）へと戻すことで、これまで通り操作できるようになった。

[^1]: 物理キーの印字に対応させたキーキャップの並べ替えも可能であるものの、キーキャップの形状が（おそらく）OEM Profileであるため（[参考](https://buildersbox.corp-sansan.com/entry/2019/08/16/110000)）、QWERTY以外の配列では横に並ぶキーの高さがばらばらになる。キーボードの段ごとにキーキャップ形状が異なることには、恥ずかしながら今回の配列の乗り換えを通じてキーキャップを入れ替えてみて初めて気づいた。
