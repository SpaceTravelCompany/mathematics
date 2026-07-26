---
title: 정보기하·자연 그래디언트
slug: information-geometry
---

## 직관적 설명

**정보기하(information geometry)**는 확률분포들의 공간을 기하학적으로 연구하는 학문이다. 확률분포 $p_\theta$를 하나의 점(point)으로, 모수 $\theta$의 변화를 그 공간 위의 곡선(curve)으로 본다. 이 공간은 **통계 다양체(statistical manifold)**라 불리며, 자연스러운 리만 계량(Riemannian metric)을 가진다.

핵심 통찰: 확률분포 공간에서 "유클리드 거리"는 통계적으로 의미 있는 거리가 아니다. 두 정규분포 $\mathcal{N}(0, 1)$과 $\mathcal{N}(10, 1)$의 유클리드 거리는 $\mu$ 차원에서 10이지만, $\mathcal{N}(0, 1)$과 $\mathcal{N}(0, 1.01)$의 거리는 0.01이다. 그러나 통계적으로 전자는 명확히 구분 가능하고 후자는 거의 동일하다. **KL 발산(Kullback-Leibler divergence)** $D_{KL}(p \| q)$는 확률분포 사이의 "정보적 거리"에 가깝다.

피셔 정보 행렬(Fisher information matrix)은 이 통계 다양체의 리만 계량이 된다:
$$g_{ij}(\theta) = \mathbb{E}\left[\frac{\partial \log p}{\partial \theta_i} \cdot \frac{\partial \log p}{\partial \theta_j}\right]$$

KL 발산을 2차 테일러 전개하면 피셔 정보가 유도된다:
$$D_{KL}(p_\theta \| p_{\theta+d\theta}) \approx \frac{1}{2} d\theta^T g(\theta) d\theta$$

**자연 그래디언트(natural gradient)**는 이 리만 계량을 고려한 최적화 방향이다. 일반 그래디언트 $\nabla \mathcal{L}(\theta)$가 유클리드 공간에서의 "가장 가파른 하강 방향"이라면, 자연 그래디언트 $\tilde{\nabla} \mathcal{L}(\theta) = g^{-1} \nabla \mathcal{L}(\theta)$는 **통계 다양체에서의 가장 가파른 하강 방향**이다. 자연 그래디언트는 모수의 재매개변수화(reparameterization)에 불변(invariant)하여, 더 효율적인 최적화를 가능하게 한다.

## 정의

**통계 다양체 (statistical manifold):** 모수 공간 $\Theta \subset \mathbb{R}^d$로 매개변수화된 확률분포족 $\{p_\theta : \theta \in \Theta\}$을 다양체(manifold)로 간주한 것. 각 점 $\theta$는 하나의 확률분포 $p_\theta$에 대응한다.

**피셔 정보 행렬 (Fisher information matrix) = 리만 계량:**
$$g_{ij}(\theta) = \mathbb{E}_{p_\theta}\left[\frac{\partial \log p_\theta}{\partial \theta_i} \cdot \frac{\partial \log p_\theta}{\partial \theta_j}\right] = -\mathbb{E}_{p_\theta}\left[\frac{\partial^2 \log p_\theta}{\partial \theta_i \partial \theta_j}\right]$$

$ds^2 = d\theta^T g(\theta) d\theta$는 다양체 위의 미소 거리 제곱(infinitesimal squared distance)이다.

**KL 발산의 국소 근사:**
$$D_{KL}(p_\theta \| p_{\theta + d\theta}) = \int p_\theta \log \frac{p_\theta}{p_{\theta+d\theta}}\,dx \approx \frac{1}{2} d\theta^T g(\theta) d\theta + o(\|d\theta\|^2)$$

**자연 그래디언트 (natural gradient):**
$$\tilde{\nabla} \mathcal{L}(\theta) = g(\theta)^{-1} \nabla \mathcal{L}(\theta)$$

