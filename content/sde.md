---
title: 확률미분방정식
slug: sde
---

## 직관적 설명

**확률미분방정식(stochastic differential equation, SDE)**은 상미분방정식(ODE)에 무작위적인 잡음(random noise)을 추가한 것이다. 현실의 시스템은 항상 외부적 교란, 측정 오차, 또는 근본적인 확률성에 노출되어 있다. SDE는 이러한 현상을 수학적으로 포착한다.

ODE가 $dx/dt = f(x, t)$라면, SDE는 미분 형식(differential form)으로

$$dX_t = f(X_t, t)\,dt + g(X_t, t)\,dW_t$$

와 같이 쓴다. 여기서 $dt$ 항은 **드리프트(drift)** — 결정론적 추세 — 를 나타내고, $dW_t$ 항은 **확산(diffusion)** — 무작위적 변동 — 을 나타낸다. $W_t$는 **브라운 운동(Brownian motion)** 또는 **위너 과정(Wiener process)** 으로, 연속적인 불규칙 보행(continuous random walk)이다.

핵심 통찰: SDE에서 $dW_t$는 $dt$의 제곱근 크기($\sqrt{dt}$)로 움직인다. 이 때문에 $(dW_t)^2 = dt$가 성립하고, 이것이 이토 미적분(Itô calculus)이 일반 미적분과 다른 이유다. 연쇄법칙(chain rule)에 $f''$ 항이 추가로 등장하는 **이토 보조법(Itô's lemma)**이 그 결과다.

---
## 정의

**브라운 운동 / 위너 과정 (Brownian motion / Wiener process):** 확률과정 $\{W_t\}_{t \geq 0}$이 다음을 만족하면 위너 과정이라 한다:

1. $W_0 = 0$ (확률 1로)
2. $W_t$는 연속적(continuous)임
3. **독립 증분(independent increments):** $0 \leq s < t$에 대해 $W_t - W_s$는 $\{W_u\}_{u \leq s}$와 독립
4. **정규 증분(normal increments):** $W_t - W_s \sim \mathcal{N}(0, t-s)$

위너 과정은 거의 모든 궤적이 어디에서도 미분가능하지 않다(nowhere differentiable). $dB_t/dt$는 존재하지 않으며, $dW_t$는 형식적인 표기법이다.

**확률미분방정식 (stochastic differential equation, SDE):**

$$dX_t = f(X_t, t)\,dt + g(X_t, t)\,dW_t$$

- $f(X_t, t)$: **드리프트 계수(drift coefficient)**, 결정론적 변화율
- $g(X_t, t)$: **확산 계수(diffusion coefficient)**, 잡음의 강도
- $dW_t$: 위너 과정의 증분

적분 형태로는:

$$X_t = X_0 + \int_0^t f(X_s, s)\,ds + \int_0^t g(X_s, s)\,dW_s$$

첫 번째 적분은 일반 리만 적분, 두 번째 적분은 **이토 적분(Itô integral)** 이다.

**이토 적분 (Itô integral):** 피적분 함수 $\phi(t, \omega)$가 $\mathcal{F}_t$-가측(non-anticipative, 미래를 보지 않음)이고 $\mathbb{E}[\int_0^T \phi^2\,ds] < \infty$를 만족할 때,

$$\int_0^T \phi(s)\,dW_s := \lim_{n \to \infty} \sum_{i=0}^{n-1} \phi(t_i)(W_{t_{i+1}} - W_{t_i})$$

극한은 $L^2$ 수렴(mean-square convergence)이다. 중요한 점: 이토 적분은 왼쪽 끝점(left endpoint) $t_i$에서 평가하므로, 적분과 피적분 함수 사이에 미래 정보가 흘러들지 않는다(non-anticipating). 이는 마팅게일(martingale) 성질을 유지하게 해준다.

**이차 변분 (quadratic variation):** $[W]_T = \lim_{\|\Delta\| \to 0} \sum_{i=0}^{n-1} (W_{t_{i+1}} - W_{t_i})^2 = T$ (확률 1 수렴). 즉, $(dW_t)^2 = dt$가 **제곱평균(mean-square)** 의미에서 성립한다.

---
## 주요 정리와 증명

### 정리 1: $(dW_t)^2 = dt$의 의미와 이차 변분

**서술:** 위너 과정 $W_t$의 구간 $[0, T]$에서의 이차 변분(quadratic variation)은 $T$이다:

$$[W]_T = \lim_{\|\Delta\| \to 0} \sum_{i=0}^{n-1} (W_{t_{i+1}} - W_{t_i})^2 = T \quad \text{(확률 1로)}$$

**증명 (개요):** 분할 $\Delta: 0 = t_0 < t_1 < \cdots < t_n = T$, $\|\Delta\| = \max_i \Delta t_i$. 증분 $\Delta W_i = W_{t_{i+1}} - W_{t_i}$는 $\mathcal{N}(0, \Delta t_i)$를 따른다.

$V_n = \sum_{i=0}^{n-1} (\Delta W_i)^2$라 하자. $\mathbb{E}[(\Delta W_i)^2] = \Delta t_i$이므로 $\mathbb{E}[V_n] = T$이다.

분산을 계산하면:

$$\text{Var}[(\Delta W_i)^2] = \mathbb{E}[(\Delta W_i)^4] - (\mathbb{E}[(\Delta W_i)^2])^2 = 3(\Delta t_i)^2 - (\Delta t_i)^2 = 2(\Delta t_i)^2$$

$$\text{Var}[V_n] = \sum_{i=0}^{n-1} 2(\Delta t_i)^2 \leq 2\|\Delta\| \sum \Delta t_i = 2\|\Delta\| T \to 0$$

따라서 $\|\Delta\| \to 0$에서 $V_n \to T$ (확률 수렴). 더 강하게, 거의 확실한 수렴도 성립한다. $\square$

**의미:** $(dW_t)^2 = dt$라는 형식적 관계는 이토 미적분의 근간이다. 일반 함수 $f(W_t)$의 미분을 계산할 때 $(dW_t)^2$가 $dt$로 대체되면서 2계 도함수 항이 발생한다.

### 정리 2: 이토 보조법 (Itô's Lemma)

**서술:** $X_t$가 SDE $dX_t = f\,dt + g\,dW_t$를 따르고 $F(X_t, t)$가 $C^2$ 함수이면,

$$dF(X_t, t) = \frac{\partial F}{\partial t} dt + \frac{\partial F}{\partial x} dX_t + \frac{1}{2} \frac{\partial^2 F}{\partial x^2} (dX_t)^2$$

$(dX_t)^2$를 전개하면 $(dt)^2 = 0$, $dt\,dW_t = 0$, $(dW_t)^2 = dt$이므로:

$$dF = \left( \frac{\partial F}{\partial t} + f\frac{\partial F}{\partial x} + \frac{1}{2} g^2 \frac{\partial^2 F}{\partial x^2} \right) dt + g\frac{\partial F}{\partial x} dW_t$$

**직관적 유도:** 테일러 전개를 2차 항까지 수행한다:

$$dF = \frac{\partial F}{\partial t} dt + \frac{\partial F}{\partial x} dX + \frac{1}{2} \frac{\partial^2 F}{\partial x^2} (dX)^2 + \frac{\partial^2 F}{\partial x \partial t} dt\,dX + \frac{1}{2} \frac{\partial^2 F}{\partial t^2} (dt)^2$$

여기에 $dX = f\,dt + g\,dW$를 대입하고 $(dt)^2 = 0$, $dt\,dW = 0$, $(dW)^2 = dt$를 적용한다. $\frac{\partial^2 F}{\partial x \partial t} dt\,dX$ 항은 $dt \cdot dW$를 포함하므로 0이 된다. 따라서

$$dF = \frac{\partial F}{\partial t} dt + \frac{\partial F}{\partial x} (f\,dt + g\,dW) + \frac{1}{2} \frac{\partial^2 F}{\partial x^2} g^2 dt$$

항을 모으면 위의 결과를 얻는다. $\square$

이토 보조법의 핵심: 일반 미적분의 연쇄법칙 $dF = F'(X)dX$와 달리 $\frac{1}{2} g^2 F'' dt$ 항이 추가된다. 이는 확률过程的의 2차 변분이 0이 아니기 때문이다.

### 정리 3: 기하 브라운 운동 (Geometric Brownian Motion)

**서술:** $dS_t = \mu S_t\,dt + \sigma S_t\,dW_t$, $S_0 > 0$의 해는

$$S_t = S_0 \exp\left( \left(\mu - \frac{\sigma^2}{2}\right) t + \sigma W_t \right)$$

이다.

**증명:** 이토 보조법을 $F(S, t) = \ln S$에 적용한다.

$\frac{\partial F}{\partial t} = 0$, $\frac{\partial F}{\partial S} = \frac{1}{S}$, $\frac{\partial^2 F}{\partial S^2} = -\frac{1}{S^2}$.

$f = \mu S$, $g = \sigma S$이므로:

$$d(\ln S) = \left( 0 + \mu S \cdot \frac{1}{S} + \frac{1}{2} \sigma^2 S^2 \cdot \left(-\frac{1}{S^2}\right) \right) dt + \sigma S \cdot \frac{1}{S} dW_t$$

$$= \left( \mu - \frac{\sigma^2}{2} \right) dt + \sigma dW_t$$

양변을 $0$부터 $t$까지 적분하면:

$$\ln S_t - \ln S_0 = \left( \mu - \frac{\sigma^2}{2} \right) t + \sigma W_t$$

$$\ln \frac{S_t}{S_0} = \left( \mu - \frac{\sigma^2}{2} \right) t + \sigma W_t$$

따라서

$$S_t = S_0 \exp\left( \left(\mu - \frac{\sigma^2}{2}\right) t + \sigma W_t \right)$$

$\square$

**관찰:** $\mathbb{E}[S_t] = S_0 e^{\mu t}$이다. 즉, 기하 브라운 운동의 기댓값은 결정론적 성장률 $\mu$를 따르지만, **중앙값(median)**은 $S_0 e^{(\mu - \sigma^2/2)t}$이다. 로그정규분포의 비대칭성(skewness) 때문이다. 이 모델은 블랙-숄즈(Black-Scholes) 옵션 가격 모형의 기초가 된다.

### 정리 4: 오른슈타인-울렌벡 과정 (Ornstein-Uhlenbeck Process)

**서술:** $dX_t = -\theta X_t\,dt + \sigma dW_t$ ($\theta > 0$)의 해는

$$X_t = X_0 e^{-\theta t} + \sigma \int_0^t e^{-\theta(t-s)} dW_s$$

이며, 정상분포(stationary distribution)는 $\mathcal{N}(0, \sigma^2/2\theta)$이다.

**증명:** 적분인자법을 확률적 버전으로 적용한다. $F(X, t) = X e^{\theta t}$에 이토 보조법을 적용한다.

$\frac{\partial F}{\partial t} = \theta X e^{\theta t}$, $\frac{\partial F}{\partial X} = e^{\theta t}$, $\frac{\partial^2 F}{\partial X^2} = 0$.

$$d(X e^{\theta t}) = (\theta X e^{\theta t}) dt + e^{\theta t} dX + 0$$

$dX = -\theta X dt + \sigma dW_t$를 대입하면:

$$d(X e^{\theta t}) = \theta X e^{\theta t} dt + e^{\theta t}(-\theta X dt + \sigma dW_t) = \sigma e^{\theta t} dW_t$$

양변을 $0$부터 $t$까지 적분:

$$X_t e^{\theta t} - X_0 = \sigma \int_0^t e^{\theta s} dW_s$$

$$X_t = X_0 e^{-\theta t} + \sigma \int_0^t e^{-\theta(t-s)} dW_s$$

이토 적분의 등장성(isometry) $\mathbb{E}[(\int_0^t \phi\,dW)^2] = \int_0^t \phi^2 ds$를 이용하면:

$$\mathbb{E}[X_t] = X_0 e^{-\theta t} \to 0$$

$$\text{Var}(X_t) = \sigma^2 \int_0^t e^{-2\theta(t-s)} ds = \sigma^2 \cdot \frac{1 - e^{-2\theta t}}{2\theta} \to \frac{\sigma^2}{2\theta}$$

$t \to \infty$에서 $X_t$는 $\mathcal{N}(0, \sigma^2/2\theta)$에 수렴하며, 이는 OU 과정의 정상분포이다. $\square$

OU 과정은 평균으로 회귀(mean-reverting)하는 성질을 가진다: $X_t$가 0보다 크면 드리프트 $-\theta X_t$가 음수여서 $X_t$를 다시 0으로 끌어당긴다. 이자율 모형(Vasicek 모형), 신경 과학(뉴런 전위), 통계 물리(속도 과정) 등에广泛应用된다.

---
## 예제

**예제 1 (이토 보조법 직접 적용 — $\ln S_t$ 전개):** $dS = \mu S\,dt + \sigma S\,dW$에서 $d(\ln S)$를 계산하고, 이를 통해 해가 로그정규분포를 따름을 보여라.

**풀이:** 위 정리 3에서 $d(\ln S) = (\mu - \sigma^2/2)dt + \sigma dW$임을 유도했다. 따라서

$$\ln S_t - \ln S_0 = \left( \mu - \frac{\sigma^2}{2} \right) t + \sigma W_t$$

$W_t \sim \mathcal{N}(0, t)$이므로 $\ln S_t \sim \mathcal{N}(\ln S_0 + (\mu - \sigma^2/2)t, \sigma^2 t)$.

$S_t$는 **로그정규분포(lognormal distribution)**를 따른다:

$$f_{S_t}(s) = \frac{1}{s\sigma\sqrt{2\pi t}} \exp\left( -\frac{(\ln s - \ln S_0 - (\mu - \sigma^2/2)t)^2}{2\sigma^2 t} \right), \quad s > 0$$

**예제 2 (적분 형태의 OU 과정):** $dX = -\theta X\,dt + \sigma dW$ ($\theta = 2$, $\sigma = 1$, $X_0 = 0$)에 대해 $\mathbb{E}[X_t^2]$를 계산하라.

**풀이:** 위 정리 4의 해:

$$X_t = \sigma \int_0^t e^{-2(t-s)} dW_s$$

이토 등장성(Itô isometry)에 의해:

$$\mathbb{E}[X_t^2] = \sigma^2 \int_0^t e^{-4(t-s)} ds = \int_0^t e^{-4(t-s)} ds = \frac{1 - e^{-4t}}{4}$$

$t = 1$에서 $\mathbb{E}[X_1^2] = (1 - e^{-4})/4 \approx 0.245$.

이는 OU 과정의 분산이 시간에 따라 단조 증가하여 $\sigma^2/2\theta = 1/4$로 수렴함을 확인해준다.

**예제 3 ($\mathbb{E}[W_t^2]$의 직접 계산):** 이토 보조법을 이용하여 $\mathbb{E}[W_t^2] = t$를 증명하라.

**풀이:** $F(W_t) = W_t^2$에 이토 보조법을 적용한다. $dW_t$에 대해 $f = 0$, $g = 1$이므로:

$$d(W_t^2) = (0 \cdot 2W_t + \frac{1}{2} \cdot 1 \cdot 2) dt + 1 \cdot 2W_t dW_t = dt + 2W_t dW_t$$

적분 형태:

$$W_t^2 = \int_0^t ds + 2 \int_0^t W_s dW_s = t + 2 \int_0^t W_s dW_s$$

이토 적분 $\int_0^t W_s dW_s$는 마팅게일이므로 기댓값이 0이다. 따라서

$$\mathbb{E}[W_t^2] = \mathbb{E}\left[ t + 2 \int_0^t W_s dW_s \right] = t + 0 = t$$

이는 위너 과정의 분산이 시간에 비례함을 확인한다. 이토 보조법이 없었다면 $d(W_t^2) = 2W_t dW_t$라고 잘못 계산할 뻔했다 — 이 예제는 확률 미적분에서 일반 미적분과의 차이를 가장 명확히 보여준다.

**예제 4 (선형 SDE의 해):** $dX_t = (aX_t + b)dt + c dW_t$, $X_0 = x_0$의 해를 구하라.

**풀이:** 이는 선형 SDE로, 적분인자법이 적용된다. $d(e^{-at}X_t)$를 계산한다.

$F(X, t) = X e^{-at}$에 이토 보조법을 적용:

$$d(e^{-at}X) = -a e^{-at} X dt + e^{-at} dX$$

$dX = (aX + b)dt + c dW$를 대입:

$$d(e^{-at}X) = -a e^{-at} X dt + e^{-at}[(aX + b)dt + c dW] = b e^{-at} dt + c e^{-at} dW$$

적분:

$$e^{-at} X_t - x_0 = b \int_0^t e^{-as} ds + c \int_0^t e^{-as} dW_s$$

$$X_t = x_0 e^{at} + \frac{b}{a}(e^{at} - 1) + c \int_0^t e^{a(t-s)} dW_s$$

이는 선형 SDE의 일반해로, $f$와 $g$가 각각 $X$에 대해 선형일 때 항상 이 방법으로 풀 수 있다.

**예제 5 (이토 적분의 등장성 확인):** $\mathbb{E}\left[ \left( \int_0^t s\,dW_s \right)^2 \right]$를 계산하라.

**풀이:** 이토 등장성(Itô isometry):

$$\mathbb{E}\left[ \left( \int_0^t \phi(s)\,dW_s \right)^2 \right] = \mathbb{E}\left[ \int_0^t \phi(s)^2\,ds \right]$$

여기서 $\phi(s) = s$이므로:

$$\mathbb{E}\left[ \left( \int_0^t s\,dW_s \right)^2 \right] = \mathbb{E}\left[ \int_0^t s^2\,ds \right] = \int_0^t s^2\,ds = \frac{t^3}{3}$$

이는 이토 적분의 분산이 시간의 세제곱으로 증가함을 보여준다. 일반 리만 적분과 달리 이토 적분은 확률변수이며, 그 분산이 이 등장성으로 계산된다.

---
## 연결

- **[상미분방정식 기초](ode-basics.html)** : SDE는 ODE에 확산항 $g\,dW$를 추가한 확장이다.
드리프트 $f$는 ODE의 우변과 동일한 역할을 한다.
- **[마르코프 체인](markov-chains.html)** : SDE의 해 $X_t$는 마르코프 성질을 만족한다 — 미래의 분포는 오직 현재 $X_t$에만 의존한다. 연속 시간·연속 공간의 마르코프 과정으로 볼 수 있다.
- **[몬테카를로](monte-carlo.html)** : SDE의 해는 해석적으로 구할 수 없는 경우가 많다. 몬테카를로 시뮬레이션(오일러-마루야마 이산화)으로 수치적 근사를 구한다.
