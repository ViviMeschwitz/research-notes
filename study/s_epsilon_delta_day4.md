# s_epsilon_delta_day4
# ε-δ論法：複雑な関数への応用 — Day 4

---

## ε-δ定義（復習）

$$\lim_{x \to a} f(x) = L \iff \forall \varepsilon > 0,\ \exists \delta > 0,\ 0 < |x-a| < \delta \Rightarrow |f(x)-L| < \varepsilon$$

**重要原則：** $\delta$ は $\varepsilon$ のみから決まる——$x$ に依存してはならない。

---

## 証明の手順

1. $|f(x) - L|$ を $|x-a|$ の式に変形する
2. 余分な因子を $\delta \leq 1$ の仮定で上から抑える
3. $\delta = \min(1,\ \varepsilon/C)$ で両条件を同時に満たす

---

## 例題1：$\lim_{x \to 2} x^2 = 4$

$\varepsilon > 0$ を任意にとる。$\delta = \min(1,\ \varepsilon/5)$ とおく。

$0 < |x-2| < \delta$ のとき：
- $\delta \leq 1$ より $|x-2| < 1$、つまり $1 < x < 3$
- よって $|x+2| < 5$
- $|x^2-4| = |x+2||x-2| < 5\delta \leq \varepsilon$ $\blacksquare$

---

## 例題2：$\lim_{x \to 3} x^2 = 9$

$\varepsilon > 0$ を任意にとる。$\delta = \min(1,\ \varepsilon/7)$ とおく。

$0 < |x-3| < \delta$ のとき：
- $\delta \leq 1$ より $2 < x < 4$
- よって $|x+3| < 7$
- $|x^2-9| = |x+3||x-3| < 7\delta \leq \varepsilon$ $\blacksquare$

---

## 例題3：$\lim_{x \to 1} x^3 = 1$

$\varepsilon > 0$ を任意にとる。$\delta = \min(1,\ \varepsilon/7)$ とおく。

$0 < |x-1| < \delta$ のとき：
- $\delta \leq 1$ より $0 < x < 2$
- よって $|x^2+x+1| \leq 4+2+1 = 7$
- $|x^3-1| = |x-1||x^2+x+1| < 7\delta \leq \varepsilon$ $\blacksquare$

---

## 例題4：$\lim_{x \to 2} \dfrac{x^2-4}{x-2} = 4$

$\varepsilon > 0$ を任意にとる。$\delta = \varepsilon$ とおく。

$0 < |x-2| < \delta$ のとき（$x \neq 2$ が保証される）：

$$\left|\frac{x^2-4}{x-2} - 4\right| = |x+2-4| = |x-2| < \delta = \varepsilon\ \blacksquare$$

**注：** $\min$ が不要な場合——余分な因子が現れないとき $\delta = \varepsilon$ そのままで済む。

---

## $\min$ が必要な場合とそうでない場合

| 場合 | 理由 |
|---|---|
| $\delta = \min(1, \varepsilon/C)$ | 余分な因子 $C$ を抑える必要があるとき |
| $\delta = \varepsilon$ | 変形後に $\vert f(x)-L \vert = \vert x-a \vert$ の形になるとき |

---

*記録日：2026-03-10 Day 4*
