---
title: 베이지안 추론
slug: bayesian-inference
---

## 직관적 설명

**베이지안 추론(Bayesian inference)**은 "새로운 데이터가 들어오면 믿음(belief)을 업데이트한다"는 원칙에 기반한다. 빈도주의(Frequentist) 통계가 "모수는 고정된 상수"라고 보는 반면, 베이지안은 "모수도 확률변수"라고 본다. 즉, 모수에 대한 불확실성을 확률분포로 표현한다.

처음에는 모수 $\theta$에 대한 **사전 믿음(prior)** $p(\theta)$이 있다. 데이터 $D$를 관측한 후에는 이 믿음이 **사후 믿음(posterior)** $p(\theta|D)$으로 갱신된다. 베이즈 정리가 이 갱신 과정을 수학적으로 정확히 기술한다.

$$p(\theta|D) = \frac{p(D|\theta)p(\theta)}{p(D)} \propto p(D|\theta)p(\theta)$$

**MAP(maximum a posteriori) 추정**은 사후분포를 최대화하는 점추정이다. MLE가 $p(D|\theta)$만 최대화했다면, MAP는 $p(D|\theta)p(\theta)$를 최대화하여 사전정보를 반영한다.

**공액 사전분포(conjugate prior)**는 사전분포와 사후분포가 같은 패밀리에 속하도록 하는 사전분포다. 계산이 크게 간편해진다. 예를 들어 베르누이 가능도의 공액 사전분포는 베타 분포다.

---
## 정의

**사전분포(prior distribution):** 데이터를 보기 전 모수 $\theta$에 대한 믿음. $p(\theta)$로 표기.

**가능도(likelihood):** $p(D|\theta) = \prod_{i=1}^n p(x_i|\theta)$ (iid 가정).

**사후분포(posterior distribution):** 데이터를 반영한 후 $\theta$에 대한 갱신된 믿음.

$$p(\theta|D) = \frac{p(D|\theta)p(\theta)}{p(D)} = \frac{p(D|\theta)p(\theta)}{\int p(D|\theta)p(\theta)\,d\theta}$$

분모 $p(D)$는 **증거(evidence)** 또는 주변가능도(marginal likelihood)라 하며, 사후분포를 정규화하는 상수다.

**MAP 추정(MAP estimation):**

$$\hat{\theta}_{\text{MAP}} = \arg\max_\theta p(\theta|D) = \arg\max_\theta \left[\ln p(D|\theta) + \ln p(\theta)\right]$$

**예측분포(predictive distribution):** 새로운 데이터 $x_{\text{new}}$의 분포를 사후분포로 평균내어 예측한다.

$$p(x_{\text{new}} | D) = \int p(x_{\text{new}} | \theta) p(\theta | D)\,d\theta$$

---
## 주요 정리와 증명

### 정리 1: 베르누이-베타 공액

$X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \text{Ber}(\theta)$이고 사전분포가 $\theta \sim \text{Beta}(\alpha, \beta)$이면, 사후분포는

$$\theta | D \sim \text{Beta}(\alpha + k,\; \beta + n - k)$$

여기서 $k = \sum_{i=1}^n x_i$는 성공 횟수다.

**증명:** 베타 분포의 PDF는

$$p(\theta) = \frac{\theta^{\alpha-1}(1-\theta)^{\beta-1}}{B(\alpha,\beta)}$$

여기서 $B(\alpha,\beta) = \Gamma(\alpha)\Gamma(\beta)/\Gamma(\alpha+\beta)$는 베타 함수(beta function)다.

베르누이 가능도는 $p(D|\theta) = \theta^k (1-\theta)^{n-k}$이다.

사후분포는 사전분포와 가능도의 곱에 비례한다.

$$p(\theta|D) \propto p(D|\theta)\,p(\theta) \propto \theta^k (1-\theta)^{n-k} \cdot \theta^{\alpha-1}(1-\theta)^{\beta-1}$$

$$= \theta^{(\alpha + k) - 1} (1-\theta)^{(\beta + n - k) - 1}$$

