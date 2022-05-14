+++
title = "Visual Studio Codeの覚え書き"
hascode = true
date = Date(2022, 5, 14)
rss = "最近よく使うエディタの覚え書き。"
tags = ["misc"]
+++

# Visual Studio Codeの覚え書き

最近よく使うエディタの覚え書き。

\toc

## References

- [Keyboard Shortcuts Reference](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

以下の分類は上記リンク先にあるチートシートのカテゴリ分けとは一致しない。

## 一般

- `Ctrl+Shift+p`, `F1`: Show Command Palette
  - 困ったらこれ（`F1`でいける）
- `Ctrl+Shift+b`: Toggle Primary Side Bar Visibility
- `Ctrl+Shift+e`: Show Explorer
- `Ctrl+Shift+f`: Search Workspace

## エディタ

- `Alt+Shift+(Left|Right)Arrow`: (Shrink|Expand) selection
  - 括弧内の文字列を選択するときなどに。
- `Ctrl+-`: Go Back / `Ctrl+=`: Go Forward
  - デフォルト設定を上書きした。

### グループ間での移動

- `Ctrl+￥`: Split editor
  - `Ctrl+/` はToggle Comment
- `Ctrl+Alt+LeftArrow`: Move Editor into Previous Group
- `Ctrl+Alt+RightArrow`: Move Editor into Next Group

グループ間での移動は[ターミナルからエディタに戻るとき](#ターミナルからエディタに戻るとき)と同じ。

## ターミナル

- `Ctrl+j`: Toggle Panel Visibility

### ターミナル間での移動

- `Alt+LeftArrow`: Focus Previous Terminal in Terminal Group
- `Alt+RightArrow`: Focus Next Terminal in Terminal Group

### エディタからターミナルに入るとき

- `Ctrl+Shift+｀`: Focus Terminal
  - デフォルトである`Ctrl+｀`が効かない（なぜか`Alt+｀`が入力されている様子。使っている端末のせい？）ので、Create New Terminalに上書きした。最初のCreate New Terminalだけはコマンドパレットから実行する。

### ターミナルからエディタに戻るとき

- `Ctrl+1`: Focus First Editor Group
- `Ctrl+2`: Focus Second Editor Group
- `Ctrl+3`: Focus Third Editor Group

## Markdown (Markdown All in One)

拡張機能[Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)を入れている。便利。

- `Ctrl+b`: Bold
- `Ctrl+i`: Italic
- [x] `Alt+c`: Toggle CheckBox
  - [x] 複数行を選択して一気にチェックすることも可
- `Ctrl+k v`: Open Preview to the Side
  - `Ctrl+Shift+v`からの`Ctrl+Alt+(Right|Left)Arrow`でもOK

### 表

| A   | B   |
| --- | --- |
| C   | D   |
| E   | F   |

- `Alt+Shift+f`: Format table

### 数式

- `Ctrl+m`: Toggle math environment

文中数式 $Re = 1.2 \times 10^6$ もしくは一行に独立した数式

$$ Ma = 3.4 $$

Franklinであれば式番号が自動で付与される：[Franklinの構文メモ](/pages/011_franklin-syntax/)

### 要おためし

便利そうだが慣れていないもの。

- `Ctrl+t`: Go to Symbol in Workspace
  - 見出しを検索して移動
- `Alt+LeftArrow`: Fold Recursively
- `Alt+RightArrow`: Unfold Recursively

## Personal Knowledge Management (Foam)

拡張機能[Foam](https://foambubble.github.io/foam/)をおためし中。楽しい。

- `Alt+d`: Open Daily Note
- `Ctrl+Alt+v`: Paste Image
  - クリップボードには画像ファイルではなく、イメージそのものを入れておく。
  - 画像ファイルはattachmentsに入る。
- `/tomorrow`など: 対応するDaily Noteの作成

| Snippet    | Date          |
| ---------- | ------------- |
| /tomorrow  | tomorrow      |
| /yesterday | yesterday     |
| /monday    | next Monday   |
| /+1d       | tomorrow      |
| /-3d       | 3 days ago    |
| /+1w       | in a week     |
| /-1m       | one month ago |
| /+1y       | in one year   |
（[foam-template](https://github.com/foambubble/foam-template)のドキュメントより引用）
