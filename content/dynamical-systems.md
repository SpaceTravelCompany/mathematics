---
title: 미분방정식과 동역학
slug: dynamical-systems
---

## 직관적 설명

**동역학계(dynamical system)**는 시간에 따라 변하는 계(system)의 진화 법칙을 연구하는 학문이다. 자연 법칙의 대부분은 미분방정식으로 표현되며, 동역학계 이론은 "해를 구하는 것"을 넘어 "해가 장기적으로 어떻게 행동하는지"를 이해하는 데 초점을 맞춘다.

핵심 질문들:
- 계가 평형 상태(equilibrium)에 도달하는가?
- 평형 상태는 안정적인가? 작은 교란이 사라지는가, 증폭되는가?
- 계가 주기적으로 진동하는가?
- 초기 조건의 아주 작은 차이가 장기적으로 엄청난 차이를 만드는가? (카오스, chaos)

**위상 공간(phase space)**은 계의 모든 가능한 상태를 나타내는 공간이다. 예를 들어 단진자(simple pendulum)의 위상 공간은 각도 $\theta$와 각속도 $\dot{\theta}$로 구성된 2차원 평면이다. 각 점 $(\theta, \dot{\theta})$는 진자의 완전한 상태를 결정하며, 미분방정식은 이 공간 위의 흐름(flow)을 정의한다.

**카오스 이론(chaos theory)**은 20세기 가장 중요한 발견 중 하나로, 결정론적(deterministic) 방정식이 예측 불가능한 행동을 만들어낼 수 있음을 보여준다. 이를 **나비 효과(butterfly effect)** — 초기 조건의 작은 차이가 장기적 예측을 불가능하게 만드는 현상 — 라고 부른다.

## 정의

**동역학계 (dynamical system):** 위상 공간 $\Omega \subseteq \mathbb{R}^n$ 위에서 시간 진화를 규정하는 법칙. 연속 시간(continuous-time) 자율계는 ODE로 표현된다:

$$\dot{x} = f(x), \quad x \in \Omega \subseteq \mathbb{R}^n$$

여기서 $\dot{x} = dx/dt$이고 $f: \Omega \to \mathbb{R}^n$은 벡터장(vector field)이다.

**고정점 / 평형점 (fixed point / equilibrium):** $f(x^*) = 0$을 만족하는 점. 이 점에서 계는 정지해 있다.

**안정성 (stability):**
- **리아푸노프 안정 (Lyapunov stable):** 임의의 $\epsilon > 0$에 대해 $\delta > 0$이 존재하여 $\|x(0) - x^*\| < \delta$이면 모든 $t \geq 0$에 대해 $\|x(t) - x^*\| < \epsilon$이다. 즉, 초기 조건이 조금 어긋나도 궤적이 $x^*$ 근처에 머무른다.
- **점근 안정 (asymptotically stable):** $x^*$가 리아푸노프 안정이고, 어떤 $\delta > 0$에 대해 $\|x(0) - x^*\| < \delta$이면 $\lim_{t\to\infty} x(t) = x^*$이다.
- **불안정 (unstable):** 리아푸노프 안정이 아닌 경우.

**선형화 (linearization):** 고정점 $x^*$ 근처에서 비선형계 $\dot{x} = f(x)$를 1차 근사:

$$\dot{x} \approx Df(x^*)(x - x^*)$$

여기서 $Df(x^*)$는 $f$의 야코비 행렬(Jacobian matrix) $J_{ij} = \partial f_i / \partial x_j$을 $x^*$에서 평가한 것이다.

**한계 순환 (limit cycle):** 위상 공간에서 고립된 폐쇄 궤도(isolated closed trajectory). 근처의 모든 궤도가 이 주기적 궤도로 수렴하거나 발산한다.

**카오스 (chaos):** 결정론적 동역학계에서 나타나는 불규칙적이고 예측 불가능한 행동. 엄밀한 정의는 아래 정리에서 다룬다.

## 주요 정리와 증명

