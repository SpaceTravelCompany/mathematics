---
title: 중심극한정리
slug: clt
---

## 직관적 설명

**중심극한정리(Central Limit Theorem, CLT)**는 아마 확률론에서 가장 놀라운 정리일 것이다: "무엇이든 많이 더하면 정규분포가 된다." 개별 확률변수의 분포가 무엇이든(균등, 지수, 포아송, 심지어 이산적이거나 비대칭적이더라도), 그 합(또는 평균)의 분포는 표본 크기가 커질수록 정규분포에 가까워진다.

이것이 "정규분포가 도처에 있는 이유"를 설명한다. 사람의 키가 정규분포를 따르는 것은 키가 수많은 유전적·환경적 요인의 합이기 때문이다. 측정 오차가 정규분포를 따르는 것은 다양한 오차 요인이 누적되기 때문이다.

중심극한정리의 핵심은 표본평균 $\bar{X}_n$을 표준화한 $Z_n = (\bar{X}_n - \mu)/(\sigma/\sqrt{n})$의 분포가 표준정규분포 $\mathcal{N}(0,1)$로 수렴한다는 것이다. 이는 가설검정, 신뢰구간, 표본오차 등 통계 추론의 모든 기본 절차를 정당화한다.

---
## 정의

**중심극한정리(CLT):** i.i.d. 확률변수 $X_1, X_2, \ldots, X_n$에 대해 $\mathbb{E}[X_i] = \mu$, $\text{Var}(X_i) = \sigma^2 < \infty$라 하자. 그러면 $n \to \infty$일 때

$$Z_n = \frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} \mathcal{N}(0, 1)$$

**CLT의 동치 형식들:**

(1) 합의 형식: $\frac{S_n - n\mu}{\sigma\sqrt{n}} \xrightarrow{d} \mathcal{N}(0,1)$, 여기서 $S_n = \sum_{i=1}^n X_i$.

(2) 평균의 형식: $\bar{X}_n \xrightarrow{d} \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right)$ (근사적으로).

(3) 표준화 형식: $\lim_{n\to\infty} P\left(\frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \leq z\right) = \Phi(z)$.

즉, 모든 $z \in \mathbb{R}$에 대해

$$\lim_{n \to \infty} P(Z_n \leq z) = \Phi(z) = \int_{-\infty}^z \frac{1}{\sqrt{2\pi}} e^{-t^2/2}\,dt$$

**분포수렴(convergence in distribution):** 확률변수열 $Y_n$이 $Y$로 분포수렴한다는 것은 $Y$의 모든 연속점 $y$에서

$$\lim_{n\to\infty} F_{Y_n}(y) = F_Y(y)$$

이다. $Y_n \xrightarrow{d} Y$로 표기한다.

**적률생성함수(moment generating function, MGF):** 확률변수 $X$의 MGF는

$$M_X(t) = \mathbb{E}[e^{tX}]$$

$t=0$ 근방에서 존재할 때, $M_X^{(k)}(0) = \mathbb{E}[X^k]$로 적률을 생성한다. 정규분포 $\mathcal{N}(\mu, \sigma^2)$의 MGF는 $M(t) = e^{\mu t + \sigma^2 t^2 / 2}$이다.

**특성함수(characteristic function):** 확률변수 $X$의 특성함수는

$$\varphi_X(t) = \mathbb{E}[e^{itX}] = \mathbb{E}[\cos(tX)] + i\,\mathbb{E}[\sin(tX)]$$

MGF와 달리 특성함수는 **항상 존재한다**($|e^{itX}| = 1$이므로). 모든 확률변수는 특성함수를 가지며(CDF와 일대일 대응), 특성함수의 수렴은 분포수렴과 동치다(연속성 정리).

