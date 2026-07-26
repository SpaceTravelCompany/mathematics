---
title: 몬테카를로
slug: monte-carlo
---

## 직관적 설명

**몬테카를로 방법(Monte Carlo method)**은 무작위 샘플을 사용하여 적분이나 기댓값을 근사하는 기법이다. "원주율 $\pi$를 다트로 계산한다"는 유명한 비유가 있다: 정사각형에 내접하는 원을 그리고, 정사각형 영역에 무작위로 점을 던지면 원 안에 들어가는 점의 비율이 $\pi/4$에 수렴한다.

수학적으로는 다음 적분(기댓값)을 근사하는 것이 핵심이다.

$$I = \int f(x) p(x)\,dx = \mathbb{E}_p[f(X)]$$

몬테카를로 추정량(estimator)은 $p$에서 추출한 $N$개의 샘플로 이 적분을 근사한다.

$$\hat{I}_N = \frac{1}{N} \sum_{i=1}^N f(X_i), \quad X_i \sim p$$

**중요도 샘플링(importance sampling)**은 샘플링이 어려운 분포 $p$ 대신 샘플링이 쉬운 분포 $q$에서 샘플을 추출하고, 가중치 $p(x)/q(x)$를 곱해 보정하는 방법이다.

$$\hat{I}_{\text{IS}} = \frac{1}{N} \sum_{i=1}^N f(X_i) \frac{p(X_i)}{q(X_i)}, \quad X_i \sim q$$

## 정의

**몬테카를로 적분(Monte Carlo integration):** $X_1, \ldots, X_N \stackrel{\text{iid}}{\sim} p$일 때

$$\hat{I}_N = \frac{1}{N} \sum_{i=1}^N f(X_i)$$

는 $I = \mathbb{E}_p[f(X)]$의 추정량이다.

**중요도 샘플링(importance sampling):** $X_1, \ldots, X_N \stackrel{\text{iid}}{\sim} q$일 때

$$\hat{I}_{\text{IS}} = \frac{1}{N} \sum_{i=1}^N f(X_i) w(X_i), \quad w(x) = \frac{p(x)}{q(x)}$$

여기서 $w(x)$를 **중요도 가중치(importance weight)**라 한다. $q$는 **제안분포(proposal distribution)** 또는 중요도 분포(importance distribution)라 부른다.

**조건:** $q(x) > 0$일 때마다 $p(x) > 0$이어야 한다($p \ll q$, 즉 $p$는 $q$에 절대연속, absolutely continuous). 또한 $\text{Var}_q[f(X)w(X)] < \infty$여야 추정량이 안정적이다.

## 주요 정리와 증명

### 정리 1: 몬테카를로 추정량의 비편향성

$\mathbb{E}[\hat{I}_N] = I$

**증명:** 각 샘플 $X_i$는 $p$에서 추출되었으므로 $\mathbb{E}[f(X_i)] = I$이다. 기댓값의 선형성을 적용하면

$$\mathbb{E}[\hat{I}_N] = \mathbb{E}\left[\frac{1}{N}\sum_{i=1}^N f(X_i)\right] = \frac{1}{N}\sum_{i=1}^N \mathbb{E}[f(X_i)] = \frac{1}{N} \cdot N \cdot I = I$$

$\square$

### 정리 2: 몬테카를로 추정량의 분산과 수렴 속도

$$\text{Var}(\hat{I}_N) = \frac{\sigma^2}{N}, \quad \text{where } \sigma^2 = \text{Var}_p(f(X))$$

표준오차(standard error)는 $\sigma/\sqrt{N}$으로, $O(1/\sqrt{N})$의 속도로 수렴한다.

**증명:** $X_i$가 iid이므로

$$\text{Var}(\hat{I}_N) = \text{Var}\left(\frac{1}{N}\sum_{i=1}^N f(X_i)\right) = \frac{1}{N^2}\sum_{i=1}^N \text{Var}(f(X_i)) = \frac{1}{N^2} \cdot N \cdot \sigma^2 = \frac{\sigma^2}{N}$$

$\square$

몬테카를로의 수렴 속도 $O(1/\sqrt{N})$는 차원 $d$에 무관하다는 점이 중요하다. 이는 결정론적 수치적분(예: 사다리꼴 공식)이 $O(N^{-2/d})$로 차원에 민감한 것과 대조된다. 고차원 적분에서 몬테카를로 방법이 효과적인 이유다.

