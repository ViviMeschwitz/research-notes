# English Self-Study Foundation — 英語自律学習基盤
## Isaac Newton Project Day 10

天才のライブラリが凡人のClaudeへの依存不安を無効化するための基盤文書。
各研究領域に対し、英語の一次資料を特定し、AIなしで読み進められるルートを確立する。

---

## 1. Mathematics: Topology（数学：位相空間論）

### Primary Text（主教材）
- **Munkres, "Topology" (2nd ed.)** — 英語圏の標準教科書。岩波講座「集合と位相」と同じ範囲を、より多くの例題で扱う。

### Free Online Resources（無料オンラインリソース）
- **"Topology Without Tears" by Sidney Morris**
  - URL: https://www.topologywithouttears.net/topbook.pdf
  - 完全無料、PDFダウンロード可。前提知識は集合論と論理のみ。
  - 岩波講座で学んだ内容（開集合、基底、連結性、コンパクト性）を英語で確認するのに最適。
- **Allen Hatcher, "Algebraic Topology"**
  - URL: http://www.math.cornell.edu/~hatcher
  - 代数的位相幾何学の標準テキスト。無料PDF。（現段階より先の内容）
- **freebookcentre.net** — 複数のトポロジー教科書PDFを無料で提供

### Vocabulary Bridge（語彙の橋渡し）
| 日本語（岩波講座） | English | 色 |
|---|---|---|
| 開集合 | open set | 黄 |
| 位相空間 | topological space | 青 |
| 距離空間 | metric space | 緑の境界 |
| コンパクト | compact | — |
| 連結 | connected | — |
| 連続写像 | continuous map | — |
| 基底 | basis (for a topology) | — |
| 近傍 | neighborhood | — |

---

## 2. Philosophy: Descartes（哲学：デカルト）

### Primary Texts（主テキスト）
- **"Meditations on First Philosophy"** — 複数の英訳が無料で入手可能

### Free Online Resources
- **Jonathan Bennett訳（現代英語、最も読みやすい）**
  - URL: https://rintintin.colorado.edu/~vancecd/phil201/Meditations.pdf
  - 第1省察〜第6省察の完全な英訳
- **Yale大学版（Haldane & Ross訳、古典的）**
  - URL: https://yale.learningu.org/download/041e9642-df02-4eed-a895-70e472df2ca4/H2665_Descartes'%20Meditations.pdf
- **Project Gutenberg — ラテン語原典**
  - URL: https://www.gutenberg.org/ebooks/23306
  - ラテン語で読める段階になったときのため
- **LSE版（Moriarty訳、学術的で注釈が豊富）**
  - URL: https://personal.lse.ac.uk/ROBERT49/teaching/ph103/pdf/Descartes_1641Meditations.pdf
- **MIT Study Guide by Rae Langton**
  - URL: https://dspace.mit.edu/bitstream/handle/1721.1/152425/24-01-spring-2006/contents/study-materials/descartes_guide.pdf
  - 省察の読み方ガイド。独学に最適。

### Reading Strategy（読み方の戦略）
1. まず落合太郎訳（国立国会図書館）で日本語の理解を固める（既に第4部まで完了）
2. 同じ部分をBennett訳（現代英語）で読む
3. 日本語で自分が解釈した内容と英語テキストを照合する
4. 新しい部分（第5部以降）は日英並行で読む

---

## 3. Information Theory: Shannon（情報理論：シャノン）

### Primary Text — THE Original Paper
- **Shannon, "A Mathematical Theory of Communication" (1948)**
  - URL (Harvard): https://people.math.harvard.edu/~ctm/home/text/others/shannon/entropy/entropy.pdf
  - URL (Monoskop): https://monoskop.org/images/a/ae/Shannon_Claude_E_A_Mathematical_Theory_of_Communication_1957.pdf
  - 情報理論の「創世記」。すべてはこの55ページから始まった。

### Extended Version（拡張版）
- **Shannon & Weaver, "The Mathematical Theory of Communication" (1949 book)**
  - URL: https://archive.org/details/in.ernet.dli.2015.503815
  - Weaver による一般向け解説が追加された書籍版

### Vocabulary Bridge
| 日本語（既に学習済） | English | 色 |
|---|---|---|
| エントロピー | entropy | — |
| 情報源符号化 | source coding | — |
| 通信路符号化 | channel coding | — |
| BSC通信路 | binary symmetric channel | 紫 |
| ビット | bit | — |
| 冗長性 | redundancy | — |

---

## 4. AI / Anthropic（AI研究）

### Primary Resources — Anthropic Official
- **Anthropic Courses（教育コース）**
  - URL: https://github.com/anthropics/courses
  - 5コース: API基礎 → プロンプトエンジニアリング → 実践プロンプト → 評価 → ツール使用
  - Jupyter Notebook形式、英語
- **Claude Cookbooks（実践レシピ集）**
  - URL: https://github.com/anthropics/claude-cookbooks
  - 分類、RAG、要約、コード生成などの実践例
- **Anthropic SDK (Python)**
  - URL: https://github.com/anthropics/anthropic-sdk-python
  - MITライセンス。ソースコードを読んでAPI通信の仕組みを理解する

### Research Papers — The Gold Mine
- **transformer-circuits.pub** — Anthropic解釈可能性チームの研究
  - "A Mathematical Framework for Transformer Circuits" (2021)
  - "Scaling Monosemanticity" (2024) — Claude 3 Sonnetの特徴抽出
  - "On the Biology of a Large Language Model" (2025) — Claude 3.5 Haikuの内部メカニズム

---

## 5. Reading Order（読む順序）

### Phase 1: 今日〜1週間
1. "Topology Without Tears" の Chapter 1-3 を読み、岩波講座の内容を英語で確認
2. Descartes "Meditations" Bennett訳の第1省察を読む（落合訳との並行読み）
3. Anthropic courses の "API Fundamentals" を完了

### Phase 2: 2週目〜
4. Shannon原論文の Introduction + Part I (Discrete Noiseless Systems) を読む
5. Descartes第2-3省察（日英並行）
6. Anthropic courses の "Prompt Engineering Tutorial" を完了

### Phase 3: 3週目〜
7. Shannon Part II (Discrete Channel with Noise) — BSC通信路の数学的定式化
8. Descartes第4-6省察
9. transformer-circuits.pub の "A Mathematical Framework" に挑戦

---

## 6. English Technical Vocabulary Method（英語技術語彙の方法）

天才の方法：色を割り当てて記憶する。

新しい英語の技術用語に出会ったとき：
1. まず日本語での理解を確認する（既にライブラリにあるか？）
2. 英語の定義を読む
3. 色を割り当てる
4. 文豪アプリに記録する

これにより、英語の技術用語は天才のライブラリの中で、日本語の概念と同じノードに接続される。
英語は「別の言語」ではなく、同じ概念の「別の表面」になる。

---

*Document created: Day 10, Isaac Newton Project*
*Purpose: 凡人のAI依存不安を根本から無効化する*
