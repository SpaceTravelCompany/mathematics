---
title: 엔트로피·KL발산·상호정보량
slug: entropy-kl
---

## 직관적 설명

**엔트로피(entropy)**는 확률분포의 불확실성을 측정한다. "공정한 동전"의 엔트로피는 높다 — 결과를 예측하기 어렵기 때문이다. 반면 "양면이 앞면인 동전"의 엔트로피는 0이다 — 항상 앞면이 나오므로 불확실성이 없다. 섀넌(Claude Shannon)은 정보이론에서 엔트로피를 "놀람(surprise)의 평균"으로 정의했다. 드문 사건이 발생하면 정보량(놀람)이 크고, 자주 일어나는 사건의 정보량은 작다.

**KL 발산(Kullback-Leibler divergence)**은 두 확률분포 $p$와 $q$가 얼마나 다른지를 측정한다. $D_{KL}(p \| q)$는 "$p$를 진정한 분포로 볼 때, $q$로 근사함으로써 추가로 필요한 정보량"으로 해석된다. KL 발산은 거리(distance)처럼 쓰이지만 대칭이 아니고($D_{KL}(p\|q) \neq D_{KL}(q\|p)$), 항상 0 이상이며 $p = q$일 때만 0이 된다.

**상호정보량(mutual information)**은 두 확률변수가 공유하는 정보량이다. $I(X;Y)$는 "$X$를 알면 $Y$에 대한 불확실성이 얼마나 줄어드는가"를 측정한다. $I(X;Y)=0$이면 $X$와 $Y$는 독립이다.

## 정의

**이산 엔트로피(discrete entropy):** $H(X) = -\sum_{x} p(x) \log p(x)$

로그의 밑(base)이 2이면 단위는 비트(bit), 자연로그이면 내츠(nat)다. 본문에서는 자연로그를 사용한다.

**미분 엔트로피(differential entropy, 연속):** $h(X) = -\int f(x) \ln f(x)\,dx$

**교차 엔트로피(cross entropy):** $H(p,q) = -\sum_{x} p(x) \ln q(x)$

교차 엔트로피는 "진짜 분포 $p$에 대한 코딩을 $q$로 할 때 필요한 평균 비트 수"다.

**KL 발산(Kullback-Leibler divergence):** $D_{KL}(p \| q) = \sum_{x} p(x) \ln \frac{p(x)}{q(x)}$ (이산)

연속의 경우 $D_{KL}(p \| q) = \int f(x) \ln \frac{f(x)}{g(x)}\,dx$.

**상호정보량(mutual information):**

$$I(X;Y) = \sum_{x,y} p(x,y) \ln \frac{p(x,y)}{p(x)p(y)}$$

## 주요 정리와 증명

### 정리 1: 깁스 부등식 (Gibbs' Inequality)

$D_{KL}(p \| q) \geq 0$, 등호는 $p = q$일 때만 성립한다.

**증명:** $\ln t \leq t - 1$ (모든 $t > 0$에 대해, 등호는 $t=1$일 때) 부등식을 이용한다.

$$-D_{KL}(p \| q) = \sum_x p(x) \ln \frac{q(x)}{p(x)}$$

$$\leq \sum_x p(x) \left(\frac{q(x)}{p(x)} - 1\right) = \sum_x (q(x) - p(x)) = 1 - 1 = 0$$

따라서 $-D_{KL} \leq 0$이므로 $D_{KL} \geq 0$이다. 등호 조건: $\ln t = t-1$이 $t=1$에서만 성립하므로, 모든 $x$에 대해 $q(x)/p(x) = 1$, 즉 $p(x) = q(x)$여야 한다. $\square$

부등식 $\ln t \leq t-1$의 증명: $f(t) = \ln t - (t-1)$이라 하면 $f'(t) = 1/t - 1$, $f'(1)=0$, $f''(t) = -1/t^2 < 0$이므로 $t=1$에서 최댓값 $f(1)=0$을 갖는다.

깁스 부등식은 KL 발산이 거리 유사 함수(divergence)로서 가져야 할 최소 조건을 보장한다.

### 정리 2: 교차 엔트로피 = 엔트로피 + KL 발산

$$H(p,q) = H(p) + D_{KL}(p \| q)$$

**증명:** 교차 엔트로피의 정의에서 직접 전개한다.

$$H(p,q) = -\sum_x p(x) \ln q(x)$$

$$= -\sum_x p(x) \ln p(x) + \sum_x p(x) \ln p(x) - \sum_x p(x) \ln q(x)$$

$$= H(p) + \sum_x p(x) \ln \frac{p(x)}{q(x)} = H(p) + D_{KL}(p \| q)$$

$\square$

깁스 부등식에 의해 $D_{KL} \geq 0$이므로 $H(p,q) \geq H(p)$이고, 등호는 $p=q$일 때 성립한다. 즉, 올바른 분포 $q=p$로 코딩할 때 교차 엔트로피가 최소화된다.

