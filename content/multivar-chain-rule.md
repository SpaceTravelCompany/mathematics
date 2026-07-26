---
title: 다변수 연쇄법칙
slug: multivar-chain-rule
---

## 직관적 설명

**연쇄법칙(chain rule)** 은 "합성함수의 변화율이 각 함수의 변화율의 곱"이라는 원리다. 1변수에서는 $\frac{d}{dx} f(g(x)) = f'(g(x)) g'(x)$로 간단하다. 다변수로 확장하면 "한 변수의 변화가 여러 경로를 통해 출력에 전파"되는 구조가 된다.

예를 들어 $z = f(x, y)$이고 $x = g(t)$, $y = h(t)$라면, $t$의 변화는 $x$를 통해, 그리고 $y$를 통해 $z$에 전달된다. 다변수 연쇄법칙은 이 두 경로의 기여를 합산한다:

$$\frac{dz}{dt} = \frac{\partial f}{\partial x} \frac{dx}{dt} + \frac{\partial f}{\partial y} \frac{dy}{dt}$$

이를 "계산 그래프(computation graph)"로 시각화할 수 있다: $t \to \{x, y\} \to z$. $t$가 변하면 $x$와 $y$가 각각 변하고, 그 변화가 $z$에 더해진다. 그래디언트가 거꾸로 흐르는 역전파(backpropagation)의 수학적 기초가 이 법칙이다.

더 일반적으로, $f: \mathbb{R}^n \to \mathbb{R}^m$과 $g: \mathbb{R}^m \to \mathbb{R}^p$의 합성 $g \circ f$의 도함수는 야코비안 행렬의 곱 $(J_g \circ J_f)$이다.

---
## 정의

**스칼라-경로 연쇄법칙 (chain rule for scalar path):** $f: \mathbb{R}^n \to \mathbb{R}$이 미분가능하고 $\gamma: \mathbb{R} \to \mathbb{R}^n$이 미분가능하면, 합성 $f \circ \gamma: \mathbb{R} \to \mathbb{R}$에 대해:

$$\frac{d}{dt} f(\gamma(t)) = \nabla f(\gamma(t)) \cdot \gamma'(t)$$

성분별로 쓰면 $\gamma(t) = (x_1(t), \ldots, x_n(t))$일 때:

$$\frac{d}{dt} f(x_1(t), \ldots, x_n(t)) = \sum_{i=1}^n \frac{\partial f}{\partial x_i}(\gamma(t)) \cdot \frac{dx_i}{dt}(t)$$

**다변수-다변수 연쇄법칙 (general chain rule):** $f: \mathbb{R}^n \to \mathbb{R}^m$이 $x \in \mathbb{R}^n$에서 미분가능하고 $g: \mathbb{R}^m \to \mathbb{R}^p$가 $f(x) \in \mathbb{R}^m$에서 미분가능하면, 합성 $h = g \circ f: \mathbb{R}^n \to \mathbb{R}^p$의 야코비안은:

$$J_h(x) = J_g(f(x)) \cdot J_f(x)$$

즉, $(p \times n)$ 야코비안 행렬은 $(p \times m)$ 야코비안과 $(m \times n)$ 야코비안의 행렬곱(matrix product)이다.

**성분별 표현:** $h_i = g_i(f_1(x), \ldots, f_m(x))$일 때:

$$\frac{\partial h_i}{\partial x_j} = \sum_{k=1}^m \frac{\partial g_i}{\partial f_k} \cdot \frac{\partial f_k}{\partial x_j}$$

이 식은 $i$번째 출력의 $j$번째 입력에 대한 변화율이 모든 중간 경로($k = 1, \ldots, m$)의 기여를 합산함을 보여준다.

**전미분 형식 (total differential form):** $z = f(x_1, \ldots, x_n)$이고 각 $x_i$가 $t$의 함수일 때:

$$dz = \frac{\partial f}{\partial x_1} dx_1 + \cdots + \frac{\partial f}{\partial x_n} dx_n$$

$dx_i = \frac{dx_i}{dt} dt$를 대입하면 $dz/dt$를 얻는다. 전미분 형식은 변수 간의 의존 관계를 명시적으로 드러낸다.

---
## 주요 정리와 증명

### 정리 1: 스칼라-경로 연쇄법칙 (Scalar-Path Chain Rule)

