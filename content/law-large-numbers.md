---
title: 대수의 법칙
slug: law-large-numbers
---

## 직관적 설명

**대수의 법칙(law of large numbers)**은 "많이 반복하면 평균이 진짜 값에 수렴한다"는 직관을 수학적으로 정당화한다. 동전을 10번 던져 앞면이 7번 나올 수 있지만, 10,000번 던지면 앞면의 비율은 0.5에 가까워진다. 이것이 바로 대수의 법칙이다.

이 법칙은 확률론의 기초이자 통계학의 근간이다. 표본 평균(sample mean)이 모평균(population mean)을 추정할 수 있는 이유, 카지노가 장기적으로 항상 이기는 이유, 보험회사가 이익을 낼 수 있는 이유를 설명해준다.

**약한 대수의 법칙(Weak Law of Large Numbers, WLLN)**은 표본평균이 모평균으로 **확률수렴(convergence in probability)**한다고 말한다. 즉, 오차가 허용 한계보다 작을 확률이 표본 크기가 커짐에 따라 1로 수렴한다.

**강한 대수의 법칙(Strong Law of Large Numbers, SLLN)**은 더 강한 주장을 한다: 표본평균이 모평균으로 **거의 확실하게(almost surely)** 수렴한다. 즉, 예외적인 경우(확률 0)를 제외하면 항상 수렴한다.

## 정의

**표본평균(sample mean):** i.i.d.(independent and identically distributed) 확률변수 $X_1, X_2, \ldots, X_n$에 대해

$$\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i$$

**확률수렴(convergence in probability):** 확률변수열 $Y_n$이 $c$로 확률수렴한다는 것은 임의의 $\epsilon > 0$에 대해

$$\lim_{n \to \infty} P(|Y_n - c| > \epsilon) = 0$$

이다. $Y_n \xrightarrow{P} c$로 표기한다.

**거의 확실 수렴(almost sure convergence):** $Y_n$이 $c$로 거의 확실하게 수렴한다는 것은

$$P\left(\lim_{n \to \infty} Y_n = c\right) = 1$$

이다. $Y_n \xrightarrow{a.s.} c$로 표기한다. a.s. 수렴은 확률수렴보다 강한 조건이다.

**약한 대수의 법칙(WLLN):** i.i.d. 확률변수 $X_1, \ldots, X_n$에 대해 $\mathbb{E}[X_i] = \mu$, $\text{Var}(X_i) = \sigma^2 < \infty$이면

$$\bar{X}_n \xrightarrow{P} \mu$$

**강한 대수의 법칙(SLLN):** i.i.d. 확률변수 $X_1, \ldots, X_n$에 대해 $\mathbb{E}[|X_i|] < \infty$이고 $\mathbb{E}[X_i] = \mu$이면

$$\bar{X}_n \xrightarrow{a.s.} \mu$$

## 주요 정리와 증명

### 정리 1: 마르코프 부등식 (Markov's Inequality)

음이 아닌 확률변수 $X \geq 0$와 $a > 0$에 대해

$$P(X \geq a) \leq \frac{\mathbb{E}[X]}{a}$$

**증명:** 지표함수(indicator function)를 이용한다. $X \geq a$일 때 $\mathbf{1}_{\{X \geq a\}} = 1$이고, $X < a$일 때 $\mathbf{1}_{\{X \geq a\}} = 0$이다. 한편 $X/a \geq 1$ when $X \geq a$이므로

$$\mathbf{1}_{\{X \geq a\}} \leq \frac{X}{a}$$

양변에 기댓값을 취하면

$$P(X \geq a) = \mathbb{E}[\mathbf{1}_{\{X \geq a\}}] \leq \mathbb{E}\left[\frac{X}{a}\right] = \frac{\mathbb{E}[X]}{a}$$

$\square$

### 정리 2: 체비셰프 부등식 (Chebyshev's Inequality)

확률변수 $X$가 유한한 분산 $\text{Var}(X) = \sigma^2$을 가질 때, 임의의 $\epsilon > 0$에 대해

$$P(|X - \mu| \geq \epsilon) \leq \frac{\sigma^2}{\epsilon^2}$$

여기서 $\mu = \mathbb{E}[X]$이다.

**증명:** $Y = (X - \mu)^2$라 하자. $Y \geq 0$이므로 마르코프 부등식을 적용할 수 있다.

