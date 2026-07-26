---
title: 확률변수·PMF/PDF
slug: random-variables
---

## 직관적 설명

**확률변수(random variable)**는 "결과를 숫자로 바꾸는 함수"다. 주사위를 던져 "1이 나왔다"라는 사건보다는 $X = 1$이라는 숫자가 더 다루기 쉽다. 확률변수는 표본공간 $\Omega$의 각 원소에 실수를 할당함으로써, 확률 계산을 숫자 위에서 할 수 있게 해준다.

확률변수에는 두 가지 주요 유형이 있다. **이산(discrete)** 확률변수는 셀 수 있는 값들(주사위 눈, 어떤 사건의 발생 횟수)을 갖는다. 이때 각 값의 확률을 알려주는 함수가 **확률질량함수(probability mass function, PMF)** 다.

**연속(continuous)** 확률변수는 연속적인 값(키, 무게, 시간)을 갖는다. 이 경우 특정 값의 확률은 0이므로, 구간의 확률을 적분으로 표현하는 **확률밀도함수(probability density function, PDF)** 를 사용한다.

두 경우 모두, **누적분포함수(cumulative distribution function, CDF)** $F(x) = P(X \leq x)$가 확률변수의 분포를 완전히 결정한다.

## 정의

**확률변수(random variable):** 확률공간 $(\Omega, \mathcal{F}, P)$에서 실수 $\mathbb{R}$로 가는 **가측함수(measurable function)** $X: \Omega \to \mathbb{R}$. 즉, 모든 보렐 집합 $B \subseteq \mathbb{R}$에 대해 $\{\omega: X(\omega) \in B\} \in \mathcal{F}$이다.

**확률질량함수(PMF, probability mass function):** 이산 확률변수 $X$에 대해

$$p_X(x) = P(X = x) = P(\{\omega: X(\omega) = x\})$$

PMF는 다음을 만족한다:
- $p_X(x) \geq 0$ 모든 $x$에 대해
- $\sum_{x \in \text{supp}(X)} p_X(x) = 1$

**확률밀도함수(PDF, probability density function):** 연속 확률변수 $X$에 대해, 다음을 만족하는 함수 $f_X: \mathbb{R} \to [0, \infty)$:

$$P(a \leq X \leq b) = \int_a^b f_X(x)\,dx$$

PMF는 확률 그 자체이지만, PDF는 확률이 아니다. PDF의 값 $f_X(x)$는 밀도(density)로, 확률을 얻으려면 적분해야 한다. $f_X(x)$ 자체는 $P(X = x)$가 아니라 $x$ 근방의 확률밀도를 나타낸다.

**누적분포함수(CDF, cumulative distribution function):** 모든 확률변수 $X$에 대해

$$F_X(x) = P(X \leq x)$$

**PDF와 CDF의 관계:** 연속 확률변수에서 $F_X$가 미분 가능하면

$$f_X(x) = \frac{d}{dx}F_X(x)$$

즉, PDF는 CDF의 도함수이고, CDF는 PDF의 (부정)적분이다:

$$F_X(x) = \int_{-\infty}^x f_X(t)\,dt$$

**분위함수(quantile function) 또는 역CDF:** $F^{-1}(p) = \inf\{x : F(x) \geq p\}$, $0 < p < 1$. 중앙값(median)은 $F^{-1}(1/2)$다.

**지지집합(support):** 확률변수 $X$의 지지집합은 $P(X \in S) = 1$인 가장 작은 닫힌 집합 $S$다. 이산의 경우 $\text{supp}(X) = \{x : p_X(x) > 0\}$, 연속의 경우 $\text{supp}(X) = \overline{\{x : f_X(x) > 0\}}$.

**결합분포(joint distribution):** 두 확률변수 $(X, Y)$의 결합 CDF는 $F_{X,Y}(x,y) = P(X \leq x, Y \leq y)$다. 이산의 경우 결합 PMF $p_{X,Y}(x,y)$, 연속의 경우 결합 PDF $f_{X,Y}(x,y)$가 있으며, 주변분포는 다른 변수에 대해 합/적분하여 얻는다.

$$p_X(x) = \sum_y p_{X,Y}(x,y), \quad f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y)\,dy$$

## 주요 정리와 증명

### 정리 1: PDF의 필요충분조건

함수 $f: \mathbb{R} \to \mathbb{R}$가 어떤 연속 확률변수의 PDF가 될 필요충분조건은

(1) $f(x) \geq 0$ for all $x \in \mathbb{R}$
(2) $\int_{-\infty}^{\infty} f(x)\,dx = 1$

**증명:**
($\Rightarrow$) $f$가 확률변수 $X$의 PDF라면 정의에 의해 $P(a \leq X \leq b) = \int_a^b f(x)\,dx$이다. $P$는 확률이므로 $P(\mathbb{R}) = 1$이고, $P$의 비음성은 $f \geq 0$을 필요로 한다.

