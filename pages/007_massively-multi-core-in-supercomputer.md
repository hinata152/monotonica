+++
title = "Massively Multi-Core in Supercomputer (Rev.2)"
hascode = false
date = Date(2022, 3, 6)
rss = "スーパーコンピューターのコアを使い切る活動を紹介します。（増補第2版）"
tags = ["tech"]
+++

# Massively Multi-Core in Supercomputer (Rev.2)

スーパーコンピューターのコアを使い切る活動を紹介します。（増補第2版）

\toc

## Reference

* YAMAMOTO, Keiji, et al. The K computer operations: experiences and statistics. Procedia Computer Science, 2014, 29: 576-585. DOI:[10.1016/j.procs.2014.05.052](https://doi.org/10.1016/j.procs.2014.05.052)

## はじめに

[Message Passing](https://messagepassing.github.io/)にあった[コアあまりのはなし](https://messagepassing.github.io/012-manycore/)が面白かった。

~~~
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">Message Passing: しごとで CPU あまってる？あまってない？みたいな回です。 w/ <a href="https://twitter.com/karino2012?ref_src=twsrc%5Etfw">@karino2012</a> <a href="https://twitter.com/kzys?ref_src=twsrc%5Etfw">@kzys</a> <a href="https://twitter.com/shinh?ref_src=twsrc%5Etfw">@shinh</a> <a href="https://twitter.com/jmuk?ref_src=twsrc%5Etfw">@jmuk</a> <br><br>マメに更新したい思いつつまた気がつくと一ヶ月たってますが、よろしくね。<a href="https://t.co/bfbuKsmlsQ">https://t.co/bfbuKsmlsQ</a></p>&mdash; Hajime Morita (@omo2009) <a href="https://twitter.com/omo2009/status/1386943450549940224?ref_src=twsrc%5Etfw">April 27, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
~~~

ここにある汎用の計算機あるいは電話機の話題は、文化圏の違いからほぼほぼ理解できていないのだけれど、しかし読んでいて一番近さを感じたのは[shinhさんのポスト](https://messagepassing.github.io/012-manycore/04-shinh/)だった。
僕は普段High-Performance Computing (HPC) の文脈でコアを使い切る活動をしていて、さきのshinhさんのポストからは、この分野ではわりとembarassingly parallelの色合いが強いのだなという気づきがあった。
それは少なくない数のアプリがメニーコアによるStrong Scalingで健闘している様子、そしてI/Oを除けば基本的には各コアで役割の違いは存在せず、単一の役割をすべてのコアで均等に分担することに由来している。
OpenMPのディレクティブ`#pragma omp parallel`（Fortranであれば`$omp parallel`）ひとつでたやすくスケールしてくれるのも、後者の特徴のおかげ。


ここで冒頭のReferenceに挙げた、スーパーコンピューター「京」の運用に関する論文を読んでみる。
京は全部で82,944ノード、1ノードあたり8コアなので、トータルでみたコア数は約66万という値になる。
後継の[富岳](https://www.fujitsu.com/jp/about/businesspolicy/tech/fugaku/specifications/)が158,976ノード、1ノードあたり48コアなので、京から富岳へと至る8年を経てコア数は1桁増えている。
ジョブスケジューラによってジョブが割り当てられたコアはそのジョブの実行だけに専念すればよく、基本的にマルチタスクを考慮する必要はない（はず）。
またこれらはすべてが同じ（もしくはほぼ同じ[^1]）コアであって、同質なコアが裏で動いている、というのも電話機とは異なる特徴といえそう。
Message Passingの元記事ではSnapdragon 888が異なる3種類のコアを備えているとあり、これはとてもじゃないが使いこなせる気がしない…

さて[jmukさんのポスト](https://messagepassing.github.io/012-manycore/06-jmuk/)のタイトルをみて、HPC分野でのコアを使い切る活動については次の2つの軸で説明できると思い立った。しかしネットにある資料を漁っていたところ、この2軸で説明しているすぐれた資料 [^2], [^3] はすでに存在していた。

* 単一のコアを使い切る
* 複数のコアを使い切る

詳細はそれらの資料を読んでもらうこととして、するとこの記事で述べる内容もそんなになくなってしまったのだけれど、それでも何かしら書いていく。
Message Passingにあった話題がコアあまり、すなわち複数のコアをいかにして使い切るかという論点だったので、まずは後者の**複数の**コアを使い切ることについて。

## 複数のコアを使い切る

京は計算ノードひとつあたり8つのコアを持っている。
前述の**OpenMP**、すなわちスレッドベースのノード内 (intra-node) 並列化であれば8並列まで実現できる。
ただし計算ノードをひとつだけ使う場面というのはごく限られていて、実際には複数のノードを同時に利用したい。
論文によれば、出来高ではノード数がO(100)～O(10000)の幅で同時利用されている (Figure. 7)。
ここで同時利用のためにはノード間 (inter-node) での並列化が必要となり、その並列化に用いられるのが**MPI**、正式名称を**Message Passing Interface**という。

少し紛らわしいが、ノード内の並列化にはOpenMPだけでなくMPIも使うことができ、かつ**実際にはMPIが用いられるケースが多い**。言い換えれば**スレッド並列が用いられないケースのほうが多い** (論文Figure 12)。このときはflat-MPI、すなわち一様にMPIで並列化されているということ。一方でOpenMPなり自動並列化なりの並列化手法がMPIと同時に採用されている場合には、それはhybrid-MPIと呼ばれる。

OpenMPとMPI、またもう一つの並列化手法であるco-arrayの歴史については、おりしも[過去記事](https://tl.hateblo.jp/entry/2021/01/05/211224)に書いていた。
また並列化にあたって参考になる資料についても[過去記事](https://tl.hateblo.jp/entry/2020/08/09/143645)に書いていたので、ここでは繰り返さない。

## 単一のコアを使い切る

流れの都合で複数コアの並列化の話を先にしたけれど、それぞれのコアが十分な性能を発揮できるように**単一の**コアに対する高速化も重要になってくる。元記事の[morritaさんのポスト](https://messagepassing.github.io/012-manycore/05-morrita/)でプロファイラの話が出てくるけど、スーパーコンピューターにおける高速化も同様に、プロファイラを使ってアプリケーションの素性を知るところからはじめる。富岳だと[このような感じ（4.3節を参照）](https://www.fujitsu.com/jp/about/resources/publications/technicalreview/2020-03/article07.html)、日本電気のSXシリーズだと[このような感じ（56ページを参照）](http://www.hpc.cmc.osaka-u.ac.jp/wp-content/uploads/2017/04/20170619_1.pdf#page=56)。

プロファイラによってコストが高く・ボトルネックとなっている箇所（ホットスポットなどと呼ぶ）が特定されたら、そこに対して高速化のチューニングを施していく。高速化は取り組むだけ数字に結果が反映されるからそれはそれで楽しいのだけれど、コア固有の高速化手法が徐々に増えてくるとソースコードの管理が難しくなる。SXシリーズであればベクトル長を大きくとることが重要であり、また富岳についてはArmベースのコアで性能が出るような書き方にする必要があるが、それらはいずれも現在のHPC向けに普及したコア、ようはIntel Xeonでの高速化とは両立しないか、むしろ逆に悪化する要因にもなりかねない。SXシリーズでは[SX-Aurora TSUBASA](https://jpn.nec.com/hpc/sxauroratsubasa/index.html)としてより汎用性を高めた最新版が登場しており、また後者のArmベースのコアについては、富岳での成功や、AppleのM1チップの評判を受けてさらに一般に普及していくのか、今後の動向を見守りたい。

ちょうど最近の[Rebuildエピソード303](https://rebuild.fm/303/)でHakuro Matsudaさんがチップ話をしていて、そこで "**HPCはバスに始まってバスに終わる**" という格言があった。
スーパーコンピューターにおけるバス幅の指標として**B/F値**というのがあって、しかしこれについても上で挙げた理化学研究所の資料で説明されているから、ここでの説明は割愛する。
このB/F値、かつては大きな数字をもったスパコンが数多く存在していたものの[^4]、徐々に見られなくなっていった。
その理由としてはメモリバス幅を確保するためのコストが高いこと（さきのRebuildエピソードでも、メモリバス幅を広げるためのAMDの工夫が語られていた）、そして高B/F値を要求する実アプリケーションの地位の相対的な低下があるものと想像している。


## その他、落ち穂拾い

ちなみにReferenceは運用についての論文なので、消費電力の話も書かれている。論文によれば京の全消費電力（冷却装置の消費電力なども含めた値）は約15,000 kWとあり (Figure. 2)、しかし数字が大きすぎるためにどれくらいなのかの感覚が掴みづらい。
例えばかつて言及した[^5]『[反秀才論](https://www.iwanami.co.jp/book/b256264.html)』にちなんで風洞の消費電力と比較してみると、[NASA Amesにある世界最大の風洞](https://www.nasa.gov/centers/ames/news/features/2012/nfac-25.html)の使用電力が"**104 megawatts of electricity or the equivalent of a 225,000-person city.**"とあり、この桁を一つ小さくしたくらいの電力消費ということになる。

ちなみに富岳は性能が京の100倍でありながら、消費電力は数倍の増加にとどまっていて[^6]、相対的に見れば富岳が相当な省エネ性能を達成していることがわかる。NASA Amesの所長であったハンス・マークのエピソードが『[反秀才論](https://www.iwanami.co.jp/book/b256264.html)』に登場するけれども、彼が指摘した計算機の進歩によるコストダウンは今でも続いている。

あとは建屋の話を。
今の富岳が入っている建屋は先代の京の構築に合わせて建造されたもので、その詳細な経緯は[日建設計の資料](http://www.ssken.gr.jp/MAINSITE/download/newsletter/2011/20111020-joint/lecture-07/SSKEN_joint2011_nikkensekkei_PPT.pdf)で読むことができる。
外観やつくりに表出された思想と哲学だけでなく、スーパーコンピューター設置のための特別な仕様と強度、それに電力・冷却設備を備えた建屋となっている様子。
良いマシンを動かそうとするならばまずはそれを収容する建屋から、というのは、もう少し抽象化すればわりと応用できる考え方な気がする。

終わりにチューニングに関する箴言を紹介しておくと、これはかつて『[まつもとゆきひろ コードの世界
](https://www.nikkeibp.co.jp/atclpubmkt/book/09/182540/)』を読んでいて見つけたものだけど、書籍では出典が書かれていなかった。
調べてみるとMichael A. Jacksonがその著書*Principles of Program Design*で語ったものであるとされている[^7]：

~~~
<blockquote>
We follow two rules in the matter of optimization:</br>
Rule 1: Don't do it.</br>
Rule 2 (for experts only). Don't do it yet.
</blockquote>
~~~

ではいつやるのか？　という話になるけれど、少なくともある程度固まってからやりましょうね、というのが先人とのお約束。
あとは、チューニングにあたってはその道のプロに入ってもらえるととても捗る、という[個人的経験](https://tl.hateblo.jp/entry/2020/05/13/210521)がある。
このときはこうする、という正解がわかりさえすればあとは自分でもある程度は真似られるようになるけれど、まずその正解を見出すのが難しいので、できる人にレクチャーしてもらうのが一番の早道に思う。

## Summary

わりとembarassingly parallelな色合いが強いHPC向けアプリケーションについて、単一コアと複数コアをそれぞれ使い切る活動を紹介した。

記事を書くにあたってはスーパーコンピューター関連の資料を久しぶりに漁ってみたけれど、ベンダーの資料はまだしも、講義や講習会の資料になるとけっこう色々な人が色々なことを言っているので（あとはすでに時代遅れになっている資料も散見され）、ひとつの資料を闇雲に信頼するよりかは、複数の資料をあたって多角的に見てやることが大事かなと感じた。
この記事もそんな資料のひとつとして、もちろん内容の正確性には十分に留意しているけれども、参考程度に読んでもらえるといいと思う。


[^1]: 納入時期によってわずかな性能の違いはありうるかもしれないが、しかし基本的には同じはず
[^2]: [京速コンピュータ「京」におけるアプリケーション高性能化](https://www.ieice.org/jpn/books/kaishikiji/2012/201202.pdf)
[^3]: [京コンピュータにおけるアプリケーションの高並列化および高性能化―基本編―](https://www.cc.kyushu-u.ac.jp/scp/doc/users/forum/forum20140805/minami_1.pdf)
[^4]: "1998年に導入したSX-4はB/F性能値が8であるが、2015年に導入した現行機種SX-ACEのB/F性能値は1であり、代を重ねるごとに減少していることがわかる。" quoted from [大規模科学計算システムにおける利用者プログラムの特性分析](https://www.ss.cc.tohoku.ac.jp/sscc/refer/pdf_data/v51-1/v51-1_p42-46.pdf)
[^5]: [最近読んだ本 | 雛形書庫](https://tl.hateblo.jp/entry/2020/07/19/123512)
[^6]: [スーパーコンピュータ「富岳」](https://www.fujitsu.com/jp/about/businesspolicy/tech/fugaku/)
[^7]: [Jackson and Gregg on optimization](https://blog.plover.com/prog/optimization.html)


## 増補：お礼、そして最近のスーパーコンピューターの話題

上の文章を書いたのは2021年4月の話で、公開して間もなくこの回の[インターネットの声](https://messagepassing.github.io/012-manycore/07-internet/)で取り上げていただけたのは嬉しかった。
どうもありがとうございました。

当時から経過した1年近くの間を振り返ると、富岳によるシミュレーションの成果がニュースになったり、またポスト富岳に向けた動きが着々と進んでいたりと、いくつか取り上げておきたい話題も出てきた。
この増補ではそうした話題をピックアップしておく。

### スーパーコンピューター関連

[Still waiting for Exascale: Japan's Fugaku outperforms all competition once again | TOP500](https://www.top500.org/news/still-waiting-exascale-japans-fugaku-outperforms-all-competition-once-again/)

昨年11月に[TOP500](https://www.top500.org/)の11月次アップデートが発表されていた。
半年前（2021年6月）の集計結果からあまり順位の変動はありませんでした、という内容。
富岳が4期連続で首位を獲得。
日本語の良い[解説記事](https://www.hpcwire.jp/archives/53541)を見つけたのでそちらを参照されたい。

[ACM Gordon Bell Special Prize for HPC-Based COVID-19 Research Awarded to Japanese Team for Novel Aerosolized Droplet Simulation](https://www.acm.org/media-center/2021/november/gordon-bell-special-prize-covid-research-2021)

同時期に開催された[SC21](https://sc21.supercomputing.org/)に合わせて[ACM Gordon Bell Special Prize for High Performance Computing-Based COVID-19 Research](https://awards.acm.org/bell/covid-19-nominations)の選考が行われていたはずだが、ここで理研の富岳を用いた飛沫シミュレーションが受賞していた（[理研のプレスリリース](https://www.riken.jp/pr/news/2021/20211119_1/index.html)）。
受賞論文は[SAGE journals](https://journals.sagepub.com/home/hpc)ではまだ掲載されていないようだけど、[arXiv](https://arxiv.org/abs/2110.09769)で原稿を読むことができる。
また記者勉強会は今でも定期的に開催されていて、最新のものとして[2022年2月2日の勉強会動画](https://www.youtube.com/watch?v=7K8fkK-dVC4)を見ることができる [^8] 。


### 次期システムの見通し

[第8回NGACIミーティング打ち合わせ資料 (2021/9/27)](https://drive.google.com/file/d/1IAm556X4KJESTOpukR2hDJocrX2PhjQw/)

昨年9月にミーティングが開催されていた。
[NGACI (Next-Generation Advanced Computing Infrastructure) のサイト](https://sites.google.com/view/ngaci/home)にある概要によれば、

> 2010年から2013年にかけて「戦略的高性能計算システム開発に関するワークショップ（SDHPC）」が開催され、本コミュニティーの多くのボランティアの方々のご協力で「今後のHPCI技術開発に関する報告書」がまとめられました。この活動が起点となり、フラッグシップ2020プロジェクトが発足し、スーパーコンピュータ「富岳」の開発に至りました。

ということで、富岳におけるSDHPCの位置づけと同様に、次期システムにおいてはこのNGACIがその役割を担うのかと想像する。
サイトで公開されている[white paper 第1.0.0版](https://drive.google.com/file/d/1cAQyBmLs529Iqz44D_j1MfCkXk7o6kla/view?usp=sharing)の発行は2020年11月と少し古いけれど、とても詳しいので読んでいて面白い。

会議資料のp.3には今後の動きの話題が載っている。
「**文科省の概算要求に「次世代情報基盤の調査検討(新規)」が要求されている　→　来年度から2012年度のようにFSが開始される可能性あり**」
FSとはフィージビリティスタディのこと、2012年度という手がかりから調べてみるとおそらくこの取り組みを指していると思われる。

[文科省委託研究アプリFS（2012年7月～2014年3月） | R-CCS](https://www.r-ccs.riken.jp/research/collab/other/appfs/)　

> スーパーコンピュータ「富岳」の開発に先立ち、2018年から2020年頃のスーパーコンピュータなどの計算インフラに求められる機能・性能等の要件を明らかにし、またそれに対する技術的知見を獲得することを目的とした調査研究プロジェクト（フィージビリティスタディ＝FS）「将来のHPCIシステムのあり方の調査研究」が文部科学省委託研究として2012年7月から2014年3月まで実施されました。

また文部科学省の概算要求を見てみると、これは[HPCI計画推進委員会](https://www.mext.go.jp/b_menu/shingi/chousa/shinkou/020/index.htm)の資料になるけれども、2021年9月の[第48回の会議資料](https://www.mext.go.jp/content/20211006-mxt_jyohoka01-000018252_01.pdf)によれば「**次世代計算基盤に係る調査研究**」が新規で計上されている。
また同年12月の[第49回の会議資料](https://www.mext.go.jp/content/20220120-mxt_jyohoka01-000019552_02.pdf)
を見ると、さらに具体化された内容とスケジュールを確認することができる。
今後のFSの推移を見守りたい。

### スーパーコンピュータの電力問題

NGACIが公開している[white paper 第1.0.0版](https://drive.google.com/file/d/1cAQyBmLs529Iqz44D_j1MfCkXk7o6kla/view?usp=sharing)で検討されているように、そして前述のHPCI計画推進委員会の[第49回の議事要旨](https://www.mext.go.jp/b_menu/shingi/chousa/shinkou/020/gijiroku/1417971_00008.htm)からなんとなく雰囲気が伝わってくるように、消費電力、電力バジェットというのはスーパーコンピュータの規模や性能を考えていくうえで比較的強めの境界条件といえそうだ。
少し調べると富岳の電力管理に関する資料 [^9] も見つけることができる。

電力事情を改善する将来の見通し、すなわち新デバイスについてはwhite paperの
2.1.1.2の項目に見ることができる。
最近の動きとして把握している限りでは、このうちの化合物半導体について
NEDOより[次世代デジタルインフラの構築として公募](https://www.nedo.go.jp/koubo/IT2_100207.html)が行われていて、つい先日に[実施体制の決定について](https://www.nedo.go.jp/koubo/IT3_100207.html)のお知らせがあった。
公募の中にはSiC [^10] に関する技術開発と、光関連の技術があって、実施予定先一覧によれば後者には富士通が含まれている。
正直なところ半導体には明るくないので [^11] 、これらの技術がどういったものなのか、あるいはwhite paperで挙げられている複数の新デバイスのうち、化合物半導体に対してどれくらいの期待がかかっているのかの相場観がわからない。
上記のNEDO公募は実施期間が8年などとなっていて、ここでの成果がスーパーコンピュータの次期システムに載ってくることはタイミング的にあまりないのかもしれないけど、新しいデバイスについても長い目で動向を追っていきたい。

[^8]: 飛沫シミュレーションの読み解き方は[Side by Side Radioのエピソード97](https://sidebysideradio.libsyn.com/97-cycling-as-a-syndrome-dr-hasizume-oyama)に詳しい。
[^9]: [スーパーコンピュータ「富岳」におけるファイルシステム・電力管理の機能強化（2020年3月）](https://www.fujitsu.com/jp/documents/about/resources/publications/technicalreview/2020-03/article05.pdf)
[^10]: 炭化ケイ素（シリコンカーバイド）。シリコンだけを用いた単元素半導体に対し、複数の元素を材料にしている半導体を化合物半導体と呼ぶ。（[参考](https://sei.co.jp/sc/com_semi/)）
[^11]: [Interaxion Podcastのエピソード13](https://interaxion-podcast.github.io/13)は半導体の解説回としても素晴らしい。[研エンの仲のエピソード76](https://anchor.fm/ken-en-no-naka/episodes/76-e1ekb33)もCPU関連技術の参考になる。
