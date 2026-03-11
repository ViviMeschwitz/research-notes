# s_git_conflict_day5
# Git：コンフリクト解消 — Day 5

*Isaac Newton Project — Day 5 CS③*

---

## コンフリクトとは

`main` と `feature` が**同じファイルの同じ行**を別々に変更した状態でマージしようとすると発生する。

Gitは「どちらが正しいかは人間が決めること」として：
- マージを途中で止める
- ファイルの中に両方の内容を並べて書き込む

```
<<<<<<< HEAD
main側の内容
=======
feature側の内容
>>>>>>> feature
```

`<<<<<<<` から `=======` → HEAD（現在のブランチ）の内容
`=======` から `>>>>>>>` → 相手ブランチの内容

ターミナルの表示も `main merge ~1` に変わる——マージ途中で止まっている状態。

---

## 今日の実験

```bash
mkdir conflict-test && cd conflict-test
git init
echo "line: original" > file.txt
git add . && git commit -m "init"

git checkout -b feature
echo "line: feature version" > file.txt
git add . && git commit -m "feature edit"

git checkout main
echo "line: main version" > file.txt
git add . && git commit -m "main edit"

git merge feature
# → CONFLICT (content): Merge conflict in file.txt
```

`cat file.txt` の出力：

```
<<<<<<< HEAD
line: main version
=======
line: feature version
>>>>>>> feature
```

---

## コンフリクト解消の手順

**1. ファイルを正しい状態に編集する**

マーカー（`<<<<<<<`・`=======`・`>>>>>>>`）を全て消し、正しい内容だけにする。

```bash
echo "line: merged version" > file.txt
```

**2. `git add` で解消済みとマーク**

```bash
git add file.txt
```

**3. `git commit` でマージを完了**

```bash
git commit -m "resolve conflict"
# → [main 93aa3f6] resolve conflict
# merge ~1 が消えて main に戻る
```

---

## ブランチの時間構造

```
main:    init → main edit ──────────── resolve conflict
                                ↑
feature: init → feature edit ───┘
```

---

## `echo` と `>` / `>>` の違い

**`echo "文字列"`**
ターミナルに文字列を出力するコマンド。

**`>` （上書き）**
出力先を画面からファイルに切り替える。ファイルの内容を**完全に上書き**する。

```bash
echo "text" > file.txt   # file.txt の内容を "text" で上書き
```

**`>>` （追記）**
ファイルの末尾に追加する。既存の内容は消えない。

```bash
echo "text" >> file.txt  # file.txt の末尾に "text" を追加
```

---

## コンフリクトの本質（Xahlenの問いより）

`>` か `>>` かはコンフリクトに関係しない。

**コンフリクトが起きる条件：同じ場所を両ブランチが変更した**

```
mainが2行目を変更 + featureも2行目を変更 → コンフリクト
mainが1行目を変更 + featureが3行目を変更 → 自動マージ成功
```

Gitが見ているのはファイルの内容の差分。変更が衝突しない限り自動で解決できる。

---

## 実際の開発での3パターン

| パターン | 内容 |
|---|---|
| 両方を活かす | 両ブランチの変更を統合した内容に編集 |
| 片方だけ採用 | どちらか一方の内容だけを残す |
| 完全に書き直す | 両方とも捨てて新しく書く |

手順はどれも同じ——ファイルを正しい状態に編集 → `git add` → `git commit`

---

## 明日への継続

- `git rebase`（ブランチ履歴の整理）
- `git stash`（作業の一時退避）

---

*Day 5 · 2026-03-11*
