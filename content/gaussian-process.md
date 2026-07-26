---
title: 가우시안 과정
slug: gaussian-process
---

## 직관적 설명

**가우시안 과정(Gaussian Process, GP)**은 "함수 위의 확률분포"다. 일반적인 확률분포가 벡터(유한 차원)에 대한 분포라면, GP는 함수(무한 차원)에 대한 분포다. 유한 개의 점에서 함수값을 관찰하면 그 값들은 **다변량 정규분포(multivariate normal distribution)**를 따른다.

GP의 핵심 아이디어: 데이터 포인트 $x$와 $x'$이 가까울수록 $f(x)$와 $f(x')$도 비슷할 것이라는 **공분산 구조(covariance structure)**를 커널(kernel) 함수 $k(x,x')$로 인코딩한다. RBF 커널 $k(x,x') = \sigma^2 \exp(-\|x-x'\|^2/(2\ell^2))$은 이 직관을 가장 잘 구현한다: 두 점이 멀어질수록 공분산이 지수적으로 감소한다.

GP 회귀(GP regression)의 강점은 **데이터가 적은 곳에서 불확실성(uncertainty)을 정량화**한다는 점이다. 관측된 데이터 근처에서는 예측이 확실하지만(좁은 신뢰구간), 데이터가 없는 영역에서는 사전 분포의 불확실성으로 돌아간다(넓은 신뢰구간). 이는 단순한 곡선 피팅(예: 최소제곱법)이 제공하지 않는 중요한 정보다.

GP의 사후(posterior)는 조건부 정규분포 공식으로 닫힌 형태(closed form)로 주어진다. 관측된 데이터 $(\mathbf{X}, \mathbf{y})$가 주어졌을 때, 새로운 입력 $\mathbf{X}_*$에서의 사후 예측 분포는
$$\mathbf{f}_* | \mathbf{X}, \mathbf{y}, \mathbf{X}_* \sim \mathcal{N}(\boldsymbol{\mu}_*, \Sigma_*)$$
이며, 평균과 공분산이 모두 해석적으로 표현된다. 이는 GP가 비모수적(non-parametric)이지만 예측이 매우 효율적임을 의미한다.

## 정의

**가우시안 과정 (Gaussian Process):** 확률과정 $\{f(x)\}_{x \in \mathcal{X}}$이 모든 유한 부분집합 $\{x_1, \ldots, x_n\} \subset \mathcal{X}$에 대해
$$(f(x_1), \ldots, f(x_n)) \sim \mathcal{N}(\boldsymbol{\mu}, K)$$
를 만족하면 $f$를 가우시안 과정이라 한다. 여기서 $\mu_i = m(x_i)$, $K_{ij} = k(x_i, x_j)$이다.

GP는 평균함수(mean function) $m(x)$와 공분산함수(covariance function, kernel) $k(x,x')$로 완전히 특정된다:
$$f \sim \mathcal{GP}(m(x), k(x,x'))$$

**평균함수 (mean function):** $m(x) = \mathbb{E}[f(x)]$. 보통 $m(x) = 0$으로 가정한다(사후 평균이 데이터에 의해 조정되므로).

**공분산함수 / 커널 (covariance function / kernel):** $k(x,x') = \mathbb{E}[(f(x)-m(x))(f(x')-m(x'))]$.

커널은 **양반정치(positive semidefinite)**여야 한다: 임의의 $n$, $\{x_i\}$, $\{c_i\}$에 대해
$$\sum_{i=1}^n \sum_{j=1}^n c_i c_j k(x_i, x_j) \geq 0$$

**RBF 커널 (Radial Basis Function kernel, squared exponential):**
$$k(x,x') = \sigma^2 \exp\left(-\frac{\|x - x'\|^2}{2\ell^2}\right)$$

- $\sigma^2$: **분산 파라미터 (variance)** — 함수값의 전반적 변동 폭.
- $\ell$: **길이 스케일 (length scale)** — 함수의 부드러움(smoothness). 작을수록 급격히 변동.

**GP 회귀 모델:** $y_i = f(x_i) + \epsilon_i$, $\epsilon_i \stackrel{\text{iid}}{\sim} \mathcal{N}(0, \sigma_n^2)$

**사전 분포 (prior):** $\mathbf{f} = (f(x_1), \ldots, f(x_n))^T \sim \mathcal{N}(\mathbf{0}, K)$ where $K_{ij} = k(x_i, x_j)$.

**관측값의 분포:** $\mathbf{y} \sim \mathcal{N}(\mathbf{0}, K + \sigma_n^2 I)$

**GP 회귀의 사후 예측 (posterior predictive):** $\mathbf{X}_*$에서의 예측 분포 $p(\mathbf{f}_* | \mathbf{X}, \mathbf{y}, \mathbf{X}_*)$는 다변량 정규분포
$$\mathbf{f}_* | D \sim \mathcal{N}(\boldsymbol{\mu}_*, \Sigma_*)$$
이며, 여기서
$$\boldsymbol{\mu}_* = K_*^T (K + \sigma_n^2 I)^{-1} \mathbf{y}$$
$$\Sigma_* = K_{**} - K_*^T (K + \sigma_n^2 I)^{-1} K_*$$

- $K = k(\mathbf{X}, \mathbf{X})$: $n \times n$ 학습 데이터 커널 행렬
- $K_* = k(\mathbf{X}, \mathbf{X}_*)$: $n \times n_*$ 학습-테스트 커널 행렬
- $K_{**} = k(\mathbf{X}_*, \mathbf{X}_*)$: $n_* \times n_*$ 테스트 데이터 커널 행렬

## 주요 정리와 증명

### 정리 1: GP 사후 분포 유도

**서술:** 관측 데이터 $D = (\mathbf{X}, \mathbf{y})$가 주어졌을 때, 테스트 포인트 $\mathbf{X}_*$에서의 $f_*$의 조건부 분포는 다음과 같다:
$$\mathbf{f}_* | \mathbf{X}, \mathbf{y}, \mathbf{X}_* \sim \mathcal{N}\left(K_*^T (K + \sigma_n^2 I)^{-1} \mathbf{y},\; K_{**} - K_*^T (K + \sigma_n^2 I)^{-1} K_*\right)$$

**증명:** $(\mathbf{y}, \mathbf{f}_*)$의 결합분포는 다변량 정규분포다:
$$\begin{pmatrix} \mathbf{y} \\ \mathbf{f}_* \end{pmatrix} \sim \mathcal{N}\left( \begin{pmatrix} \mathbf{0} \\ \mathbf{0} \end{pmatrix}, \begin{pmatrix} K + \sigma_n^2 I & K_* \\ K_*^T & K_{**} \end{pmatrix} \right)$$

다변량 정규분포의 조건부 분포 공식을 적용한다. $\mathbf{x} = (\mathbf{x}_1^T, \mathbf{x}_2^T)^T \sim \mathcal{N}(\boldsymbol{\mu}, \Sigma)$일 때,
$$\mathbf{x}_2 | \mathbf{x}_1 \sim \mathcal{N}(\boldsymbol{\mu}_2 + \Sigma_{21} \Sigma_{11}^{-1} (\mathbf{x}_1 - \boldsymbol{\mu}_1),\; \Sigma_{22} - \Sigma_{21} \Sigma_{11}^{-1} \Sigma_{12})$$

여기서 $\boldsymbol{\mu}_1 = \boldsymbol{\mu}_2 = \mathbf{0}$, $\Sigma_{11} = K + \sigma_n^2 I$, $\Sigma_{12} = K_*$, $\Sigma_{22} = K_{**}$을 대입한다:
$$\boldsymbol{\mu}_* = \mathbf{0} + K_*^T (K + \sigma_n^2 I)^{-1} (\mathbf{y} - \mathbf{0}) = K_*^T (K + \sigma_n^2 I)^{-1} \mathbf{y}$$
$$\Sigma_* = K_{**} - K_*^T (K + \sigma_n^2 I)^{-1} K_*$$

$\square$

**조건부 정규분포 공식의 유도 (참조):** 위 공식은 완전제곱(completing the square) 또는 슈어 보수(Schur complement)로 유도된다. 결합 로그밀도에서 $\mathbf{x}_2$와 관련된 항만 모아 정리하면 $\mathbf{x}_2$의 조건부 분포가 위와 같음을 보일 수 있다.

**의미:** GP 사후 평균 $\boldsymbol{\mu}_*$는 학습 데이터 $\mathbf{y}$의 선형 결합이며, 그 가중치는 커널을 통해 결정된다. 사후 공분산 $\Sigma_*$은 학습 데이터에서 멀어질수록 $K_{**}$에 가까워져(불확실성 증가), 데이터 근처에서는 $K_*^T (K + \sigma_n^2 I)^{-1} K_*$만큼 줄어든다.

### 정리 2: 커널의 양반정치성과 머서 정리

**서술:** $k(x,x')$가 유효한 GP의 공분산 함수가 될 필요충분조건은 $k$가 양반정치(positive semidefinite) 커널인 것이다. 머서 정리(Mercer's theorem)에 따르면 연속 대칭 양반정치 커널은 다음과 같이 고유함수(eigenfunction) 전개가 가능하다:
$$k(x,x') = \sum_{i=1}^\infty \lambda_i \phi_i(x) \phi_i(x')$$
여기서 $\lambda_i \geq 0$는 고유값, $\phi_i$는 직교 고유함수(orthonormal eigenfunction)다.

**증명 (서술):** $k$가 양반정치 커널이면, 임의의 유한 점집합에 대한 그람 행렬(Gram matrix) $K$가 양반정치행렬이다. 이는 다변량 정규분포의 공분산 행렬이 양반정치여야 한다는 요구사항을 만족시킨다.

머서 정리의 핵심: $k$가 양반정치이면 적분 연산자 $T_k f = \int k(\cdot, x') f(x') d\mu(x')$가 음이 아닌 고유값을 가지며, 이 고유함수로 $k$를 분해할 수 있다. 이는 $k(x,x')$를 무한차원 내적(inner product) $\langle \Phi(x), \Phi(x') \rangle_{\mathcal{H}}$으로 해석할 수 있게 해준다(재생커널 힐베르트 공간, RKHS). $\square$

### 정리 3: GP 사후 평균의 BLUE 성질

**서술:** GP 회귀에서 사후 평균 $\mu_*(x) = \mathbb{E}[f(x) | D]$은 최소분산 선형 비편향 추정량(BLUE)이며, 이는 크리깅(kriging) 추정량과 동치다.

**증명 (서술):** GP 사후 평균 $\mu_*(x) = \sum_{i=1}^n \alpha_i k(x, x_i)$는 $\alpha = (K + \sigma_n^2 I)^{-1} \mathbf{y}$로 표현되는 선형 추정량이다.

크리깅(지구통계학, geostatistics)에서 이 추정량은 공간적으로 상관된 데이터의 최적 선형 예측량(Best Linear Unbiased Predictor, BLUP)으로 알려져 있다. GP의 사후 평균은 정규성 가정 하에서 조건부 기댓값 $\mathbb{E}[f_* | \mathbf{y}]$으로, 모든 $L^2$ 추정량(선형뿐 아니라 비선형까지) 중에서 최소 평균제곱오차(mean squared error)를 가진다. $\square$

### 정리 4: 로그 한계 가능도 (Log Marginal Likelihood)

**서술:** GP의 하이퍼파라미터 $\boldsymbol{\theta} = (\sigma^2, \ell, \sigma_n^2)$는 로그 한계 가능도(log marginal likelihood)를 최대화하여 학습한다:
$$\log p(\mathbf{y} | \mathbf{X}, \boldsymbol{\theta}) = -\frac{1}{2} \mathbf{y}^T (K_\theta + \sigma_n^2 I)^{-1} \mathbf{y} - \frac{1}{2} \log |K_\theta + \sigma_n^2 I| - \frac{n}{2} \log 2\pi$$

**증명:** $\mathbf{y} \sim \mathcal{N}(\mathbf{0}, K_\theta + \sigma_n^2 I)$이므로 다변량 정규분포의 로그밀도에서 직접 유도된다.

첫 항 $-\frac12 \mathbf{y}^T (K + \sigma_n^2 I)^{-1} \mathbf{y}$: 데이터 적합도(data fit).
둘째 항 $-\frac12 \log |K + \sigma_n^2 I|$: 복잡도 페널티(complexity penalty). 커널 행렬의 고유값이 클수록(함수가 더 복잡할수록) 페널티가 커진다.
셋째 항: 정규화 상수.

하이퍼파라미터 최적화는 이 가능도를 $\boldsymbol{\theta}$에 대해 미분하여 수행한다(공액 그래디언트, L-BFGS 등). $\square$

## 예제

**예제 1 (1D GP 회귀 — 5개 점):** $x = (-4, -2, 0, 2, 4)$, $y = (-1.5, -0.8, 0.2, 0.9, 1.8)$의 5개 관측 데이터에 대해 GP 회귀를 수행하라. RBF 커널 $\sigma^2 = 1$, $\ell = 1$, $\sigma_n^2 = 0.01$을 사용한다.

**풀이:** 먼저 커널 행렬 $K$를 계산한다. $K_{ij} = \exp(-(x_i - x_j)^2 / 2)$.

예: $K_{11} = 1$, $K_{12} = \exp(-(-4+2)^2/2) = \exp(-2) \approx 0.135$, $K_{13} = \exp(-16/2) = \exp(-8) \approx 0.000335$, etc.

$K + \sigma_n^2 I$를 계산하고, $(K + \sigma_n^2 I)^{-1} \mathbf{y}$를 구한 후, 테스트 그리드 $x_* \in [-5, 5]$에서의 사후 평균과 분산을 계산한다.

사후 평균: $\mu_*(x) = \sum_i \alpha_i k(x, x_i)$ — 데이터 포인트 근처에서 $y$에 가깝고, 멀어질수록 0으로 돌아간다.
사후 분산: $\sigma_*^2(x) = k(x,x) - k_*^T(K + \sigma_n^2 I)^{-1}k_*$ — 데이터 포인트 근처에서 작고, 멀어질수록 $\sigma^2 = 1$에 가까워진다.

**예제 2 (RBF 커널 파라미터 효과):** 동일한 데이터에서 $\ell$을 변화시킬 때의 영향을 비교한다.

(1) $\ell = 0.3$ (짧은 길이 스케일): 함수가 급격히 변동한다. 데이터 포인트 사이에서 사후 평균이 빠르게 0으로 돌아가고, 불확실성도 빠르게 증가한다. 데이터가 없는 영역의 예측이 불안정하다.

(2) $\ell = 1$ (중간): 적절한 부드러움. 데이터 사이를 부드럽게 보간(interpolate)하고, 데이터 밖에서는 점차 사전 평균(0)으로 돌아간다.

(3) $\ell = 5$ (긴 길이 스케일): 매우 부드러운 함수. 데이터가 서로 강하게 상관되어 있어, 데이터가 없는 영역에서도 사후 평균이 데이터의 전반적 추세를 유지한다. 불확실성 증가가 느리다.

**예제 3 (불확실성 밴드 해석):** GP 회귀의 95% 신뢰구간(credible interval)은 $\mu_*(x) \pm 1.96 \sigma_*(x)$이다.

- 데이터 포인트 $x = 0$에서: $\sigma_*^2(0) \approx \sigma_n^2 = 0.01$ (잡음 분산 수준). 신뢰구간 폭 $\approx 2 \times 1.96 \times 0.1 = 0.392$.
- 데이터에서 먼 $x = 10$에서: $\sigma_*^2(10) \approx k(10,10) = 1$. 신뢰구간 폭 $\approx 2 \times 1.96 \times 1 = 3.92$.

즉, 데이터가 없는 영역에서는 불확실성이 약 10배 증가한다. 이는 GP가 "모르는 것을 모른다"고 말해주는 중요한 특성이다.

**예제 4 (GP 분류 — 개념):** GP는 회귀뿐 아니라 분류에도 사용된다. 관측값이 이진(binary)일 때, $f(x)$에 시그모이드(sigmoid) 또는 프로빗(probit) 함수를 적용하여 $p(y=1|x) = \Phi(f(x))$로 모델링한다. 이 경우 사후 분포가 더 이상 닫힌 형태로 주어지지 않으므로, 라플라스 근사(Laplace approximation), 기대 전파(expectation propagation), MCMC 등의 근사 방법이 필요하다.

**예제 5 (커널 선택):** RBF 외에도 다양한 커널이 있다.

(1) **마탄 커널 (Matérn kernel):**
$$k_{\text{Matérn}}(x,x') = \frac{2^{1-\nu}}{\Gamma(\nu)} \left(\frac{\sqrt{2\nu}\|x-x'\|}{\ell}\right)^\nu K_\nu\left(\frac{\sqrt{2\nu}\|x-x'\|}{\ell}\right)$$
$\nu = 1/2$: 지수 커널(라플라스, 매우 거침), $\nu = 3/2$: 1회 미분 가능, $\nu = 5/2$: 2회 미분 가능, $\nu \to \infty$: RBF(무한히 미분 가능).

(2) **주기 커널 (Periodic kernel):**
$$k(x,x') = \sigma^2 \exp\left(-\frac{2\sin^2(\pi\|x-x'\|/p)}{\ell^2}\right)$$
주기적 패턴(예: 계절성) 모델링에 사용.

(3) **선형 커널 (Linear kernel):**
$$k(x,x') = x^T x'$$
선형 회귀와 동등한 GP를 생성한다.

**예제 6 (GP의 계산 복잡도):** GP의 주요 단점은 계산 비용이다. $K + \sigma_n^2 I$가 $n \times n$ 행렬이므로, 역행렬 계산에 $O(n^3)$, 메모리에 $O(n^2)$이 필요하다. $n > 10^4$이면 현실적이지 않다.

**해결책:** (a) 희소 GP(sparse GP): $m \ll n$개의 유도 포인트(inducing points) 사용, (b) KISS-GP: 커널 행렬을 구조화된 행렬로 근사, (c) 확률적 경사 GP: 미니배치 학습.

## 연결

- **[베이즈 추론](topics/bayesian-inference.html)** : GP 회귀는 베이즈 추론의 틀을 따른다 — 사전(prior) $f \sim \mathcal{GP}(0, k)$, 우도(likelihood) $y|f \sim \mathcal{N}(f, \sigma_n^2 I)$, 사후(posterior) $f|D$가 닫힌 형태로 주어진다.
- **[스코어 함수·피셔 정보](topics/score-function.html)** : GP의 하이퍼파라미터 학습은 로그 한계 가능도의 그래디언트를 계산하며, 이는 스코어 함수와 연결된다. GP의 로그 한계 가능도 최적화는 모든 하이퍼파라미터에 대한 정보를 통합한다.
- **[확률 행렬·마르코프 체인](topics/markov-chains.html)** : GP는 연속 공간에서 마르코프 성질을 일반화한다 — 특정 커널(예: Matérn $\nu=1/2$)은 GP를 마르코프 과정으로 만든다.
- **[최소제곱법](topics/least-squares.html)** : GP 사후 평균 $\mu_*(x) = k_*^T (K + \sigma_n^2 I)^{-1} \mathbf{y}$는 최소제곱법과 유사한 형태를 가진다. 능형 회귀(ridge regression)의 커널 버전으로 볼 수 있다.
- **[양반정치 행렬](topics/positive-definite.html)** : 커널 함수의 양반정치성은 공분산 행렬이 양반정치여야 하는 필요조건에서 비롯된다.