이는 $\text{Beta}(\alpha+k, \beta+n-k)$의 PDF의 핵(kernel)과 동일한 형태다. 정규화 상수를 포함해 쓰면

$$p(\theta|D) = \frac{\theta^{\alpha+k-1}(1-\theta)^{\beta+n-k-1}}{B(\alpha+k,\;\beta+n-k)}$$

$\square$

베타 분포의 모수가 데이터에 의해 단순히 덧셈으로 갱신된다. $\alpha$는 성공 횟수만큼, $\beta$는 실패 횟수만큼 증가한다. 사전분포의 $\alpha$와 $\beta$를 "가상의 성공/실패 횟수"로 해석할 수 있다.

### 정리 2: 정규-정규 공액 (Normal-Normal Conjugate)

$X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \mathcal{N}(\theta, \sigma^2)$이고 $\sigma^2$는 알려져 있다. 사전분포가 $\theta \sim \mathcal{N}(\mu_0, \tau^2)$이면 사후분포는

$$\theta | D \sim \mathcal{N}\left(\frac{\frac{\mu_0}{\tau^2} + \frac{n\bar{x}}{\sigma^2}}{\frac{1}{\tau^2} + \frac{n}{\sigma^2}},\; \frac{1}{\frac{1}{\tau^2} + \frac{n}{\sigma^2}}\right)$$

**증명:** 정규분포의 PDF를 이용하여 사후분포의 비례식을 전개한다.

$$p(\theta|D) \propto p(D|\theta)\,p(\theta) = \left[\prod_{i=1}^n \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x_i-\theta)^2}{2\sigma^2}}\right] \cdot \frac{1}{\sqrt{2\pi}\,\tau} e^{-\frac{(\theta-\mu_0)^2}{2\tau^2}}$$

로그를 취하면 (정규화 상수를 무시하고 $\theta$에 의존하는 항만)

$$\ln p(\theta|D) = -\frac{1}{2\sigma^2}\sum_{i=1}^n (x_i-\theta)^2 - \frac{1}{2\tau^2}(\theta-\mu_0)^2 + \text{const}$$

$\sum (x_i-\theta)^2 = \sum (x_i^2 - 2x_i\theta + \theta^2) = \sum x_i^2 - 2n\bar{x}\theta + n\theta^2$를 대입한다.

$$\ln p(\theta|D) = -\frac{1}{2\sigma^2}\left(\sum x_i^2 - 2n\bar{x}\theta + n\theta^2\right) - \frac{1}{2\tau^2}(\theta^2 - 2\mu_0\theta + \mu_0^2) + \text{const}$$

$\theta$에 관한 이차항과 일차항만 모은다.

$$\ln p(\theta|D) = -\frac{1}{2}\left(\frac{n}{\sigma^2} + \frac{1}{\tau^2}\right)\theta^2 + \left(\frac{n\bar{x}}{\sigma^2} + \frac{\mu_0}{\tau^2}\right)\theta + \text{const}$$

이차식 $-\frac{1}{2}A\theta^2 + B\theta + \text{const}$의 형태는 정규분포의 로그 PDF와 같다. 완전제곱(completing the square)을 수행한다.

$$-\frac{1}{2}A\left(\theta^2 - 2\frac{B}{A}\theta\right) = -\frac{1}{2}A\left(\theta - \frac{B}{A}\right)^2 + \frac{B^2}{2A}$$

따라서 사후분포는 $\theta \sim \mathcal{N}(B/A, 1/A)$이다. 즉

$$A = \frac{1}{\tau^2} + \frac{n}{\sigma^2}, \qquad B = \frac{\mu_0}{\tau^2} + \frac{n\bar{x}}{\sigma^2}$$

$$\mu_n = \frac{B}{A} = \frac{\frac{\mu_0}{\tau^2} + \frac{n\bar{x}}{\sigma^2}}{\frac{1}{\tau^2} + \frac{n}{\sigma^2}}, \qquad \tau_n^2 = \frac{1}{A} = \frac{1}{\frac{1}{\tau^2} + \frac{n}{\sigma^2}}$$

$\square$

