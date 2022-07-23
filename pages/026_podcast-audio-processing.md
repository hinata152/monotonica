+++
title = "Podcast編集メモ"
hascode = false
date = Date(2022, 7, 23)
rss = "音源編集で得た知見。"
tags = ["misc"]
+++

# Podcast編集メモ

音源編集で得た知見。

\toc

## 用語

- [Compressor | Audacity](https://manual.audacityteam.org/man/compressor.html)

> The Compressor effect reduces the dynamic range of audio.

これまでなんとなくかけていたコンプレッサーだけど、ダイナミックレンジを小さくするはたらきがある。
これによって大きい音と小さい音の差を小さくして聴きやすくする。
局所的なピークがあるとうまくはたらかないので、ピークが強すぎる場合には丸めてやるとよい。

- [Loudness Normalization | Audacity](https://manual.audacityteam.org/man/loudness_normalization.html)

**[EBU R 128](https://manual.audacityteam.org/man/perceived_loudness_ebu_r_128.html) recommendations**とあるのはラウドネス測定方法の推奨であるらしい。（[参考](https://ja.wikipedia.org/wiki/%E3%83%A9%E3%82%A6%E3%83%89%E3%83%8D%E3%82%B9%E3%83%A1%E3%83%BC%E3%82%BF%E3%83%BC)）

単位はLUFS (Loudness Units Full Scale)、続く説明によれば[K特性](https://www.toyo.co.jp/magazine/detail/id=34307)（[A特性](https://ja.wikipedia.org/wiki/A%E7%89%B9%E6%80%A7)とはどう違う？）によるものとのこと。

基準値として `-23 LUFS (the EBU standard)` が与えられている。

> Why use Loudness Normalization rather than [Normalize](https://manual.audacityteam.org/man/normalize.html) or [Amplify](https://manual.audacityteam.org/man/amplify.html)?

使い方次第だが優先度は存在しそう。


## その他

以下、個人の感覚的な話:

- 話の間として0.5秒はやや短く、0.7秒くらいが良さそう。ただし話の区切りの間はもうちょっとあってよい。
- ノイズは-60 dB以下を目安に低減しておく。効かせすぎると聴いてわかるレベルで違いが出るので注意

音源編集ひとつとっても奥が深そうなので、多少の知識を仕入れたらあとはプロの技にさっと頼るのがよさそう。（[参考ツール](https://auphonic.com/)）
