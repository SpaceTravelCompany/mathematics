---
title: 상미분방정식 기초
slug: ode-basics
---

## 직관적 설명

**상미분방정식(ordinary differential equation, ODE)**은 "변화율 = 현재 상태의 함수"라는 아이디어를 수학적으로 표현한다. 세상의 수많은 동역학 — 인구 성장, 행성 공전, 전류의 흐름, 감염병 확산 — 이 미분방정식으로 모델링된다: 시간 $t$에 따른 어떤 양 $x(t)$의 변화율 $dx/dt$가 현재의 $x$와 $t$에 의존한다는 것이다.

1계 ODE의 일반 형태는 $\frac{dx}{dt} = f(x, t)$이다. $f$가 $t$에 명시적으로 의존하지 않으면 $\frac{dx}{dt} = f(x)$ — 이를 **자율(autonomous)** 계라 부른다. 자율계는 시간이 흘러도 방정식 자체가 변하지 않기 때문에 분석이 더 단순하다.

초기값 문제(initial value problem, IVP)는 특정 시점 $t_0$에서의 상태 $x(t_0) = x_0$가 주어졌을 때 미분방정식의 해를 구하는 문제다. 즉,

$$\frac{dx}{dt} = f(x, t), \quad x(t_0) = x_0$$

이것이 미분방정식 이론의 가장 기본적인 문제 설정이다. 모든 해는 이 초기조건에 의해 유일하게 결정되며(조건이 충족될 때), 이는 물리적 인과율(causality)의 수학적 반영이다.

---
## 정의

**상미분방정식(ODE):** 미지의 함수 $x: \mathbb{R} \to \mathbb{R}^n$와 그 도함수들 사이의 관계를 나타내는 방정식. $n$계 ODE의 일반형:

$$F(t, x, x', x'', \ldots, x^{(n)}) = 0$$

여기서 $x^{(k)}$는 $k$계 도함수다. **상미분방정식**이란 용어는 편미분방정식(PDE)과 대비되어, 오직 하나의 독립변수 $t$에 대한 도함수만 포함함을 의미한다.

**1계 ODE (first-order ODE):** 가장 기본적인 형태:

$$\frac{dx}{dt} = f(x, t)$$

$f: \mathbb{R}^n \times \mathbb{R} \to \mathbb{R}^n$이 연속이면 국소적 해가 존재한다.

**자율계 (autonomous system):** $f$가 $t$에 의존하지 않는 경우:

$$\frac{dx}{dt} = f(x)$$

자율계에서는 시간 이동(translation) 불변성이 성립한다: $x(t)$가 해이면 $x(t + c)$도 해이다.

**초기값 문제 (initial value problem, IVP):**

$$\frac{dx}{dt} = f(x, t), \quad x(t_0) = x_0$$

주어진 초기조건을 만족하는 해를 찾는 문제.

**1계 선형 ODE (first-order linear ODE):**

$$x' + p(t)x = q(t)$$

선형성의 핵심: $x$와 $x'$에 대해 일차(linear)이며, $x$의 제곱이나 비선형 함수가 포함되지 않는다. $q(t) = 0$이면 **동차(homogeneous)**, $q(t) \neq 0$이면 **비동차(inhomogeneous)** 라 한다.

**상수계수 선형계 (constant-coefficient linear system):**

$$x' = A x$$

여기서 $A$는 $n \times n$ 상수 행렬이다. 이 계는 완전히 분석 가능하며, 해는 행렬 지수(matrix exponential)로 표현된다.

**해의 존재·유일성 (existence and uniqueness):** 함수 $f$가 충분히 매끄럽다면 (특히 $x$에 대해 립시츠 연속), 초기값 문제는 국소적으로 유일한 해를 가진다.

---
## 주요 정리와 증명

### 정리 1: 피카르-린델뢰프 정리 (Picard–Lindelöf Theorem)

**서술:** $f: \mathbb{R}^n \times \mathbb{R} \to \mathbb{R}^n$이 $x$에 대해 립시츠 연속(Lipschitz continuous)이고 $t$에 대해 연속이라고 하자. 즉, 어떤 $L > 0$이 존재하여 모든 $x, y$와 $t$에 대해

$$\|f(x, t) - f(y, t)\| \leq L\|x - y\|$$

가 성립한다. 그러면 임의의 초기조건 $x(t_0) = x_0$에 대해, 어떤 $\delta > 0$이 존재하여 구간 $[t_0 - \delta, t_0 + \delta]$에서 IVP의 유일한 해 $x(t)$가 존재한다.

**증명 (개요 — 피카르 반복, Picard iteration):**

**1단계: 적분 방정식으로 변환.** IVP를 양변 적분하면:

$$x(t) = x_0 + \int_{t_0}^t f(x(s), s)\,ds$$

미분가능한 해는 이 적분방정식을 만족하고, 그 역도 성립한다.

**2단계: 피카르 반복 정의.** 연산자 $T$를 다음과 같이 정의한다:

$$(T\phi)(t) = x_0 + \int_{t_0}^t f(\phi(s), s)\,ds$$

그리고 반복열(iterative sequence)을 $\phi_0(t) = x_0$ (상수함수), $\phi_{n+1} = T\phi_n$으로 정의한다. 즉,

$$\phi_{n+1}(t) = x_0 + \int_{t_0}^t f(\phi_n(s), s)\,ds$$

**3단계: 축소사상(contraction mapping).** 적절한 노름을 가진 완비 거리공간(complete metric space)에서 $T$가 축소사상임을 보인다. 구체적으로, $\delta$를 충분히 작게 잡아 $L\delta < 1$이 되게 하면, $C([t_0-\delta, t_0+\delta])$ 위에서 $T$가 립시츠 상수 $L\delta < 1$을 가지는 축소사상이 된다.

**4단계: 바나흐 고정점 정리.** 축소사상은 유일한 고정점 $x = Tx$를 가진다. 이 고정점이 적분방정식의 유일해이며, 따라서 원래 IVP의 유일해가 된다.

**5단계: 수렴.** 반복열 $\phi_n$은 이 고정점에 균등 수렴(uniformly converge)한다. $\square$

**의의:** 피카르-린델뢰프 정리는 미분방정식 이론의 출발점이다. 해의 존재를 보장하지 않으면 어떤 분석도 의미가 없다. 또한 피카르 반복은 수치 해법의 이론적 기초를 제공한다.

### 정리 2: 1계 선형 ODE의 해법 — 적분인자법

**서술:** 1계 선형 ODE $x' + p(t)x = q(t)$의 일반해는

$$x(t) = e^{-\int p\,dt} \left( \int e^{\int p\,dt} q(t)\,dt + C \right)$$

이다.

**증명:** **적분인자(integrating factor)** $\mu(t) = e^{\int p(t)\,dt}$를 정의한다. $\mu$의 도함수는

$$\mu'(t) = p(t) e^{\int p\,dt} = p(t)\mu(t)$$

이다. 원래 방정식의 양변에 $\mu$를 곱하면:

$$\mu x' + \mu p x = \mu q$$

좌변은 $\frac{d}{dt}(\mu x)$임을 확인한다:

$$\frac{d}{dt}(\mu x) = \mu' x + \mu x' = \mu p x + \mu x' = \mu(x' + p x)$$