$f: \mathbb{R}^n \to \mathbb{R}$이 $a \in \mathbb{R}^n$에서 미분가능하고 $\gamma: \mathbb{R} \to \mathbb{R}^n$이 $t_0$에서 미분가능하며 $\gamma(t_0) = a$이면, $h(t) = f(\gamma(t))$는 $t_0$에서 미분가능하고:

$$h'(t_0) = \nabla f(a) \cdot \gamma'(t_0)$$

**증명:** $f$의 $a$에서의 미분가능성:

$$f(a + v) = f(a) + \nabla f(a) \cdot v + \epsilon(v)\|v\|$$

여기서 $\epsilon(v) \to 0$ ($v \to 0$)이다. $v = \gamma(t_0 + \Delta t) - \gamma(t_0)$로 두자.

$$h(t_0 + \Delta t) - h(t_0) = f(\gamma(t_0 + \Delta t)) - f(\gamma(t_0))$$
$$= f(a + v) - f(a)$$
$$= \nabla f(a) \cdot v + \epsilon(v)\|v\|$$

$\gamma$의 미분가능성: $\gamma(t_0 + \Delta t) - \gamma(t_0) = \gamma'(t_0)\Delta t + \eta(\Delta t)\Delta t$, 여기서 $\eta(\Delta t) \to 0$ ($\Delta t \to 0$). 따라서 $v = \gamma'(t_0)\Delta t + \eta(\Delta t)\Delta t$이고:

$$\frac{h(t_0 + \Delta t) - h(t_0)}{\Delta t} = \nabla f(a) \cdot (\gamma'(t_0) + \eta(\Delta t)) + \epsilon(v) \frac{\|v\|}{\Delta t}$$

$\Delta t \to 0$일 때 $\eta(\Delta t) \to 0$이고, $\frac{\|v\|}{\Delta t} \to \|\gamma'(t_0)\|$이며 $\epsilon(v) \to 0$이므로:

$$h'(t_0) = \nabla f(a) \cdot \gamma'(t_0)$$

$\square$

### 정리 2: 일반 연쇄법칙 — 야코비안 곱 (General Chain Rule, Jacobian Product)

$f: \mathbb{R}^n \to \mathbb{R}^m$이 $x$에서 미분가능하고 $g: \mathbb{R}^m \to \mathbb{R}^p$가 $f(x)$에서 미분가능하면, $h = g \circ f$의 야코비안은:

$$J_h(x) = J_g(f(x)) \cdot J_f(x)$$

**증명 (성분별):** $h_i(x) = g_i(f_1(x), \ldots, f_m(x))$를 $x_j$로 편미분한다. $g_i$에 다변수 연쇄법칙(정리 1을 각 성분에 적용)을 적용하면:

$$\frac{\partial h_i}{\partial x_j} = \sum_{k=1}^m \frac{\partial g_i}{\partial f_k}(f(x)) \cdot \frac{\partial f_k}{\partial x_j}(x)$$

좌변은 $(J_h(x))_{ij}$이고, 우변은 $\sum_{k=1}^m (J_g(f(x)))_{ik} \cdot (J_f(x))_{kj}$로, 행렬곱 $J_g \cdot J_f$의 $(i,j)$ 성분과 정확히 일치한다.

$\square$

**의미:** 이 정리는 합성함수의 미분이 "각 단계의 야코비안을 순서대로 곱하는 것"임을 보여준다. 차원을 확인하면: $p \times m$ 행렬과 $m \times n$ 행렬의 곱이 $p \times n$ 행렬이 되며, 이는 $h: \mathbb{R}^n \to \mathbb{R}^p$의 야코비안 차원과 일치한다.

### 정리 3: 음함수 미분 (Implicit Differentiation via Chain Rule)

$F(x, y) = 0$이 $y$를 $x$의 음함수(implicit function)로 정의할 때:

$$\frac{dy}{dx} = -\frac{\partial F / \partial x}{\partial F / \partial y} \quad \text{(단, } \frac{\partial F}{\partial y} \neq 0\text{)}$$

**증명:** $F(x, y(x)) = 0$의 양변을 $x$로 미분한다. 연쇄법칙에 의해:

$$\frac{d}{dx} F(x, y(x)) = \frac{\partial F}{\partial x} + \frac{\partial F}{\partial y} \frac{dy}{dx} = 0$$

$dy/dx$에 대해 풀면 $\frac{dy}{dx} = -\frac{\partial F / \partial x}{\partial F / \partial y}$를 얻는다.

$\square$

**다변수 음함수 정리 (implicit function theorem):** $F: \mathbb{R}^{n+m} \to \mathbb{R}^m$이 $C^1$이고 $F(a, b) = 0$이며 $\frac{\partial F}{\partial y}(a, b)$가 가역($m \times m$ 야코비안 행렬이 가역)이면, $a$ 근방에서 $F(x, y(x)) = 0$을 만족하는 $C^1$ 함수 $y: \mathbb{R}^n \to \mathbb{R}^m$가 존재하고:

$$J_y(x) = -\left(\frac{\partial F}{\partial y}\right)^{-1} \frac{\partial F}{\partial x}$$

### 정리 4: 연쇄법칙의 1계 보존 (Chain Rule Preserves Differentiability Class)

$f$가 $C^k$($k$번 연속 미분가능)이고 $g$가 $C^k$이면 $g \circ f$도 $C^k$이다.

**증명:** $h = g \circ f$의 1계 도함수는 $g'$과 $f'$의 다항식 조합(야코비안 곱)으로 표현된다. $g'$과 $f'$이 $C^{k-1}$이므로 $h'$도 $C^{k-1}$이다. 귀납적으로 $h$는 $C^k$이다.

$\square$

---
## 예제

**예제 1 (극좌표 연쇄법칙):** $f(x, y)$를 극좌표 $(r, \theta)$로 표현할 때, $x = r\cos\theta$, $y = r\sin\theta$에 대해 $f_r$과 $f_\theta$를 $f_x$, $f_y$로 표현하라.

**풀이:** 연쇄법칙에 의해:

$$\frac{\partial f}{\partial r} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial r} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial r} = f_x \cos\theta + f_y \sin\theta$$

