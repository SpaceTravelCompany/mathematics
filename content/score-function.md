---
title: 스코어 함수·피셔 정보·크라메르-라오 하한
slug: score-function
---

## 직관적 설명

**스코어 함수(score function)** $s(x) = \nabla_x \log p(x)$는 확률밀도의 **"로그 기울기"** 이다. 밀도가 급격히 변하는 곳에서 스코어의 크기가 크며, 밀도가 증가하는 방향을 가리킨다. 스코어 함수의 기댓값은 항상 0이다($\mathbb{E}[\nabla \log p(X)] = 0$). 이는 확률분포의 "중심"을 정의하는 자연스러운 기준이다.

모수 $\theta$에 대한 스코어 함수 $s(\theta; x) = \nabla_\theta \log p(x|\theta)$는 최대가능도추정(MLE)의 핵심이다. MLE는 $\nabla_\theta \log p(x|\theta) = 0$을 풀어 구한다. 즉, MLE는 관측된 데이터에서 스코어를 0으로 만드는 $\theta$를 찾는 과정이다.

**피셔 정보(Fisher information)** $\mathcal{I}(\theta)$는 스코어 함수의 분산이다:
$$\mathcal{I}(\theta) = \mathbb{E}[(\nabla_\theta \log p(X|\theta))(\nabla_\theta \log p(X|\theta))^T]$$

피셔 정보는 데이터가 모수 $\theta$에 대해 제공하는 정보의 양을 측정한다. 기울기가 클수록(스코어가 $\theta$에 민감할수록) 한 번의 관측으로 더 많은 정보를 얻는다.

**크라메르-라오 하한(Cramér-Rao Lower Bound, CRLB)**은 추정량의 분산에 대한 이론적 하한을 제공한다:
$$\text{Var}(\hat{\theta}) \geq \frac{1}{\mathcal{I}(\theta)}$$

이는 어떤 불편 추정량(unbiased estimator)도 피셔 정보의 역수보다 작은 분산을 가질 수 없음을 의미한다. MLE는 점근적으로(asymptotically) 이 하한에 도달한다.

**랭주뱅 동역학(Langevin dynamics)**은 스코어 함수를 사용하여 복잡한 분포에서 샘플링하는 방법이다:
$$dX_t = \nabla \log p(X_t)\,dt + \sqrt{2}\,dW_t$$

이 SDE의 정상분포(stationary distribution)가 $p$가 됨은 포커-플랑크 방정식(Fokker-Planck equation)으로 증명된다. 즉, 분포의 "로그 기울기"를 따라 이동하는 확률 과정은 결국 그 분포로 수렴한다.

## 정의

**스코어 함수 (score function) — 데이터 공간:**
$$s(x) = \nabla_x \log p(x)$$

**스코어 함수 (score function) — 모수 공간:**
$$s(\theta; x) = \nabla_\theta \log p(x|\theta)$$

**스코어의 기댓값 = 0:**
$$\mathbb{E}_{p(x|\theta)}[\nabla_\theta \log p(X|\theta)] = 0$$

**피셔 정보량 (Fisher information) — 1차원:**
$$\mathcal{I}(\theta) = \mathbb{E}\left[(\nabla_\theta \log p(X|\theta))^2\right] = \int \left(\frac{\partial}{\partial\theta} \log p(x|\theta)\right)^2 p(x|\theta)\,dx$$

**피셔 정보량 (Fisher information) — 다차원:**
$$\mathcal{I}_{ij}(\theta) = \mathbb{E}\left[\frac{\partial}{\partial\theta_i} \log p(X|\theta) \cdot \frac{\partial}{\partial\theta_j} \log p(X|\theta)\right]$$

**피셔 정보 = 음의 로그가능도 2계 미분의 기댓값:**
$$\mathcal{I}(\theta) = -\mathbb{E}[\nabla_\theta^2 \log p(X|\theta)]$$

**크라메르-라오 하한 (Cramér-Rao Lower Bound) — 1차원:**
$$\text{Var}_\theta(\hat{\theta}(X)) \geq \frac{1}{\mathcal{I}(\theta)}$$