**자연 그래디언트 하강 (natural gradient descent):**
$$\theta_{t+1} = \theta_t - \eta \, g(\theta_t)^{-1} \nabla \mathcal{L}(\theta_t)$$

**e-접속과 m-접속 (exponential and mixture connections):** 정보기하에서 중요한 두 가지 affine 접속(connection)으로, 각각 지수족(exponential family)과 혼합족(mixture family)의 자연스러운 기하를 정의한다. 이중 평탄 구조(dually flat structure)를 형성한다.

## 주요 정리와 증명

### 정리 1: KL 발산의 2차 테일러 전개 → 피셔 정보

**서술:** $\theta$의 충분히 작은 변화 $d\theta$에 대해
$$D_{KL}(p_\theta \| p_{\theta+d\theta}) = \frac{1}{2} \sum_{i,j} g_{ij}(\theta) d\theta_i d\theta_j + o(\|d\theta\|^2)$$

**증명:** $p_{\theta+d\theta}(x)$를 $\theta$ 주변에서 2차 테일러 전개한다.
$$\log p_{\theta+d\theta} = \log p_\theta + \sum_i d\theta_i \frac{\partial \log p_\theta}{\partial \theta_i} + \frac{1}{2}\sum_{i,j} d\theta_i d\theta_j \frac{\partial^2 \log p_\theta}{\partial \theta_i \partial \theta_j} + o(\|d\theta\|^2)$$

이를 KL 발산 정의에 대입한다:
$$D_{KL}(p_\theta \| p_{\theta+d\theta}) = \int p_\theta [\log p_\theta - \log p_{\theta+d\theta}]\,dx$$
$$= -\int p_\theta\left[\sum_i d\theta_i \partial_i \log p_\theta + \frac{1}{2}\sum_{i,j} d\theta_i d\theta_j \partial_i\partial_j \log p_\theta\right]dx + o(\|d\theta\|^2)$$

첫 항은 스코어의 기댓값이므로 0이다:
$$-\sum_i d\theta_i \mathbb{E}[\partial_i \log p_\theta] = 0$$

따라서
$$D_{KL} = -\frac{1}{2}\sum_{i,j} d\theta_i d\theta_j \mathbb{E}[\partial_i\partial_j \log p_\theta] + o(\|d\theta\|^2)$$

$\mathbb{E}[\partial_i\partial_j \log p_\theta] = -g_{ij}(\theta)$이므로,
$$D_{KL} = \frac{1}{2}\sum_{i,j} d\theta_i d\theta_j g_{ij}(\theta) + o(\|d\theta\|^2)$$

$\square$

**의미:** KL 발산은 국소적으로 피셔 정보를 계량으로 하는 2차 형식(quadratic form)으로 근사된다. 이는 유클리드 공간에서 거리가 $ds^2 = dx^T I dx$로 주어지는 것과 유사하다.

### 정리 2: 피셔 정보 행렬의 양반정치성

**서술:** 피셔 정보 행렬 $g(\theta)$는 양반정치(positive semidefinite)이며, 모수 $\theta$가 식별 가능(identifiable)하면 양정치(positive definite)이다.

**증명:** 임의의 벡터 $v \in \mathbb{R}^d$에 대해
$$v^T g(\theta) v = \sum_{i,j} v_i v_j \mathbb{E}[\partial_i \log p \cdot \partial_j \log p]$$
$$= \mathbb{E}\left[\left(\sum_i v_i \partial_i \log p\right)^2\right] \geq 0$$

이는 스코어 함수의 선형 결합의 제곱 기댓값으로, 항상 0 이상이다.

$v^T g(\theta) v = 0$이면 $\sum_i v_i \partial_i \log p_\theta = 0$ (almost everywhere). 이는 $p_\theta$가 $v$ 방향으로 변하지 않음을 의미하며, $\theta$가 식별 불가능(non-identifiable)함을 의미한다. 따라서 식별 가능하면 $g(\theta)$는 양정치이다.