따라서

$$\frac{d}{dt}(\mu x) = \mu q$$

양변을 적분하면:

$$\mu x = \int \mu q\,dt + C$$

$\mu$로 나누어 $x$를 얻는다:

$$x(t) = \frac{1}{\mu(t)} \left( \int \mu(t) q(t)\,dt + C \right) = e^{-\int p\,dt} \left( \int e^{\int p\,dt} q(t)\,dt + C \right)$$

$\square$

**비동차 선형 ODE의 해 구조:** 일반해 = 동차해(homogeneous solution) $x_h = Ce^{-\int p\,dt}$ + 특수해(particular solution) $x_p$. 즉, $x = x_h + x_p$.

### 정리 3: 상수계수 선형계 $x' = Ax$의 해

**서술:** $x' = Ax$, $x(t_0) = x_0$의 유일해는

$$x(t) = e^{A(t-t_0)} x_0$$

이다. 여기서 행렬 지수(matrix exponential)는 $e^{At} = \sum_{n=0}^\infty \frac{(At)^n}{n!}$로 정의된다.

**증명:** 행렬 지수의 정의를 $x(t)$에 대입하여 검증한다. 먼저 $x(t) = e^{A(t-t_0)}x_0$라고 가정하고, 급수 표현을 미분한다:

$$\frac{d}{dt} e^{A(t-t_0)} = \frac{d}{dt} \sum_{n=0}^\infty \frac{A^n (t-t_0)^n}{n!} = \sum_{n=1}^\infty \frac{A^n (t-t_0)^{n-1}}{(n-1)!} = A \sum_{n=0}^\infty \frac{A^n (t-t_0)^n}{n!} = A e^{A(t-t_0)}$$

따라서

$$x'(t) = \frac{d}{dt} \left( e^{A(t-t_0)} x_0 \right) = A e^{A(t-t_0)} x_0 = A x(t)$$

초기조건: $x(t_0) = e^{A \cdot 0} x_0 = I x_0 = x_0$. 따라서 위 식이 해임이 증명되었다. 유일성은 피카르-린델뢰프 정리에 의해 보장된다. $\square$

**고유값 분해를 통한 계산:** $A$가 대각화 가능하여 $A = PDP^{-1}$ ($D$ 대각행렬)이면:

