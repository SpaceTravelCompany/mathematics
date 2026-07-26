---
title: 결합·주변·조건부 분포
slug: joint-marginal-conditional
---

## 직관적 설명

**결합분포(joint distribution)**는 여러 확률변수의 동시적인 거동을 완전히 기술한다. 예를 들어 키(height)와 몸무게(weight)의 결합분포는 "175cm이고 70kg일 확률"을 모든 키-몸무게 쌍에 대해 알려준다.

**주변분포(marginal distribution)**는 결합분포에서 일부 변수만 보는 것이다. 키와 몸무게의 결합분포에서 몸무게에 관계없이 "키가 175cm일 확률"만 뽑아낸 것이 주변분포다. 이름은 결합분포표의 여백(margin)에 합계를 적는 관행에서 유래했다.

**조건부분포(conditional distribution)**는 한 변수의 값을 고정했을 때 다른 변수의 분포다. "몸무게가 70kg인 사람들 중에서 키의 분포"가 조건부분포의 예시다. 정보가 주어졌을 때 불확실성이 어떻게 변하는지 보여준다.

## 정의

두 확률변수 $X$, $Y$를 고려하자.

**결합분포(joint distribution):**
- 이산(discrete) 확률변수의 경우: $p_{X,Y}(x,y) = P(X = x, Y = y)$
- 연속(continuous) 확률변수의 경우: $f_{X,Y}(x,y)$ (결합확률밀도함수, joint PDF)

연속인 경우 $(x,y)$ 근방의 미소 영역에 대한 확률은 $P(x \leq X \leq x+dx,\; y \leq Y \leq y+dy) \approx f_{X,Y}(x,y)\,dx\,dy$이다.

**주변분포(marginal distribution):**
- 이산: $p_X(x) = \sum_{y} p_{X,Y}(x,y)$
- 연속: $f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y)\,dy$

주변분포는 결합분포에서 다른 변수에 대해 "합산(이산)" 또는 "적분(연속)"하여 얻는다.

**조건부분포(conditional distribution):**
- 이산: $p_{X|Y}(x|y) = \frac{p_{X,Y}(x,y)}{p_Y(y)}$, 단 $p_Y(y) > 0$
- 연속: $f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)}$, 단 $f_Y(y) > 0$

**다변량 정규분포(multivariate normal distribution):** $d$차원 확률벡터 $\mathbf{X} = (X_1,\ldots,X_d)^\top$가 평균벡터 $\boldsymbol{\mu} \in \mathbb{R}^d$와 공분산행렬 $\Sigma \in \mathbb{R}^{d \times d}$(양의 정부호, positive definite)를 가질 때

$$f_{\mathbf{X}}(\mathbf{x}) = \frac{1}{(2\pi)^{d/2} |\Sigma|^{1/2}} \exp\left(-\frac{1}{2} (\mathbf{x} - \boldsymbol{\mu})^\top \Sigma^{-1} (\mathbf{x} - \boldsymbol{\mu})\right)$$

## 주요 정리와 증명

### 정리 1: 조건부 = 결합 / 주변 (베이즈 정리의 연속 형태)

**증명:** 조건부분포의 정의에서 직접 유도된다.

$$f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)}$$

분자를 조건부분포 $f_{Y|X}(y|x)$로 표현하면

$$f_{X,Y}(x,y) = f_{Y|X}(y|x) f_X(x)$$

이를 대입하면 베이즈 정리의 연속 형태를 얻는다.

$$f_{X|Y}(x|y) = \frac{f_{Y|X}(y|x) f_X(x)}{f_Y(y)}$$

분모 $f_Y(y)$는 주변분포로, $\int f_{Y|X}(y|x) f_X(x)\,dx$와 같다. $\square$

이 형태는 $X$를 모수(parameter), $Y$를 데이터(observation)로 해석할 때 베이지안 추론의 기초가 된다.

### 정리 2: 독립 ⟺ 결합 = 주변의 곱

$X$와 $Y$가 독립(independent)일 필요충분조건은