$$P(|X - \mu| \geq \epsilon) = P((X-\mu)^2 \geq \epsilon^2) \leq \frac{\mathbb{E}[(X-\mu)^2]}{\epsilon^2} = \frac{\text{Var}(X)}{\epsilon^2}$$

$\square$

체비셰프 부등식은 분포에 관계없이 적용되는 보편적인 부등식이라는 점에서 강력하다. 단, 분산이 유한해야 한다.

### 정리 3: 약한 대수의 법칙 (WLLN)

i.i.d. 확률변수 $X_1, \ldots, X_n$에 대해 $\mathbb{E}[X_i] = \mu$, $\text{Var}(X_i) = \sigma^2 < \infty$이면

$$\lim_{n \to \infty} P(|\bar{X}_n - \mu| \geq \epsilon) = 0$$

**증명 (체비셰프 부등식 활용):** 표본평균 $\bar{X}_n$의 기댓값과 분산을 먼저 계산한다.

$$\mathbb{E}[\bar{X}_n] = \frac{1}{n}\sum_{i=1}^n \mathbb{E}[X_i] = \mu$$

$$\text{Var}(\bar{X}_n) = \frac{1}{n^2}\sum_{i=1}^n \text{Var}(X_i) = \frac{\sigma^2}{n}$$

(독립일 때 분산의 합 공식과 공분산이 0임을 이용.)

이제 $\bar{X}_n$에 체비셰프 부등식을 적용한다.

$$P(|\bar{X}_n - \mu| \geq \epsilon) \leq \frac{\text{Var}(\bar{X}_n)}{\epsilon^2} = \frac{\sigma^2}{n\epsilon^2}$$

$n \to \infty$일 때 $\sigma^2/(n\epsilon^2) \to 0$이므로

$$\lim_{n \to \infty} P(|\bar{X}_n - \mu| \geq \epsilon) = 0$$

$\square$

이 증명은 분산이 유한할 때만 성립한다. SLLN은 분산이 무한대여도 기댓값만 유한하면 성립하지만, 증명은 더 복잡하다(보렐-칸텔리 보조정리 등 필요).

### 정리 4: 확률의 기본 부등식

**보렐-칸텔리 보조정리(Borel-Cantelli Lemma, 서술):** 사건열 $A_1, A_2, \ldots$에 대해 $\sum_{n=1}^\infty P(A_n) < \infty$이면 $P(\limsup A_n) = 0$이다. 즉, $A_n$이 무한히 많이 발생할 확률은 0이다.

이 보조정리는 SLLN 증명의 핵심 도구 중 하나다. SLLN의 증명에서는 $\bar{X}_n$이 $\mu$에서 $\epsilon$ 이상 벗어나는 사건의 확률합이 유한함을 보여, 그런 일이 무한히 반복될 확률이 0임을 증명한다.

### 정리 5: 야브론스키 부등식과 지수 부등식 (Exponential Inequality, 서술)

마르코프와 체비셰프 부등식의 일반화로, 더 빠른 수렴 속도를 제공하는 지수 부등식이 있다. 확률변수 $X$의 적률생성함수(moment generating function) $M(t) = \mathbb{E}[e^{tX}]$가 유한할 때, 체르노프 부등식(Chernoff bound)은

$$P(X \geq a) \leq \inf_{t > 0} \frac{\mathbb{E}[e^{tX}]}{e^{ta}} = \inf_{t > 0} e^{-ta} M(t)$$

를 제공한다. 이는 WLLN의 $O(1/n)$보다 훨씬 빠른 지수적 수렴(exponential convergence)을 보여준다.

### 정리 6: 수렴의 관계

확률변수열의 수렴 개념들 사이에는 다음과 같은 포함 관계가 있다.

$$\text{a.s. 수렴} \;\Rightarrow\; \text{확률수렴} \;\Rightarrow\; \text{분포수렴}$$

$L^p$ 수렴($\mathbb{E}[|Y_n - Y|^p] \to 0$)은 확률수렴을 함의하지만, 그 역은 성립하지 않는다.

**증명 (a.s. 수렴 ⇒ 확률수렴):** $Y_n \xrightarrow{a.s.} c$라면 $P(\lim Y_n = c) = 1$이다. 임의의 $\epsilon > 0$에 대해 사건 $A_n(\epsilon) = \sup_{k \geq n} |Y_k - c| > \epsilon$은 감소하여 $\limsup A_n$으로 수렴하며, 그 확률은 0이다. 따라서 $P(|Y_n - c| > \epsilon) \leq P(A_n(\epsilon)) \to 0$이다. $\square$

