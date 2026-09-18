---
title: 정보기하·자연 그래디언트
slug: information-geometry
---

> 학습 순서 73 / 75 · [처음부터 읽기](math-language.html)

## 작은 예제로 시작하기

**앞에서 가져올 것:** 피셔 정보는 분포가 모수 변화에 얼마나 민감한지 재고, KL 발산은 두 분포의 차이를 잰다.

평균을 0에서 1로 옮기는 변화라도 표준편차가 1인 정규분포에서는 뚜렷하고, 표준편차가 100이면 거의 구별되지 않는다. 두 경우 모수의 숫자 차이는 1로 같으므로 그 차이만으로 분포의 변화를 잴 수 없다.

분산을 고정한 정규분포의 피셔 정보는 $g=1/\sigma^2$다. 작은 평균 변화 $d\mu$의 길이 제곱을 $ds^2=(d\mu)^2/\sigma^2$로 재면, 폭이 넓은 분포에서는 같은 평균 이동이 더 짧게 측정된다. 이 ‘위치에 따라 달라지는 자’가 계량이다. 여러 모수에서는 이를 행렬 $g$로 적는다.

자연 그래디언트는 일반 기울기에 $g^{-1}$를 적용해 분포의 민감도를 보정한다. **하강 방향**은 $-g^{-1}\nabla L$이다. 예를 들어 $\sigma^2=4$이면 $g=1/4$여서 평균 방향 기울기에 4를 곱한다. 같은 정도의 분포 변화를 기준으로 보폭을 조정하는 것이다.

**본문으로 이어 읽기:** 다양체는 가까운 곳에서 좌표로 기술할 수 있는 공간, 계량은 그 좌표 변화의 길이를 재는 규칙이라고 읽자. 양의 정부호 피셔 계량과 매끄러운 가역 좌표변환 아래 연속시간 자연 그래디언트의 방향장은 좌표 선택에 일관된다. 유한한 보폭의 단순 업데이트까지 완전히 같은 경로를 보장하는 것은 아니다.

---

## 직관적 설명

**정보기하(information geometry)**는 확률분포들의 공간을 기하학적으로 연구하는 학문이다. 확률분포 $p_\theta$를 하나의 점(point)으로, 모수 $\theta$의 변화를 그 공간 위의 곡선(curve)으로 본다. 이 공간은 **통계 다양체(statistical manifold)**라 불리며, 자연스러운 리만 계량(Riemannian metric)을 가진다.

핵심 통찰: 모수 좌표의 유클리드 거리만으로는 분포의 구별 가능성을 일관되게 재기 어렵다. 평균을 1만큼 옮겨도 표준편차 1인 정규분포와 표준편차 100인 정규분포가 받는 영향은 다르다. 측정 단위를 바꾸면 같은 분포를 표현하는 모수의 숫자 차이도 달라진다. **KL 발산(Kullback-Leibler divergence)** $D_{KL}(p \| q)$는 확률분포 사이의 "정보적 거리"에 가깝다.

피셔 정보 행렬(Fisher information matrix)은 이 통계 다양체의 리만 계량이 된다:
$$g_{ij}(\theta) = \mathbb{E}\left[\frac{\partial \log p}{\partial \theta_i} \cdot \frac{\partial \log p}{\partial \theta_j}\right]$$

KL 발산을 2차 테일러 전개하면 피셔 정보가 유도된다:
$$D_{KL}(p_\theta \| p_{\theta+d\theta}) \approx \frac{1}{2} d\theta^T g(\theta) d\theta$$

**자연 그래디언트(natural gradient)**는 이 리만 계량을 고려한 최적화 방향이다. 일반 그래디언트 $\nabla \mathcal{L}(\theta)$는 유클리드 계량에서의 상승 방향이며, 자연 그래디언트 $\tilde{\nabla}\mathcal L=g^{-1}\nabla\mathcal L$는 피셔 계량에서의 상승 방향이다. 최소화를 위한 **하강 방향은 각각 그 음수**다. 자연 그래디언트의 방향장은 매끄러운 가역 재매개변수화 아래 일관되게 변환된다. 이는 모수화에 따른 불필요한 차이를 줄이지만, 유한 보폭 알고리즘의 경로나 계산 효율이 항상 같거나 더 좋다는 보장은 아니다.