### 정리 3: 중요도 샘플링의 비편향성

$\mathbb{E}_q[\hat{I}_{\text{IS}}] = I$

**증명:** 제안분포 $q$에 대한 기댓값을 계산한다.

$$\mathbb{E}_q[\hat{I}_{\text{IS}}] = \frac{1}{N}\sum_{i=1}^N \mathbb{E}_q\left[f(X_i)\frac{p(X_i)}{q(X_i)}\right]$$

$$= \mathbb{E}_q\left[f(X)\frac{p(X)}{q(X)}\right] = \int f(x)\frac{p(x)}{q(x)} q(x)\,dx = \int f(x)p(x)\,dx = I$$

$\square$

중요도 샘플링은 분포 가중치 $w(x) = p(x)/q(x)$를 통해 분포를 "우회"하는 방법이다. $q(x)$를 현명하게 선택하면 분산을 원래 몬테카를로보다 줄일 수도 있다.

### 정리 4: 중요도 샘플링의 분산

$$\text{Var}_q(\hat{I}_{\text{IS}}) = \frac{1}{N} \left( \mathbb{E}_q\left[f(X)^2 w(X)^2\right] - I^2 \right)$$

$= \frac{1}{N} \left( \int \frac{f(x)^2 p(x)^2}{q(x)}\,dx - I^2 \right)$

**증명:**

$$\text{Var}_q(\hat{I}_{\text{IS}}) = \frac{1}{N} \text{Var}_q(f(X)w(X))$$

$$= \frac{1}{N} \left( \mathbb{E}_q[f(X)^2 w(X)^2] - (\mathbb{E}_q[f(X)w(X)])^2 \right)$$

$\mathbb{E}_q[f(X)w(X)] = I$이므로, 첫 항만 전개하면

$$\mathbb{E}_q[f(X)^2 w(X)^2] = \int f(x)^2 \frac{p(x)^2}{q(x)^2} q(x)\,dx = \int \frac{f(x)^2 p(x)^2}{q(x)}\,dx$$

$\square$

$q(x)$를 $|f(x)|p(x)$에 비례하도록 선택하면 분산이 최소화된다(최적 제안분포, optimal proposal). 이는 $p(x)$와 $|f(x)|$의 곱에 비례하는 제안이 가장 효율적임을 의미한다.

### 정리 5: 대수의 법칙에 의한 거의 확실 수렴

$X_1, X_2, \ldots$가 iid이고 $\mathbb{E}[|f(X_1)|] < \infty$이면

$$\hat{I}_N = \frac{1}{N}\sum_{i=1}^N f(X_i) \xrightarrow{\text{a.s.}} I$$

**증명 (서술):** **강대수의 법칙(strong law of large numbers, SLLN)**에 의해 iid 확률변수의 표본평균은 기댓값으로 거의 확실히(almost surely) 수렴한다. 즉 $P(\lim_{N\to\infty} \hat{I}_N = I) = 1$이다. 이는 몬테카를로 방법의 이론적 근거를 제공한다. $\square$

## 예제

**예제 1 (몬테카를로로 $\pi$ 추정):** 단위원(unit circle)이 내접하는 정사각형 $[-1,1]^2$에 균등하게 점을 던진다. 원 안에 들어갈 확률은 $\pi/4$다.

```python
import random, math
N = 1000000
count = 0
for _ in range(N):
    x = random.uniform(-1, 1)
    y = random.uniform(-1, 1)
    if x*x + y*y <= 1:
        count += 1
pi_est = 4 * count / N
```

$N=10^6$일 때 $\pi \approx 3.1416$ 근처 값을 얻는다. 표준오차는 $\sqrt{\pi(4-\pi)/N} \approx 0.0016$이다.

더 엄밀히: $I = \int_{-1}^1 \int_{-1}^1 \mathbf{1}(x^2+y^2 \leq 1) \cdot \frac{1}{4}\,dx\,dy = \frac{\pi}{4}$이므로 $\hat{I}_N$으로 $\pi/4$를 추정하고 4를 곱한다.

**예제 2 ($\int_0^1 e^{-x^2}\,dx$의 근사):** 이 적분은 초등함수로 표현할 수 없다(오차함수, error function). 몬테카를로로 $p(x) = \text{U}(0,1)$(즉 $f(x)=e^{-x^2}$)에서 $N$개 샘플을 추출한다.