$$f_{X,Y}(x,y) = f_X(x) f_Y(y) \quad \text{(모든 } x, y \text{에 대해)}$$

이다.

**증명:** ($\Rightarrow$) $X$와 $Y$가 독립이면 모든 $A, B \subseteq \mathbb{R}$에 대해 $P(X \in A, Y \in B) = P(X \in A) P(Y \in B)$이다. $A = [x, x+dx]$, $B = [y, y+dy]$로 잡으면 $f_{X,Y}(x,y) = f_X(x) f_Y(y)$를 얻는다.

($\Leftarrow$) 역으로 $f_{X,Y} = f_X f_Y$이면 임의의 측정가능 집합 $A, B$에 대해

$$P(X \in A, Y \in B) = \int_A \int_B f_X(x) f_Y(y)\,dy\,dx = \left(\int_A f_X(x)\,dx\right)\left(\int_B f_Y(y)\,dy\right) = P(X \in A) P(Y \in B)$$

이므로 $X$와 $Y$는 독립이다. $\square$

독립의 중요한 함의: 조건부분포는 주변분포와 같아진다. 즉 $f_{X|Y}(x|y) = f_X(x)$이다. "$Y$를 알아도 $X$에 대한 정보가 전혀 추가되지 않는다."

### 정리 3: 다변량 정규분포의 조건부도 정규

$(X, Y)$가 2변량 정규분포(bivariate normal distribution)를 따른다고 하자.

$$\begin{pmatrix} X \\ Y \end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix} \mu_X \\ \mu_Y \end{pmatrix}, \begin{pmatrix} \sigma_X^2 & \rho\sigma_X\sigma_Y \\ \rho\sigma_X\sigma_Y & \sigma_Y^2 \end{pmatrix}\right)$$

이때 $Y = y$가 주어졌을 때 $X$의 조건부분포는 다음과 같은 정규분포다.

$$X | (Y = y) \sim \mathcal{N}\left(\mu_X + \rho\frac{\sigma_X}{\sigma_Y}(y - \mu_Y),\; \sigma_X^2 (1 - \rho^2)\right)$$

**증명:** 결합밀도함수를 직접 전개하여 완전제곱(completing the square) 형태로 만든다.

결합 PDF는

$$f_{X,Y}(x,y) = \frac{1}{2\pi\sigma_X\sigma_Y\sqrt{1-\rho^2}} \exp\left(-\frac{1}{2(1-\rho^2)} Q(x,y)\right)$$

여기서 $Q(x,y)$는 이차형식(quadratic form)이다.

$$Q(x,y) = \frac{(x-\mu_X)^2}{\sigma_X^2} - 2\rho\frac{(x-\mu_X)(y-\mu_Y)}{\sigma_X\sigma_Y} + \frac{(y-\mu_Y)^2}{\sigma_Y^2}$$

$Y=y$를 고정하면 $f_{X|Y}(x|y) = f_{X,Y}(x,y) / f_Y(y)$이다. $f_Y(y)$는 주변 정규분포 $\mathcal{N}(\mu_Y, \sigma_Y^2)$의 PDF다. 두 PDF의 비율을 계산하면 $x$에 관한 항만 남는다.

$f_{X,Y}(x,y)$에서 $x$를 포함하는 부분은

$$\exp\left(-\frac{1}{2(1-\rho^2)} \left[\frac{(x-\mu_X)^2}{\sigma_X^2} - 2\rho \frac{(x-\mu_X)(y-\mu_Y)}{\sigma_X\sigma_Y}\right]\right)$$

$f_Y(y)$에서 $x$와 무관한 항을 제외하고, $x$에 관한 이차식을 완전제곱 형태로 정리한다.

$$\frac{(x-\mu_X)^2}{\sigma_X^2} - 2\rho \frac{(x-\mu_X)(y-\mu_Y)}{\sigma_X\sigma_Y} = \frac{1}{\sigma_X^2}\left[(x-\mu_X)^2 - 2\rho\frac{\sigma_X}{\sigma_Y}(x-\mu_X)(y-\mu_Y)\right]$$