피셔 정보가 공분산 행렬(스코어 벡터의 공분산)이라는 점에서 양반정치는 자명하다. $\square$

### 정리 3: 정규분포 $\mathcal{N}(\mu, \sigma^2)$의 피셔 계량

**서술:** 2차원 모수 $\theta = (\mu, \sigma^2)$에 대한 피셔 정보 행렬과 계량은
$$g(\mu, \sigma^2) = \begin{pmatrix} \frac{1}{\sigma^2} & 0 \\ 0 & \frac{1}{2\sigma^4} \end{pmatrix}$$
$$ds^2 = \frac{d\mu^2}{\sigma^2} + \frac{d\sigma^4}{2\sigma^4} = \frac{d\mu^2}{\sigma^2} + \frac{2 d\sigma^2}{\sigma^2}$$

(마지막 등식은 $d\sigma^4 = 4\sigma^2 d\sigma^2$와 정리 후 $d\sigma^2$로 표현한 것)

**증명:** $\log p(x|\mu,\sigma^2) = -\frac{1}{2}\log(2\pi\sigma^2) - \frac{(x-\mu)^2}{2\sigma^2}$

1계 도함수:
$$\frac{\partial \log p}{\partial \mu} = \frac{x-\mu}{\sigma^2}, \quad \frac{\partial \log p}{\partial \sigma^2} = -\frac{1}{2\sigma^2} + \frac{(x-\mu)^2}{2\sigma^4}$$

피셔 정보의 각 성분:
$$g_{11} = \mathbb{E}\left[\left(\frac{X-\mu}{\sigma^2}\right)^2\right] = \frac{1}{\sigma^4} \cdot \sigma^2 = \frac{1}{\sigma^2}$$
$$g_{12} = \mathbb{E}\left[\frac{X-\mu}{\sigma^2}\left(-\frac{1}{2\sigma^2} + \frac{(X-\mu)^2}{2\sigma^4}\right)\right]$$
$$= \frac{1}{\sigma^2}\left(-\frac{1}{2\sigma^2}\mathbb{E}[X-\mu] + \frac{1}{2\sigma^4}\mathbb{E}[(X-\mu)^3]\right) = 0$$

(정규분포의 3차 중심적률 = 0)

$$g_{22} = \mathbb{E}\left[\left(-\frac{1}{2\sigma^2} + \frac{(X-\mu)^2}{2\sigma^4}\right)^2\right]$$
$$= \frac{1}{4\sigma^4} - \frac{1}{2\sigma^6}\mathbb{E}[(X-\mu)^2] + \frac{1}{4\sigma^8}\mathbb{E}[(X-\mu)^4]$$
$$= \frac{1}{4\sigma^4} - \frac{1}{2\sigma^4} + \frac{1}{4\sigma^8} \cdot 3\sigma^4 = \frac{1}{4\sigma^4} - \frac{1}{2\sigma^4} + \frac{3}{4\sigma^4} = \frac{1}{2\sigma^4}$$

$\square$

**계량의 해석:** $ds^2 = d\mu^2/\sigma^2 + d\sigma^4/(2\sigma^4)$에서 $\sigma$가 클수록 $\mu$ 방향의 거리가 짧게 측정된다 — 분산이 클수록 평균의 차이를 구분하기 어렵다는 직관과 일치한다.

### 정리 4: 자연 그래디언트의 좌표 불변성

**서술:** 자연 그래디언트 $\tilde{\nabla}\mathcal{L}(\theta) = g(\theta)^{-1}\nabla\mathcal{L}(\theta)$는 모수의 재매개변수화(reparameterization)에 불변이다. 즉, $\phi = \phi(\theta)$로 재매개변수화해도 자연 그래디언트 하강의 궤적(trajectory)은 동일하다.

**증명 (스케치):** $\phi$ 좌표계에서 손실함수 $\mathcal{L}'(\phi) = \mathcal{L}(\theta(\phi))$를 고려하자. 연쇄법칙에 의해
$$\nabla_\phi \mathcal{L}' = \frac{\partial\theta}{\partial\phi}^T \nabla_\theta \mathcal{L}$$

