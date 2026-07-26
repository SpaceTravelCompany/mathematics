---
title: 중요도 샘플링·재파라미터 트릭
slug: importance-sampling
---

## 직관적 설명

**중요도 샘플링(importance sampling)**은 "구하기 힘든 분포의 기댓값을, 구하기 쉬운 분포로 우회하여 계산하는 방법"이다. 우리가 관심 있는 분포 $p$에서 직접 샘플링하기 어려울 때, 샘플링이 쉬운 분포 $q$에서 샘플을 추출하고 가중치 $w(x) = p(x)/q(x)$를 곱해 보정한다:

$$\mathbb{E}_p[f(X)] = \mathbb{E}_q\left[f(X)\frac{p(X)}{q(X)}\right]$$

이 아이디어는 몬테카를로 방법에서 매우 중요하다. 특히 희귀 사건(rare event) 추정, 베이즈 통계에서 사후분포(posterior)의 기댓값 계산, 강화학습에서 off-policy 평가 등에 사용된다.

**재파라미터 트릭(reparameterization trick)**은 미분 가능한 샘플링을 가능하게 하는 기술이다. 확률변수 $x \sim p_\theta(x)$에서 샘플링하는 대신, $x = g_\theta(\epsilon)$, $\epsilon \sim p(\epsilon)$으로 표현한다. 이렇게 하면 $\theta$에 대한 기댓값의 그래디언트를 샘플 내부로 전파할 수 있다:

$$\nabla_\theta \mathbb{E}_{p_\theta}[f(x)] = \mathbb{E}_{p(\epsilon)}[\nabla_\theta f(g_\theta(\epsilon))]$$

이 트릭의 핵심은 확률적 샘플링 과정을 결정론적 변환으로 "우회"하여, 미분 불가능한 샘플링 연산을 미분 가능한 함수 $g_\theta$로 대체하는 것이다.

---
## 정의

**중요도 샘플링 추정량 (importance sampling estimator):** $X_i \stackrel{\text{iid}}{\sim} q$일 때
$$\hat{I}_{\text{IS}} = \frac{1}{N} \sum_{i=1}^N f(X_i) w(X_i), \quad w(x) = \frac{p(x)}{q(x)}$$

여기서 $w(x)$를 **중요도 가중치(importance weight)**라 한다.

**지지 조건 (support condition):** $q(x) > 0$ whenever $p(x) > 0$, 즉 $p \ll q$ ($p$는 $q$에 절대연속).

**자기정규화 중요도 샘플링 (self-normalized importance sampling, SNIS):**
$$\hat{I}_{\text{SNIS}} = \frac{\sum_{i=1}^N f(X_i) w(X_i)}{\sum_{i=1}^N w(X_i)}$$

$p$가 정규화 상수(normalizing constant)까지 알려져 있지 않을 때(베이즈 사후분포 등) 유용하다.

**최적 제안분포 (optimal proposal distribution):** 분산을 최소화하는 $q^*$는
$$q^*(x) \propto |f(x)| p(x)$$

단, $f(x) \geq 0$일 때 $q^*(x) \propto f(x) p(x)$가 되며, 이 경우 분산이 0이 된다(즉 모든 가중치가 동일).

**재파라미터 트릭 (reparameterization trick):** 확률변수 $x \sim p_\theta(x)$를 $x = g_\theta(\epsilon)$, $\epsilon \sim p(\epsilon)$으로 재파라미터화하면
$$\nabla_\theta \mathbb{E}_{p_\theta}[f(x)] = \mathbb{E}_{p(\epsilon)}[\nabla_\theta f(g_\theta(\epsilon))]$$

**유효 표본 크기 (effective sample size, ESS):**
$$N_{\text{eff}} = \frac{N}{1 + \text{Var}_q(w(X))} \approx \frac{(\sum w_i)^2}{\sum w_i^2}$$

가중치의 분산이 클수록 실제 정보량이 줄어듦을 나타낸다.

---
## 주요 정리와 증명

### 정리 1: 중요도 샘플링의 비편향성

