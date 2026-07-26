---
title: 기댓값·분산·공분산·상관계수
slug: expectation-variance
---

## 직관적 설명

**기댓값(expected value)**은 "확률변수의 장기 평균"이다. 주사위를 무한히 던져 나온 눈의 평균은 $(1+2+3+4+5+6)/6 = 3.5$로 수렴한다. 기댓값은 확률분포의 **무게중심(center of mass)** 역할을 한다.

**분산(variance)**은 "데이터가 평균에서 얼마나 퍼져 있는지"를 측정한다. 분산이 크면 값들이 평균에서 멀리 흩어져 있고, 작으면 평균 주변에 밀집되어 있다. 표준편차(standard deviation)는 분산의 제곱근으로, 원래 단위로 해석 가능하게 만든다.

**공분산(covariance)**은 "두 확률변수가 함께 움직이는 정도"를 나타낸다. 양의 공분산은 한 변수가 클 때 다른 변수도 큰 경향을, 음의 공분산은 반대 경향을 의미한다. **상관계수(correlation coefficient)**는 공분산을 각각의 표준편차로 나누어 -1에서 1 사이로 정규화한 값으로, 단위에 무관하게 관계의 강도를 측정한다.

---
## 정의

**기댓값(expected value, mean):** 확률변수 $X$의 기댓값 $\mathbb{E}[X]$ (또는 $\mu_X$)는

- 이산: $\mathbb{E}[X] = \sum_{x} x \cdot p_X(x)$
- 연속: $\mathbb{E}[X] = \int_{-\infty}^{\infty} x \cdot f_X(x)\,dx$

적분 또는 급수가 절대수렴(absolute convergence)할 때 정의된다.

**분산(variance):**

$$\text{Var}(X) = \mathbb{E}[(X - \mu)^2] = \mathbb{E}[X^2] - \mu^2$$

**표준편차(standard deviation):** $\sigma_X = \sqrt{\text{Var}(X)}$

**공분산(covariance):** 두 확률변수 $X$, $Y$에 대해

$$\text{Cov}(X, Y) = \mathbb{E}[(X - \mu_X)(Y - \mu_Y)] = \mathbb{E}[XY] - \mu_X \mu_Y$$

**상관계수(correlation coefficient):**

$$\rho_{XY} = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}$$

---
## 주요 정리와 증명

### 정리 0: 기댓값의 선형성 (Linearity of Expectation)

상수 $a, b$와 확률변수 $X, Y$에 대해

$$\mathbb{E}[aX + bY] = a\mathbb{E}[X] + b\mathbb{E}[Y]$$

**증명 (연속의 경우):**

$$
\begin{aligned}
\mathbb{E}[aX + bY] &= \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} (ax + by) f_{X,Y}(x,y) \,dx\,dy \\
&= a \int x \left(\int f_{X,Y}\,dy\right) dx + b \int y \left(\int f_{X,Y}\,dx\right) dy \\
&= a \int x f_X(x)\,dx + b \int y f_Y(y)\,dy = a\mathbb{E}[X] + b\mathbb{E}[Y]
\end{aligned}
$$

$\square$

기댓값의 선형성은 $X$와 $Y$의 독립 여부와 무관하게 성립한다는 점이 중요하다.

### 정리 1: 분산의 계산 공식

