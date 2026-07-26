---
title: 마르코프 체인·MCMC
slug: mcmc
---

## 직관적 설명

**MCMC(Markov Chain Monte Carlo)**는 직접 샘플링하기 어려운 확률분포에서 표본을 추출하는 방법이다. 핵심 아이디어는 "목표 분포(target distribution)를 정상분포(stationary distribution)로 가지는 마르코프 체인을 설계하고, 체인이 수렴할 때까지 기다린 후 샘플을 수집한다"는 것이다.

**마르코프 성질(Markov property)**은 "다음 상태는 오직 현재 상태에만 의존한다"는 조건이다. $P(X_{n+1} | X_n, X_{n-1}, \ldots) = P(X_{n+1} | X_n)$. 이 성질 덕분에 체인의 장기적 거동을 분석하기 쉬워진다.

**메트로폴리스-헤이스팅스(Metropolis-Hastings, MH)**는 가장 널리 쓰이는 MCMC 알고리즘이다. 제안 분포(proposal distribution) $q(x'|x)$에서 후보를 생성하고, 이를 수락할지 결정하는 방식으로 체인이 목표 분포를 탐색하게 한다.

**깁스 샘플링(Gibbs sampling)**은 MH의 특수한 경우로, 조건부 분포에서 한 번에 한 변수씩 샘플링한다. 모든 조건부 분포에서 샘플링이 가능할 때 효과적이다.

---
## 정의

**마르코프 체인(Markov chain):** 상태공간 $\mathcal{S}$ 위의 확률과정 $\{X_n\}_{n=0}^\infty$이 다음을 만족하면 마르코프 체인이다.

$$P(X_{n+1} = x_{n+1} | X_n = x_n, \ldots, X_0 = x_0) = P(X_{n+1} = x_{n+1} | X_n = x_n)$$

**전이 확률(transition probability):** $T(x \to x') = P(X_{n+1} = x' | X_n = x)$

**정상분포(stationary distribution):** $\pi$가 다음을 만족하면 $\pi$를 정상분포라 한다.

$$\sum_x \pi(x) T(x \to x') = \pi(x') \quad \text{(모든 } x' \in \mathcal{S}\text{에 대해)}$$

**메트로폴리스-헤이스팅스 알고리즘:** 목표분포 $\pi(x)$에서 샘플링하기 위해

1. 현재 상태 $x$에서 제안분포 $q(x'|x)$로 후보 $x'$를 생성한다.
2. 다음 확률로 $x'$를 수락(accept)한다.

$$\alpha(x, x') = \min\left(1, \frac{\pi(x') q(x|x')}{\pi(x) q(x'|x)}\right)$$

3. 수락되면 $x_{n+1} = x'$, 거절되면 $x_{n+1} = x$.

**깁스 샘플링:** $d$차원 $\mathbf{x} = (x_1, \ldots, x_d)$의 각 변수를 조건부 분포에서 순차적으로 샘플링한다.

$$x_1^{(t+1)} \sim p(x_1 | x_2^{(t)}, x_3^{(t)}, \ldots, x_d^{(t)})$$
$$x_2^{(t+1)} \sim p(x_2 | x_1^{(t+1)}, x_3^{(t)}, \ldots, x_d^{(t)})$$
$$\vdots$$
$$x_d^{(t+1)} \sim p(x_d | x_1^{(t+1)}, \ldots, x_{d-1}^{(t+1)})$$

---
## 주요 정리와 증명

### 정리 1: 상세 균형(Detailed Balance)이면 정상분포

상세 균형 조건(detailed balance):

$$\pi(x) T(x \to x') = \pi(x') T(x' \to x) \quad \text{(모든 } x, x' \in \mathcal{S}\text{에 대해)}$$

이 조건이 성립하면 $\pi$는 정상분포다.

**증명:** 상세 균형 조건에서 양변을 $x'$에 대해 합산한다.

$$\sum_x \pi(x) T(x \to x') = \sum_x \pi(x') T(x' \to x) = \pi(x') \sum_x T(x' \to x) = \pi(x') \cdot 1 = \pi(x')$$

첫 번째 등식은 상세 균형, 두 번째는 $\pi(x')$가 합 기호 밖으로 나옴, 세 번째는 전이확률의 합이 1(stochastic matrix의 성질)임을 이용했다. 이는 정상분포의 정의 $\sum_x \pi(x) T(x \to x') = \pi(x')$와 정확히 일치한다. $\square$

상세 균형은 정상분포의 **충분조건(sufficient condition)**이지 필요조건은 아니다. 즉 상세 균형을 만족하지 않아도 정상분포는 존재할 수 있지만, 많은 MCMC 알고리즘은 상세 균형을 설계 원칙으로 사용한다.

### 정리 2: MH 알고리즘이 상세 균형을 만족

메트로폴리스-헤이스팅스 알고리즘의 전이 확률 $T(x \to x') = q(x'|x) \alpha(x, x')$는 $\pi$에 대해 상세 균형을 만족한다.

**증명:** $x \neq x'$인 경우를 보인다. MH의 수락 확률은

$$\alpha(x, x') = \min\left(1, \frac{\pi(x') q(x|x')}{\pi(x) q(x'|x)}\right)$$

$\pi(x) T(x \to x')$를 계산한다.

$$\pi(x) T(x \to x') = \pi(x) q(x'|x) \cdot \min\left(1, \frac{\pi(x') q(x|x')}{\pi(x) q(x'|x)}\right)$$

$$= \min\left(\pi(x) q(x'|x),\; \pi(x') q(x|x')\right)$$

마찬가지로 $\pi(x') T(x' \to x)$를 계산하면

$$\pi(x') T(x' \to x) = \min\left(\pi(x') q(x|x'),\; \pi(x) q(x'|x)\right)$$

두 식이 같으므로 상세 균형이 성립한다.

$$ \pi(x) T(x \to x') = \pi(x') T(x' \to x) $$

$\square$

대칭 제안분포(symmetric proposal) $q(x'|x) = q(x|x')$인 경우(예: 정규분포 제안), 수락 확률은 단순히

$$\alpha(x, x') = \min\left(1, \frac{\pi(x')}{\pi(x)}\right)$$

이 된다. 이를 **메트로폴리스 알고리즘(Metropolis algorithm)**이라 부른다.

### 정리 3: 깁스 샘플링은 MH의 특수한 경우

깁스 샘플링에서 $i$번째 변수를 갱신하는 단계는 제안분포가 $q(x_i' | \mathbf{x}) = p(x_i' | \mathbf{x}_{-i})$인 MH 단계이며, 수락 확률이 항상 1이다.

**증명:** $\mathbf{x}_{-i}$를 $i$번째 변수를 제외한 모든 변수라 하자. 깁스 샘플링의 제안은 $q(x_i' | \mathbf{x}) = p(x_i' | \mathbf{x}_{-i})$이다. 이 제안의 수락 확률을 계산한다.

$$\alpha(\mathbf{x}, \mathbf{x}') = \min\left(1, \frac{\pi(\mathbf{x}') q(\mathbf{x} | \mathbf{x}')}{\pi(\mathbf{x}) q(\mathbf{x}' | \mathbf{x})}\right)$$

깁스 샘플링은 한 변수만 바꾸므로 $\mathbf{x}' = (x_1, \ldots, x_i', \ldots, x_d)$이고, $\mathbf{x}_{-i}' = \mathbf{x}_{-i}$이다. 따라서

$$\frac{\pi(\mathbf{x}')}{\pi(\mathbf{x})} = \frac{p(x_i' | \mathbf{x}_{-i}) p(\mathbf{x}_{-i})}{p(x_i | \mathbf{x}_{-i}) p(\mathbf{x}_{-i})} = \frac{p(x_i' | \mathbf{x}_{-i})}{p(x_i | \mathbf{x}_{-i})}$$

제안분포의 비는 $q(\mathbf{x} | \mathbf{x}') / q(\mathbf{x}' | \mathbf{x}) = p(x_i | \mathbf{x}_{-i}) / p(x_i' | \mathbf{x}_{-i})$이다(깁스는 변수 하나만 바꾸므로 $q(\mathbf{x}'|\mathbf{x}) = p(x_i'|\mathbf{x}_{-i})$, $q(\mathbf{x}|\mathbf{x}') = p(x_i|\mathbf{x}_{-i})$). 따라서

$$\frac{\pi(\mathbf{x}') q(\mathbf{x} | \mathbf{x}')}{\pi(\mathbf{x}) q(\mathbf{x}' | \mathbf{x})} = \frac{p(x_i' | \mathbf{x}_{-i})}{p(x_i | \mathbf{x}_{-i})} \cdot \frac{p(x_i | \mathbf{x}_{-i})}{p(x_i' | \mathbf{x}_{-i})} = 1$$

$\alpha = \min(1, 1) = 1$이므로, 깁스 제안은 항상 수락된다. $\square$

### 정리 4: 에르고드 정리 (Ergodic Theorem)

기약(irreducible)이고 비주기(aperiodic)인 마르코프 체인은 유일한 정상분포 $\pi$를 가지며, 초기 분포와 무관하게 $P^n \to \pi$로 수렴한다.

**증명 (서술):** 기약성은 모든 상태가 다른 모든 상태로부터 도달 가능함을, 비주기성은 상태로 돌아오는 주기가 1임을 의미한다. 이 조건 하에서 전이 행렬 $P$의 가장 큰 고유값은 1이고(페론-프로베니우스 정리, Perron-Frobenius theorem), 이에 대응하는 고유벡터가 유일한 정상분포 $\pi$다. $P^n$의 모든 행이 $\pi$로 수렴함은 고유값 분해로 보일 수 있다. $\square$

이 정리는 MCMC의 이론적 기초다. 체인을 충분히 오래 돌리면($n \to \infty$), 수집된 샘플이 목표 분포 $\pi$에서 온 것처럼 간주할 수 있다.

---
## 예제

**예제 1 (MH 알고리즘 구조 — 2차원 정규분포):** 2차원 정규분포 $\pi(\mathbf{x}) = \mathcal{N}(\mathbf{0}, I_2)$에서 MH로 샘플링하는 구조를 설명하라.

**풀이:** 제안분포로 대칭 정규분포 $q(\mathbf{x}'|\mathbf{x}) = \mathcal{N}(\mathbf{x}, \sigma^2 I_2)$를 사용한다.

1. 현재 $\mathbf{x}^{(t)} = (x_1, x_2)$에서 $\mathbf{x}' \sim \mathcal{N}(\mathbf{x}^{(t)}, \sigma^2 I_2)$를 생성한다.
2. 수락 확률을 계산한다. 대칭 제안이므로

$$\alpha = \min\left(1, \frac{\pi(\mathbf{x}')}{\pi(\mathbf{x}^{(t)})}\right) = \min\left(1, \exp\left(-\frac{\|\mathbf{x}'\|^2 - \|\mathbf{x}^{(t)}\|^2}{2}\right)\right)$$

3. $u \sim \text{U}(0,1)$를 생성하여 $u < \alpha$이면 $\mathbf{x}^{(t+1)} = \mathbf{x}'$, 아니면 $\mathbf{x}^{(t+1)} = \mathbf{x}^{(t)}$.

$\sigma$는 중요한 튜닝 파라미터다. $\sigma$가 너무 작으면 체인이 상태공간을 느리게 탐색하고(높은 수락률이지만 상관관계가 큼), 너무 크면 대부분의 제안이 거절된다(낮은 수락률). 일반적으로 수락률이 20~50%가 되도록 $\sigma$를 조정한다.

**예제 2 (깁스 샘플링 — 2변량 정규 조건부):** $\mathbf{X} = (X_1, X_2)$가 다음 2변량 정규분포를 따른다고 하자.

$$\begin{pmatrix} X_1 \\ X_2 \end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix} 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 & \rho \\ \rho & 1 \end{pmatrix}\right)$$

조건부 분포를 이용한 깁스 샘플링 절차를 서술하라.

**풀이:** [결합·주변·조건부 분포](joint-marginal-conditional.html)에서 유도했듯이

$$X_1 | X_2 = x_2 \sim \mathcal{N}(\rho x_2,\; 1-\rho^2)$$
$$X_2 | X_1 = x_1 \sim \mathcal{N}(\rho x_1,\; 1-\rho^2)$$

깁스 샘플링의 각 반복:

1. $x_1^{(t+1)} \sim \mathcal{N}(\rho x_2^{(t)},\; 1-\rho^2)$
2. $x_2^{(t+1)} \sim \mathcal{N}(\rho x_1^{(t+1)},\; 1-\rho^2)$

$\rho = 0$이면 $X_1$과 $X_2$가 독립이므로 두 변수를 독립적으로 샘플링하는 것과 같다. $\rho = 0.9$처럼 큰 경우 체인의 혼합(mixing)이 느려져 많은 반복이 필요하다.

**예제 3 (수락률 계산):** 목표분포가 $\pi(x) \propto e^{-x^2/2}$이고 제안분포가 $q(x'|x) = \text{U}(x-1, x+1)$(대칭)일 때, $x=0$에서 $x'=1.5$로의 제안에 대한 수락 확률을 구하라.

**풀이:** 대칭 제안이므로 $\alpha = \min(1, \pi(x')/\pi(x))$이다.

$$\frac{\pi(1.5)}{\pi(0)} = \frac{e^{-1.5^2/2}}{e^{0}} = e^{-1.125} \approx 0.325$$

따라서 $\alpha = \min(1, 0.325) = 0.325$다. 즉, 약 32.5%의 확률로 이 제안이 수락된다.

반대로 $x=1.5$에서 $x'=0$으로의 제안은 $\pi(0)/\pi(1.5) = e^{1.125} \approx 3.08$이므로 $\alpha = 1$이다(항상 수락). MH 알고리즘은 "더 높은 확률의 상태로는 항상 이동하고, 더 낮은 확률의 상태로는 일정 확률로 이동한다."

**예제 4 (버닝인과 수렴 진단):** MCMC에서 초기 $B$개의 샘플(버닝인, burn-in period)은 체인이 정상분포에 수렴하기 전의 과도기(transient)이므로 폐기한다. 또한 연속 샘플 간의 상관관계를 줄이기 위해 $K$개마다 하나씩 저장한다(thinning).

$\rho=0.9$인 2변량 정규 깁스 샘플링에서 $B=1000$, $K=10$이 일반적인 선택이다. trace plot을 그려 체인이 안정적으로 혼합하는지 시각적으로 확인한다.

---
## 연결

- **[확률 행렬·마르코프 체인](markov-chains.html)** : MCMC의 "MC"는 마르코프 체인이다. 전이 행렬, 정상분포, 기약성·비주기성 등의 개념이 MCMC의 이론적 토대다.
- **[몬테카를로](monte-carlo.html)** : MCMC의 "MC"는 몬테카를로다. 수집된 샘플로 기댓값 $\mathbb{E}_\pi[f(X)] \approx \frac{1}{N}\sum f(x_i)$을 계산하는 몬테카를로 적분이 MCMC의 최종 목적이다.
- **[가우시안 과정](gaussian-process.html)** : 가우시안 과정의 초모수(hyperparameter) 추론은 종종 MCMC로 수행된다. 사후분포 $p(\theta|D)$가 복잡한 형태를 가질 때 MH나 깁스 샘플링으로 샘플링한다.
