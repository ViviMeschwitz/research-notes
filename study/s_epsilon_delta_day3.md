# s_epsilon_delta_day3
**作成：2026-03-09**
**セッション：物理 Day 3**

---

## テーマ：微分の厳密化

---

## 高校の微分（直観）

$$\frac{dx}{dt} = \lim_{\Delta t \to 0} \frac{x(t + \Delta t) - x(t)}{\Delta t}$$

$\Delta t \to 0$ のときの差分商の極限値。

---

## ε-δ論法（厳密な定義）

$$\lim_{\Delta t \to 0} \frac{\Delta x}{\Delta t} = L$$

$$\iff \forall \varepsilon > 0,\ \exists \delta > 0,\ \forall \Delta t : 0 < |\Delta t| < \delta \Rightarrow \left|\frac{\Delta x}{\Delta t} - L\right| < \varepsilon$$

### 各変数の役割
- $\varepsilon$：誤差の許容範囲
- $\delta$：$\Delta t$ の制御範囲——「$\Delta t$ をどこまで小さくすれば $\frac{\Delta x}{\Delta t}$ が $L$ に十分近くなるか」を制御する

---

## 具体例：$x(t) = t^2$、$t = 1$ における微分

### 差分商の計算
$$\frac{\Delta x}{\Delta t} = \frac{(1+\Delta t)^2 - 1}{\Delta t} = 2 + \Delta t$$

極限値 $L = 2$。

### ε-δ証明
$$\left|\frac{\Delta x}{\Delta t} - 2\right| = |2 + \Delta t - 2| = |\Delta t|$$

$\delta = \varepsilon$ ととれば：

$$0 < |\Delta t| < \delta \Rightarrow \left|\frac{\Delta x}{\Delta t} - 2\right| = |\Delta t| < \varepsilon$$

$$\therefore \frac{d}{dt}t^2\bigg|_{t=1} = 2$$

---

## 複雑な関数への対応

複雑な関数 → 単純な関数の組み合わせとして分解する。

**合成関数の微分（chain rule）：**

$$\frac{d}{dt}f(g(t)) = f'(g(t)) \cdot g'(t)$$

---

## 微分不可能な関数の存在

$$f(t) = \begin{cases} \sin\dfrac{1}{t} & (t \neq 0) \\ 0 & (t = 0) \end{cases}$$

$t = 0$ で：

$$\lim_{\Delta t \to 0} \frac{\sin\frac{1}{\Delta t}}{\Delta t}$$

$\sin\dfrac{1}{\Delta t}$ は $\Delta t \to 0$ のとき $-1$ と $1$ の間を無限に振動する。よって $\dfrac{\sin\frac{1}{\Delta t}}{\Delta t}$ は $-\infty$ と $+\infty$ の間を無限に振動し、極限値が存在しない。

**→ $t = 0$ で微分不可能。**

ε-δの言葉で：どんな $\delta$ をとっても、$|\Delta t| < \delta$ の範囲に $\dfrac{\Delta x}{\Delta t}$ が $\varepsilon$ の中に収まらない $\Delta t$ が存在する。

---

## 探求路線の交差

### 位相空間・距離空間との対応（今日の数学）

| 位相・距離空間 | 微分の極限 |
|--------------|-----------|
| $\varepsilon$（open ballの半径） | $\varepsilon$（誤差の許容範囲） |
| $\delta$（近傍の制御） | $\delta$（$\Delta t$ の制御） |
| $B(a, \varepsilon)$ | $\left|\dfrac{\Delta x}{\Delta t} - L\right| < \varepsilon$ |

同じ数学的運動：**「どんな小さな $\varepsilon$ にも対応する $\delta$ が存在する」**

### ゲーデルとの接続
- 微分不可能な関数の存在＝分解できない問題の存在
- どんなに強力な道具も、原理的に届かない対象がある
- → Day 2のゲーデル的問い「AIは真偽が原理的に確定できない問題を扱えるか」と同構造

### 小説との交差
- 主人公の理想像（天才）＝「どんな概念にも境界を与えられる人間」
- 微分不可能な関数のように**原理的に境界を与えられない概念**が存在するとしたら——
- 理想像は最初から不可能な存在なのかもしれない
- →「錯覚は救済か崩壊か」という未決問題に触れる

---

## 全体構造

```
高校の微分（直観）
　↓ 厳密化
ε-δ論法
　↓ 対応
位相空間のopen ball（数学セッション）
　↓
微分不可能な関数の存在
　↓
原理的に境界を与えられない概念の存在
　↓
ゲーデル・小説の未決問題と接続
```

---

## 次回予定
- より複雑な関数のε-δ証明
- 偏微分・多変数関数への拡張
- ランダウ=リフシッツ力学との接続
