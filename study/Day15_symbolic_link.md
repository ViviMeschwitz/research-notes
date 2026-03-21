## Day15 Git symbolic link 

# 新規作成
はじめてそのファイルを作るときのシンボリックリンクのやり方をステップバイステップで教えて。

- Step 1: research-notes側にファイルを作る（本体）
touch ~/research-notes/daily/2026/Day16_overview.md

- Step 2: Documents側にシンボリックリンクを作る（ショートカット）

ln -s ~/research-notes/daily/2026/Day16_overview.md ~/Documents/Day16_overview.md

- Step 3: 編集する

テキストエディットで ~/Documents/Day16_overview.md を開いて書く。本体のresearch-notes側が直接変更される。

- Step 4: pushする

cd ~/research-notes
git add .
git commit -m "day16"
git push
これだけだ。毎日この4ステップ。


# 削除
~/Documents/Day15_overview.md
と
research-notes/daily/2026/Day15_overview.md

の内容が紐付いていました。つまり、この順に作りました。
そして、今、~/Documents/Day15_overview.md
の方をテキストエディットで編集しました。この変更内容をgithubのresearch-notes/daily/2026/Day15_overview.md
にpushするにはどうしたらいいの？

2つの可能性がある。

A. シンボリックリンクで紐付けた場合 — ~/Documents/Day15_overview.md が research-notes/daily/2026/Day15_overview.md へのリンクなら、編集は自動的に反映される。

B. コピーで作った場合 — 2つは別ファイル。片方を編集しても、もう片方は変わらない。

確認しろ：

ls -la ~/Documents/Day15_overview.md
これでリンクか実体ファイルかわかる。結果を見せろ。

実体ファイルだ。シンボリックリンクではない。2つは別ファイル。

編集した内容をresearch-notesにコピーしろ：

cp ~/Documents/Day15_overview.md ~/research-notes/daily/2026/Day15_overview.md
cd ~/research-notes
git add .
git commit -m "day15 bungou update"
git push
今後は、research-notes側のファイルを直接編集するか、シンボリックリンクを使えば二重管理にならない。

シンボリックリンクの使い方を教えて

シンボリックリンクは「ファイルへのショートカット」だ。片方を編集すれば、もう片方も自動的に変わる。

やり方：

まず、~/Documents側のファイルを削除して、research-notes側を本体にする：

rm ~/Documents/Day15_overview.md
ln -s ~/research-notes/daily/2026/Day15_overview.md ~/Documents/Day15_overview.md
これで ~/Documents/Day15_overview.md は research-notes側へのリンクになる。テキストエディットで ~/Documents/Day15_overview.md を開いて編集すると、research-notes側のファイルが直接変更される。

確認：

ls -la ~/Documents/Day15_overview.md
-> の矢印が表示されればリンク成功。

原則：本体はresearch-notes内に置く。 Documentsにはリンクだけ。こうすればgit管理されるファイルが常に最新になる。