$$\text{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2$$

**증명:** $\mu = \mathbb{E}[X]$라 하자.

$$
\begin{aligned}
\text{Var}(X) &= \mathbb{E}[(X - \mu)^2] = \mathbb{E}[X^2 - 2\mu X + \mu^2] \\
&= \mathbb{E}[X^2] - 2\mu \mathbb{E}[X] + \mu^2 \\
&= \mathbb{E}[X^2] - 2\mu^2 + \mu^2 = \mathbb{E}[X^2] - \mu^2
\end{aligned}
$$

$\square$

### 정리 2: 분산의 선형 변환

$\text{Var}(aX + b) = a^2 \text{Var}(X)$, 여기서 $a, b$는 상수.

**증명:** $\mu = \mathbb{E}[X]$라 하면 $\mathbb{E}[aX + b] = a\mu + b$이다.

$$
\begin{aligned}
\text{Var}(aX + b) &= \mathbb{E}[(aX + b - (a\mu + b))^2] \\
&= \mathbb{E}[a^2(X - \mu)^2] = a^2 \mathbb{E}[(X - \mu)^2] = a^2 \text{Var}(X)
\end{aligned}
$$

$\square$

참고: 상수 $b$는 분산에 영향을 주지 않는다(분포의 위치 이동은 퍼짐을 바꾸지 않음).

### 정리 3: 독립이면 공분산은 0 (역은 성립 안 함)

$X$와 $Y$가 독립이면 $\text{Cov}(X, Y) = 0$이다.

**증명:** $X$와 $Y$가 독립이면 모든 함수 $g, h$에 대해 $\mathbb{E}[g(X)h(Y)] = \mathbb{E}[g(X)]\mathbb{E}[h(Y)]$가 성립한다. $g(x) = x$, $h(y) = y$를 대입하면

$$\mathbb{E}[XY] = \mathbb{E}[X]\mathbb{E}[Y]$$

따라서 $\text{Cov}(X, Y) = \mathbb{E}[XY] - \mu_X \mu_Y = \mu_X \mu_Y - \mu_X \mu_Y = 0$. $\square$

**역이 성립하지 않는 반례:** $X \sim \text{U}(-1, 1)$(균등분포)이고 $Y = X^2$이라 하자. $Y$는 $X$의 결정적 함수이므로 당연히 독립이 아니다. 그런데

$$\mathbb{E}[X] = 0,\quad \mathbb{E}[XY] = \mathbb{E}[X^3] = 0$$

이므로 $\text{Cov}(X, Y) = 0$이다. 즉, 공분산이 0이어도 두 변수 사이에 비선형 의존성이 존재할 수 있다.

### 정리 4: 상관계수의 범위

$$|\rho_{XY}| \leq 1$$

**증명 (코시-슈바르츠 부등식, Cauchy-Schwarz inequality):** 확률변수에 대한 코시-슈바르츠 부등식은

$$|\mathbb{E}[UV]|^2 \leq \mathbb{E}[U^2] \cdot \mathbb{E}[V^2]$$

여기서 $U = X - \mu_X$, $V = Y - \mu_Y$라 두면

$$|\text{Cov}(X,Y)|^2 = |\mathbb{E}[UV]|^2 \leq \mathbb{E}[U^2] \cdot \mathbb{E}[V^2] = \text{Var}(X) \cdot \text{Var}(Y)$$

양변에 제곱근을 취하고 $\sigma_X \sigma_Y$로 나누면 $|\rho_{XY}| \leq 1$. $\square$

등호는 $Y$가 $X$의 선형함수일 때($Y = aX + b$) 성립한다.

### 정리 5: 합의 분산

$$\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X, Y)$$

**증명:**

$$
\begin{aligned}
\text{Var}(X + Y) &= \mathbb{E}[(X + Y - \mu_X - \mu_Y)^2] \\
&= \mathbb{E}[((X - \mu_X) + (Y - \mu_Y))^2] \\
&= \mathbb{E}[(X - \mu_X)^2] + \mathbb{E}[(Y - \mu_Y)^2] + 2\mathbb{E}[(X - \mu_X)(Y - \mu_Y)] \\
&= \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X, Y)
\end{aligned}
$$

$\square$

일반화: $n$개 확률변수에 대해 $\text{Var}\left(\sum_{i=1}^n a_i X_i\right) = \sum_{i=1}^n a_i^2 \text{Var}(X_i) + 2\sum_{i<j} a_i a_j \text{Cov}(X_i, X_j)$.

---
## 예제

**예제 1 (이항분포의 기댓값과 분산):** $X \sim \text{Bin}(n, p)$일 때 $\mathbb{E}[X] = np$, $\text{Var}(X) = np(1-p)$임을 보여라.

**풀이:** $X = \sum_{i=1}^n X_i$, $X_i \sim \text{Ber}(p)$ (i.i.d.)로 표현하자. $X_i$의 기댓값은

$$\mathbb{E}[X_i] = 1 \cdot p + 0 \cdot (1-p) = p$$

기댓값의 선형성에 의해 $\mathbb{E}[X] = \sum \mathbb{E}[X_i] = np$.

$\mathbb{E}[X_i^2] = 1^2 \cdot p + 0^2 \cdot (1-p) = p$이므로

$$\text{Var}(X_i) = \mathbb{E}[X_i^2] - (\mathbb{E}[X_i])^2 = p - p^2 = p(1-p)$$

독립인 베르누이 변수의 합이므로 공분산 항은 0이고

$$\text{Var}(X) = \sum_{i=1}^n \text{Var}(X_i) = np(1-p)$$

**예제 2 (균등분포의 기댓값과 분산):** $X \sim \text{U}(a, b)$의 기댓값과 분산을 구하라.

**풀이:** PDF는 $f(x) = 1/(b-a)$ ($a \leq x \leq b$)이다.

$$\mathbb{E}[X] = \int_a^b x \cdot \frac{1}{b-a}\,dx = \frac{1}{b-a} \left[ \frac{x^2}{2} \right]_a^b = \frac{b^2 - a^2}{2(b-a)} = \frac{a+b}{2}$$

$$\mathbb{E}[X^2] = \int_a^b x^2 \cdot \frac{1}{b-a}\,dx = \frac{1}{b-a} \left[ \frac{x^3}{3} \right]_a^b = \frac{b^3 - a^3}{3(b-a)} = \frac{a^2 + ab + b^2}{3}$$

