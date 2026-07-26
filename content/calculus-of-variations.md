---
title: 변분법
slug: calculus-of-variations
---

## 직관적 설명

**변분법(calculus of variations)**은 "함수"를 입력받아 숫자를 내놓는 **범함수(functional)**의 최적화 이론이다. 일반 미적분이 점 $x$에서 함수 $f(x)$의 최솟값을 찾는 반면, 변분법은 함수 $y(x)$ 전체를 선택하여 적분값 $J[y]$를 최소화하는 것을 목표로 한다.

고전적인 문제들:
- **최단 경로 문제:** 두 점을 잇는 가장 짧은 곡선은 무엇인가? (답: 직선)
- **브라키스토크론(brachistochrone) 문제:** 중력만 작용할 때, 두 점 사이를 가장 빠르게 내려가는 곡선은 무엇인가? (답: 사이클로이드)
- **최소 곡면 문제:** 주어진 경계를 지나는 가장 작은 면적의 곡면은 무엇인가? (비누 막의 형태)

변분법의 핵심 아이디어: 후보 함수 $y(x)$에 작은 변형 $\epsilon\eta(x)$을 가하고, 이에 따른 범함수의 변화가 1차(order $\epsilon$)에서 0이 되도록 조건을 세운다. 이로부터 유명한 **오일러-라그랑주 방정식(Euler-Lagrange equation)**이 유도된다. 물리학에서 **최소 작용 원리(principle of least action)**는 변분법의 가장 중요한 응용으로, 모든 기본 물리 법칙(뉴턴 역학, 전자기학, 일반 상대성 이론, 양자장론)을 지배한다.

---
## 정의

**범함수 (functional):** 함수를 입력받아 실수를 출력하는 함수. 변분법의 표준 형태:

