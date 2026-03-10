# s_git_branch_day4
# Gitブランチ操作 — Day 4

---

## ブランチとは

木の枝のイメージ——幹（`main`）は確定した研究の本流。枝（新しいブランチ）は本流に影響を与えずに実験する場所。実験が成功したら幹に合流させる——これを**マージ**という。

---

## 基本コマンド

| コマンド | 意味 |
|---|---|
| `git branch` | ブランチ一覧を表示（`*`が現在地） |
| `git branch <名前>` | 新しいブランチを作成 |
| `git checkout <名前>` | ブランチを移動 |
| `git merge <名前>` | 現在のブランチに指定ブランチを合流 |

---

## ブランチの命名規則

`experiment/topology` の `/` はファイル構造とは無関係——人間が読みやすくするための慣習的な区切り文字。

ただしGitは内部的に `/` を本物のディレクトリ構造として保存する：

```
.git/refs/heads/
├── main
└── experiment/
    └── topology
```

`experiment/` という名前空間でブランチをグループ化できる：

```
experiment/topology
experiment/lullaby-field
experiment/shannon
```

---

## マージの種類

**Fast-forward：** 枝が幹から分岐した後、幹側に変更がなかった場合。枝の変更がそのまま幹に取り込まれる。最もシンプルなマージ。

---

## xyz空間との対応

`main` は幹——確定した時間軸。ブランチは**分岐した時間**——実験的な別の軌跡。マージは**時間の合流**——別の軌跡が本流に戻る。

---

## 本日の操作記録

```bash
git branch experiment/topology        # ブランチ作成
git checkout experiment/topology      # 移動
echo "..." > ideas/topology_experiment.md
git add .
git commit -m "Add topology experiment ideas"
git checkout main                     # mainに戻る
ls ideas/                             # ファイルが存在しないことを確認
git merge experiment/topology         # マージ
ls ideas/                             # ファイルが現れたことを確認
```

---

*記録日：2026-03-10 Day 4*