여기서 $\hat{\theta}(X)$는 $\theta$의 불편 추정량(unbiased estimator), 즉 $\mathbb{E}[\hat{\theta}(X)] = \theta$이다.

**랭주뱅 동역학 (Langevin dynamics):**
$$dX_t = \nabla \log p(X_t)\,dt + \sqrt{2}\,dW_t$$

**포커-플랑크 방정식 (Fokker-Planck equation):** 위 SDE에 대응하는 확률밀도 $p_t(x)$의 시간 진화:
$$\frac{\partial p_t}{\partial t} = -\nabla \cdot (p_t \nabla \log p) + \nabla^2 p_t$$

## 주요 정리와 증명

### 정리 1: 스코어 함수의 기댓값 = 0

**서술:** $\mathbb{E}_{p(x|\theta)}[\nabla_\theta \log p(X|\theta)] = 0$

**증명:** 적분 형태로 전개한다.
$$\mathbb{E}[\nabla_\theta \log p(X|\theta)] = \int \nabla_\theta \log p(x|\theta) \cdot p(x|\theta)\,dx$$
$$= \int \frac{\nabla_\theta p(x|\theta)}{p(x|\theta)} \cdot p(x|\theta)\,dx = \int \nabla_\theta p(x|\theta)\,dx$$

미분과 적분의 교환(적절한 정규 조건 하에서):
$$= \nabla_\theta \int p(x|\theta)\,dx = \nabla_\theta 1 = 0$$

이는 스코어 함수의 가장 기본적이면서도 중요한 성질이다. $\square$

**의미:** 스코어 함수는 모수 $\theta$의 변화에 대한 로그가능도의 민감도를 측정하며, 그 방향은 데이터에 따라 무작위로 변하지만 평균적으로는 0이다. 즉, 스코어는 "어느 방향으로 치우치지 않는다."

### 정리 2: 피셔 정보 = 스코어의 분산 = 음의 2계 미분 기댓값

**서술:** 정규 조건(regularity condition: 미분-적분 교환 가능) 하에서
$$\mathcal{I}(\theta) = \mathbb{E}[(\nabla_\theta \log p)^2] = -\mathbb{E}[\nabla_\theta^2 \log p]$$

**증명:** 첫 번째 등호는 정의다. 두 번째 등호를 증명한다.

$\nabla_\theta^2 \log p$를 전개한다:
$$\nabla_\theta^2 \log p = \nabla_\theta \left(\frac{\nabla_\theta p}{p}\right) = \frac{\nabla_\theta^2 p}{p} - \left(\frac{\nabla_\theta p}{p}\right)^2 = \frac{\nabla_\theta^2 p}{p} - (\nabla_\theta \log p)^2$$

양변에 기댓값을 취한다:
$$\mathbb{E}[\nabla_\theta^2 \log p] = \int \frac{\nabla_\theta^2 p}{p} \cdot p\,dx - \mathbb{E}[(\nabla_\theta \log p)^2]$$
$$= \int \nabla_\theta^2 p\,dx - \mathcal{I}(\theta)$$

$\int \nabla_\theta^2 p\,dx = \nabla_\theta^2 \int p\,dx = \nabla_\theta^2 1 = 0$이므로,
$$\mathbb{E}[\nabla_\theta^2 \log p] = -\mathcal{I}(\theta)$$

따라서 $\mathcal{I}(\theta) = -\mathbb{E}[\nabla_\theta^2 \log p]$. $\square$

**의미:** 피셔 정보는 로그가능도의 곡률(curvature)의 기댓값(음의 부호)이다. 곡률이 클수록(로그가능도가 $\theta$에 대해 뾰족할수록) 정보가 많고, 추정이 더 정밀해진다.

### 정리 3: 크라메르-라오 하한 (CRLB)

**서술:** $\hat{\theta}(X)$가 $\theta$의 불편 추정량일 때(정규 조건 하에서),
$$\text{Var}_\theta(\hat{\theta}(X)) \geq \frac{1}{\mathcal{I}(\theta)}$$

**증명:** 스코어 함수 $s(\theta; X) = \nabla_\theta \log p(X|\theta)$와 추정량 $\hat{\theta}(X)$의 공분산을 고려한다.