사후평균 $\mu_n$은 사전평균 $\mu_0$와 표본평균 $\bar{x}$의 **정밀도 가중 평균(precision-weighted average)**이다. 정밀도(precision)는 분산의 역수 $1/\tau^2$, $n/\sigma^2$으로 정의된다. 데이터가 많을수록($n$이 클수록) $\bar{x}$의 가중치가 커진다.

### 정리 3: MAP vs MLE — 점근적 동등성

$n \to \infty$일 때 사전분포의 영향은 사라지고, MAP 추정량은 MLE와 일치한다.

**증명 (서술):** MAP 추정은 $\ln p(\theta|D) = \ell(\theta) + \ln p(\theta) + \text{const}$를 최대화한다. 여기서 $\ell(\theta) = \sum_{i=1}^n \ln p(x_i|\theta)$는 로그가능도다. $n$이 커짐에 따라 $\ell(\theta)$는 $O(n)$으로 증가하는 반면, $\ln p(\theta)$는 $O(1)$로 고정된다. 따라서 $n \to \infty$에서 사전 항 $\ln p(\theta)$는 무시 가능해지고, MAP는 MLE로 수렴한다.

더 정확히는 $\frac{1}{n}\ell(\theta) \to \mathbb{E}[\ln p(X|\theta)]$이고, 이 기댓값이 KL 발산 $D_{KL}(p(\cdot|\theta_0) \| p(\cdot|\theta))$와 연결되어 참값 $\theta_0$에서 최대화된다. $\square$

MLE는 균등 사전분포(uniform prior) $p(\theta) \propto 1$의 MAP와 같다. 균등 사전은 "모든 모수 값에 동일한 사전 확률"을 부여하므로, 사후 최대화는 가능도 최대화와 동일해진다.

### 정리 4: 예측분포의 계산

예측분포 $p(x_{\text{new}} | D) = \int p(x_{\text{new}} | \theta) p(\theta | D)\,d\theta$는 사후분포를 가중치로 한 가능도의 평균이다.

**증명 (서술):** 조건부확률의 연쇄법칙과 주변화(marginalization)를 적용한다. $x_{\text{new}}$와 $D$는 $\theta$가 주어졌을 때 조건부 독립이므로

$$p(x_{\text{new}} | D, \theta) = p(x_{\text{new}} | \theta)$$

따라서

$$p(x_{\text{new}} | D) = \int p(x_{\text{new}}, \theta | D)\,d\theta = \int p(x_{\text{new}} | \theta, D) p(\theta | D)\,d\theta$$

$$= \int p(x_{\text{new}} | \theta) p(\theta | D)\,d\theta$$

$\square$

---
## 예제

**예제 1 (동전 던지기 베타-이항 업데이트):** 동전의 앞면 확률 $\theta$에 대한 사전분포를 $\text{Beta}(2, 2)$로 둔다(어느 쪽으로도 치우치지 않았다는 믿음). 동전을 10번 던져 7번 앞면이 나왔다. 사후분포를 구하라.

**풀이:** $n=10$, $k=7$, $\alpha=2$, $\beta=2$이므로

$$\theta|D \sim \text{Beta}(2+7,\; 2+10-7) = \text{Beta}(9, 5)$$

사후평균은 $\mathbb{E}[\theta|D] = \frac{9}{9+5} \approx 0.643$이다. 사전평균이 $0.5$였던 것과 비교하면 데이터(7/10=0.7) 쪽으로 이동했다.

MAP 추정치는 베타 분포의 최빈값(mode) $(\alpha-1)/(\alpha+\beta-2) = 8/12 \approx 0.667$이다. MLE는 $0.7$로, 사전의 영향으로 MAP가 MLE보다 약간 낮다.

**예제 2 (정규 평균의 사후분포):** 한 제품의 무게가 정규분포 $\mathcal{N}(\theta, 4)$를 따른다고 알려져 있다($\sigma^2=4$). 사전분포를 $\theta \sim \mathcal{N}(50, 9)$로 두었다($\mu_0=50$, $\tau^2=9$). 5개의 표본 $[52, 49, 51, 53, 50]$을 관측했다. 사후분포를 구하라.