**서술:** $\mathbb{E}_q[\hat{I}_{\text{IS}}] = I = \mathbb{E}_p[f(X)]$.

**증명:** 제안분포 $q$에 대한 기댓값을 직접 계산한다.
$$\mathbb{E}_q[\hat{I}_{\text{IS}}] = \mathbb{E}_q\left[\frac{1}{N}\sum_{i=1}^N f(X_i) \frac{p(X_i)}{q(X_i)}\right] = \frac{1}{N}\sum_{i=1}^N \mathbb{E}_q\left[f(X)\frac{p(X)}{q(X)}\right]$$
$$= \mathbb{E}_q\left[f(X)\frac{p(X)}{q(X)}\right] = \int f(x)\frac{p(x)}{q(x)} q(x)\,dx = \int f(x) p(x)\,dx = \mathbb{E}_p[f(X)]$$

단, $q$의 지지 영역이 $p$의 지지 영역을 포함해야 한다($p \ll q$). 만약 어떤 $x$에서 $q(x)=0$이고 $p(x) > 0$이면 적분이 정의되지 않는다. $\square$

### 정리 2: 중요도 샘플링의 분산

**서술:** 
$$\text{Var}_q(\hat{I}_{\text{IS}}) = \frac{1}{N} \left( \mathbb{E}_q[f(X)^2 w(X)^2] - I^2 \right) = \frac{1}{N} \left( \int \frac{f(x)^2 p(x)^2}{q(x)}\,dx - I^2 \right)$$

**증명:** $X_i$가 iid이므로
$$\text{Var}_q(\hat{I}_{\text{IS}}) = \frac{1}{N} \text{Var}_q(f(X)w(X))$$
$$= \frac{1}{N} \left( \mathbb{E}_q[f(X)^2 w(X)^2] - (\mathbb{E}_q[f(X)w(X)])^2 \right)$$

$\mathbb{E}_q[f(X)w(X)] = I$이므로, 첫 항을 전개한다:
$$\mathbb{E}_q[f(X)^2 w(X)^2] = \int f(x)^2 \frac{p(x)^2}{q(x)^2} q(x)\,dx = \int \frac{f(x)^2 p(x)^2}{q(x)}\,dx$$

$\square$

**분산 발산 조건:** $q$의 꼬리가 $p$보다 가벼우면(light-tailed), $p(x)/q(x)$가 $x$의 큰 값에서 폭발하여 적분이 발산할 수 있다. 즉, 분산이 무한대가 될 수 있다. 따라서 제안분포 $q$는 $p$보다 꼬리가 두꺼워야(heavy-tailed) 안정적이다.

### 정리 3: 최적 제안분포

**서술:** $\text{Var}_q(\hat{I}_{\text{IS}})$를 최소화하는 제안분포는
$$q^*(x) = \frac{|f(x)| p(x)}{\int |f(t)| p(t)\,dt}$$

**증명:** 분산 공식에서 $I^2$는 $q$에 무관한 상수이므로, $\mathbb{E}_q[f(X)^2 w(X)^2] = \int f(x)^2 p(x)^2 / q(x)\,dx$를 $q$에 대해 최소화하면 된다. 제약 조건 $\int q(x)\,dx = 1$, $q(x) \geq 0$ 하에서 라그랑주 승수법을 적용한다.

$$\mathcal{L}[q] = \int \frac{f(x)^2 p(x)^2}{q(x)}\,dx + \lambda \left( \int q(x)\,dx - 1 \right)**

함수 $q$에 대한 변분 도함수(variational derivative)를 취한다:
$$\frac{\delta \mathcal{L}}{\delta q(x)} = -\frac{f(x)^2 p(x)^2}{q(x)^2} + \lambda = 0$$

따라서 $q(x)^2 = f(x)^2 p(x)^2 / \lambda$, 즉 $q(x) \propto |f(x)| p(x)$.

정규화 상수 $Z = \int |f(t)| p(t)\,dt$를 도입하면
$$q^*(x) = \frac{|f(x)| p(x)}{\int |f(t)| p(t)\,dt}$$