$$e^{At} = P e^{Dt} P^{-1}, \quad e^{Dt} = \text{diag}(e^{\lambda_1 t}, \ldots, e^{\lambda_n t})$$

이는 $e^{At}$가 $A$의 고유값 $\lambda_i$에 의해 결정되는 지수적 시간 진화를 나타냄을 의미한다. $A$가 대각화 불가능한 경우에도 조르당 표준형(Jordan normal form)을 통해 유사한 표현이 가능하다.

### 정리 4: 해의 존재 조건 — 상수계수계의 분류

$n \times n$ 행렬 $A$에 대해 $\dot{x} = Ax$의 해 $x(t) = e^{At}x_0$의 장기적 행동은 $A$의 고유값에 의해 결정된다.

- $\text{Re}(\lambda_i) < 0$ $\forall i$ : 모든 해가 $t \to \infty$에서 $0$에 수렴 (점근 안정, asymptotically stable)
- $\text{Re}(\lambda_i) > 0$인 $\lambda_i$ 존재 : 대부분의 해가 발산 (불안정, unstable)
- $\text{Re}(\lambda_i) = 0$이고 대수적 중복도 = 기하적 중복도 : 중심(center) — 해는 유계
- $\text{Re}(\lambda_i) = 0$이고 대수적 중복도 > 기하적 중복도 : 다항식 항이 나타나 발산 가능

**증명:** $e^{At} = Pe^{Dt}P^{-1}$ (대각화 가능한 경우)이므로 $x(t)$의 $i$번째 성분은 $e^{\lambda_i t}$의 선형결합이다. $\lambda_i = a_i + ib_i$일 때 $|e^{\lambda_i t}| = e^{a_i t}$이므로, $a_i < 0$이면 $t \to \infty$에서 소멸하고 $a_i > 0$이면 발산한다. 대각화 불가능한 경우에는 $t^k e^{\lambda_i t}$ 형태의 항이 추가로 나타나지만, $a_i < 0$이면 지수적 감쇠가 다항식 증가를 압도한다. $\square$

---
## 예제

**예제 1 (가장 단순한 ODE — 지수 성장, exponential growth):** 인구 성장 모델 $\frac{dx}{dt} = rx$, $x(0) = x_0$의 해를 구하라.

**풀이:** $\frac{dx}{dt} = rx$는 변수분리형(separable)이다.

$$\frac{dx}{x} = r\,dt \;\Longrightarrow\; \int \frac{dx}{x} = \int r\,dt \;\Longrightarrow\; \ln|x| = rt + C$$

$$x(t) = \pm e^{rt + C} = Ce^{rt}$$

초기조건 $x(0) = x_0$에서 $C = x_0$. 따라서 $x(t) = x_0 e^{rt}$.

$r > 0$이면 지수적 증가, $r < 0$이면 지수적 감쇠, $r = 0$이면 정지 상태. 이 단순한 모델은 인구 성장, 복리 이자, 방사성 붕괴 등 다양한 현상을 설명한다.

**예제 2 (로지스틱 성장, logistic growth):** $\frac{dx}{dt} = rx(1 - x/K)$의 해를 구하고 장기적 행동을 분석하라.

**풀이:** 변수분리형:

$$\frac{dx}{x(1-x/K)} = r\,dt$$

부분분수 분해(partial fraction decomposition):

$$\frac{1}{x(1-x/K)} = \frac{1}{x} + \frac{1/K}{1-x/K}$$

적분:

$$\int \left(\frac{1}{x} + \frac{1/K}{1-x/K}\right) dx = \int r\,dt$$

$$\ln|x| - \ln|1 - x/K| = rt + C$$

$$\ln\left|\frac{x}{1-x/K}\right| = rt + C$$

$$\frac{x}{1-x/K} = Ce^{rt}$$

$x$에 대해 풀면:

$$x(t) = \frac{K}{1 + (K/x_0 - 1)e^{-rt}}$$

$t \to \infty$에서 $x(t) \to K$ (환경 수용력, carrying capacity). $x_0$가 $K$보다 작으면 S자형(sigmoid) 곡선을 그리며 $K$에 접근하고, $x_0 > K$이면 감소하여 $K$에 수렴한다.

**예제 3 (적분인자법):** $x' + 2tx = t$, $x(0) = 1$의 해를 구하라.

**풀이:** $p(t) = 2t$, $q(t) = t$.

적분인자: $\mu(t) = e^{\int 2t\,dt} = e^{t^2}$.

$$\frac{d}{dt}(e^{t^2} x) = e^{t^2} \cdot t$$

$$e^{t^2} x = \int t e^{t^2}\,dt = \frac{1}{2} e^{t^2} + C$$