### 정리 3: 상호정보량과 KL 발산의 관계

$$I(X;Y) = D_{KL}(p_{XY} \| p_X p_Y)$$

**증명:** 상호정보량의 정의에서 직접 유도된다.

$$I(X;Y) = \sum_{x,y} p(x,y) \ln \frac{p(x,y)}{p(x)p(y)} = D_{KL}(p(x,y) \| p(x)p(y))$$

$\square$

즉, 상호정보량은 결합분포와 주변분포의 곱(즉 독립인 경우의 분포) 사이의 KL 발산이다. 이 관계에서 $I(X;Y) \geq 0$이 자명하며, 등호는 $X$와 $Y$가 독립일 때 성립한다.

### 정리 4: 상호정보량 = 엔트로피 차이

$$I(X;Y) = H(X) - H(X|Y)$$

여기서 $H(X|Y) = -\sum_{x,y} p(x,y) \ln p(x|y)$는 조건부 엔트로피(conditional entropy)다.

**증명:**

$$H(X) - H(X|Y) = -\sum_x p(x)\ln p(x) + \sum_{x,y} p(x,y) \ln p(x|y)$$

$p(x) = \sum_y p(x,y)$이고 $p(x|y) = p(x,y)/p(y)$를 대입한다.

$$= -\sum_{x,y} p(x,y) \ln p(x) + \sum_{x,y} p(x,y) \ln \frac{p(x,y)}{p(y)}$$

$$= \sum_{x,y} p(x,y) \ln \frac{p(x,y)}{p(x)p(y)} = I(X;Y)$$

$\square$

이 항등식은 정보이론의 핵심 관계다. "상호정보량 = $X$의 불확실성 - $Y$를 안 후의 $X$ 불확실성"으로, $Y$가 $X$에 대해 제공하는 정보의 양을 측정한다.

### 정리 5: 이산 엔트로피의 최대 — 균등분포

$n$개의 가능한 값을 가지는 이산 확률변수 $X$에 대해, 엔트로피 $H(X)$는 균등분포(uniform distribution) $p_i = 1/n$일 때 최대가 된다. 최댓값은 $H_{\max} = \ln n$이다.

**증명:** 라그랑주 승수법(Lagrange multiplier method)을 사용한다. 제약 조건은 $\sum_{i=1}^n p_i = 1$, $p_i \geq 0$이다.

라그랑주 함수: $\mathcal{L}(p_1, \ldots, p_n, \lambda) = -\sum_{i=1}^n p_i \ln p_i + \lambda\left(\sum_{i=1}^n p_i - 1\right)$

각 $p_i$에 대해 편미분하여 0으로 둔다.

$$\frac{\partial \mathcal{L}}{\partial p_i} = -\ln p_i - 1 + \lambda = 0 \quad \Longrightarrow \quad \ln p_i = \lambda - 1$$

따라서 모든 $p_i$가 같다: $p_1 = p_2 = \cdots = p_n$. 제약 조건 $\sum p_i = 1$에서 $p_i = 1/n$을 얻는다.

$$H_{\max} = -\sum_{i=1}^n \frac{1}{n} \ln \frac{1}{n} = \ln n$$

$\square$

KL 발산을 이용한 대안 증명: 균등분포 $u(x) = 1/n$에 대해 $0 \leq D_{KL}(p \| u) = \sum p \ln(p / (1/n)) = -H(p) + \ln n$이므로 $H(p) \leq \ln n$이다.

## 예제

**예제 1 (공정한 동전 vs 편향 동전):**
- 공정한 동전: $p(\text{H}) = 0.5$, $p(\text{T}) = 0.5$

$$H = -(0.5 \ln 0.5 + 0.5 \ln 0.5) = -\ln 0.5 = \ln 2 \approx 0.693 \text{ nats} = 1 \text{ bit}$$

- 편향 동전: $p(\text{H}) = 0.9$, $p(\text{T}) = 0.1$

$$H = -(0.9 \ln 0.9 + 0.1 \ln 0.1) \approx -(0.9 \times (-0.105) + 0.1 \times (-2.303)) = 0.095 + 0.230 = 0.325 \text{ nats}$$

편향될수록 엔트로피가 낮아진다. $p=0.9$일 때보다 $p=0.5$일 때 예측이 더 어렵기 때문이다.

**예제 2 (편향 동전의 엔트로피 함수):** 앞면 확률 $p$에 따른 엔트로피 $H(p) = -p\ln p - (1-p)\ln(1-p)$를 **이진 엔트로피 함수(binary entropy function)**라 한다. $p=0$ 또는 $p=1$에서 $H=0$, $p=0.5$에서 최댓값 $\ln 2$를 갖는다.

**예제 3 (두 정규분포의 KL 발산):** $p = \mathcal{N}(\mu_1, \sigma_1^2)$, $q = \mathcal{N}(\mu_2, \sigma_2^2)$일 때