이때 분산을 계산하면
$$\int \frac{f(x)^2 p(x)^2}{q^*(x)}\,dx = \int \frac{f(x)^2 p(x)^2 \cdot Z}{|f(x)| p(x)}\,dx = Z \int |f(x)| p(x)\,dx = Z^2$$

따라서 $\text{Var}_{q^*}(\hat{I}_{\text{IS}}) = (Z^2 - I^2)/N$이다. 특히 $f(x) \geq 0$이면 $Z = I$이므로 분산이 0이 된다! $\square$

**의미:** 분산이 0이 되려면 $f(x) \geq 0$이고 $q^* \propto f(x)p(x)$여야 한다. 즉, 최적 제안분포는 $f(x)$의 부호가 변하지 않을 때만 실현 가능하다. 실제로는 정규화 상수를 알 수 없으므로 완벽한 최적은 불가능하지만, 이 정리는 제안분포 설계의 방향을 제시한다.

### 정리 4: 재파라미터 트릭의 정당성

**서술:** $x = g_\theta(\epsilon)$, $\epsilon \sim p(\epsilon)$이고 $g_\theta$가 $\theta$에 대해 미분 가능하며, $f$가 미분 가능하고 $\nabla_\theta f(g_\theta(\epsilon))$가 적분 가능하다면,
$$\nabla_\theta \mathbb{E}_{p_\theta}[f(x)] = \mathbb{E}_{p(\epsilon)}[\nabla_\theta f(g_\theta(\epsilon))]$$

**증명:** 확률변수의 변환 공식(change of variables)을 사용한다. $x \sim p_\theta(x)$이고 $x = g_\theta(\epsilon)$이므로 $p_\theta(x) = p(\epsilon) |\det J_{g_\theta^{-1}}|$이다. 그러나 재파라미터 트릭의 핵심은 기댓값을 $\epsilon$에 대한 적분으로 직접 쓴다는 점이다.

$$\mathbb{E}_{p_\theta}[f(x)] = \int f(x) p_\theta(x)\,dx = \int f(g_\theta(\epsilon)) p(\epsilon)\,d\epsilon$$

양변을 $\theta$로 미분한다. $p(\epsilon)$은 $\theta$와 무관하므로 미분-적분 교환(지배 수렴 정리, dominated convergence theorem, 적절한 정규 조건 하에서)이 가능하다:
$$\nabla_\theta \int f(g_\theta(\epsilon)) p(\epsilon)\,d\epsilon = \int \nabla_\theta f(g_\theta(\epsilon)) p(\epsilon)\,d\epsilon = \mathbb{E}_{p(\epsilon)}[\nabla_\theta f(g_\theta(\epsilon))]$$

$\square$

**재파라미터 트릭 없이:** $\nabla_\theta \mathbb{E}_{p_\theta}[f(x)] = \int f(x) \nabla_\theta p_\theta(x)\,dx$로, $\nabla_\theta p_\theta$를 계산해야 한다. 이는 $\nabla_\theta \log p_\theta(x)$로 표현할 수 있지만(스코어 함수 트릭), 분산이 클 수 있다.

**스코어 함수 트릭과의 비교:** 
$$\nabla_\theta \mathbb{E}_{p_\theta}[f(x)] = \mathbb{E}_{p_\theta}[f(x) \nabla_\theta \log p_\theta(x)] \quad\text{(REINFORCE)}$$
$$\nabla_\theta \mathbb{E}_{p_\theta}[f(x)] = \mathbb{E}_{p(\epsilon)}[\nabla_\theta f(g_\theta(\epsilon))] \quad\text{(재파라미터)}$$

재파라미터 트릭은 일반적으로 분산이 더 작지만, $p_\theta$가 재파라미터화 가능해야 하고(reparameterizable, 예: 정규분포), $f$가 미분 가능해야 한다는 제약이 있다.

---
## 예제