$$\frac{\partial f}{\partial \theta} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial \theta} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial \theta} = f_x (-r\sin\theta) + f_y (r\cos\theta) = r(-f_x \sin\theta + f_y \cos\theta)$$

행렬 형태로 쓰면:

$$\begin{pmatrix} f_r \\ f_\theta \end{pmatrix} = \begin{pmatrix} \cos\theta & \sin\theta \\ -r\sin\theta & r\cos\theta \end{pmatrix} \begin{pmatrix} f_x \\ f_y \end{pmatrix}$$

야코비안 행렬 $\frac{\partial(x, y)}{\partial(r, \theta)}$의 전치행렬(transpose)이 등장함에 주목하라. 이는 그래디언트가 공변 벡터(covariant vector)임을 보여준다.

**예제 2 (3단계 합성):** $h(t) = f(g(t))$에서 $f(u, v) = u^2 + v^2$, $g(t) = (\cos t, \sin t)$일 때 $dh/dt$를 구하라.

**풀이:** 연쇄법칙을 직접 적용한다.

$$\frac{dh}{dt} = \frac{\partial f}{\partial u} \frac{du}{dt} + \frac{\partial f}{\partial v} \frac{dv}{dt} = (2u)(-\sin t) + (2v)(\cos t)$$

$u = \cos t$, $v = \sin t$를 대입:

$$\frac{dh}{dt} = 2\cos t (-\sin t) + 2\sin t (\cos t) = -2\cos t \sin t + 2\sin t \cos t = 0$$

검증: $h(t) = \cos^2 t + \sin^2 t = 1$이므로 $h'(t) = 0$이 맞다.

**예제 3 (야코비안 연쇄법칙):** $f(u, v) = (u^2, uv, v^2)$ ($\mathbb{R}^2 \to \mathbb{R}^3$)와 $g(x, y, z) = x + yz$ ($\mathbb{R}^3 \to \mathbb{R}$)에 대해 $h = g \circ f$의 그래디언트를 $h$의 야코비안으로서 구하라.

**풀이:** $h(u, v) = g(f(u, v)) = u^2 + (uv)(v^2) = u^2 + uv^3$.

야코비안 곱으로 검증:

$$J_f(u, v) = \begin{pmatrix} 2u & 0 \\ v & u \\ 0 & 2v \end{pmatrix}, \quad J_g(x, y, z) = \begin{pmatrix} 1 & z & y \end{pmatrix}$$

$f(u, v) = (u^2, uv, v^2)$이므로 $g(f(u,v))$에서 $J_g$의 인수: $x = u^2$, $y = uv$, $z = v^2$.