$$D_{KL}(p \| q) = \ln\frac{\sigma_2}{\sigma_1} + \frac{\sigma_1^2 + (\mu_1 - \mu_2)^2}{2\sigma_2^2} - \frac{1}{2}$$

**유도:** 정규분포의 KL 발산 공식을 직접 계산한다.

$$D_{KL}(p\|q) = \int \frac{1}{\sqrt{2\pi}\sigma_1} e^{-\frac{(x-\mu_1)^2}{2\sigma_1^2}} \ln\left( \frac{\sigma_2}{\sigma_1} \exp\left[ -\frac{(x-\mu_1)^2}{2\sigma_1^2} + \frac{(x-\mu_2)^2}{2\sigma_2^2} \right] \right) dx$$

$$= \ln\frac{\sigma_2}{\sigma_1} + \mathbb{E}_p\left[ -\frac{(X-\mu_1)^2}{2\sigma_1^2} + \frac{(X-\mu_2)^2}{2\sigma_2^2} \right]$$

$X \sim \mathcal{N}(\mu_1,\sigma_1^2)$일 때 $\mathbb{E}[(X-\mu_1)^2] = \sigma_1^2$, $\mathbb{E}[(X-\mu_2)^2] = \sigma_1^2 + (\mu_1-\mu_2)^2$를 대입하면 위 결과를 얻는다.

예: $\mu_1=0$, $\sigma_1=1$, $\mu_2=1$, $\sigma_2=1$이면

$$D_{KL} = 0 + \frac{1 + 1}{2} - \frac{1}{2} = 0.5 \text{ nats}$$

**예제 4 (상호정보량 계산):** 다음 결합분포를 가지는 $(X,Y)$의 $I(X;Y)$를 구하라.

| $X \setminus Y$ | 0 | 1 |
|---|---|---|
| 0 | 0.3 | 0.1 |
| 1 | 0.2 | 0.4 |

**풀이:** 주변분포를 먼저 구한다.
$p_X(0) = 0.4$, $p_X(1) = 0.6$
$p_Y(0) = 0.5$, $p_Y(1) = 0.5$

$$I(X;Y) = \sum_{x,y} p(x,y) \ln \frac{p(x,y)}{p(x)p(y)}$$

각 항을 계산한다:

$(0,0): 0.3 \ln\frac{0.3}{0.4 \times 0.5} = 0.3 \ln(1.5) \approx 0.3 \times 0.405 = 0.122$

$(0,1): 0.1 \ln\frac{0.1}{0.4 \times 0.5} = 0.1 \ln(0.5) \approx 0.1 \times (-0.693) = -0.069$

$(1,0): 0.2 \ln\frac{0.2}{0.6 \times 0.5} = 0.2 \ln(0.667) \approx 0.2 \times (-0.405) = -0.081$

$(1,1): 0.4 \ln\frac{0.4}{0.6 \times 0.5} = 0.4 \ln(1.333) \approx 0.4 \times 0.288 = 0.115$

$$I(X;Y) \approx 0.122 - 0.069 - 0.081 + 0.115 = 0.087 \text{ nats}$$

$X$와 $Y$는 완전히 독립이 아니며, 약 0.087 nats의 정보를 공유한다.

**예제 5 (이진 분류의 교차 엔트로피):** 실제 레이블 분포가 $p(1)=0.8$, $p(0)=0.2$이고, 모델 예측이 $q(1)=0.6$, $q(0)=0.4$라고 하자.

$$H(p,q) = -0.8\ln 0.6 - 0.2\ln 0.4 \approx -0.8(-0.511) - 0.2(-0.916) = 0.409 + 0.183 = 0.592$$

이에 비해 $H(p) = -0.8\ln 0.8 - 0.2\ln 0.2 \approx 0.178 + 0.322 = 0.500$이다. $D_{KL}(p\|q) = 0.592 - 0.500 = 0.092$ nats다.

## 연결

- **[기댓값·분산·공분산](topics/expectation-variance.html)** : 엔트로피 $H(X) = -\sum p(x)\ln p(x)$는 $\ln(1/p(X))$의 기댓값이다. KL 발산도 로그 비율의 기댓값으로, 기댓값 연산자의 일반성이 드러난다.
- **[정보기하](topics/information-geometry.html)** : KL 발산은 확률분포 공간에 리만 계량(Riemannian metric)을 유도한다. 피셔 정보 행렬(Fisher information matrix)이 이 계량을 결정하며, 자연 그래디언트(natural gradient)의 기초다.
- **[최대가능도추정](topics/mle.html)** : MLE는 관측 데이터 분포 $p_{\text{data}}$와 모델 분포 $p_\theta$ 사이의 KL 발산 $D_{KL}(p_{\text{data}} \| p_\theta)$를 최소화하는 것과 동등하다. 가능도 최대화는 교차 엔트로피 최소화와 같다.