$$x(t) = \frac{1}{2} + Ce^{-t^2}$$

초기조건 적용: $x(0) = \frac{1}{2} + C = 1$ → $C = \frac{1}{2}$.

$$x(t) = \frac{1}{2}(1 + e^{-t^2})$$

$t \to \infty$에서 $x(t) \to \frac{1}{2}$.

**예제 4 (선형계의 고유값 풀이):** $x' = Ax$, $A = \begin{pmatrix} -2 & 1 \\ 1 & -2 \end{pmatrix}$, $x(0) = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$의 해를 구하라.

**풀이:** $A$의 고유값:

$$\det(A - \lambda I) = \det\begin{pmatrix} -2-\lambda & 1 \\ 1 & -2-\lambda \end{pmatrix} = (\lambda+2)^2 - 1 = \lambda^2 + 4\lambda + 3 = (\lambda+1)(\lambda+3)$$

$\lambda_1 = -1$, $\lambda_2 = -3$.

고유벡터: $\lambda_1 = -1$: $(A+I)v = \begin{pmatrix} -1 & 1 \\ 1 & -1 \end{pmatrix}v = 0$ → $v_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$.
$\lambda_2 = -3$: $(A+3I)v = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}v = 0$ → $v_2 = \begin{pmatrix} 1 \\ -1 \end{pmatrix}$.

일반해: $x(t) = c_1 e^{-t} v_1 + c_2 e^{-3t} v_2$.

초기조건 적용: $x(0) = c_1 v_1 + c_2 v_2$.

$$c_1 \begin{pmatrix} 1 \\ 1 \end{pmatrix} + c_2 \begin{pmatrix} 1 \\ -1 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$$

$c_1 + c_2 = 1$, $c_1 - c_2 = 0$ → $c_1 = c_2 = \frac{1}{2}$.

$$x(t) = \frac{1}{2} e^{-t} \begin{pmatrix} 1 \\ 1 \end{pmatrix} + \frac{1}{2} e^{-3t} \begin{pmatrix} 1 \\ -1 \end{pmatrix} = \frac{1}{2} \begin{pmatrix} e^{-t} + e^{-3t} \\ e^{-t} - e^{-3t} \end{pmatrix}$$

두 고유값 모두 음수이므로 $t \to \infty$에서 $x(t) \to 0$이며, 느린 모드($\lambda = -1$)가 우세하다.

**예제 5 (감쇠 진동, damped oscillation):** 2계 ODE $x'' + 2\gamma x' + \omega^2 x = 0$ ($\gamma, \omega > 0$)을 1계 연립계로 변환하고 해를 분석하라.

**풀이:** $x_1 = x$, $x_2 = x'$로 치환하면:

$$\begin{pmatrix} x_1 \\ x_2 \end{pmatrix}' = \begin{pmatrix} 0 & 1 \\ -\omega^2 & -2\gamma \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$$

특성방정식: $\det(A - \lambda I) = \lambda^2 + 2\gamma\lambda + \omega^2 = 0$.

근: $\lambda = -\gamma \pm \sqrt{\gamma^2 - \omega^2}$.

- **과감쇠(overdamped, $\gamma > \omega$):** 두 실근 음수 → 지수적 감쇠, 진동 없음
- **임계감쇠(critically damped, $\gamma = \omega$):** 중근 → $x = (A + Bt)e^{-\gamma t}$
- **저감쇠(underdamped, $\gamma < \omega$):** 복소공액근 $\lambda = -\gamma \pm i\sqrt{\omega^2 - \gamma^2}$ → $x = e^{-\gamma t}(A\cos\omega_d t + B\sin\omega_d t)$, 여기서 $\omega_d = \sqrt{\omega^2 - \gamma^2}$

저감쇠 케이스는 주파수 $\omega_d$로 진동하면서 지수적 감쇠하는 해를 나타낸다. 감쇠비(damping ratio) $\zeta = \gamma/\omega$는 진동의 성격을 결정한다.

---
## 연결

- **[지수·로그 함수 미분](exp-log-calculus.html)** : ODE 해의 지수 함수 $e^{rt}$,
  $e^{At}$는 지수·로그 미분의 자연스러운 확장이다.
- **[확률미분방정식](sde.html)** : ODE에 무작위 잡음($dW$)을 추가하면 SDE가 된다.
드리프트 $f$는 ODE의 우변과 동일한 역할을 한다.
- **[미분방정식과 동역학](dynamical-systems.html)** : ODE 해의 장기적 행동(안정성, 고정점, 한계 순환)을 분석하는 것이 동역학계 이론이다.
- **[고유값·고유벡터](eigenvalues.html)** : 선형계 $x' = Ax$의 해는 $A$의 고유값으로 완전히 분석된다. $e^{At}$의 계산은 고유값 분해에 의존한다.