**풀이:** $n=5$, $\bar{x}=51$, $\sigma^2=4$, $\mu_0=50$, $\tau^2=9$이다.

$$\mu_n = \frac{\frac{50}{9} + \frac{5 \times 51}{4}}{\frac{1}{9} + \frac{5}{4}} = \frac{5.556 + 63.75}{0.111 + 1.25} = \frac{69.306}{1.361} \approx 50.93$$

$$\tau_n^2 = \frac{1}{\frac{1}{9} + \frac{5}{4}} = \frac{1}{0.111 + 1.25} = \frac{1}{1.361} \approx 0.735$$

따라서 $\theta | D \sim \mathcal{N}(50.93, 0.735)$이다. 사후 표준편차는 $\sqrt{0.735} \approx 0.857$로, 사전 표준편차 $3$에 비해 크게 줄었다.

**예제 3 (예측분포):** 예제 2의 사후분포를 이용해 새로운 제품의 무게 $x_{\text{new}}$에 대한 예측분포를 구하라.

**풀이:** 예측분포는 $p(x_{\text{new}} | D) = \int \mathcal{N}(x_{\text{new}} | \theta, 4) \cdot \mathcal{N}(\theta | 50.93, 0.735)\,d\theta$이다.

정규분포의 적분 공식에 의해

$$x_{\text{new}} | D \sim \mathcal{N}(50.93,\; 4 + 0.735) = \mathcal{N}(50.93,\; 4.735)$$

예측분포의 분산은 관측 오차(4)와 모수 추정의 불확실성(0.735)이 합쳐진 것이다. 표본이 많아질수록 $\tau_n^2$가 줄어들어 예측분포는 $\mathcal{N}(\bar{x}, \sigma^2)$에 가까워진다.

**예제 4 (MAP 추정 — L2 정규화):** 선형회귀에서 $y_i \sim \mathcal{N}(w^\top x_i, \sigma^2)$이고 사전분포를 $w \sim \mathcal{N}(0, \lambda^{-1}I)$로 두면, MAP 추정은 L2 정규화(ridge regression)와 동일하다. $\ln p(w|D)$를 최대화하는 것은 다음을 최소화하는 것과 같다.

$$\sum_{i=1}^n (y_i - w^\top x_i)^2 + \frac{\sigma^2}{\lambda} \|w\|^2$$

즉, 오차 제곱합에 가중치의 제곱합을 패널티로 더한 것이다. 사전분포가 "가중치가 0 근처에 있을 것이다"라는 믿음을 반영한다.

**예제 5 (사전분포의 영향이 사라지는 과정):** $\text{Beta}(1,1)$(균등분포)를 사전으로 하고 동전을 $n$번 던져 $k$번 앞면이 나온 경우를 생각하자. 사후평균은

$$\mathbb{E}[\theta|D] = \frac{1+k}{1+k+1+n-k} = \frac{k+1}{n+2}$$

$n$이 작을 때(예: $n=1$, $k=1$) 사후평균은 $2/3 \approx 0.667$으로, MLE($1.0$)보다 덜 극단적이다. $n$이 커질수록 사후평균은 $k/n$에 수렴한다.

---
## 연결

- **[확률·조건부확률·베이즈 정리](conditional-bayes.html)** : 베이지안 추론의 수학적 기반은 베이즈 정리 $P(\theta|D) \propto P(D|\theta)P(\theta)$다. 조건부확률의 연속적인 적용으로 사전→사후 갱신이 이루어진다.
- **[가우시안 과정](gaussian-process.html)** : 가우시안 과정(GP)은 베이지안 추론을 함수 공간으로 확장한 것이다. GP 사후분포는 관측 데이터에 의해 조건부로 갱신되며, 정규-정규 공액 구조의 무한차원 일반화로 볼 수 있다.
- **[엔트로피·KL발산](entropy-kl.html)** : 사후분포는 데이터가 제공하는 정보량을 KL 발산으로 측정하여 사전분포로부터 얼마나 이동했는지 정량화할 수 있다. $D_{KL}(p(\theta|D) \| p(\theta))$는 데이터의 정보 기여도를 나타낸다.