---
## 정의

**통계 다양체 (statistical manifold):** 모수 공간 $\Theta \subset \mathbb{R}^d$로 매개변수화된 확률분포족 $\{p_\theta : \theta \in \Theta\}$을 다양체(manifold)로 간주한 것. 각 점 $\theta$는 하나의 확률분포 $p_\theta$에 대응한다.

**피셔 정보 행렬 (Fisher information matrix):** 아래에서 스코어 평균 0, 음의 기대 헤시안과의 일치, KL 전개를 사용할 때는 모수에 무관한 지지집합과 미분·적분 교환 및 나머지항 제어 등 정규성 조건을 가정한다. 리만 계량으로 쓰려면 이 행렬이 양정치여야 한다.
$$g_{ij}(\theta) = \mathbb{E}_{p_\theta}\left[\frac{\partial \log p_\theta}{\partial \theta_i} \cdot \frac{\partial \log p_\theta}{\partial \theta_j}\right] = -\mathbb{E}_{p_\theta}\left[\frac{\partial^2 \log p_\theta}{\partial \theta_i \partial \theta_j}\right]$$

$ds^2 = d\theta^T g(\theta) d\theta$는 다양체 위의 미소 거리 제곱(infinitesimal squared distance)이다.

**KL 발산의 국소 근사:**
$$D_{KL}(p_\theta \| p_{\theta + d\theta}) = \int p_\theta \log \frac{p_\theta}{p_{\theta+d\theta}}\,dx = \frac{1}{2} d\theta^T g(\theta) d\theta + o(\|d\theta\|^2)$$

**자연 그래디언트 (natural gradient):**
$$\tilde{\nabla} \mathcal{L}(\theta) = g(\theta)^{-1} \nabla \mathcal{L}(\theta)$$

**자연 그래디언트 하강 (natural gradient descent):**
$$\theta_{t+1} = \theta_t - \eta \, g(\theta_t)^{-1} \nabla \mathcal{L}(\theta_t)$$

**e-접속과 m-접속 (exponential and mixture connections):** 정보기하에서 중요한 두 가지 affine 접속(connection)으로, 각각 지수족(exponential family)과 혼합족(mixture family)의 자연스러운 기하를 정의한다. 정규 지수족 등 적절한 조건에서는 이중 평탄 구조(dually flat structure)를 이룬다. 모든 통계모형이 이런 구조를 갖는 것은 아니다.

---
## 주요 정리와 증명

### 정리 1: KL 발산의 2차 테일러 전개 → 피셔 정보

**서술:** $\theta$의 충분히 작은 변화 $d\theta$에 대해
$$D_{KL}(p_\theta \| p_{\theta+d\theta}) = \frac{1}{2} \sum_{i,j} g_{ij}(\theta) d\theta_i d\theta_j + o(\|d\theta\|^2)$$

**증명:** $\log p_{\theta+d\theta}(x)$를 $\theta$ 주변에서 2차 테일러 전개한다.
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

**서술:** 유한한 피셔 정보 행렬 $g(\theta)$는 양반정치다. 양정치이려면 모든 $v\ne0$에 대해 $v^T\nabla_\theta\log p_\theta(X)$가 확률 1로 0이 되지 않아야 한다. 서로 다른 모수들이 다른 분포라는 식별가능성만으로 이 일차 민감도 조건이 보장되지는 않는다.

**증명:** 임의의 벡터 $v \in \mathbb{R}^d$에 대해
$$v^T g(\theta) v = \sum_{i,j} v_i v_j \mathbb{E}[\partial_i \log p \cdot \partial_j \log p]$$
$$= \mathbb{E}\left[\left(\sum_i v_i \partial_i \log p\right)^2\right] \geq 0$$

이는 스코어 함수의 선형 결합의 제곱 기댓값으로, 항상 0 이상이다.

$v^Tg(\theta)v=0$이면 $v^T\nabla_\theta\log p_\theta(X)=0$이 확률 1로 성립한다. 이는 해당 점에서 그 방향의 일차 변화가 없다는 뜻이며, 모형 전체의 비식별성을 뜻하지 않는다. 예를 들어 $X\sim\mathcal N(\theta^3,1)$은 실수 $\theta$에서 식별 가능하지만 피셔 정보가 $9\theta^4$여서 $\theta=0$에서는 0이다. 0이 아닌 방향의 스코어가 항상 비영인 확률을 가질 때 위 제곱의 기댓값이 양수가 되어 양정치를 얻는다.