($\Leftarrow$) 조건 (1), (2)를 만족하는 $f$가 주어지면 $F(x) = \int_{-\infty}^x f(t)\,dt$로 CDF를 정의할 수 있다. $F$는 단조증가, 오른연속, $\lim_{x\to-\infty}F(x)=0$, $\lim_{x\to\infty}F(x)=1$을 만족하므로 어떤 확률변수의 CDF가 되며, $f$는 그 PDF가 된다. $\square$

### 정리 2: CDF의 성질

확률변수 $X$의 CDF $F_X$는 다음 성질을 만족한다.

(1) **단조증가(monotone non-decreasing):** $x \leq y$이면 $F(x) \leq F(y)$.
(2) **오른쪽 연속(right-continuous):** $\lim_{h \to 0^+} F(x+h) = F(x)$.
(3) **극한:** $\lim_{x \to -\infty} F(x) = 0$, $\lim_{x \to \infty} F(x) = 1$.

**증명:**
(1) $x \leq y$이면 $\{X \leq x\} \subseteq \{X \leq y\}$이므로 $F(x) = P(X \leq x) \leq P(X \leq y) = F(y)$.

(2) $h_n \to 0^+$인 감소수열을 잡자. 사건 $\{X \leq x + h_n\}$은 감소하는 집합열로, 그 극한은 $\bigcap_n \{X \leq x + h_n\} = \{X \leq x\}$이다. 확률의 연속성(하방 연속, continuity from above)에 의해

$$\lim_{n \to \infty} F(x + h_n) = \lim_{n \to \infty} P(X \leq x + h_n) = P(X \leq x) = F(x)$$

(3) 증가수열 $x_n \to -\infty$에 대해 $\{X \leq x_n\}$은 감소하여 $\emptyset$로 수렴하므로 $F(x_n) \to 0$. 마찬가지로 $x_n \to \infty$에 대해 $\{X \leq x_n\}$은 증가하여 $\Omega$로 수렴하므로 $F(x_n) \to 1$. $\square$

### 정리 3: 연속 확률변수에서 개별 점의 확률

연속 확률변수 $X$에 대해, 모든 실수 $a$에서 $P(X = a) = 0$이다.

**증명:** PDF $f$를 가진다고 가정하자. 임의의 $n \in \mathbb{N}$에 대해

$$P(X = a) \leq P(a \leq X \leq a + \tfrac{1}{n}) = \int_a^{a+1/n} f(x)\,dx$$

$f$는 적분 가능하므로 $n \to \infty$일 때 우변의 적분은 0으로 수렴한다(르베그 미분가능성 정리 또는 단순히 $f$의 유계성으로). 따라서 $P(X = a) = 0$. $\square$

### 정리 4: 변환된 확률변수의 분포 (LOTUS의 서술)

**LOTUS (Law of the Unconscious Statistician):** 확률변수 $X$와 함수 $g: \mathbb{R} \to \mathbb{R}$에 대해 $Y = g(X)$의 기댓값은 $X$의 분포만으로 계산할 수 있다.

이산의 경우:
$$\mathbb{E}[g(X)] = \sum_{x} g(x) p_X(x)$$

연속의 경우:
$$\mathbb{E}[g(X)] = \int_{-\infty}^{\infty} g(x) f_X(x)\,dx$$

이 공식은 $Y$의 분포를 직접 구하지 않고도 $Y$의 기댓값을 계산할 수 있게 해준다.

## 예제

**예제 1 (주사위 PMF):** 공정한 6면체 주사위의 눈금 $X$의 PMF는

$$p_X(x) = \begin{cases}
\frac{1}{6}, & x \in \{1, 2, 3, 4, 5, 6\} \\
0, & \text{otherwise}
\end{cases}$$

CDF는

$$F_X(x) = \begin{cases}
0, & x < 1 \\
\frac{1}{6}, & 1 \leq x < 2 \\
\frac{2}{6}, & 2 \leq x < 3 \\
\vdots & \vdots \\
1, & x \geq 6
\end{cases}$$

계단 함수(step function) 형태임을 확인할 수 있다.

**예제 2 (균등분포 PDF와 CDF):** 구간 $[0, 1]$에서의 연속 균등분포 $\text{U}(0, 1)$의 PDF는

$$f_X(x) = \begin{cases}
1, & 0 \leq x \leq 1 \\
0, & \text{otherwise}
\end{cases}$$

CDF는

$$F_X(x) = \begin{cases}
0, & x < 0 \\
x, & 0 \leq x \leq 1 \\
1, & x > 1
\end{cases}$$

$F'(x) = f(x)$임을 직접 확인할 수 있다: $0 \leq x \leq 1$에서 $\frac{d}{dx}x = 1 = f(x)$.

**예제 3 (지수분포 CDF):** 모수 $\lambda > 0$인 지수분포 $\text{Exp}(\lambda)$의 PDF는 $f(x) = \lambda e^{-\lambda x}$ ($x \geq 0$)이다. CDF를 구하라.

**풀이:**