피셰 정보는 좌표 변환 아래 2차 텐서로 변환된다:
$$g_\phi = \frac{\partial\theta}{\partial\phi}^T g_\theta \frac{\partial\theta}{\partial\phi}$$

따라서 $\phi$ 좌표계의 자연 그래디언트는
$$\tilde{\nabla}_\phi \mathcal{L}' = g_\phi^{-1} \nabla_\phi \mathcal{L}' = \left(\frac{\partial\theta}{\partial\phi}\right)^{-1} g_\theta^{-1} \left(\frac{\partial\theta}{\partial\phi}^T\right)^{-1} \frac{\partial\theta}{\partial\phi}^T \nabla_\theta \mathcal{L}$$
$$= \left(\frac{\partial\theta}{\partial\phi}\right)^{-1} g_\theta^{-1} \nabla_\theta \mathcal{L} = \left(\frac{\partial\theta}{\partial\phi}\right)^{-1} \tilde{\nabla}_\theta \mathcal{L}$$

이는 $\phi$ 좌표계의 자연 그래디언트가 $\theta$ 좌표계의 자연 그래디언트를 좌표 변환한 것과 동일함을 의미한다. 즉, 자연 그래디언트 하강의 궤적은 좌표계 선택과 무관하다. $\square$

**대비 — 일반 그래디언트:** 일반 그래디언트 $\nabla_\theta \mathcal{L}$은 좌표 변환 아래 공변(covariant)하지 않는다. 같은 방향이라도 다른 좌표계에서 다르게 표현된다. 이는 일반 그래디언트 하강이 모수화(parameterization)에 민감한 이유다.

## 예제

**예제 1 (베르누이 분포의 피셔 계량):** $X \sim \text{Bernoulli}(p)$, $\theta = p \in (0,1)$.

$$\log p(x|p) = x\log p + (1-x)\log(1-p)$$
$$\frac{\partial \log p}{\partial p} = \frac{x}{p} - \frac{1-x}{1-p}$$
$$g(p) = \mathbb{E}\left[\left(\frac{X}{p} - \frac{1-X}{1-p}\right)^2\right] = \frac{1}{p(1-p)}$$

$$ds^2 = \frac{dp^2}{p(1-p)}$$

변환 $p = \sin^2(\phi)$를 적용하면:
$$dp = 2\sin\phi\cos\phi\,d\phi, \quad p(1-p) = \sin^2\phi\cos^2\phi$$
$$ds^2 = \frac{4\sin^2\phi\cos^2\phi\,d\phi^2}{\sin^2\phi\cos^2\phi} = 4\,d\phi^2$$

즉, $\phi$ 좌표계에서 베르누이 분포의 다양체는 거리가 균일한 1차원 공간(원의 1/4)이 된다. 이는 피셔 계량이 좌표 변환에 의해 단순화되는 좋은 예시다.

**예제 2 (자연 그래디언트 vs 유클리드 그래디언트):** 정규분포 $\mathcal{N}(\mu, \sigma^2)$의 로그가능도 최적화를 생각하자. 손실 $\mathcal{L}(\mu, \sigma^2) = -\frac{1}{N}\sum \log p(x_i|\mu, \sigma^2)$.

**유클리드 그래디언트:**
$$\nabla \mathcal{L} = \left(\frac{\partial\mathcal{L}}{\partial\mu}, \frac{\partial\mathcal{L}}{\partial\sigma^2}\right)$$

**자연 그래디언트:**
$$\tilde{\nabla}\mathcal{L} = g^{-1}\nabla\mathcal{L} = \begin{pmatrix} \sigma^2 & 0 \\ 0 & 2\sigma^4 \end{pmatrix} \begin{pmatrix} \partial\mathcal{L}/\partial\mu \\ \partial\mathcal{L}/\partial\sigma^2 \end{pmatrix} = \begin{pmatrix} \sigma^2 \partial\mathcal{L}/\partial\mu \\ 2\sigma^4 \partial\mathcal{L}/\partial\sigma^2 \end{pmatrix}$$