피셔 정보가 공분산 행렬(스코어 벡터의 공분산)이라는 점에서 양반정치는 자명하다. $\square$

### 정리 3: 정규분포 $\mathcal{N}(\mu, \sigma^2)$의 피셔 계량

**서술:** 2차원 모수 $\theta = (\mu, \sigma^2)$에 대한 피셔 정보 행렬과 계량은
$$g(\mu, \sigma^2) = \begin{pmatrix} \frac{1}{\sigma^2} & 0 \\ 0 & \frac{1}{2\sigma^4} \end{pmatrix}$$
$$ds^2 = \frac{(d\mu)^2}{\sigma^2} + \frac{(d\sigma^2)^2}{2\sigma^4}$$

여기서 $d\sigma^2$는 $\sigma^2$라는 모수 성분의 미소 변화 $d(\sigma^2)$를 뜻한다. $\sigma$ 자체를 변수로 쓰면 $d(\sigma^2) = 2\sigma\,d\sigma$이므로
$$ds^2 = \frac{(d\mu)^2}{\sigma^2} + \frac{2(d\sigma)^2}{\sigma^2}$$

로도 표현된다.

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

**계량의 해석:** $ds^2 = (d\mu)^2/\sigma^2 + (d\sigma^2)^2/(2\sigma^4)$에서 $\sigma$가 클수록 $\mu$ 방향의 거리가 짧게 측정된다 — 분산이 클수록 평균의 차이를 구분하기 어렵다는 직관과 일치한다.

### 정리 4: 자연 그래디언트의 좌표 불변성

**서술:** 자연 그래디언트 $\tilde{\nabla}\mathcal{L}(\theta) = g(\theta)^{-1}\nabla\mathcal{L}(\theta)$는 모수의 재매개변수화(reparameterization)에 불변이다. 즉, 야코비안이 가역인 매끄러운 좌표변환 아래 연속시간 흐름 $d\theta/dt=-g^{-1}\nabla\mathcal L$는 같은 분포 경로를 나타낸다. 각 좌표에서 유한 보폭으로 단순히 빼는 이산 업데이트의 경로까지 정확히 같다는 주장은 아니다.

**증명 (스케치):** $\phi$ 좌표계에서 손실함수 $\mathcal{L}'(\phi) = \mathcal{L}(\theta(\phi))$를 고려하자. 연쇄법칙에 의해
$$\nabla_\phi \mathcal{L}' = \frac{\partial\theta}{\partial\phi}^T \nabla_\theta \mathcal{L}$$

피셔 정보는 좌표 변환 아래 2차 텐서로 변환된다:
$$g_\phi = \frac{\partial\theta}{\partial\phi}^T g_\theta \frac{\partial\theta}{\partial\phi}$$

따라서 $\phi$ 좌표계의 자연 그래디언트는
$$\tilde{\nabla}_\phi \mathcal{L}' = g_\phi^{-1} \nabla_\phi \mathcal{L}' = \left(\frac{\partial\theta}{\partial\phi}\right)^{-1} g_\theta^{-1} \left(\frac{\partial\theta}{\partial\phi}^T\right)^{-1} \frac{\partial\theta}{\partial\phi}^T \nabla_\theta \mathcal{L}$$
$$= \left(\frac{\partial\theta}{\partial\phi}\right)^{-1} g_\theta^{-1} \nabla_\theta \mathcal{L} = \left(\frac{\partial\theta}{\partial\phi}\right)^{-1} \tilde{\nabla}_\theta \mathcal{L}$$

이는 $\phi$ 좌표계의 자연 그래디언트가 $\theta$ 좌표계의 자연 그래디언트를 좌표 변환한 것과 동일함을 의미한다. 따라서 연속시간 자연 그래디언트 흐름의 분포 경로는 좌표계 선택에 일관된다. $\square$

**대비 — 일반 그래디언트:** 손실의 편미분 성분은 공변벡터(일차 미분)의 변환 규칙을 따른다. 이를 매 좌표계에서 유클리드 이동 벡터로 그대로 취급하면 일반적인 비선형 좌표변환과 일관되지 않는다. 이는 일반 그래디언트 하강이 모수화(parameterization)에 민감한 이유다.