$$F(x) = \int_0^x \lambda e^{-\lambda t}\,dt = \left[-e^{-\lambda t}\right]_0^x = 1 - e^{-\lambda x}$$

따라서 $F(x) = 1 - e^{-\lambda x}$ for $x \geq 0$, $F(x) = 0$ for $x < 0$이다.

**예제 4 ($P(X > 2)$ 계산):** $X$가 PDF $f(x) = \frac{1}{2}e^{-x/2}$ ($x \geq 0$)인 지수분포를 따를 때, $P(X > 2)$를 구하라.

**풀이 1 (직접 적분):**

$$P(X > 2) = \int_2^\infty \frac{1}{2}e^{-x/2}\,dx = \left[-e^{-x/2}\right]_2^\infty = e^{-1} \approx 0.368$$

**풀이 2 (CDF 이용):** $F(x) = 1 - e^{-x/2}$이므로 $P(X > 2) = 1 - F(2) = 1 - (1 - e^{-1}) = e^{-1}$.

**예제 5 (PDF에서 확률 계산):** 확률변수 $X$의 PDF가 $f_X(x) = 2x$ ($0 \leq x \leq 1$)일 때 $P(X > 0.5)$를 구하라.

**풀이:**

$$P(X > 0.5) = \int_{0.5}^1 2x\,dx = [x^2]_{0.5}^1 = 1 - 0.25 = 0.75$$

**예제 7 (CDF에서 PDF 도출):** 확률변수 $X$의 CDF가 $F(x) = 1 - e^{-2x}$ ($x \geq 0$)일 때 PDF를 구하라.

**풀이:** $f(x) = F'(x) = 2e^{-2x}$ ($x \geq 0$), $x < 0$에서는 $f(x) = 0$이다.

**예제 8 (분위수 계산):** $X$의 CDF가 $F(x) = x^2$ ($0 \leq x \leq 1$)일 때 중앙값을 구하라.

**풀이:** $F^{-1}(p) = \sqrt{p}$이므로 중앙값 $m = F^{-1}(0.5) = \sqrt{0.5} \approx 0.707$.

**예제 9 (결합분포에서 주변분포):** 결합 PDF $f_{X,Y}(x,y) = x + y$ ($0 \leq x, y \leq 1$)에서 $X$의 주변 PDF를 구하라.

**풀이:**
$$f_X(x) = \int_0^1 (x + y)\,dy = \left[xy + \frac{y^2}{2}\right]_0^1 = x + \frac{1}{2}, \quad 0 \leq x \leq 1$$

**예제 10 (PDF의 정규화 상수 결정):** $f(x) = c x^2$ ($0 \leq x \leq 1$)가 PDF가 되도록 상수 $c$를 결정하라.

**풀이:** PDF 조건 $\int_{-\infty}^{\infty} f(x)\,dx = 1$을 적용한다.

$$\int_0^1 c x^2\,dx = c \left[ \frac{x^3}{3} \right]_0^1 = \frac{c}{3} = 1$$

따라서 $c = 3$이고, $f(x) = 3x^2$ ($0 \leq x \leq 1$)이 PDF이다.

**예제 11 (CDF로 확률 계산):** $X$의 CDF $F(x) = 1 - (1+x)e^{-x}$ ($x \geq 0$)일 때 $P(1 < X < 2)$를 구하라.

**풀이:**
$$
\begin{aligned}
P(1 < X < 2) &= F(2) - F(1) \\
&= (1 - 3e^{-2}) - (1 - 2e^{-1}) \\
&= 2e^{-1} - 3e^{-2} \approx 0.736 - 0.406 = 0.330
\end{aligned}
$$

**예제 12 (이산 확률변수의 CDF):** $X$의 PMF가 $p(0) = 0.2$, $p(1) = 0.5$, $p(2) = 0.3$일 때 CDF $F(x)$를 구하고 그래프의 형태를 설명하라.

**풀이:**
$$F(x) = \begin{cases}
0, & x < 0 \\
0.2, & 0 \leq x < 1 \\
0.7, & 1 \leq x < 2 \\
1, & x \geq 2
\end{cases}$$

CDF는 계단 함수(step function) 형태로, 각 PMF가 양수인 점에서 불연속이며 도약의 크기가 해당 PMF 값과 같다.

## 연결

- **[함수](functions.html)** : 확률변수는 함수의 일종이다. 정의역이 표본공간이고 공역이 실수인 특수한 함수로, 가측성(measurability)이라는 추가 조건을 만족해야 한다.
- **[기댓값·분산·공분산](expectation-variance.html)** : 확률변수의 분포(PMF/PDF)가 주어지면 기댓값, 분산 등 특성값을 계산할 수 있다. $f_X$와 $F_X$는 모든 확률적 특성의 출발점이다.
- **[주요 분포](distributions.html)** : 베르누이, 이항, 포아송, 정규, 지수 등 구체적인 분포들은 각각 특별한 PMF/PDF를 가진다.