$$\hat{I}_N = \frac{1}{N}\sum_{i=1}^N e^{-U_i^2},\quad U_i \sim \text{U}(0,1)$$

$N=10^5$일 때 대략 $0.7468$ 근처 값이 나온다(참값: $\sqrt{\pi}/2 \cdot \text{erf}(1) \approx 0.746824$). 표준오차는 $\sigma/\sqrt{N}$으로, $\sigma^2 = \int_0^1 e^{-2x^2}dx - I^2 \approx 0.0409$이므로 $\sigma/\sqrt{N} \approx 0.00064$다.

**예제 3 (중요도 샘플링으로 희귀 사건 추정):** $X \sim \mathcal{N}(0,1)$일 때 $P(X > 5) = \Phi(-5) \approx 2.87 \times 10^{-7}$를 추정한다. 일반 몬테카를로로는 $10^7$개 샘플 중 약 3개만이 임계값을 넘는다 — 매우 비효율적이다.

대신 제안분포 $q(x) = \mathcal{N}(5, 1)$(평균을 5로 이동)를 사용한다.

$$\hat{P} = \frac{1}{N}\sum_{i=1}^N \mathbf{1}(X_i > 5) \frac{\phi(X_i)}{\phi(X_i-5)},\quad X_i \sim \mathcal{N}(5, 1)$$

여기서 $\phi$는 표준정규분포의 PDF다. $q$에서 추출된 샘플의 대부분이 $X > 5$ 영역에 있으므로, 가중치로 보정하더라도 훨씬 적은 샘플로 정확한 추정이 가능하다.

**예제 4 (몬테카를로 적분의 차원 무관성):** $d$차원 단위 초입방체 $[0,1]^d$에서 적분 $I = \int_{[0,1]^d} g(\mathbf{x})\,d\mathbf{x}$를 근사한다고 하자. 몬테카를로 오차는 $O(1/\sqrt{N})$로 $d$와 무관하다. 반면 결정론적 수치적분(직사각형 격자)의 오차는 $O(N^{-1/d})$로, $d$가 커지면 급격히 나빠진다. $d=10$에서 $N=10^6$개의 격자점을 쓰면 각 차원당 간격이 $N^{-1/d} = 10^{-0.6} \approx 0.25$로 매우 거칠다. 이 현상을 **차원의 저주(curse of dimensionality)**라 한다.

**예제 5 (분산 비교 — 중요도 샘플링의 효율):** $I = \int_0^1 \frac{1}{1+x^2}\,dx = \pi/4 \approx 0.7854$를 추정한다.

(a) 일반 MC: $X \sim \text{U}(0,1)$, $f(x)=1/(1+x^2)$. $f(x)$가 $[0,1]$에서 0.5에서 1 사이이므로 분산이 크지 않다.

(b) 중요도 샘플링: $g(x) \propto 1/(1+x^2)$에 비례하는 제안을 사용한다면(정규화 상수를 알고 있다고 가정), 분산이 0이 된다. 실제로는 근사적으로 $q(x) = \text{Beta}(0.5, 0.5)$를 사용할 수 있다(이 분포는 $x=0$과 $x=1$에서 밀도가 높아 $1/(1+x^2)$의 형태와 유사하다).

중요도 샘플링의 효율은 **유효 표본 크기(effective sample size, ESS)**로 측정한다.

$$N_{\text{eff}} = \frac{N}{1 + \text{Var}_q(w(X))} \approx \frac{N}{\sum w_i^2 / (\sum w_i)^2}$$

가중치의 분산이 클수록 $N_{\text{eff}}$가 작아진다.

## 연결

- **[대수의 법칙](law-large-numbers.html)** : 몬테카를로 방법의 이론적 근거는 대수의 법칙이다. $N \to \infty$에서 $\frac{1}{N}\sum f(X_i) \to \mathbb{E}[f(X)]$가 거의 확실히 성립한다.
- **[중요도 샘플링](importance-sampling.html)** : 중요도 샘플링은 몬테카를로 적분을 일반화하여 샘플링이 어려운 분포를 우회한다. 최적 제안분포 선택, 가중치의 안정성, $N_{\text{eff}}$ 등이 핵심 주제다.
- **[마르코프 체인·MCMC](mcmc.html)** : MCMC는 몬테카를로 방법과 마르코프 체인을 결합한다. 직접 샘플링이 불가능한 고차원 사후분포에서도 마르코프 체인의 정상분포를 이용해 샘플을 수집할 수 있다.