먼저, 비편향성 $\mathbb{E}[\hat{\theta}] = \theta$를 $\theta$로 미분한다:
$$1 = \frac{d}{d\theta} \mathbb{E}[\hat{\theta}(X)] = \frac{d}{d\theta} \int \hat{\theta}(x) p(x|\theta)\,dx = \int \hat{\theta}(x) \nabla_\theta p(x|\theta)\,dx$$
$$= \int \hat{\theta}(x) \frac{\nabla_\theta p(x|\theta)}{p(x|\theta)} p(x|\theta)\,dx = \int \hat{\theta}(x) s(\theta; x) p(x|\theta)\,dx = \mathbb{E}[\hat{\theta} \cdot s]$$

스코어의 기댓값이 0($\mathbb{E}[s] = 0$)이므로,
$$\text{Cov}(\hat{\theta}, s) = \mathbb{E}[\hat{\theta} s] - \mathbb{E}[\hat{\theta}] \mathbb{E}[s] = 1 - 0 = 1$$

코시-슈바르츠 부등식(Cauchy-Schwarz inequality)을 적용한다:
$$|\text{Cov}(\hat{\theta}, s)|^2 \leq \text{Var}(\hat{\theta}) \cdot \text{Var}(s)$$

$$\text{Var}(s) = \mathbb{E}[s^2] = \mathcal{I}(\theta)$$이므로,
$$1 \leq \text{Var}(\hat{\theta}) \cdot \mathcal{I}(\theta)$$

따라서 $\text{Var}(\hat{\theta}) \geq 1/\mathcal{I}(\theta)$. $\square$

**등호 조건:** 코시-슈바르츠의 등호 조건은 $s(\theta; x) = \mathcal{I}(\theta)(\hat{\theta}(x) - \theta)$일 때 성립한다. 즉, 스코어 함수가 추정 오차에 선형 비례할 때 하한에 도달한다. 이 조건을 만족하는 분포를 지수족(exponential family)이라 한다.

**다차원 CRLB:** $\hat{\boldsymbol{\theta}}$가 $\boldsymbol{\theta}$의 불편 추정량일 때,
$$\text{Cov}(\hat{\boldsymbol{\theta}}) \succeq \mathcal{I}(\boldsymbol{\theta})^{-1}$$

여기서 $\succeq$는 행렬 차이 $\text{Cov}(\hat{\boldsymbol{\theta}}) - \mathcal{I}(\boldsymbol{\theta})^{-1}$이 양반정치(positive semidefinite)임을 의미한다.

### 정리 4: 랭주뱅 동역학이 $p$를 정상분포로 가짐

**서술:** SDE $dX_t = \nabla \log p(X_t)\,dt + \sqrt{2}\,dW_t$의 해 $X_t$의 분포 $p_t(x)$는 $t \to \infty$에서 $p(x)$로 수렴한다.

**증명 (포커-플랑크 방정식):** SDE $dX_t = f(X_t)dt + \sqrt{2}\,dW_t$의 확률밀도 $p_t(x)$는 다음 포커-플랑크 방정식을 만족한다:
$$\frac{\partial p_t}{\partial t} = -\frac{\partial}{\partial x}(f p_t) + \frac{\partial^2 p_t}{\partial x^2}$$

$f(x) = \nabla \log p(x)$를 대입하면:
$$\frac{\partial p_t}{\partial t} = -\frac{\partial}{\partial x}(p_t \cdot \nabla \log p) + \frac{\partial^2 p_t}{\partial x^2}$$

정상 상태(stationary state) $\partial p_t/\partial t = 0$에서:
$$-\frac{\partial}{\partial x}(p \cdot \nabla \log p) + \frac{\partial^2 p}{\partial x^2} = 0$$
$$-\frac{\partial}{\partial x}\left(p \cdot \frac{\nabla p}{p}\right) + \nabla^2 p = 0$$
$$-\nabla^2 p + \nabla^2 p = 0$$

따라서 $p$가 정상분포임을 확인할 수 있다. 보다 엄밀한 증명은 $D_{KL}(p_t \| p)$가 시간에 따라 단조 감소함을 보이는 것이다.
$$\frac{d}{dt} D_{KL}(p_t \| p) = -\int p_t(x) \|\nabla \log p_t(x) - \nabla \log p(x)\|^2\,dx \leq 0$$