### 정리 7: 완전 수렴과 강한 대수의 법칙 — 코시 분포 반례

코시 분포(Cauchy distribution)는 기댓값이 존재하지 않는 분포의 대표적인 예시다. $X_1, \ldots, X_n$이 i.i.d. 표준 코시 분포 $\text{Cauchy}(0,1)$ (PDF $f(x) = 1/(\pi(1+x^2))$)를 따르면, 표본평균 $\bar{X}_n$도 같은 코시 분포를 따른다. 따라서 $\bar{X}_n$은 어떤 상수로도 수렴하지 않는다. 이는 대수의 법칙이 성립하려면 기댓값의 존재($\mathbb{E}[|X|] < \infty$)가 필요함을 보여주는 반례다.

### 정리 8: 점근 정규성 (CLT와 WLLN의 관계)

WLLN은 $\bar{X}_n \to \mu$를 말하고, CLT는 $\sqrt{n}(\bar{X}_n - \mu)$의 분포가 정규분포로 수렴함을 말한다. CLT는 WLLN보다 **더 강한 정보**를 제공한다: WLLN은 수렴의 "위치"를, CLT는 수렴의 "속도"와 "형태"를 알려준다.

구체적으로, WLLN은 $|\bar{X}_n - \mu|$가 $n \to \infty$에서 작아진다고 말하지만, 얼마나 빨리 작아지는지는 알려주지 않는다. CLT는 $\bar{X}_n - \mu \approx \mathcal{N}(0, \sigma^2/n)$임을 알려주어, 오차의 크기가 $O_p(1/\sqrt{n})$임을 보여준다.

### 정리 9: 콜모고로프의 강한 대수의 법칙 (Kolmogorov's SLLN)

$X_1, X_2, \ldots$가 i.i.d.일 때, $\mathbb{E}[|X_1|] < \infty$이면

$$\bar{X}_n \xrightarrow{a.s.} \mathbb{E}[X_1]$$

역도 성립한다: $\bar{X}_n$이 a.s. 수렴하면 $\mathbb{E}[|X_1|] < \infty$이다.

**증명의 개요:** SLLN의 증명은 WLLN보다 훨씬 정교하다. 주요 단계는 다음과 같다.