### 정리 1: 선형 안정성 정리 (Linear Stability)

**서술:** 선형계 $\dot{x} = Ax$ ($A$는 $n \times n$ 상수 행렬)에 대해:
- $\text{Re}(\lambda_i) < 0$ $\forall i$ $\Longleftrightarrow$ 원점 $\mathbf{0}$은 점근 안정(asymptotically stable)
- $\text{Re}(\lambda_i) > 0$인 $\lambda_i$ 존재 $\Longrightarrow$ 원점은 불안정(unstable)
- $\text{Re}(\lambda_i) = 0$인 $\lambda_i$가 있고 음의 실수부만 있는 것은 아님 $\Longrightarrow$ 경계선(borderline) — 추가 분석 필요

**증명:** 해 $x(t) = e^{At} x_0$이다. $A$가 대각화 가능하다고 가정하고 $A = PDP^{-1}$ ($D$ 대각행렬)이라 하자. $y = P^{-1}x$로 변수변환하면 각 성분이 독립적으로 진화한다:

$$y_i(t) = e^{\lambda_i t} y_i(0)$$

$\lambda_i = a_i + ib_i$라 하면 $|e^{\lambda_i t}| = e^{a_i t}$이다.

- $a_i < 0$: $t \to \infty$에서 $y_i(t) \to 0$.
- $a_i > 0$: $t \to \infty$에서 $|y_i(t)| \to \infty$.
- $a_i = 0$: $|y_i(t)| = |y_i(0)|$ (유계이지만 0으로 수렴하지 않음).

따라서 모든 $a_i < 0$이면 $y(t) \to 0$이고, 따라서 $x(t) = Py(t) \to 0$이다. 하나라도 $a_i > 0$이면 $y(t)$의 해당 성분이 발산하여 $x(t)$도 발산한다.

대각화 불가능한 경우에는 $t^k e^{\lambda_i t}$ 형태의 항이 나타나지만, $a_i < 0$이면 지수적 감쇠가 다항식 증가를 압도하여 여전히 $x(t) \to 0$이다. $\square$

**의의:** 이 정리는 고정점의 안정성을 고유값만으로 판정할 수 있게 해준다. 비선형계의 국소 안정성 분석의 기초가 된다. 실수부의 부호에 따라 고정점이 분류된다(안정 노드/나선, 불안정 노드/나선, 안장점, 중심 등). $2 \times 2$ 계의 경우, $\det A$와 $\operatorname{tr} A$로 고정점의 성질이 완전히 결정된다.

고정점 분류($2 \times 2$ 선형계 $\dot{x} = Ax$에서):
- $\det A < 0$: 안장점(saddle) — 항상 불안정
- $\det A > 0$, $\operatorname{tr} A < 0$: 안정 노드(stable node) 또는 안정 나선(stable spiral) — $\operatorname{tr}^2 A - 4\det A \geq 0$이면 노드, < 0이면 나선
- $\det A > 0$, $\operatorname{tr} A > 0$: 불안정 노드/나선
- $\det A > 0$, $\operatorname{tr} A = 0$: 중심(center) — 순허수 고유값, 리아푸노프 안정이지만 점근 안정은 아님
- $\operatorname{tr}^2 A - 4\det A = 0$: 축퇴 노드(degenerate node) 또는 별 노드(star node)

### 정리 2: 하트만-그롭만 정리 (Hartman–Grobman Theorem)

**서술:** $f: \mathbb{R}^n \to \mathbb{R}^n$이 $C^1$ 함수이고 $x^*$가 **쌍곡 고정점(hyperbolic fixed point)**이라고 하자. 즉, $Df(x^*)$의 모든 고유값이 실수부가 0이 아니다($\text{Re}(\lambda_i) \neq 0$ $\forall i$). 그러면 $x^*$의 충분히 작은 근방에서 비선형계 $\dot{x} = f(x)$는 선형화된 계 $\dot{x} = Df(x^*)(x - x^*)$와 **위상적으로 동등(topologically equivalent)**하다. 즉, 두 계 사이에 연속적인 좌표 변환(위상 동형사상, homeomorphism)이 존재하여 궤도의 구조가 보존된다.