이를 $\left(x - \mu_X - \rho\frac{\sigma_X}{\sigma_Y}(y-\mu_Y)\right)^2 / \sigma_X^2$ 꼴로 완전제곱하면 교차항이 일치함을 확인할 수 있다. 결과적으로

$$f_{X|Y}(x|y) = \frac{1}{\sqrt{2\pi}\,\sigma_X\sqrt{1-\rho^2}} \exp\left(-\frac{\left[x - \left(\mu_X + \rho\frac{\sigma_X}{\sigma_Y}(y-\mu_Y)\right)\right]^2}{2\sigma_X^2(1-\rho^2)}\right)$$

이므로 $X|Y=y$는 정규분포 $\mathcal{N}(\mu_X + \rho\frac{\sigma_X}{\sigma_Y}(y-\mu_Y),\; \sigma_X^2(1-\rho^2))$를 따른다. $\square$

조건부 평균이 $y$에 대한 선형함수이고, 조건부 분산이 $y$와 무관하다는 점이 주목할 만하다. 이 성질을 **동분산성(homoscedasticity)**이라 한다.

### 정리 4: 주변화(Marginalization)

연속 확률변수 $X$, $Y$에 대해

$$f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y)\,dy$$

**증명:** $F_X(x) = P(X \leq x) = \lim_{\Delta x \to 0} \frac{1}{\Delta x} P(x \leq X \leq x + \Delta x)$의 정의와 결합분포의 관계에서 직접 유도된다.

$$F_X(x) = P(X \leq x) = \int_{-\infty}^{x} \int_{-\infty}^{\infty} f_{X,Y}(t, y)\,dy\,dt$$

양변을 $x$로 미분하면(라이프니츠 규칙, Leibniz rule)

$$f_X(x) = \frac{d}{dx} F_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y)\,dy$$

$\square$

## 예제

**예제 1 (2변량 정규 조건부 분포):** $X$와 $Y$가 다음 결합 정규분포를 따른다고 하자.

$$\mu_X = 0,\quad \mu_Y = 0,\quad \sigma_X = 2,\quad \sigma_Y = 1,\quad \rho = 0.5$$

$Y = 1$일 때 $X$의 조건부 평균과 분산을 구하라.

**풀이:** 정리 3의 결과를 적용한다.

$$\mathbb{E}[X|Y=1] = 0 + 0.5 \times \frac{2}{1} \times (1 - 0) = 1$$

$$\text{Var}(X|Y=1) = 2^2 \times (1 - 0.5^2) = 4 \times 0.75 = 3$$

따라서 $X|Y=1 \sim \mathcal{N}(1, 3)$이다. $Y$의 정보가 없을 때 $X \sim \mathcal{N}(0, 4)$였으므로, 조건부 분포는 평균이 이동하고 분산이 감소했다.

**예제 2 (이산 결합표에서 주변·조건부):** 다음 결합확률표를 보자.

| $X \setminus Y$ | 0 | 1 | 2 |
|---|---|---|---|
| 0 | 0.05 | 0.10 | 0.05 |
| 1 | 0.10 | 0.20 | 0.10 |
| 2 | 0.05 | 0.10 | 0.25 |

(a) $X$의 주변분포를 구하라.
(b) $P(Y=1 | X=1)$을 구하라.
(c) $X$와 $Y$가 독립인지 판정하라.

**풀이:**
(a) $p_X(0) = 0.05 + 0.10 + 0.05 = 0.20$
$p_X(1) = 0.10 + 0.20 + 0.10 = 0.40$
$p_X(2) = 0.05 + 0.10 + 0.25 = 0.40$

(b) $P(Y=1|X=1) = \frac{p_{X,Y}(1,1)}{p_X(1)} = \frac{0.20}{0.40} = 0.50$