자연 그래디언트는 $\sigma^2$에 비례하여 스케일링한다. $\sigma^2$가 클 때(데이터 분산이 클 때) $\mu$ 방향 업데이트를 더 크게 하고, $\sigma^2$가 작을 때 업데이트를 더 작게 한다. 이는 통계적으로 자연스러운 보폭 조정이다.

**예제 3 (KL 발산의 국소 근사 검증):** $p = \mathcal{N}(0, 1)$, $q = \mathcal{N}(\epsilon, 1)$일 때 KL 발산과 피셔 근사를 비교하라.

**정확한 KL 발산:** $D_{KL}(p\|q) = \epsilon^2/2$ (정규분포 KL 공식에서 $\sigma_1=\sigma_2=1$, $\mu_1=0$, $\mu_2=\epsilon$이므로).

**피셔 근사:** $g = 1/\sigma^2 = 1$, $ds^2 = d\mu^2$, $D_{KL} \approx \epsilon^2/2$.

정확히 일치한다! 이는 정규분포(지수족, exponential family)의 경우 2차 이상의 항이 0이기 때문이다.

**예제 4 (지수족의 피셔 계량):** 지수족(exponential family) $p(x|\theta) = h(x)\exp(\theta^T T(x) - A(\theta))$의 피셔 계량은
$$g_{ij}(\theta) = \frac{\partial^2 A(\theta)}{\partial\theta_i\partial\theta_j}$$

즉, 로그 정규화 함수(log-partition function) $A(\theta)$의 헤세 행렬( Hessian )이다. 이는 지수족에서 피셔 정보의 계산이 특히 간단해짐을 의미한다.

예: 베르누이 분포를 지수족으로 표현하면 $\theta = \log(p/(1-p))$, $A(\theta) = \log(1+e^\theta)$, $g(\theta) = A''(\theta) = e^\theta/(1+e^\theta)^2 = p(1-p)$.

**예제 5 (정보기하의 e-접속과 m-접속):** 두 분포 $p$와 $q$ 사이의 KL 발산 $D_{KL}(p\|q)$는 $p$와 $q$를 잇는 e-측지선(e-geodesic)을 따라 변하지 않는다. 반대로 $D_{KL}(q\|p)$는 m-측지선(m-geodesic)을 따라 변하지 않는다. 이중 평탄 구조(dually flat structure)에서는 발산이 측지선(geodesic)을 따라 선형으로 변한다:
$$D_{KL}(p_\theta \| p_{\theta'}) = \psi(\theta) + \phi(\theta') - \theta \cdot \theta'$$

여기서 $\psi$와 $\phi$는 각각 지수족과 혼합족의 potential 함수다.

## 연결

- **[스코어 함수·피셔 정보](score-function.html)** : 피셔 정보 행렬은 스코어 함수의 공분산으로 정의되며, 정보기하의 리만 계량이 된다. 스코어 함수는 다양체 위의 접벡터(tangent vector)로 해석된다.
- **[양반정치 행렬](positive-definite.html)** : 피셔 정보 행렬이 양반정치행렬임을 증명하는 데 필요한 개념이다. 공분산 행렬의 양반정치성과 직접 연결된다.
- **[엔트로피·KL 발산](entropy-kl.html)** : KL 발산은 정보기하에서 가장 기본적인 발산 함수(divergence function)다. KL 발산의 2차 근사가 피셔 계량이며, KL 발산 자체가 다양체 위의 비대칭 "거리"를 정의한다.
- **[확률미분방정식](sde.html)** : 자연 그래디언트는 랭주뱅 동역학의 확률적 버전인 SGLD(stochastic gradient Langevin dynamics)와 결합되어 확률적 자연 그래디언트를 형성한다.