**예제 1 (정규 제안으로 코시 분포 기댓값 추정):** 표준 코시 분포(Cauchy distribution) $p(x) = 1/(\pi(1+x^2))$에서 $\mathbb{E}[|X|]$를 추정하라. 코시 분포는 꼬리가 두꺼워 분산이 무한대이므로 일반 몬테카를로가 불안정하다.

**풀이:** 제안분포로 $q(x) = \mathcal{N}(0, \sigma^2)$를 사용한다. $N = 10000$, $\sigma = 5$로 설정한다.

$$w(x) = \frac{p(x)}{q(x)} = \frac{1/(\pi(1+x^2))}{(1/\sqrt{2\pi}\sigma) e^{-x^2/(2\sigma^2)}}$$

$$\hat{I}_{\text{IS}} = \frac{1}{N}\sum_{i=1}^N |X_i| w(X_i), \quad X_i \sim \mathcal{N}(0, 25)$$

큰 $\sigma$를 선택한 이유: 코시 분포가 정규분포보다 꼬리가 훨씬 두껍다. 만약 $\sigma=1$을 사용하면, $|x|$가 큰 영역에서 $p(x)/q(x)$가 폭발하여 분산이 무한대가 된다. $\sigma=5$를 사용하면 $q$의 꼬리가 더 두꺼워져 가중치가 안정적이다.

**예제 2 (재파라미터 트릭 — 정규분포):** $x \sim \mathcal{N}(\mu, \sigma^2)$일 때 $\mathbb{E}[x^2]$의 $\mu$에 대한 그래디언트를 재파라미터 트릭으로 계산하라.

**풀이:** $x = \mu + \sigma\epsilon$, $\epsilon \sim \mathcal{N}(0, 1)$로 재파라미터화한다.
$$\mathbb{E}[x^2] = \mathbb{E}[(\mu + \sigma\epsilon)^2] = \mathbb{E}[\mu^2 + 2\mu\sigma\epsilon + \sigma^2\epsilon^2] = \mu^2 + \sigma^2$$

$$\nabla_\mu \mathbb{E}[x^2] = \nabla_\mu(\mu^2 + \sigma^2) = 2\mu$$

재파라미터 트릭으로:
$$\nabla_\mu \mathbb{E}[x^2] = \mathbb{E}[\nabla_\mu (\mu + \sigma\epsilon)^2] = \mathbb{E}[2(\mu + \sigma\epsilon)] = 2\mu$$

같은 결과를 얻는다. 스코어 함수 트릭으로는:
$$\nabla_\mu \mathbb{E}[x^2] = \mathbb{E}[x^2 \cdot \nabla_\mu \log p_\mu(x)] = \mathbb{E}\left[x^2 \cdot \frac{x-\mu}{\sigma^2}\right]$$

이 방법은 $\mathbb{E}[x^3]$를 계산해야 하므로 분산이 더 크다.

**예제 3 (희귀 사건 추정):** $X \sim \mathcal{N}(0, 1)$일 때 $P(X > 6) \approx 9.87 \times 10^{-10}$를 추정하라.

**일반 MC:** $10^9$개 샘플 중 약 1개만 $X > 6$을 만족한다. 비현실적이다.

**중요도 샘플링:** 제안분포 $q(x) = \mathcal{N}(6, 1)$(평균을 6으로 이동)을 사용한다.
$$\hat{P} = \frac{1}{N}\sum_{i=1}^N \mathbf{1}(X_i > 6) \frac{\phi(X_i)}{\phi(X_i - 6)}, \quad X_i \sim \mathcal{N}(6, 1)$$

여기서 $\phi$는 표준정규분포의 PDF다. $N = 10^5$이면 대부분의 샘플이 $X > 6$ 영역에서 추출되므로, 가중치가 작아도 안정적인 추정이 가능하다. 분산은 이론적으로 $O(1/N)$이다.