1. **절단(truncation):** $Y_k = X_k \mathbf{1}_{\{|X_k| \leq k\}}$로 정의하여 무한한 값을 제거한다.
2. **크네친 부등식(Khintchine's inequality):** $\sum \text{Var}(Y_k)/k^2 < \infty$임을 보인다.
3. **크론커커 보조정리(Kronecker's lemma):** $\sum Y_k/k$가 수렴하면 $(\sum_{i=1}^n Y_i)/n \to 0$이다.
4. **보렐-칸텔리:** 절단된 변수와 원래 변수의 차이가 유한 번만 발생함을 보인다.

이 증명은 확률론에서 가장 우아한 증명 중 하나로 꼽힌다.

## 예제

**예제 1 (주사위 평균 수렴):** 공정한 주사위를 $n$번 던졌을 때 눈의 평균을 시뮬레이션해보자. $X_i$를 $i$번째 주사위 눈금이라 하면 $\mathbb{E}[X_i] = 3.5$, $\text{Var}(X_i) = 35/12 \approx 2.917$이다.

$n = 100$일 때 체비셰프 부등식으로 $|\bar{X}_n - 3.5| \geq 0.5$일 확률의 상한을 계산하면

$$P(|\bar{X}_{100} - 3.5| \geq 0.5) \leq \frac{2.917}{100 \times 0.25} \approx 0.117$$

$n = 1000$일 때는

$$P(|\bar{X}_{1000} - 3.5| \geq 0.5) \leq \frac{2.917}{1000 \times 0.25} \approx 0.0117$$

로 1% 수준으로 줄어든다. 실제로 $n$이 커질수록 표본평균은 3.5로 수렴한다.

**예제 2 (카지노의 기댓값):** 룰렛(유럽식, 37개 칸)에서 단일 숫자에 베팅하면 당첨 확률은 $1/37$, 배당은 35배다. 한 번 베팅의 기댓값은

$$\mathbb{E}[X] = 35 \cdot \frac{1}{37} + (-1) \cdot \frac{36}{37} = -\frac{1}{37} \approx -0.027$$

즉, 1유로 베팅당 평균 약 2.7센트의 손실이다. 대수의 법칙에 의해 카지노는 장기적으로 이 금액만큼 확정적으로 수익을 얻는다. 개별 플레이어는 단기적으로 이길 수 있지만, 충분히 많은 게임을 반복하면 카지노의 수익은 예측 가능해진다.

**예제 3 (몬테카를로로 $\pi$ 추정의 근거):** 단위 정사각형 $[0,1] \times [0,1]$에 무작위로 점 $(X, Y)$를 균등하게 찍는다. 원점을 중심으로 반지름 1인 원의 1/4에 들어갈 확률은 $\pi/4$다.

$$P(X^2 + Y^2 \leq 1) = \frac{\pi}{4}$$

표본비율 $\hat{p}_n$을 $X_i^2 + Y_i^2 \leq 1$인 점의 비율이라 하면, 대수의 법칙에 의해

$$\hat{p}_n \xrightarrow{P} \frac{\pi}{4}$$

따라서 $\pi$의 추정값 $\hat{\pi}_n = 4\hat{p}_n$은 $n \to \infty$일 때 $\pi$로 수렴한다.

**예제 4 (오차의 점근적 크기):** $\bar{X}_n$이 $\mu$로 수렴할 때, 그 오차의 크기는 체비셰프 부등식에 의해 $O_p(1/\sqrt{n})$임을 알 수 있다. $P(|\bar{X}_n - \mu| \geq c/\sqrt{n}) \leq \sigma^2/c^2$이므로, $c$를 크게 잡으면 확률을 작게 만들 수 있다. 이는 CLT($\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} \mathcal{N}$)와 직접 연결된다.

**예제 5 (표본분산의 일치성):** $\hat{\sigma}^2_n = \frac{1}{n}\sum_{i=1}^n (X_i - \bar{X}_n)^2$는 대수의 법칙에 의해 모분산 $\sigma^2$로 확률수렴한다.

$$\hat{\sigma}^2_n = \frac{1}{n}\sum X_i^2 - \bar{X}_n^2 \xrightarrow{P} \mathbb{E}[X^2] - (\mathbb{E}[X])^2 = \sigma^2$$

이는 표본분산이 모분산의 일치추정량(consistent estimator)임을 보여준다.

**예제 6 (보험의 원리):** 보험회사는 대수의 법칙에 기반해 운영된다. 개별 보험 계약은 손실의 분산이 크지만, 수많은 독립 계약을 모으면 평균 손실률이 예측 가능해진다.

$n$명의 보험 가입자가 각각 연간 평균 10만 원의 보험금을 청구하고(분산 $\sigma^2$), 보험료를 12만 원씩 낸다면, 회사의 연간 수익은 $\sum (12\text{만} - X_i)$이다. 대수의 법칙에 의해 1인당 평균 수익은 $12\text{만} - 10\text{만} = 2\text{만}$ 원으로 수렴한다.

### 정리 9: 케일리 부등식과 분산의 존재

분산이 존재하지 않는 분포에서도 WLLN이 성립할 수 있을까? 일반적으로 분산이 무한대이면 체비셰프 부등식을 통한 증명은 작동하지 않지만, **약한 대수의 법칙은 분산이 유한하지 않아도 성립할 수 있다**($\mathbb{E}[|X|] < \infty$면 충분하다는 것이 크네친-콜모고로프 정리). 단, 증명은 더 복잡한 절단(truncation) 기법을 필요로 한다.

**예: 파레토 분포** $f(x) = \frac{\alpha}{x^{\alpha+1}}$ ($x \geq 1$)에서 $\alpha > 2$면 분산이 유한하지만 $1 < \alpha \leq 2$면 분산이 무한대이고, $\alpha \leq 1$면 기댓값조차 존재하지 않는다. 이때 $\alpha > 1$이면 WLLN이 성립하고, $\alpha \leq 1$이면 성립하지 않는다.

## 연결

- **[기댓값·분산·공분산](expectation-variance.html)** : WLLN 증명은 표본평균의 기댓값과 분산을 사용한다. $\mathbb{E}[\bar{X}_n] = \mu$, $\text{Var}(\bar{X}_n) = \sigma^2/n$이 핵심 계산이다.
- **[몬테카를로](monte-carlo.html)** : 대수의 법칙이 몬테카를로 방법의 이론적 근거다. $\frac{1}{n}\sum f(X_i) \xrightarrow{P} \mathbb{E}[f(X)]$를 이용해 적분을 근사한다.