**연속성 정리(continuity theorem, Lévy's theorem):** $X_n$의 특성함수 $\varphi_{X_n}(t)$가 어떤 함수 $\varphi(t)$로 점별 수렴하고, $\varphi(t)$가 $t=0$에서 연속이면 $\varphi$는 어떤 확률변수 $X$의 특성함수이며 $X_n \xrightarrow{d} X$이다.

---
## 주요 정리와 증명

### 정리 1: 중심극한정리 (특성함수 증명)

**증명:** $Z_i = (X_i - \mu)/\sigma$라 하면 $\mathbb{E}[Z_i] = 0$, $\text{Var}(Z_i) = 1$이다. $Z_n = \frac{1}{\sqrt{n}}\sum_{i=1}^n Z_i$이며, $Z_i$가 i.i.d.이므로

$$\varphi_{Z_n}(t) = \mathbb{E}\left[\exp\left(it\frac{1}{\sqrt{n}}\sum Z_i\right)\right] = \prod_{i=1}^n \mathbb{E}\left[\exp\left(i\frac{t}{\sqrt{n}}Z_i\right)\right] = [\varphi_Z(t/\sqrt{n})]^n$$

이제 $\varphi_Z(s)$를 $s=0$ 주변에서 테일러 전개한다. $\varphi_Z(0) = 1$, $\varphi'_Z(0) = i\mathbb{E}[Z] = 0$, $\varphi''_Z(0) = i^2 \mathbb{E}[Z^2] = -1$이므로

$$\varphi_Z(s) = 1 + \frac{\varphi'_Z(0)}{1!}s + \frac{\varphi''_Z(0)}{2!}s^2 + o(s^2) = 1 - \frac{s^2}{2} + o(s^2)$$

$s = t/\sqrt{n}$을 대입하면

$$\varphi_Z(t/\sqrt{n}) = 1 - \frac{t^2}{2n} + o\left(\frac{1}{n}\right)$$

따라서

$$\varphi_{Z_n}(t) = \left[1 - \frac{t^2}{2n} + o\left(\frac{1}{n}\right)\right]^n$$

유명한 극한 $\lim_{n\to\infty}(1 + a_n/n)^n = e^{\lim a_n}$을 사용하면

$$\lim_{n\to\infty} \varphi_{Z_n}(t) = e^{-t^2/2}$$

이는 $\mathcal{N}(0,1)$의 특성함수다. 연속성 정리에 의해 $Z_n \xrightarrow{d} \mathcal{N}(0,1)$이다. $\square$

### 정리 2: 드무아브르-라플라스 정리 (De Moivre-Laplace Theorem)

$S_n \sim \text{Bin}(n, p)$일 때, $n \to \infty$에 대해

$$\frac{S_n - np}{\sqrt{np(1-p)}} \xrightarrow{d} \mathcal{N}(0, 1)$$

**증명:** 이항분포는 $n$개의 i.i.d. 베르누이 확률변수의 합 $S_n = \sum_{i=1}^n X_i$이며, $\mathbb{E}[X_i] = p$, $\text{Var}(X_i) = p(1-p)$이다. CLT를 직접 적용하면 위 결과를 얻는다. $\square$

이것은 역사적으로 CLT의 최초 형태였다(1733년 드무아브르, 1812년 라플라스).

**연속성 수정(continuity correction):** 이항분포와 같은 이산분포를 정규분포로 근사할 때는 연속성 수정을 적용한다. $P(X = k) \approx P(k-0.5 < Y < k+0.5)$ where $Y \sim \mathcal{N}(np, np(1-p))$.

### 정리 3: 델타 방법 (Delta Method)

CLT의 확장으로, 확률변수의 함수에도 CLT를 적용할 수 있다. $g: \mathbb{R} \to \mathbb{R}$이 미분 가능하고 $g'(\mu) \neq 0$일 때

$$\sqrt{n}(g(\bar{X}_n) - g(\mu)) \xrightarrow{d} \mathcal{N}(0, [g'(\mu)]^2 \sigma^2)$$

**증명 (1차 테일러 전개):** $\bar{X}_n$을 $\mu$ 주변에서 1차 테일러 전개한다.

$$g(\bar{X}_n) = g(\mu) + g'(\mu)(\bar{X}_n - \mu) + o(|\bar{X}_n - \mu|)$$

양변을 정리하면

$$\sqrt{n}(g(\bar{X}_n) - g(\mu)) = g'(\mu) \sqrt{n}(\bar{X}_n - \mu) + o(1)$$

CLT에 의해 $\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$이므로, 우변은 분포수렴하여 $\mathcal{N}(0, [g'(\mu)]^2 \sigma^2)$이 된다. $\square$

### 정리 4: 린데베르그 조건 (Lindeberg Condition, 서술)

CLT는 i.i.d. 가정 아래 증명되었지만, 실제로는 훨씬 더 일반적인 조건에서 성립한다. 린데베르그-레비 CLT는 독립(동일 분포일 필요는 없음) 확률변수열이 다음 린데베르그 조건을 만족하면 CLT가 성립함을 보여준다.

$$\lim_{n\to\infty} \frac{1}{\sum_{i=1}^n \sigma_i^2} \sum_{i=1}^n \mathbb{E}\left[(X_i - \mu_i)^2 \cdot \mathbf{1}_{\{|X_i - \mu_i| > \epsilon s_n\}}\right] = 0,\quad \forall \epsilon > 0$$

여기서 $s_n^2 = \sum_{i=1}^n \sigma_i^2$이다. 이 조건은 개별 항의 분산이 전체 분산에 비해 지나치게 크지 않음을 의미한다. 직관적으로 말해, 어떤 단일 확률변수도 합의 분포를 지배하지 못한다는 조건이다.

---
## 예제

**예제 1 (주사위 30개 합의 분포):** 공정한 주사위 $n=30$개를 던져 눈금의 합 $S_{30}$의 분포를 구하라.

**풀이:** 각 주사위 $X_i$에 대해 $\mathbb{E}[X_i] = 3.5$, $\text{Var}(X_i) = 35/12 \approx 2.917$이다. CLT에 의해

$$\frac{S_{30} - 30 \times 3.5}{\sqrt{30 \times 35/12}} = \frac{S_{30} - 105}{\sqrt{87.5}} \approx \frac{S_{30} - 105}{9.354} \xrightarrow{d} \mathcal{N}(0,1)$$

따라서 $S_{30}$의 분포는 근사적으로 $\mathcal{N}(105, 87.5)$이다. 예를 들어 $S_{30}$이 100에서 110 사이일 확률은 표준정규분포표를 이용해 근사할 수 있다.

$$P(100 \leq S_{30} \leq 110) \approx \Phi\left(\frac{110-105}{9.354}\right) - \Phi\left(\frac{100-105}{9.354}\right) = \Phi(0.535) - \Phi(-0.535) \approx 0.407$$

**예제 2 (이항→정규 근사):** 동전을 100번 던질 때 앞면이 45번에서 55번 사이 나올 확률을 구하라.

**풀이:** $X \sim \text{Bin}(100, 0.5)$이며, $np = 50$, $np(1-p) = 25$이다. 연속성 수정(continuity correction)을 적용하면

$$
\begin{aligned}
P(45 \leq X \leq 55) &\approx P\left(\frac{44.5 - 50}{5} \leq Z \leq \frac{55.5 - 50}{5}\right) \\
&= P(-1.1 \leq Z \leq 1.1) = 2\Phi(1.1) - 1 \approx 0.7287
\end{aligned}
$$

연속성 수정은 이산 분포를 연속 분포로 근사할 때 구간 경계를 0.5만큼 조정하는 방법이다.

**예제 3 (표본오차, standard error):** CLT는 표본평균의 표준오차가 $\sigma/\sqrt{n}$임을 알려준다. $n$이 커질수록 $\bar{X}_n$의 분산이 $\sigma^2/n$으로 줄어들어 추정의 정밀도가 높아진다.

예를 들어 모평균 $\mu$, 모분산 $\sigma^2 = 100$인 모집단에서 $n=400$인 표본을 추출하면 표본평균의 표준오차는

$$\text{SE}(\bar{X}) = \frac{10}{\sqrt{400}} = 0.5$$

CLT에 의해 $\bar{X} \pm 1.96 \times 0.5$는 약 95% 신뢰구간이 된다.

**예제 4 (CLT 실험 — 다양한 분포):** 다음 각 경우에 대해 $n=30$일 때 표본평균의 분포가 정규분포에 얼마나 가까운지 살펴보자.

(a) **균등분포 $\text{U}(0,1)$:** 원래 분포는 완전히 평평하지만, 30개 균등변수의 평균은 정규분포에 매우 가깝다.

(b) **지수분포 $\text{Exp}(1)$:** 원래 분포는 심하게 비대칭(왜도 2)이지만, 30개 지수변수의 평균은 이미 상당히 대칭적인 정규분포에 가깝다.

(c) **포아송분포 $\text{Pois}(0.5)$:** 원래 분포는 대부분의 질량이 0과 1에 몰려 있지만, 표본평균의 분포는 $n=30$에서 정규분포로 근사된다.

**예제 5 (델타 방법 — 분산 안정화 변환):** $X \sim \text{Pois}(\lambda)$일 때 $\sqrt{X}$의 점근 분포를 구하라. $n=1$이므로 CLT를 직접 적용할 수 없지만, 여러 포아송 변수의 합에 델타 방법을 적용할 수 있다.

**풀이:** $X_1, \ldots, X_n \sim \text{Pois}(\lambda)$ i.i.d.라 하면 $\mathbb{E}[X_i] = \lambda$, $\text{Var}(X_i) = \lambda$이다. CLT에 의해

$$\sqrt{n}(\bar{X}_n - \lambda) \xrightarrow{d} \mathcal{N}(0, \lambda)$$

$g(x) = \sqrt{x}$에 델타 방법을 적용하면 $g'(x) = 1/(2\sqrt{x})$이고

$$\sqrt{n}(\sqrt{\bar{X}_n} - \sqrt{\lambda}) \xrightarrow{d} \mathcal{N}\left(0, \lambda \cdot \left(\frac{1}{2\sqrt{\lambda}}\right)^2\right) = \mathcal{N}\left(0, \frac{1}{4}\right)$$

즉, $\sqrt{\bar{X}_n}$의 점근 분산은 모수 $\lambda$와 무관한 $1/(4n)$이다. 이를 분산 안정화 변환(variance-stabilizing transformation)이라 한다.

**예제 6 (정규 Q-Q plot의 이해):** Q-Q plot(quantile-quantile plot)은 표본 분위수와 정규분포의 이론적 분위수를 비교하는 그래프다. CLT에 의해 표본평균의 분포가 정규분포에 가까우면 점들이 대각선 근처에 모인다. 꼬리가 두꺼운 분포(예: t-분포)에서는 양 끝에서 대각선에서 이탈한다.

**예제 7 (표본 크기 결정 — 오차 한계):** 어떤 모집단의 표준편차가 $\sigma = 15$라고 알려져 있다. 표본평균이 모평균과 $\pm 3$ 이내에 있을 확률이 95%가 되려면 필요한 표본 크기는?

**풀이:** CLT에 의해 $\bar{X} \approx \mathcal{N}(\mu, \sigma^2/n)$이다. 95% 확률로 $|\bar{X} - \mu| \leq 1.96 \cdot \sigma/\sqrt{n}$이므로

$$1.96 \cdot \frac{15}{\sqrt{n}} \leq 3 \quad \Rightarrow \quad \sqrt{n} \geq \frac{1.96 \times 15}{3} = 9.8 \quad \Rightarrow \quad n \geq 96.04$$

따라서 최소 97개의 표본이 필요하다.

**예제 8 (CLT의 한계 — 느린 수렴):** 모든 분포가 같은 속도로 정규분포에 수렴하는 것은 아니다. 대칭분포는 빠르게 수렴하지만, 심하게 비대칭인 분포(예: $\text{Exp}(0.1)$)는 더 많은 표본이 필요하다. 왜도(skewness)가 클수록 수렴이 느리다. 일반적으로 $n \geq 30$이면 충분하다고 알려져 있지만, 이는 분포의 형태에 따라 달라진다.

**예제 9 (모멘트 방법과 CLT):** 모멘트 방법(method of moments) 추정량의 점근 분포도 CLT를 따른다. 예를 들어 모평균 $\mu$의 추정량 $\hat{\mu} = \bar{X}_n$은 $\sqrt{n}(\hat{\mu} - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$을 만족한다. 모분산 $\sigma^2$의 추정량 $\hat{\sigma}^2 = \frac{1}{n}\sum (X_i - \bar{X})^2$도 CLT에 의해 점근 정규성을 가진다.

**예제 10 (Edgeworth 팽창 — CLT의 고차 보정):** CLT는 1차 근사(first-order approximation)다. 더 정확한 근사를 위해 Edgeworth 팽창(Edgeworth expansion)을 사용할 수 있다:

$$F_n(x) \approx \Phi(x) + \frac{\gamma_1}{6\sqrt{n}}(1 - x^2)\phi(x) + O\left(\frac{1}{n}\right)$$

여기서 $\gamma_1$은 왜도(skewness), $\phi$는 표준정규 PDF다. 이 팽창은 정규 근사의 오차를 보정하여, 특히 분포의 비대칭성이 클 때 유용하다.

**예제 11 (Berry-Esseen 정리 — CLT의 오차 한계):** Berry-Esseen 정리는 CLT 근사의 오차에 대한 상한을 제공한다. $X_1, \ldots, X_n$이 i.i.d.이고 $\mathbb{E}[|X_1|^3] < \infty$이면

$$\sup_{z \in \mathbb{R}} \left| P\left( \frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \leq z \right) - \Phi(z) \right| \leq \frac{C \cdot \mathbb{E}[|X_1 - \mu|^3]}{\sigma^3 \sqrt{n}}$$

여기서 $C$는 약 $0.5$의 상수다. 이는 CLT 근사의 오차가 $O(1/\sqrt{n})$ 이하임을 보장한다.

**예제 12 (CLT의 다변량 버전):** $d$차원 확률벡터 $\mathbf{X}_1, \ldots, \mathbf{X}_n$이 i.i.d.이고 $\mathbb{E}[\mathbf{X}_i] = \boldsymbol{\mu}$, 공분산행렬 $\Sigma$일 때

$$\sqrt{n}(\bar{\mathbf{X}}_n - \boldsymbol{\mu}) \xrightarrow{d} \mathcal{N}_d(\mathbf{0}, \Sigma)$$

여기서 $\mathcal{N}_d$는 $d$차원 정규분포다. 이는 각 개별 성분의 CLT가 결합분포로 확장된 것으로, 다변량 통계추론의 기초다.

---
## 연결

- **[주요 분포](distributions.html)** : CLT가 수렴하는 대상인 정규분포의 정의와 성질을 다룬다. 정규분포가 특별한 이유가 바로 CLT다.
- **[가설검정](hypothesis-testing.html)** : CLT는 z-검정(z-test)과 t-검정(t-test)의 이론적 근거다. 표본평균의 분포가 정규분포에 가깝다는 사실로부터 p-value를 계산한다.
- **[기댓값·분산](expectation-variance.html)** : CLT 증명에 등장하는 $\mu$와 $\sigma^2$이 기댓값과 분산이다. $Z_n$의 표준화 과정은 기댓값과 분산을 제거하는 과정이다.