$$J[y] = \int_a^b L(x, y(x), y'(x))\,dx$$

여기서 $L$을 **라그랑지안(Lagrangian)**이라 부른다. $y$는 미분가능한 함수이고, 경계 조건 $y(a) = A$, $y(b) = B$가 주어진다.

**변분 (variation):** 함수 $y$의 작은 변화 $\delta y = \epsilon\eta(x)$. 여기서 $\eta(x)$는 경계에서 0인 매끄러운 함수($\eta(a) = \eta(b) = 0$)이고 $\epsilon$은 작은 매개변수이다.

**일차 변분 (first variation):** 범함수 $J$의 일차 변분 $\delta J$는 다음과 같이 정의된다:

$$\delta J = \left. \frac{d}{d\epsilon} J[y + \epsilon\eta] \right|_{\epsilon=0}$$

극값(최소 또는 최대)에서는 $\delta J = 0$이 모든 허용된 $\eta$에 대해 성립한다.

**오일러-라그랑주 방정식 (Euler-Lagrange equation):**

$$\frac{\partial L}{\partial y} - \frac{d}{dx}\frac{\partial L}{\partial y'} = 0$$

이것이 $J[y]$가 극값을 가질 필요조건이다.

**벨트라미 항등식 (Beltrami identity):** $L$이 $x$에 명시적으로 의존하지 않을 때($L = L(y, y')$),

$$L - y'\frac{\partial L}{\partial y'} = C \quad (\text{상수})$$

이는 오일러-라그랑주 방정식의 첫 적분(first integral)이다.

---
## 주요 정리와 증명

### 정리 1: 오일러-라그랑주 방정식의 유도

**서술:** $J[y] = \int_a^b L(x, y, y')\,dx$, 경계 조건 $y(a) = A$, $y(b) = B$가 주어졌을 때, $J$가 $y$에서 극값을 가지면 다음 방정식을 만족한다:

$$\frac{\partial L}{\partial y} - \frac{d}{dx}\frac{\partial L}{\partial y'} = 0$$

**증명:**

**1단계: 변분 설정.** 허용된 변분 함수 $\eta(x)$ ($\eta(a) = \eta(b) = 0$)와 작은 매개변수 $\epsilon$에 대해 $y_\epsilon(x) = y(x) + \epsilon\eta(x)$를 정의한다. $y_0 = y$이다. $J$의 $\epsilon$에 대한 함수를 고려한다:

$$J(\epsilon) = J[y_\epsilon] = \int_a^b L(x, y + \epsilon\eta, y' + \epsilon\eta')\,dx$$

$y$가 극값이므로 $J'(0) = 0$이어야 한다.

**2단계: 미분과 연쇄법칙.** $\epsilon$에 대해 미분하면:

$$\frac{dJ}{d\epsilon} = \int_a^b \left( \frac{\partial L}{\partial y} \eta + \frac{\partial L}{\partial y'} \eta' \right) dx$$

$\epsilon = 0$에서 $J'(0) = 0$이므로:

$$\int_a^b \left( \frac{\partial L}{\partial y} \eta + \frac{\partial L}{\partial y'} \eta' \right) dx = 0$$

**3단계: 부분적분.** 두 번째 항에 부분적분을 적용한다:

$$\int_a^b \frac{\partial L}{\partial y'} \eta'\,dx = \left[ \frac{\partial L}{\partial y'} \eta \right]_a^b - \int_a^b \frac{d}{dx}\left( \frac{\partial L}{\partial y'} \right) \eta\,dx$$

경계 조건 $\eta(a) = \eta(b) = 0$에 의해 경계항(boundary term)은 0이다. 따라서:

$$\int_a^b \left( \frac{\partial L}{\partial y} - \frac{d}{dx}\frac{\partial L}{\partial y'} \right) \eta(x)\,dx = 0$$

**4단계: 기본 보조정리 (fundamental lemma of calculus of variations).** 모든 매끄러운 $\eta$ (경계에서 0)에 대해 $\int_a^b f(x)\eta(x)\,dx = 0$이면 $f(x) = 0$ (연속성 가정 하). 이는 $\eta$로 임의의 국소 변형을 만들 수 있기 때문이다. 만약 어떤 $x_0$에서 $f(x_0) \neq 0$이면, 그 근처에서 부호가 일정한 $\eta$를 선택하여 적분을 0이 아니게 만들 수 있다.

**5단계:** 따라서 피적분 함수가 항등적으로 0이어야 한다:

$$\frac{\partial L}{\partial y} - \frac{d}{dx}\frac{\partial L}{\partial y'} = 0$$

$\square$

**의의:** 이 방정식은 변분법의 핵심이다. 수많은 물리 법칙이 이 하나의 방정식에서 유도된다. 라그랑지안 $L$만 주어지면 해당 시스템의 운동 방정식을 얻을 수 있다.

### 정리 2: 최단 경로 문제 — 두 점 사이의 가장 짧은 곡선

**서술:** 평면 위의 두 점 $(a, A)$와 $(b, B)$를 잇는 곡선 중 길이가 최소인 것은 직선이다.

**증명:** 곡선 $y(x)$의 길이는:

$$J[y] = \int_a^b \sqrt{1 + (y')^2}\,dx$$

라그랑지안 $L = \sqrt{1 + (y')^2}$는 $x$와 $y$에 명시적으로 의존하지 않으므로, 오일러-라그랑주 방정식을 직접 적용한다.

$\frac{\partial L}{\partial y} = 0$ (명시적 $y$ 의존 없음). $\frac{\partial L}{\partial y'} = \frac{y'}{\sqrt{1 + (y')^2}}$.

오일러-라그랑주 방정식에 대입하면:

$$\frac{d}{dx}\left( \frac{y'}{\sqrt{1 + (y')^2}} \right) = 0$$

따라서 $\frac{y'}{\sqrt{1 + (y')^2}} = C$ (상수). $y'$에 대해 풀면 $y' = \frac{C}{\sqrt{1 - C^2}} = m$ (상수). 따라서 $y(x) = mx + c$. 경계 조건을 만족하는 유일한 해는 두 점을 잇는 직선이다. $\square$

### 정리 3: 벨트라미 항등식 (Beltrami Identity)

**서술:** $L$이 $x$에 명시적으로 의존하지 않을 때 ($L = L(y, y')$), 오일러-라그랑주 방정식의 결과로:

$$L - y'\frac{\partial L}{\partial y'} = C \quad (\text{상수})$$

**증명:** $\frac{d}{dx}\left( L - y'\frac{\partial L}{\partial y'} \right)$를 계산한다:

$$\frac{dL}{dx} = \frac{\partial L}{\partial y} y' + \frac{\partial L}{\partial y'} y''$$

( $\frac{\partial L}{\partial x} = 0$ 가정).

$$\frac{d}{dx}\left( y'\frac{\partial L}{\partial y'} \right) = y''\frac{\partial L}{\partial y'} + y'\frac{d}{dx}\left( \frac{\partial L}{\partial y'} \right)$$

따라서:

$$\frac{d}{dx}\left( L - y'\frac{\partial L}{\partial y'} \right) = \left( \frac{\partial L}{\partial y} y' + \frac{\partial L}{\partial y'} y'' \right) - \left( y''\frac{\partial L}{\partial y'} + y'\frac{d}{dx}\frac{\partial L}{\partial y'} \right)$$

$$= y'\left( \frac{\partial L}{\partial y} - \frac{d}{dx}\frac{\partial L}{\partial y'} \right) = y' \cdot 0 = 0$$

(마지막 등호는 오일러-라그랑주 방정식에 의함). 따라서 $L - y'\partial L/\partial y'$는 상수이다. $\square$

**의의:** 벨트라미 항등식은 오일러-라그랑주 방정식을 1계 ODE로 낮춰준다. 이는 특히 $L$이 $x$에 무관할 때 매우 유용하다.

### 정리 4: 브라키스토크론 문제의 서술

**문제:** 중력만 작용하는 환경에서 한 점 $P_1$에서 $P_2$($P_2$는 $P_1$보다 낮은 위치)까지 가장 짧은 시간에 도달하는 곡선을 구하라.

**서술:** 에너지 보존 $mgy = \frac{1}{2}mv^2$에서 $v = \sqrt{2gy}$. 소요 시간 범함수:

$$T[y] = \int_{x_1}^{x_2} \frac{\sqrt{1 + (y')^2}}{\sqrt{2gy}}\,dx$$

라그랑지안 $L(y, y') = \frac{\sqrt{1 + (y')^2}}{\sqrt{2gy}}$는 $x$에 무관하므로 벨트라미 항등식을 적용한다:

$$L - y'\frac{\partial L}{\partial y'} = C$$

이를 정리하면 $y(1 + (y')^2) = \text{상수}$가 되고, 이는 사이클로이드(cycloid)의 미분방정식이다. 매개변수 형태:

$$x = \frac{C}{2}(\theta - \sin\theta), \quad y = \frac{C}{2}(1 - \cos\theta)$$

이 곡선이 **브라키스토크론** — 최단 강하 곡선이다. (전체 증명은 길어 생략하나, 위의 범함수에서 벨트라미 항등식과 변수분리로 유도된다.)

---
## 예제

**예제 1 (최단 경로 — 벨트라미 항등식 활용):** $L = \sqrt{1 + (y')^2}$에 벨트라미 항등식을 직접 적용하여 해가 직선임을 보여라.

**풀이:** $L$이 $x$에 무관하므로 벨트라미 항등식이 적용된다.

$$\frac{\partial L}{\partial y'} = \frac{y'}{\sqrt{1 + (y')^2}}$$

벨트라미 항등식 $L - y'\partial L/\partial y' = C$:

$$\sqrt{1 + (y')^2} - y' \cdot \frac{y'}{\sqrt{1 + (y')^2}} = C$$

$$\frac{1 + (y')^2 - (y')^2}{\sqrt{1 + (y')^2}} = \frac{1}{\sqrt{1 + (y')^2}} = C$$

따라서 $\sqrt{1 + (y')^2} = 1/C$, 즉 $y' = \sqrt{1/C^2 - 1} = m$ (상수). $y = mx + c$로 직선이다.

**예제 2 (최소 곡면, minimal surface — 벨트라미 항등식):** 두 고리가 만드는 비누 막의 모양은 $L = y\sqrt{1 + (y')^2}$로 주어지는 범함수의 극값을 구해 얻어진다. 해를 구하라.

**풀이:** $L = y\sqrt{1 + (y')^2}$, $L$은 $x$에 무관. $\frac{\partial L}{\partial y'} = y \cdot \frac{y'}{\sqrt{1 + (y')^2}}$.

벨트라미 항등식:

$$y\sqrt{1 + (y')^2} - y' \cdot \frac{y y'}{\sqrt{1 + (y')^2}} = C$$

$$\frac{y(1 + (y')^2) - y(y')^2}{\sqrt{1 + (y')^2}} = \frac{y}{\sqrt{1 + (y')^2}} = C$$

$$y = C\sqrt{1 + (y')^2} \;\Longrightarrow\; y^2 = C^2(1 + (y')^2)$$

$$(y')^2 = \frac{y^2}{C^2} - 1 \;\Longrightarrow\; y' = \pm\sqrt{\frac{y^2}{C^2} - 1}$$

변수분리:

$$\frac{dy}{\sqrt{y^2/C^2 - 1}} = \pm dx$$

적분: $y = C\cosh\left(\frac{x - x_0}{C}\right)$ (카테나리 곡선, catenary). 따라서 회전체 표면은 카테나리 곡선의 회전면인 **카테노이드(catenoid)**가 된다.

**예제 3 (물리: 최소 작용 원리 — 뉴턴 방정식 유도):** $L = \frac{1}{2}m\dot{x}^2 - V(x)$ (운동에너지 - 위치에너지)에서 오일러-라그랑주 방정식이 뉴턴의 제2법칙을 유도함을 보여라.

**풀이:** 범함수 $S[x] = \int L(x, \dot{x})\,dt$가 **작용(action)**이다. 여기서 변수는 $t$ (시간), $x$ (위치), $\dot{x}$ (속도)이다.

오일러-라그랑주 방정식:

$$\frac{\partial L}{\partial x} - \frac{d}{dt}\frac{\partial L}{\partial \dot{x}} = 0$$

$L = \frac{1}{2}m\dot{x}^2 - V(x)$에 대해:

$$\frac{\partial L}{\partial x} = -V'(x), \quad \frac{\partial L}{\partial \dot{x}} = m\dot{x}$$

$$\frac{d}{dt}(m\dot{x}) = m\ddot{x}$$

따라서:

$$-V'(x) - m\ddot{x} = 0 \;\Longrightarrow\; m\ddot{x} = -V'(x) = F(x)$$

즉, 뉴턴의 제2법칙 $F = ma$가 유도된다. $\square$

**의의:** 이 결과는 물리학의 모든 기본 방정식이 최소 작용 원리에서 유도될 수 있음을 보여준다. 라그랑지안만 정해지면 (예: 전자기장의 $L = -\frac{1}{4}F_{\mu\nu}F^{\mu\nu} + J_\mu A^\mu$), 모든 운동 방정식이 오일러-라그랑주 방정식으로 얻어진다.

**예제 4 (측지선, geodesic):** 구면 위의 최단 경로(측지선) 문제를 설명하라.

**풀이:** 구면 좌표 $(r, \theta, \phi)$에서 반지름 $R$인 구면 $r = R$ 위의 곡선 $\theta(\phi)$를 생각하자. 선소(line element)는 $ds = R\sqrt{\theta'^2 + \sin^2\theta}\,d\phi$이고, 따라서:

$$J[\theta] = R \int_{\phi_1}^{\phi_2} \sqrt{\theta'^2 + \sin^2\theta}\,d\phi$$

$L = \sqrt{\theta'^2 + \sin^2\theta}$, $L$은 $\phi$에 무관하므로 벨트라미 항등식 적용:

$$\frac{\sin^2\theta}{\sqrt{\theta'^2 + \sin^2\theta}} = C$$

이를 정리하면 대원(great circle)의 방정식을 얻는다. 구면 위의 최단 경로는 항상 대원의 일부이며, 이는 비행기의 장거리 항로(북극을 경유하는 경로)로 유명하다.

**예제 5 (브라키스토크론의 매개변수 해):** 사이클로이드 $x = \frac{C}{2}(\theta - \sin\theta)$, $y = \frac{C}{2}(1 - \cos\theta)$가 최단 강하 곡선의 해임을 검증하라. ($\theta$는 매개변수)

**풀이:** $dx/d\theta = \frac{C}{2}(1 - \cos\theta)$, $dy/d\theta = \frac{C}{2}\sin\theta$.

$$y' = \frac{dy}{dx} = \frac{dy/d\theta}{dx/d\theta} = \frac{\sin\theta}{1 - \cos\theta} = \cot(\theta/2)$$

$$1 + (y')^2 = 1 + \cot^2(\theta/2) = \csc^2(\theta/2)$$

$$y(1 + (y')^2) = \frac{C}{2}(1 - \cos\theta) \cdot \csc^2(\theta/2) = \frac{C}{2}(2\sin^2(\theta/2)) \cdot \frac{1}{\sin^2(\theta/2)} = C$$

이는 브라키스토크론 문제의 벨트라미 항등식에서 유도된 조건 $y(1 + (y')^2) = \text{상수}$를 정확히 만족한다. 따라서 사이클로이드가 최단 강하 곡선임이 확인된다.

---
## 연결

- **[적분의 의미](integral-meaning.html)** : 변분법의 범함수 $J[y] = \int L\,dx$는 적분의 개념을 기반으로 한다. 미적분학의 기본정리와 부분적분이 오일러-라그랑주 유도의 핵심 도구다.
- **[라그랑주 승수법](lagrange-multipliers.html)** : 라그랑주 승수법(제약 조건 아래 함수 최적화)의 함수 공간 버전이 변분법이다. 제약 변분 문제(예: 등주 문제, isoperimetric problem)는 라그랑주 승수법을 범함수로 확장하여 푼다.