$$\text{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2 = \frac{a^2 + ab + b^2}{3} - \frac{(a+b)^2}{4} = \frac{(b-a)^2}{12}$$

**예제 3 (공분산 행렬):** 세 확률변수 $X$, $Y$, $Z$의 공분산 행렬은

$$\Sigma = \begin{pmatrix}
\text{Var}(X) & \text{Cov}(X, Y) & \text{Cov}(X, Z) \\
\text{Cov}(Y, X) & \text{Var}(Y) & \text{Cov}(Y, Z) \\
\text{Cov}(Z, X) & \text{Cov}(Z, Y) & \text{Var}(Z)
\end{pmatrix}$$

공분산 행렬은 항상 대칭(symmetric)이고 양의 준정치(positive semidefinite)이다. 예를 들어 $X, Y, Z$가 각각 키, 몸무게, 나이라고 하면 대각 성분은 각 변수의 분산, 비대각 성분은 변수 간 공분산을 나타낸다.

**예제 4 (상관계수 계산):** 다음 결합분포를 가지는 $(X, Y)$의 상관계수를 구하라.

| $X \setminus Y$ | 0 | 1 |
|---|---|---|
| 0 | 0.2 | 0.3 |
| 1 | 0.1 | 0.4 |

**풀이:** 먼저 주변분포를 구한다.
- $P(X=0) = 0.2 + 0.3 = 0.5$, $P(X=1) = 0.1 + 0.4 = 0.5$
- $P(Y=0) = 0.2 + 0.1 = 0.3$, $P(Y=1) = 0.3 + 0.4 = 0.7$

$\mathbb{E}[X] = 0 \cdot 0.5 + 1 \cdot 0.5 = 0.5$
$\mathbb{E}[Y] = 0 \cdot 0.3 + 1 \cdot 0.7 = 0.7$
$\mathbb{E}[XY] = 0\cdot0\cdot0.2 + 0\cdot1\cdot0.3 + 1\cdot0\cdot0.1 + 1\cdot1\cdot0.4 = 0.4$

$\text{Cov}(X,Y) = 0.4 - 0.5 \times 0.7 = 0.4 - 0.35 = 0.05$
$\text{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2 = 0.5 - 0.25 = 0.25$, $\sigma_X = 0.5$
$\text{Var}(Y) = \mathbb{E}[Y^2] - (\mathbb{E}[Y])^2 = 0.7 - 0.49 = 0.21$, $\sigma_Y = \sqrt{0.21} \approx 0.458$

$$\rho = \frac{0.05}{0.5 \times 0.458} \approx 0.218$$

**예제 5 (기댓값의 선형성 활용 — 구간 추정):** $n$개의 i.i.d. 확률변수 $X_1, \ldots, X_n$의 표본분산 $S^2 = \frac{1}{n-1}\sum (X_i - \bar{X})^2$에 대해 $\mathbb{E}[S^2] = \sigma^2$임을 보여라.

**풀이:** $\mathbb{E}[(X_i - \bar{X})^2]$를 먼저 계산한다.

$$
\begin{aligned}
\mathbb{E}\left[\sum_{i=1}^n (X_i - \bar{X})^2\right] &= \mathbb{E}\left[\sum_{i=1}^n X_i^2 - n\bar{X}^2\right] \\
&= \sum_{i=1}^n \mathbb{E}[X_i^2] - n\mathbb{E}[\bar{X}^2] \\
&= n(\sigma^2 + \mu^2) - n\left(\frac{\sigma^2}{n} + \mu^2\right) \\
&= n\sigma^2 + n\mu^2 - \sigma^2 - n\mu^2 = (n-1)\sigma^2
\end{aligned}
$$

따라서 $\mathbb{E}[S^2] = \frac{1}{n-1} \cdot (n-1)\sigma^2 = \sigma^2$, 즉 $S^2$는 $\sigma^2$의 불편추정량(unbiased estimator)이다.

---
## 연결

- **[적분의 의미](integral-meaning.html)** : 연속 확률변수의 기댓값 $\int x f(x)\,dx$는 적분의 직접적인 응용이다. 가중평균(weighted average)으로서의 적분 해석이 확률로 확장된다.
- **[중심극한정리](clt.html)** : CLT는 $\sqrt{n}(\bar{X}_n - \mu)/\sigma \xrightarrow{d} \mathcal{N}(0,1)$로, 표본평균의 분포가 정규분포로 수렴함을 보여준다. 이때 분산 $\sigma^2$이 핵심 역할을 한다.
- **[회귀분석](regression-analysis.html)** : 상관계수는 회귀분석에서 두 변수의 선형 관계 강도를 측정한다. 회귀계수 $\beta = \text{Cov}(X,Y)/\text{Var}(X)$와 직접 연결된다.