등호는 $p_t = p$일 때만 성립한다. $\square$

**의미:** 랭주뱅 동역학은 "스코어 함수를 따라 확률적으로 이동"하는 과정으로, 복잡한 분포 $p$에서 샘플링하는 도구다. 실제로는 시간 이산화(discretization)가 필요하며, 이로 인한 오차를 보정하는 메트로폴리스 조정 단계를 추가하면 메트로폴리스-조정 랭주뱅 알고리즘(MALA)이 된다.

## 예제

**예제 1 (정규분포의 스코어와 피셔 정보):** $X \sim \mathcal{N}(\mu, \sigma^2)$일 때 스코어 함수와 피셔 정보를 계산하라.

**풀이:** $\log p(x|\mu) = -\frac{1}{2}\log(2\pi\sigma^2) - \frac{(x-\mu)^2}{2\sigma^2}$

스코어 (모평균 $\mu$에 대해):
$$s(\mu; x) = \frac{\partial}{\partial\mu} \log p = \frac{x - \mu}{\sigma^2}$$

스코어의 크기는 $x$가 $\mu$에서 멀수록 커진다(더 많은 정보를 제공).

기댓값 확인: $\mathbb{E}[s(\mu; X)] = \frac{\mathbb{E}[X] - \mu}{\sigma^2} = 0$ ✓

피셔 정보:
$$\mathcal{I}(\mu) = \mathbb{E}\left[\left(\frac{X-\mu}{\sigma^2}\right)^2\right] = \frac{\text{Var}(X)}{\sigma^4} = \frac{\sigma^2}{\sigma^4} = \frac{1}{\sigma^2}$$

음의 2계 미분으로도 확인:
$$\frac{\partial^2}{\partial\mu^2} \log p = -\frac{1}{\sigma^2}, \quad -\mathbb{E}[\partial_\mu^2 \log p] = \frac{1}{\sigma^2}$$

CRLB: $\text{Var}(\hat{\mu}) \geq \sigma^2/n$ (표본평균 $\bar{X}$는 $\text{Var}(\bar{X}) = \sigma^2/n$으로 하한에 도달).

**모분산 $\sigma^2$에 대한 스코어:**
$$s(\sigma^2; x) = \frac{\partial}{\partial\sigma^2} \log p = -\frac{1}{2\sigma^2} + \frac{(x-\mu)^2}{2\sigma^4}$$

$$\mathcal{I}(\sigma^2) = \mathbb{E}\left[\left(-\frac{1}{2\sigma^2} + \frac{(X-\mu)^2}{2\sigma^4}\right)^2\right] = \frac{1}{2\sigma^4}$$

**예제 2 (크라메르-라오 하한 확인 — 포아송 분포):** $X \sim \text{Pois}(\lambda)$, $p(x|\lambda) = \lambda^x e^{-\lambda}/x!$

$$\log p = x\log\lambda - \lambda - \log x!$$
$$s(\lambda; x) = \frac{x}{\lambda} - 1$$
$$\mathcal{I}(\lambda) = \mathbb{E}\left[\left(\frac{X}{\lambda} - 1\right)^2\right] = \frac{\text{Var}(X)}{\lambda^2} = \frac{\lambda}{\lambda^2} = \frac{1}{\lambda}$$

CRLB: $\text{Var}(\hat{\lambda}) \geq \lambda/n$. 표본평균 $\bar{X}$는 $\text{Var}(\bar{X}) = \lambda/n$이므로 하한에 도달한다.

**예제 3 (크라메르-라오 하한 — 베르누이 분포):** $X \sim \text{Bernoulli}(p)$

$$\log p = x\log p + (1-x)\log(1-p)$$
$$s(p; x) = \frac{x}{p} - \frac{1-x}{1-p}$$
$$\mathcal{I}(p) = \mathbb{E}\left[\left(\frac{X}{p} - \frac{1-X}{1-p}\right)^2\right] = \frac{1}{p(1-p)}$$