$$J_h(u, v) = J_g(f(u,v)) \cdot J_f(u, v) = \begin{pmatrix} 1 & v^2 & uv \end{pmatrix} \begin{pmatrix} 2u & 0 \\ v & u \\ 0 & 2v \end{pmatrix}$$
$$= \begin{pmatrix} 2u + v^3 & 0 + uv^2 + 2uv^2 \end{pmatrix} = \begin{pmatrix} 2u + v^3 & 3uv^2 \end{pmatrix}$$

직접 미분: $\frac{\partial h}{\partial u} = 2u + v^3$, $\frac{\partial h}{\partial v} = 3uv^2$ — 일치한다.

**예제 4 (음함수 미분):** $x^2 + y^2 + xy = 10$에서 $dy/dx$를 구하라.

**풀이:** $F(x, y) = x^2 + y^2 + xy - 10 = 0$으로 두자.

$$\frac{\partial F}{\partial x} = 2x + y, \quad \frac{\partial F}{\partial y} = 2y + x$$

$$\frac{dy}{dx} = -\frac{\partial F / \partial x}{\partial F / \partial y} = -\frac{2x + y}{2y + x}$$

**예제 5:** $z = f(x, y)$, $x = s^2 + t^2$, $y = st$일 때 $\partial z/\partial s$와 $\partial z/\partial t$를 $f$의 편도함수로 표현하라.

**풀이:**

$$\frac{\partial z}{\partial s} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial s} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial s} = f_x \cdot 2s + f_y \cdot t$$

$$\frac{\partial z}{\partial t} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial t} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial t} = f_x \cdot 2t + f_y \cdot s$$

**예제 6 (역전파 계산):** $f(x, y) = (x + y) \cdot (x \cdot y)$의 그래디언트를 연쇄법칙으로 계산하라(계산 그래프 사용).

**풀이:** 중간 변수를 도입한다: $a = x + y$, $b = x \cdot y$, $f = a \cdot b$.

$$\frac{\partial f}{\partial a} = b, \quad \frac{\partial f}{\partial b} = a$$

$$\frac{\partial a}{\partial x} = 1, \quad \frac{\partial a}{\partial y} = 1, \quad \frac{\partial b}{\partial x} = y, \quad \frac{\partial b}{\partial y} = x$$

연쇄법칙:

$$\frac{\partial f}{\partial x} = \frac{\partial f}{\partial a} \frac{\partial a}{\partial x} + \frac{\partial f}{\partial b} \frac{\partial b}{\partial x} = b \cdot 1 + a \cdot y = xy + (x + y)y = xy + xy + y^2 = 2xy + y^2$$

$$\frac{\partial f}{\partial y} = \frac{\partial f}{\partial a} \frac{\partial a}{\partial y} + \frac{\partial f}{\partial b} \frac{\partial b}{\partial y} = b \cdot 1 + a \cdot x = xy + (x + y)x = xy + x^2 + xy = x^2 + 2xy$$

직접 전개: $f(x, y) = (x+y)xy = x^2 y + xy^2$의 미분과 동일하다.

**예제 7 (온도 변화율):** 온도 $T(x, y, z) = x^2 + 2y^2 + 3z^2$이고 입자의 위치가 $\gamma(t) = (t, t^2, t^3)$일 때, 입자가 느끼는 온도 변화율 $dT/dt$를 $t = 1$에서 구하라.

**풀이:** 연쇄법칙: $\frac{dT}{dt} = \nabla T(\gamma(t)) \cdot \gamma'(t)$.

$\nabla T = (2x, 4y, 6z)$, $\gamma'(t) = (1, 2t, 3t^2)$.

$t = 1$에서 $\gamma(1) = (1, 1, 1)$, $\nabla T(1, 1, 1) = (2, 4, 6)$, $\gamma'(1) = (1, 2, 3)$.

$$\frac{dT}{dt}(1) = (2, 4, 6) \cdot (1, 2, 3) = 2 + 8 + 18 = 28$$

---
## 연결

- **[미분 법칙·연쇄법칙](differentiation-rules.html)** : 1변수 연쇄법칙이 다변수 확장의 기초다.
- **[야코비안·헤시안](jacobian-hessian.html)** : 야코비안 행렬로 연쇄법칙을 행렬곱으로 표현한다.
- **[편도함수·기울기 벡터](partial-derivatives.html)** : 연쇄법칙의 구성 요소인 편도함수를 정의한다.
- **[행렬 미분](matrix-calculus.html)** : 연쇄법칙을 행렬과 벡터의 미분으로 일반화한다.