**예제 4 (자기정규화 중요도 샘플링):** 베이즈 사후분포 $p(\theta|D) \propto p(D|\theta)p(\theta)$의 기댓값 $\mathbb{E}[h(\theta)|D]$를 추정한다. 정규화 상수 $p(D) = \int p(D|\theta)p(\theta)\,d\theta$를 알 수 없으므로, 사전분포 $p(\theta)$를 제안으로 사용한다:
$$\hat{h} = \frac{\sum_{i=1}^N h(\theta_i) w_i}{\sum_{i=1}^N w_i}, \quad \theta_i \sim p(\theta), \quad w_i = p(D|\theta_i)$$

이 추정량은 약간 편향되어 있지만(bias $O(1/N)$), 일치 추정량(consistent estimator)이다.

**예제 5 (분산 비교 — 일반 MC vs 중요도 샘플링):** $I = \int_0^1 e^x\,dx = e-1 \approx 1.7183$를 추정한다.

(1) 일반 MC: $X \sim \text{U}(0,1)$
$$\hat{I}_{\text{MC}} = \frac{1}{N}\sum e^{X_i}, \quad \text{Var} = \frac{1}{N}\left(\int_0^1 e^{2x}dx - I^2\right) = \frac{e^2-1}{2N} - \frac{I^2}{N} \approx \frac{0.242}{N}$$

(2) 중요도 샘플링: $q(x) \propto e^x$에 비례하는 제안(정규화 상수 $C = e-1$):
$$q(x) = \frac{e^x}{e-1}, \quad w(x) = \frac{1}{e^x/(e-1)} = \frac{e-1}{e^x}$$

$$\hat{I}_{\text{IS}} = \frac{e-1}{N}\sum_{i=1}^N 1 = e-1 \quad \text{(분산 0!)}$$

최적 제안 $q^* \propto f(x)p(x) = e^x \cdot 1 = e^x$를 사용했으므로 분산이 0이 된다. 물론 이 예제는 $I$를 이미 알아야 $q$를 구성할 수 있어 현실적이지 않지만, 최적 제안의 원리를 극명하게 보여준다.

**예제 6 (재파라미터 트릭의 실제 사용):** 변분 오토인코더(variational autoencoder)에서 재파라미터 트릭이 어떻게 사용되는지 개념적으로 설명한다. $z \sim q_\phi(z|x) = \mathcal{N}(\mu_\phi(x), \sigma_\phi^2(x))$일 때,
$$z = \mu_\phi(x) + \sigma_\phi(x) \odot \epsilon, \quad \epsilon \sim \mathcal{N}(0, I)$$

이렇게 하면 $\phi$에 대한 ELBO의 그래디언트를 $\epsilon$에 대한 기댓값으로 계산할 수 있어, 낮은 분산의 그래디언트 추정이 가능하다.

---
## 연결

- **[몬테카를로](monte-carlo.html)** : 중요도 샘플링은 몬테카를로 적분의 일반화다. 비편향성과 수렴 속도 $O(1/\sqrt{N})$을 계승하지만, 분산이 제안분포 선택에 크게 의존한다.
- **[베이즈 추론](bayesian-inference.html)** : 베이즈 사후분포의 기댓값 계산은 중요도 샘플링의 주요 응용처다. MCMC와 함께 사후 예측(posterior predictive) 분포 계산에 사용된다.
- **[MCMC](mcmc.html)** : 메트로폴리스-헤이스팅스(Metropolis-Hastings) 알고리즘은 중요도 샘플링과 마르코프 체인을 결합한 것으로, 제안 분포에서 샘플링한 후 수락/기각으로 중요도 가중치를 대체한다.
- **[스코어 함수](score-function.html)** : 재파라미터 트릭과 스코어 함수 트릭(REINFORCE)은 그래디언트 추정의 두 축이다. 재파라미터 트릭은 분산이 작지만 적용 가능성이 제한적이고, 스코어 함수 트릭은 더 일반적이나 분산이 크다.
- **[확률미분방정식](sde.html)** : 중요도 샘플링은 SDE 시뮬레이션에서 희귀 사건 확률을 추정하는 데 사용된다(겔서-스트라톤 변환, Girsanov's theorem).