**의의:** 이 정리는 쌍곡 고정점 근처에서 비선형 효과가 위상적 구조를 바꾸지 않음을 보장한다. 따라서 선형화를 통해 안정성 판정을 내리는 것이 정당화된다. 단, 비쌍곡 고정점(non-hyperbolic, $\text{Re}(\lambda_i) = 0$인 고유값 존재)에서는 선형화만으로 충분하지 않으며, 중심 다양체(center manifold) 이론이 필요하다.

### 정리 3: 리아푸노프 안정성 정리 (Lyapunov's Stability Theorem)

**서술:** 고정점 $x^* = 0$ (일반성을 잃지 않고 $x^*$를 원점으로 이동)을 가진 $\dot{x} = f(x)$를 고려하자. 다음을 만족하는 **리아푸노프 함수(Lyapunov function)** $V: \Omega \to \mathbb{R}$ (여기서 $\Omega$는 원점 포함 열린 집합)가 존재하면 원점은 안정(stable)하다:

1. $V(0) = 0$이고 $\Omega \setminus \{0\}$에서 $V(x) > 0$ (양정치, positive definite)
2. $V$는 $C^1$이고 $\dot{V}(x) = \nabla V(x) \cdot f(x) \leq 0$ (반정치 음수, negative semidefinite)

추가로 $\dot{V}(x) < 0$ (음정치, negative definite)이면 원점은 점근 안정(asymptotically stable)하다.

**증명:** $V$의 연속성과 양정치성에 의해, 임의의 $\epsilon > 0$에 대해 $\delta > 0$이 존재하여 $\|x\| < \delta$이면 $V(x) < \min_{\|y\| = \epsilon} V(y)$가 성립한다 ( $V$가 $0$에서 0이고 연속이므로 가능).

초기 조건 $x_0$가 $\|x_0\| < \delta$를 만족한다고 하자. $\dot{V}(x(t)) \leq 0$이므로 $V(x(t))$는 시간에 따라 감소하지 않는다(비증가): $V(x(t)) \leq V(x_0) < \min_{\|y\| = \epsilon} V(y)$.

만약 어떤 $t_1$에서 $\|x(t_1)\| = \epsilon$이면, $V(x(t_1)) \geq \min_{\|y\| = \epsilon} V(y)$가 되어 모순이다. 따라서 모든 $t \geq 0$에 대해 $\|x(t)\| < \epsilon$이 유지되며, 이는 리아푸노프 안정을 의미한다.

추가로 $\dot{V}(x) < 0$이면 $V(x(t))$는 단조 감소하고 $V(x(t)) \to 0$임을 보일 수 있으며, $V$의 양정치성에 의해 $x(t) \to 0$이다. $\square$

**의의:** 리아푸노프 함수는 에너지의 일반화다. 물리계에서 에너지가 감소하면 계가 평형에 도달하는 것처럼, 리아푸노프 함수가 감소하면 계가 고정점으로 수렴한다. 리아푸노프 함수를 찾는 일반적인 방법은 없지만, 물리적 에너지, 2차형식 $V(x) = x^T P x$ ($P$ 양정치), 또는 시행착오로 구성한다.

### 정리 4: 카오스의 정의적 특성 (Defining Properties of Chaos)

**서술 (Devaney의 정의):** 컴팩트 집합 $\Omega$ 위에서 연속 사상 $f: \Omega \to \Omega$가 다음 세 조건을 만족하면 **카오스(chaotic)**라 한다:

1. **초기 조건에 대한 민감 의존성 (sensitive dependence on initial conditions):** $\delta > 0$이 존재하여, 임의의 $x \in \Omega$와 임의의 $\epsilon > 0$에 대해 $|x - y| < \epsilon$이고 $\limsup_{n\to\infty} |f^n(x) - f^n(y)| \geq \delta$인 $y \in \Omega$가 존재한다. 즉, 아무리 가까운 두 점도 시간이 지나면 일정 거리 이상 벌어진다.