(c) 독립이라면 $p_{X,Y}(x,y) = p_X(x) p_Y(y)$가 모든 $(x,y)$에 대해 성립해야 한다. $Y$의 주변분포를 먼저 구한다.
$p_Y(0) = 0.05+0.10+0.05 = 0.20$
$p_Y(1) = 0.10+0.20+0.10 = 0.40$
$p_Y(2) = 0.05+0.10+0.25 = 0.40$

$(x,y) = (0,0)$을 확인하면 $p_X(0)p_Y(0) = 0.20 \times 0.20 = 0.04$이나 결합확률은 $0.05$로 일치하지 않는다. 따라서 $X$와 $Y$는 독립이 아니다.

**예제 3 (결합분포에서 조건부 기댓값):** 예제 2의 표에서 $\mathbb{E}[X|Y=2]$를 구하라.

**풀이:** $p_Y(2) = 0.40$이다.

$$p_{X|Y}(x|2) = \frac{p_{X,Y}(x,2)}{p_Y(2)} = \begin{cases} 0.05/0.40 = 0.125 & (x=0) \\ 0.10/0.40 = 0.250 & (x=1) \\ 0.25/0.40 = 0.625 & (x=2) \end{cases}$$

$$\mathbb{E}[X|Y=2] = 0 \times 0.125 + 1 \times 0.250 + 2 \times 0.625 = 1.5$$

**예제 4 (연속 결합분포의 주변화):** $X$와 $Y$의 결합 PDF가 $f_{X,Y}(x,y) = 2e^{-x}e^{-2y}$ ($x \geq 0$, $y \geq 0$)일 때 $X$의 주변 PDF를 구하라.

**풀이:**

$$f_X(x) = \int_0^\infty 2e^{-x}e^{-2y}\,dy = 2e^{-x} \int_0^\infty e^{-2y}\,dy = 2e^{-x} \cdot \frac{1}{2} = e^{-x},\quad x \geq 0$$

따라서 $X \sim \text{Exp}(1)$이다. 마찬가지로 $f_Y(y) = 2e^{-2y}$ ($y \geq 0$)이므로 $Y \sim \text{Exp}(2)$이다. $f_{X,Y}(x,y) = e^{-x} \cdot 2e^{-2y} = f_X(x) f_Y(y)$이므로 $X$와 $Y$는 독립이다.

**예제 5 (결합분포의 정규화 상수):** $f_{X,Y}(x,y) = c \cdot e^{-x^2 - y^2}$ ($x, y \in \mathbb{R}$)가 PDF가 되도록 상수 $c$를 구하라.

**풀이:** 전체 적분값이 1이 되어야 한다.

$$\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} c e^{-x^2 - y^2}\,dx\,dy = c \left(\int_{-\infty}^{\infty} e^{-x^2}\,dx\right) \left(\int_{-\infty}^{\infty} e^{-y^2}\,dy\right) = c \cdot \sqrt{\pi} \cdot \sqrt{\pi} = c\pi$$

$\int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}$임을 이용했다. $c\pi = 1$이므로 $c = 1/\pi$이다.

## 연결

- **[확률·조건부확률·베이즈 정리](conditional-bayes.html)** : 조건부분포의 정의 $P(A|B) = P(A \cap B)/P(B)$는 확률변수로 확장되어 $f_{X|Y}(x|y) = f_{X,Y}(x,y)/f_Y(y)$가 된다. 베이즈 정리는 조건부분포를 "뒤집는" 도구다.
- **[최대가능도추정](mle.html)** : 관측 데이터의 결합분포 $f(x_1,\ldots,x_n|\theta)$를 모수 $\theta$의 함수로 보는 것이 가능도(likelihood)다. iid 가정 하에 결합분포는 각 주변분포의 곱으로 인수분해된다.
- **[베이지안 추론](bayesian-inference.html)** : 사후분포 $p(\theta|D) \propto p(D|\theta)p(\theta)$는 조건부분포의 연속적 적용이다. 분모의 $p(D)$는 주변화 $p(D) = \int p(D|\theta)p(\theta)\,d\theta$로 계산된다.
