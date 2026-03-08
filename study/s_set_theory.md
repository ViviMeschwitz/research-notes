# 集合論基礎

作成日: 2026-03-08
関連: [[s_logic]], [[q_set_of_unknowable]]
分野: 数学

---

## 集合の定義

任意の要素 $x$ に対して、「$x$ がその集まりに属するか属さないか」が**一意に定まる**とき、その集まりを**集合**という。

> 命題と同じ構造：真か偽か一意に定まる。

---

## 記法

### 外延的記法（列挙）
$$A = \{1, 2, 3, 4, 5\}$$

### 内包的記法（条件）
$$A = \{x \in \mathbb{R} \mid x^2 = 9\}$$

---

## 重要な数の集合

$$\mathbb{N} \subset \mathbb{Z} \subset \mathbb{Q} \subset \mathbb{R}$$

| 記号 | 名前 | 例 |
|------|------|----|
| $\mathbb{N}$ | 自然数 | $0, 1, 2, \ldots$ |
| $\mathbb{Z}$ | 整数 | $\ldots, -1, 0, 1, \ldots$ |
| $\mathbb{Q}$ | 有理数 | $\frac{1}{2}, 0.75$ |
| $\mathbb{R}$ | 実数 | $\sqrt{2}, \pi$ |

---

## ∈ と ⊆ の違い

- $\in$ : 要素と集合の関係　例）$3 \in \{1,2,3\}$
- $\subseteq$ : 集合と集合の関係　例）$\{1,2\} \subseteq \{1,2,3\}$

---

## 集合の演算

$$A \cup B = \{x \mid x \in A \text{ または } x \in B\}$$
$$A \cap B = \{x \mid x \in A \text{ かつ } x \in B\}$$
$$\bar{A} = \{x \mid x \notin A\}$$

---

## ド・モルガンの法則

$$\overline{A \cup B} = \bar{A} \cap \bar{B}$$
$$\overline{A \cap B} = \bar{A} \cup \bar{B}$$

### 証明（両側包含法）

**Step 1: $\overline{A \cup B} \subseteq \bar{A} \cap \bar{B}$**

任意の $x \in \overline{A \cup B}$ をとる。
$\Rightarrow x \notin A \cup B$
$\Rightarrow x \notin A$ かつ $x \notin B$
$\Rightarrow x \in \bar{A} \cap \bar{B}$ ✓

**Step 2: $\bar{A} \cap \bar{B} \subseteq \overline{A \cup B}$**

任意の $x \in \bar{A} \cap \bar{B}$ をとる。
$\Rightarrow x \notin A$ かつ $x \notin B$
$\Rightarrow x \notin A \cup B$
$\Rightarrow x \in \overline{A \cup B}$ ✓