2. **위상적 추이성 (topological transitivity):** 임의의 열린 집합 $U, V \subset \Omega$에 대해 $f^n(U) \cap V \neq \emptyset$인 $n > 0$이 존재한다. 즉, 궤도가 공간 전체에 퍼져 있다.

3. **조밀한 주기 궤도 (dense periodic orbits):** $\Omega$의 임의의 점에 임의로 가까운 주기점(periodic point)이 존재한다.

**로렌츠 계 (Lorenz system, 1963):** 기상학자 에드워드 로렌츠가 발견한 3차원 자율계:

$$\begin{aligned}
\dot{x} &= \sigma(y - x) \\
\dot{y} &= x(\rho - z) - y \\
\dot{z} &= xy - \beta z
\end{aligned}$$

$\sigma = 10$, $\beta = 8/3$, $\rho = 28$에서 유명한 **로렌츠 어트랙터(Lorenz attractor)**가 나타난다. 이 계는 결정론적이지만 예측 불가능한 카오스 행동을 보이며, **나비 효과**라는 이름으로 유명해졌다.

**의의:** 카오스는 무작위성(randomness)이 아니라 결정론적 규칙에서 발생하는 복잡성이다. 카오스계는 단기적으로는 예측 가능하지만(기상 예보가 며칠까지는 유효), 장기적 예측은 초기 조건의 미세한 차이로 인해 불가능하다.

## 예제

**예제 1 (로지스틱 방정식의 고정점 안정성):** $\dot{x} = x(1 - x)$의 고정점과 그 안정성을 분석하라.

**풀이:** $f(x) = x(1 - x)$에서 $f(x^*) = 0$ → $x^*(1 - x^*) = 0$ → $x^* = 0$ 또는 $x^* = 1$.

$f'(x) = 1 - 2x$.

- $x^* = 0$: $f'(0) = 1 > 0$ → 불안정(고유값 양수). $x$가 0 근처에서 작으면 $f(x) \approx x$이므로 지수적 증가.
- $x^* = 1$: $f'(1) = -1 < 0$ → 점근 안정(고유값 음수). $x$가 1 근처에 있으면 $f(x) \approx -(x-1)$이므로 지수적으로 1에 접근.

이를 일반화하면 $x^* = 1$은 안정 고정점(환경 수용력)이고 $x^* = 0$은 불안정 고정점(작은 개체군도 성장)이다. 위상 공간의 분석: $x \in (0, 1)$에서는 $f(x) > 0$이므로 $x$가 증가하여 $1$로 수렴하고, $x > 1$에서는 $f(x) < 0$이므로 감소하여 $1$로 수렴한다.

**예제 2 (감쇠 진자의 고정점):** $\ddot{\theta} + b\dot{\theta} + \sin\theta = 0$ ($b > 0$)의 고정점을 찾고 안정성을 분석하라.

**풀이:** $x_1 = \theta$, $x_2 = \dot{\theta}$로 변환:

$$\begin{pmatrix} \dot{x}_1 \\ \dot{x}_2 \end{pmatrix} = \begin{pmatrix} x_2 \\ -\sin x_1 - b x_2 \end{pmatrix}$$

고정점: $x_2 = 0$, $\sin x_1 = 0$ → $x_1 = n\pi$ ($n \in \mathbb{Z}$). ($x_1, x_2) = (0, 0), (\pi, 0), (-\pi, 0), \ldots$

야코비 행렬:

$$Df = \begin{pmatrix} 0 & 1 \\ -\cos x_1 & -b \end{pmatrix}$$

**$(0, 0)$에서:** $Df = \begin{pmatrix} 0 & 1 \\ -1 & -b \end{pmatrix}$.

특성방정식: $\det(Df - \lambda I) = \det\begin{pmatrix} -\lambda & 1 \\ -1 & -b-\lambda \end{pmatrix} = \lambda(b+\lambda) + 1 = \lambda^2 + b\lambda + 1 = 0$.

