+++
title = "忘れがちなGitコマンドまとめ"
hascode = true
date = Date(2022, 3, 2)
rss = "何度も調べているGitコマンドを自分用にまとめておく。（随時アップデート）"
tags = ["misc"]
+++

# 忘れがちなGitコマンドまとめ

何度も調べているGitコマンドを自分用にまとめておく。（随時アップデート）

\toc

## ファイルの変更を部分的にステージングする

```
$ git add -p <file名>
```

追加時にオプション`-p`を付ける。
するとそれぞれの変更部分に対して以下のような選択肢が発生する。

```
(1/1) Stage this hunk [y,n,q,a,d,e,?]?
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
e - manually edit the current hunk
? - print help
```

`y, n, e`あたりを活用する。
`e` (= edit) では終わりの空行を含めるとエラーになるので、空行は残さない。

参考: [git add -p 使ってますか？ | Qiita](https://qiita.com/cotton_desu/items/bf08ac57d59b37dd5188)

## ステージングした変更を表示する

```
$ git diff --cached
```

ファイルに加えた変更をステージングしてしまうと、その変更は`git diff`では見られなくなる。
ステージングした変更を見るためにはオプション`--cached`を付ける。

参考: [https://gist.github.com/kurotaky/5483492](https://gist.github.com/kurotaky/5483492)

## すべてのファイルをステージングする

```
$ git add -A
```

引数は不要。
`.gitignore`で指定したファイルは無視される。

> If no <pathspec> is given when -A option is used, all files in the entire working tree are updated (old versions of Git used to limit the update to the current directory and its subdirectories).

参考: [https://git-scm.com/docs/git-add](https://git-scm.com/docs/git-add)

## ファイルだけチェックアウトする

```
git checkout コミットID file_path
```

`git checkout コミットID`の後ろに`file_path`をさらに付けることで、ファイルだけチェックアウトできる。

参考: [git checkoutで特定のファイルをチェックアウトする | Qiita](https://qiita.com/takaaki4cards/items/36ac6b7536bc1fcb945b)

## ステージングを取り消す

```
git restore --staged <file>
```

`git status`したときに使い方が表示される。

参考: [https://git-scm.com/docs/git-restore](https://git-scm.com/docs/git-restore)