---
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

이 예에서는 정확히 일치한다. 분산을 고정한 정규분포에서 평균 차이에 대한 KL이 정확히 이차식이기 때문이다. 일반적인 정규분포 모수 변화나 모든 지수족에서 고차항이 사라지는 것은 아니다.

**예제 4 (지수족의 피셔 계량):** 지수족(exponential family) $p(x|\theta) = h(x)\exp(\theta^T T(x) - A(\theta))$의 피셔 계량은
$$g_{ij}(\theta) = \frac{\partial^2 A(\theta)}{\partial\theta_i\partial\theta_j}$$

즉, 로그 정규화 함수(log-partition function) $A(\theta)$의 헤시안 행렬(Hessian)이다. 이는 지수족에서 피셔 정보의 계산이 특히 간단해짐을 의미한다.

예: 베르누이 분포를 지수족으로 표현하면 $\theta = \log(p/(1-p))$, $A(\theta) = \log(1+e^\theta)$, $g(\theta) = A''(\theta) = e^\theta/(1+e^\theta)^2 = p(1-p)$.

**예제 5 (두 분포 사이를 잇는 두 방법):** $p=(0.8,0.2)$와 $q=(0.2,0.8)$처럼 각 확률이 양수인 분포를 생각하자. 혼합 경로는 각 확률을 직접 섞는 $r_t=(1-t)p+tq$이며, $t=0$에서 $p$, $t=1$에서 $q$다. 지수 경로는 $r_t(i)\propto p(i)^{1-t}q(i)^t$로 로그확률을 선형 보간한 뒤 합이 1이 되도록 정규화한다. 이들이 각각 m-경로와 e-경로의 기본 예다.

경로를 따라 KL이 일정하거나 선형으로 변한다는 일반 법칙은 없다. 예를 들어 $D_{KL}(p\|p)=0$이지만 $D_{KL}(p\|q)=0.6\ln4>0$이므로 두 끝점에서부터 값이 다르다. ‘평탄’은 선택한 연결과 좌표에서 경로를 직선처럼 기술할 수 있다는 기하학적 성질이지, KL 값이 일정하다는 말이 아니다.

정규 지수족 $p_\theta(x)=h(x)\exp(\theta^TT(x)-A(\theta))$에서는 $\eta(\theta)=\mathbb E_\theta[T(X)]=\nabla A(\theta)$라 놓아
$$D_{KL}(p_\theta\|p_{\theta'})=A(\theta')-A(\theta)-(\theta'-\theta)^T\eta(\theta)$$
로 쓸 수 있다. 로그밀도의 차이를 $p_\theta$로 평균하면 얻는 식이다. 자연 모수 $\theta$와 평균 모수 $\eta$를 구별해야 하며 서로 다른 역할의 좌표를 같은 기호로 섞지 않는다.

---
## 연결

- **[스코어 함수·피셔 정보](score-function.html)** : 피셔 정보 행렬은 스코어 함수의 공분산으로 정의되며, 정보기하의 리만 계량이 된다. 모수 방향으로의 로그밀도 미분을 이용해 분포의 접방향을 나타내며, 스코어의 제곱 기댓값으로 그 방향의 길이를 잰다.
- **[양반정치 행렬](positive-definite.html)** : 피셔 정보 행렬이 양반정치행렬임을 증명하는 데 필요한 개념이다. 공분산 행렬의 양반정치성과 직접 연결된다.
- **[엔트로피·KL 발산](entropy-kl.html)** : KL 발산은 정보기하에서 가장 기본적인 발산 함수(divergence function)다. KL 발산의 2차 근사가 피셔 계량이며, KL 발산 자체가 다양체 위의 비대칭 "거리"를 정의한다.
- **[확률미분방정식](sde.html)** : 자연 그래디언트는 랭주뱅 동역학의 확률적 버전인 SGLD(stochastic gradient Langevin dynamics)와 결합되어 확률적 자연 그래디언트를 형성한다.

---

[← 이전: 스코어 함수·피셔 정보·크라메르-라오 하한](score-function.html) · [다음: 임베딩 공간의 기하학 →](embedding-geometry.html)