$\lambda = \frac{-b \pm \sqrt{b^2 - 4}}{2}$. $b > 0$이므로 모든 $b$에 대해 $\text{Re}(\lambda) < 0$. 즉, (0, 0)은 점근 안정 — 진자가 아래쪽에서 멈춘다.

**$(\pi, 0)$에서:** $Df = \begin{pmatrix} 0 & 1 \\ 1 & -b \end{pmatrix}$.

특성방정식: $\lambda^2 + b\lambda - 1 = 0$. $\lambda = \frac{-b \pm \sqrt{b^2 + 4}}{2}$ — 하나의 양수 고유값과 하나의 음수 고유값. 따라서 $(\pi, 0)$은 **안장점(saddle point)** — 불안정하다. 이는 진자가 위쪽(거꾸로 선 상태)에서의 평형이 불안정함을 의미한다.

**예제 3 (로렌츠 계의 기본 특성):** 로렌츠 계에서 $\rho < 1$일 때 원점의 안정성을 분석하라.

**풀이:** $\dot{x} = \sigma(y-x)$, $\dot{y} = x(\rho - z) - y$, $\dot{z} = xy - \beta z$에서 원점 $(0, 0, 0)$에서의 야코비 행렬:

$$Df(0) = \begin{pmatrix} -\sigma & \sigma & 0 \\ \rho & -1 & 0 \\ 0 & 0 & -\beta \end{pmatrix}$$

$\lambda_3 = -\beta$, 나머지 두 고유값은 $2 \times 2$ 블록에서:

$$\det\begin{pmatrix} -\sigma - \lambda & \sigma \\ \rho & -1 - \lambda \end{pmatrix} = (\sigma + \lambda)(1 + \lambda) - \sigma\rho = \lambda^2 + (\sigma + 1)\lambda + \sigma(1 - \rho) = 0$$

$\rho < 1$이면 상수항 $\sigma(1 - \rho) > 0$이고 모든 계수가 양수이므로 모든 고유값이 음의 실수부를 가진다. 따라서 원점은 점근 안정 — 모든 궤도가 원점으로 수렴한다.

$\rho > 1$이면 상수항이 음수가 되어 하나의 양수 고유값이 나타나고, 원점은 불안정해진다. 이때 두 개의 새로운 고정점 $(\pm\sqrt{\beta(\rho-1)}, \pm\sqrt{\beta(\rho-1)}, \rho-1)$이 생기며, 이는 $\rho$가 충분히 커지면 불안정해져 카오스로 이어진다.

**예제 4 (리아푸노프 함수 구성):** $\dot{x} = -x^3$, $\dot{y} = -y$의 원점 안정성을 리아푸노프 함수를 이용해 증명하라.

**풀이:** $V(x, y) = \frac{1}{2}(x^2 + y^2)$를 후보로 한다.

- $V(0, 0) = 0$, $(x, y) \neq (0, 0)$에서 $V > 0$ → 양정치.
- $f(x, y) = (-x^3, -y)$.

$$\dot{V} = \nabla V \cdot f = (x, y) \cdot (-x^3, -y) = -x^4 - y^2 \leq 0$$

$\dot{V}$는 반정치 음수(음정치는 아니다 — $x = 0, y = 0$에서만 0). 따라서 원점은 리아푸노프 안정.