CRLB: $\text{Var}(\hat{p}) \geq p(1-p)/n$. 표본비율 $\hat{p} = \bar{X}$의 분산은 $p(1-p)/n$으로 하한에 도달한다.

**예제 4 (CRLB에 도달하지 못하는 추정량):** $X \sim \mathcal{N}(\mu, \sigma^2)$에서 $\sigma^2$의 불편 추정량 $\hat{\sigma}^2 = \frac{1}{n-1}\sum (X_i - \bar{X})^2$의 분산은
$$\text{Var}(\hat{\sigma}^2) = \frac{2\sigma^4}{n-1}$$

CRLB는 $\mathcal{I}(\sigma^2)^{-1} = 2\sigma^4/n$이므로,
$$\text{Var}(\hat{\sigma}^2) = \frac{2\sigma^4}{n-1} > \frac{2\sigma^4}{n}$$

즉, $\hat{\sigma}^2$는 CRLB에 도달하지 못한다. 이는 $n \to \infty$에서 CRLB에 접근하지만(점근적 효율성), 유한 표본에서는 효율적이지 않다.

**예제 5 (랭주뱅 동역학 — 가우시안):** $p(x) = \mathcal{N}(0, 1)$일 때 랭주뱅 동역학은
$$dX_t = \nabla\log p(X_t)\,dt + \sqrt{2}\,dW_t = -X_t\,dt + \sqrt{2}\,dW_t$$

이것은 바로 오른슈타인-울렌벡(Ornstein-Uhlenbeck) 과정이다. 위 정리 4에서 보인 대로, 이 SDE의 정상분포는 $\mathcal{N}(0, 1)$이다.

**예제 6 (스코어 매칭 — 개념):** 데이터의 스코어 함수 $\nabla \log p_{\text{data}}(x)$를 직접 추정하는 것이 **스코어 매칭(score matching)**이다. $p_\theta(x)$의 스코어와 데이터의 스코어 사이의 피셔 발산(Fisher divergence)을 최소화한다:
$$D_F(p_{\text{data}} \| p_\theta) = \mathbb{E}_{p_{\text{data}}}[\|\nabla \log p_{\text{data}}(X) - \nabla \log p_\theta(X)\|^2]$$

스코어 매칭의 장점: 정규화 상수(증명 어려운 marginal likelihood)를 계산할 필요 없이, 스코어 함수(로그 기울기)만으로 밀도 추정이 가능하다.

**예제 7 (확산 모델과 스코어):** 최근 확산 모델(diffusion model)은 스코어 함수를 사용하여 데이터 분포를 학습한다. 전방 확산 과정(forward diffusion)으로 데이터에 노이즈를 점진적으로 추가하고, 역방향 과정(reverse process)에서 스코어 함수(노이즈 제거 방향)를 학습한다. 역방향 SDE는 랭주뱅 동역학과 밀접한 관련이 있다:
$$dX_t = [f(X_t, t) - g(t)^2 \nabla \log p_t(X_t)]\,dt + g(t)\,d\bar{W}_t$$

## 연결

- **[엔트로피·KL 발산](topics/entropy-kl.html)** : 피셰 정보는 KL 발산의 2차 테일러 전개 계수로 나타난다. $D_{KL}(p_\theta \| p_{\theta+d\theta}) \approx \frac{1}{2} d\theta^T \mathcal{I}(\theta) d\theta$.
- **[정보기하·자연 그래디언트](topics/information-geometry.html)** : 피셔 정보 행렬은 통계 다양체(statistical manifold)의 리만 계량(Riemannian metric)이다. 자연 그래디언트는 이 계량을 고려한 최적화 방향이다.
- **[확률미분방정식](topics/sde.html)** : 랭주뱅 동역학은 SDE의 한 형태로, 확산 모델(diffusion model)의 수학적 기초다.
- **[최대가능도추정](topics/mle.html)** : MLE의 점근 분산은 피셔 정보의 역수에 도달한다. MLE는 점근적으로 효율적(asymptotically efficient)이며, CRLB를 점근적으로 달성한다.
- **[가우시안 과정](topics/gaussian-process.html)** : GP 회귀의 하이퍼파라미터 학습은 로그 한계 가능도의 그래디언트(스코어 함수)를 사용한다.