점근 안정을 보이려면 $\dot{V} < 0$이 필요하지만, 여기서는 $x = 0, y \neq 0$에서 $\dot{V} = -y^2 < 0$이고, $x \neq 0, y = 0$에서 $\dot{V} = -x^4 < 0$이다. 라살레 불변 원리(LaSalle's invariance principle)에 의해 $\dot{V} = 0$인 집합 $\{(0, 0)\}$만 불변이므로 원점은 점근 안정이다.

**예제 5 (분기, bifurcation — 새들의 탄생, saddle-node bifurcation):** $\dot{x} = r + x^2$ ($r$ 매개변수)의 분기(bifurcation)를 분석하라.

**풀이:** $f(x) = r + x^2$. 고정점은 $r + x^2 = 0$에서 $x^* = \pm\sqrt{-r}$.

- $r > 0$: 실수 고정점 없음. $f(x) > 0$이므로 모든 $x$가 증가.
- $r = 0$: $x^* = 0$ (중근). $f'(0) = 0$ — 비쌍곡 고정점. $f(x) = x^2 \geq 0$이므로 $x > 0$에서는 증가, $x < 0$에서는 감소(하지만 느리게). 이 지점이 **분기점(bifurcation point)**이다.
- $r < 0$: 두 고정점 $x^* = \pm\sqrt{-r}$. $f'(x) = 2x$에서 $f'(\sqrt{-r}) = 2\sqrt{-r} > 0$ (불안정), $f'(-\sqrt{-r}) = -2\sqrt{-r} < 0$ (안정).

$r$이 양수에서 음수로 감소하면 고정점이 없는 상태에서 갑자기 안정-불안정 고정점 쌍이 나타난다. 이를 **안장-매듭 분기(saddle-node bifurcation)**라 한다. 이는 가장 기본적인 분기 형태로, 레이저 물리, 신경과학, 생태학 등에서 관찰된다.

**예제 6 (호프 분기, Hopf bifurcation):** 2차원계 $\dot{r} = r(\mu - r^2)$, $\dot{\theta} = 1$ (극좌표)의 동역학을 분석하라.

**풀이:** 반지름 $r$의 방정식 $\dot{r} = r(\mu - r^2)$에 주목한다.

- $\mu < 0$: $\dot{r} < 0$ (항상) → $r = 0$이 유일한 고정점이며 안정(안정 나선, stable spiral).
- $\mu = 0$: 분기점. $r = 0$ 근처에서 $\dot{r} = -r^3$ — 느린 감쇠.
- $\mu > 0$: $r = 0$은 불안정해지고($\dot{r} \approx \mu r$), $r^* = \sqrt{\mu}$의 안정 한계 순환(stable limit cycle)이 출현한다.

이는 **초임계 호프 분기(supercritical Hopf bifurcation)**의 전형적 예다. 한계 순환의 반지름은 $\sqrt{\mu}$로, 분기 직후 $\sqrt{\mu}\propto\sqrt{\mu}$로 연속적으로 성장한다(2차 분기). 유체역학의 푸앵카레-레일리의 베나드 대류(Bénard convection), 뉴런의 호지킨-헉슬리 모형에서 진동의 출현을 설명한다.

## 연결

- **[상미분방정식 기초](ode-basics.html)** : 동역학계의 기초는 ODE 이론이다. $\dot{x} = f(x)$의 해와 그 성질이 모든 동역학 분석의 출발점이다. 피카르-린델뢰프 정리는 동역학계 해의 존재를 보장한다.
- **[고유값·고유벡터](eigenvalues.html)** : 선형 안정성 분석은 $Df(x^*)$의 고유값에 의존한다. 안정성의 모든 정보는 고유값의 실수부 부호에 담겨 있으며, 행렬 지수 $e^{At}$는 고유값 분해를 통해 계산된다.
- **[마르코프 체인](markov-chains.html)** : 이산 시간(discrete-time) 동역학계로서의 마르코프 체인은 전이확률행렬 $P$의 고유값에 의해 수렴 속도가 결정된다. 이산 동역학계와 연속 동역학계 사이의 자연스러운 연결이다.
- **[확률미분방정식](sde.html)** : SDE는 노이즈가 추가된 동역학계로 볼 수 있다. 드리프트 $f$는 결정론적 흐름을, 확산 $g$는 확률적 교란을 나타낸다.
- **[푸리에 해석](fourier.html)** : 선형 동역학계의 진동 모드는 푸리에 모드와 밀접하게 연결된다. 특히 편미분방정식에서의 공간적 모드 분해는 푸리에 급수로 이루어진다.
