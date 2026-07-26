---
title: 방향 도함수
slug: directional-derivative
---

## 직관적 설명

**방향 도함수(directional derivative)** 는 편도함수를 "임의의 방향"으로 확장한다. 편도함수는 $x$축이나 $y$축 방향으로만 변화율을 측정하지만, 방향 도함수는 어떤 방향으로든 변화율을 구할 수 있다.

등산에 비유하면: 편도함수는 정확히 동쪽($x$축)이나 북쪽($y$축)으로 걸을 때의 경사지만, 방향 도함수는 북동쪽, 남서쪽 등 원하는 방향으로 걸을 때의 경사까지 알려준다. 미분가능한 함수의 경우 이 값은 매우 간단하다: $D_u f = \nabla f \cdot u$, 즉 그래디언트와 방향벡터의 내적(dot product)이다.

이 공식은 방향 도함수가 "그래디언트의 방향 성분"임을 의미한다. $\nabla f$와 같은 방향이면 내적이 최대, 반대 방향이면 최소, 수직이면 0이다.

## 정의

**방향 도함수 (directional derivative):** 함수 $f: \mathbb{R}^n \to \mathbb{R}$의 점 $a \in \mathbb{R}^n$에서 단위벡터 $u$($\|u\| = 1$) 방향의 방향 도함수는:

$$D_u f(a) = \lim_{t \to 0} \frac{f(a + tu) - f(a)}{t}$$

이 극한이 존재할 때 $f$는 $a$에서 $u$ 방향으로 방향 미분가능(directionally differentiable)하다고 한다.

**그래디언트와의 관계:** $f$가 $a$에서 미분가능하면:

$$D_u f(a) = \nabla f(a) \cdot u$$

이는 연쇄법칙을 통해 증명된다(아래 정리 1).

**비단위 벡터로의 확장:** 단위벡터가 아닌 임의의 벡터 $v \neq 0$에 대해서도 방향 도함수를 정의할 수 있다:

$$D_v f(a) = \lim_{t \to 0} \frac{f(a + tv) - f(a)}{t}$$

이 경우 $D_v f(a) = \nabla f(a) \cdot v$이며, 단위벡터 방향으로 $D_v f(a) = \|v\| D_{v/\|v\|} f(a)$ 관계가 성립한다.

**양측과 편측 방향 도함수:** 방향 도함수는 $t \to 0$의 양극한(both sides)을 취한다. $t \to 0^+$만 취하면 편측 방향 도함수(one-sided directional derivative)가 된다. $D_{-u} f(a) = -D_u f(a)$가 성립한다(미분가능할 때).

**좌표축 방향:** $u = e_i$($i$번째 표준기저벡터)이면 $D_{e_i} f(a) = \frac{\partial f}{\partial x_i}(a)$로 편도함수와 일치한다.

## 주요 정리와 증명

### 정리 1: $D_u f = \nabla f \cdot u$ (Directional Derivative via Gradient)

$f: \mathbb{R}^n \to \mathbb{R}$이 $a$에서 미분가능하면, 모든 단위벡터 $u$에 대해 $u$ 방향의 방향 도함수가 존재하고:

$$D_u f(a) = \nabla f(a) \cdot u$$

**증명 (연쇄법칙):** $g(t) = f(a + tu)$로 정의하자. $g: \mathbb{R} \to \mathbb{R}$은 $t = 0$에서 미분가능한 합성함수다. 연쇄법칙(chain rule)에 의해:

$$g'(0) = \nabla f(a) \cdot \frac{d}{dt}(a + tu)\big|_{t=0} = \nabla f(a) \cdot u$$

그런데 $g'(0)$은 방향 도함수의 정의와 정확히 일치한다:

$$g'(0) = \lim_{t \to 0} \frac{g(t) - g(0)}{t} = \lim_{t \to 0} \frac{f(a + tu) - f(a)}{t} = D_u f(a)$$

따라서 $D_u f(a) = \nabla f(a) \cdot u$가 성립한다.

$\square$

**미분가능성이 필요한 이유:** $f$가 $a$에서 미분가능하지 않으면 $\nabla f(a)$가 존재해도 $D_u f(a) = \nabla f(a) \cdot u$가 성립하지 않을 수 있다(반례: 아래 정리 3).

### 정리 2: 최대/최소 방향 도함수 (Extremal Directional Derivatives)

$f: \mathbb{R}^n \to \mathbb{R}$이 $a$에서 미분가능하고 $\nabla f(a) \neq 0$이라 하자. 단위벡터 $u$ 중에서 $D_u f(a)$를 최대화하는 $u$는 $\nabla f(a)$ 방향이며, 그 최대값은 $\|\nabla f(a)\|$다. 최소화하는 $u$는 $-\nabla f(a)$ 방향이며, 최소값은 $-\|\nabla f(a)\|$다.

**증명:** $D_u f(a) = \nabla f(a) \cdot u$이고 $u$가 단위벡터이므로, 코시-슈바르츠 부등식(Cauchy-Schwarz inequality)에 의해:

$$|\nabla f(a) \cdot u| \leq \|\nabla f(a)\| \cdot \|u\| = \|\nabla f(a)\|$$

따라서:

$$-\|\nabla f(a)\| \leq D_u f(a) \leq \|\nabla f(a)\|$$

- 최댓값 $\|\nabla f(a)\|$: $u = \nabla f(a) / \|\nabla f(a)\|$일 때
- 최솟값 $-\|\nabla f(a)\|$: $u = -\nabla f(a) / \|\nabla f(a)\|$일 때

$\square$

**따름정리:** $\nabla f(a) \neq 0$이면:
- $\nabla f(a)$ 방향: 함수가 가장 빠르게 증가
- $-\nabla f(a)$ 방향: 함수가 가장 빠르게 감소
- $\nabla f(a)$에 수직인 방향($u \perp \nabla f(a)$): 함수가 변하지 않음($D_u f = 0$). 이는 등고선의 접선 방향과 일치한다.

### 정리 3: 방향 도함수 존재 ≠ 미분가능 (Directional Derivatives Exist ≠ Differentiable)

모든 방향의 방향 도함수가 존재한다고 해서 함수가 미분가능한 것은 아니다.

**반례:**

$$f(x, y) = \begin{cases} \frac{x^2 y}{x^4 + y^2}, & (x, y) \neq (0, 0) \\ 0, & (x, y) = (0, 0) \end{cases}$$

**증명:** 임의의 단위벡터 $u = (u_1, u_2)$에 대해:

$$D_u f(0, 0) = \lim_{t \to 0} \frac{f(t u_1, t u_2) - f(0, 0)}{t} = \lim_{t \to 0} \frac{t^3 u_1^2 u_2 / (t^4 u_1^4 + t^2 u_2^2)}{t} = \lim_{t \to 0} \frac{t u_1^2 u_2}{t^2 u_1^4 + u_2^2}$$

$u_2 = 0$이면 $0$이고, $u_2 \neq 0$이면 $\lim_{t \to 0} \frac{t u_1^2 u_2}{u_2^2} = 0$이다. 따라서 모든 방향의 방향 도함수가 존재하고 0이다.

그러나 $f$는 $(0, 0)$에서 연속이 아니다. $y = x^2$을 따라 접근하면:

$$\lim_{x \to 0} f(x, x^2) = \lim_{x \to 0} \frac{x^2 \cdot x^2}{x^4 + (x^2)^2} = \lim_{x \to 0} \frac{x^4}{2x^4} = \frac{1}{2} \neq 0$$

따라서 $f$는 $(0, 0)$에서 불연속이고, 미분가능할 수 없다. 이 예는 모든 방향 도함수가 존재해도 함수가 연속이 아닐 수 있음을 보여준다(편도함수만으로는 더 약한 조건).

$\square$

### 정리 4: 방향 도함수의 선형성 (Linearity of Directional Derivatives)

$f$와 $g$가 $a$에서 미분가능하면, 임의의 스칼라 $\alpha, \beta \in \mathbb{R}$와 모든 단위벡터 $u$에 대해:

$$D_u(\alpha f + \beta g)(a) = \alpha D_u f(a) + \beta D_u g(a)$$

**증명:** $D_u(\alpha f + \beta g)(a) = \nabla(\alpha f + \beta g)(a) \cdot u = (\alpha \nabla f(a) + \beta \nabla g(a)) \cdot u = \alpha D_u f(a) + \beta D_u g(a)$

$\square$

### 정리 5: 방향 도함수와 미분가능성의 관계 (Directional Derivatives and Differentiability)

모든 방향의 방향 도함수가 존재하고, 방향에 대해 선형($D_{u+v} f = D_u f + D_v f$)이며 $u \mapsto D_u f(a)$가 연속이면, $f$는 $a$에서 미분가능하다.

이는 위 정리 3의 반례에서 방향 도함수는 존재하지만 방향에 대한 선형성이 깨져 있음을 관찰할 수 있다(이 함수의 경우 방향 도함수가 모든 방향에서 0이지만 $f$는 연속조차 아니다).

**증명 개요:** $F(h) = f(a+h) - f(a) - D_h f(a)$를 정의한다. $D_h f(a)$가 $h$에 대해 선형이므로 $L(h) = D_h f(a)$는 선형함수다. 방향 도함수의 존재성과 연속성 조건 하에서 $\lim_{h \to 0} \frac{|F(h)|}{\|h\|} = 0$을 보일 수 있으며, 이는 $L$이 $f$의 $a$에서의 미분(derivative)임을 의미한다.

$\square$

### 정리 6: 방향 도함수와 접선 공간 (Directional Derivative and Tangent Space)

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^1$이고 $\nabla f(a) \neq 0$일 때, 집합 $\{v \in \mathbb{R}^n \mid D_v f(a) = 0\}$은 $a$에서 등위면 $f(x) = f(a)$의 접선 공간(tangent space)을 이룬다.

**증명:** $D_v f(a) = \nabla f(a) \cdot v$이다. $D_v f(a) = 0$인 $v$의 집합은 $\nabla f(a)$에 직교하는 벡터들의 $(n-1)$차원 부분공간이다. 정리 1에 의해 이는 등위면의 접선 공간과 일치한다. 즉, $\nabla f(a) \neq 0$일 때 등위면의 접선 공간은 $\nabla f(a)$의 직교 여공간(orthogonal complement)이다.

$\square$

**의미:** 이 정리는 방향 도함수가 0인 방향이 등고선의 방향임을 공식화한다. 국소적으로 함수가 변하지 않는 방향들의 집합이 바로 등위면의 접선 공간이다.

## 예제

**예제 1:** $f(x, y) = x^2 + xy + y^2$의 점 $(1, 1)$에서 방향 $u = (\cos\theta, \sin\theta)$의 방향 도함수를 $\theta$의 함수로 표현하고, 최대 증가 방향과 값을 구하라.

**풀이:** $\nabla f = (2x + y, x + 2y)$, $\nabla f(1, 1) = (3, 3)$.

$$D_u f(1, 1) = (3, 3) \cdot (\cos\theta, \sin\theta) = 3(\cos\theta + \sin\theta)$$

최댓값: $\cos\theta + \sin\theta$의 최댓값은 $\sqrt{2}$($\theta = \pi/4$일 때)이므로, $D_u f$의 최댓값은 $3\sqrt{2}$이다. 방향은 $\theta = \pi/4$, 즉 $(1, 1)/\sqrt{2}$ 방향. 최솟값은 $-3\sqrt{2}$($\theta = 5\pi/4$).

$\nabla f(1, 1) = (3, 3)$ 방향이 $(1, 1)/\sqrt{2}$임을 확인할 수 있다.

**예제 2:** $f(x, y, z) = xyz$의 점 $(1, 2, 1)$에서 방향 $v = (1, -1, 1)$의 방향 도함수를 구하라.

**풀이:** $\nabla f = (yz, xz, xy)$, $\nabla f(1, 2, 1) = (2, 1, 2)$.

$v$가 단위벡터가 아니므로 먼저 단위벡터로 바꾼다: $\|v\| = \sqrt{1 + 1 + 1} = \sqrt{3}$, $u = v/\sqrt{3} = (1/\sqrt{3}, -1/\sqrt{3}, 1/\sqrt{3})$.

$$D_v f(1, 2, 1) = \nabla f \cdot v = (2, 1, 2) \cdot (1, -1, 1) = 2 - 1 + 2 = 3$$

단위벡터 방향: $D_u f(1, 2, 1) = \nabla f \cdot u = 3/\sqrt{3} = \sqrt{3}$.

**예제 3:** $f(x, y) = \sin x \cos y$의 점 $(\pi/4, \pi/4)$에서 $\theta$ 방향의 방향 도함수가 0이 되는 $\theta$를 구하라.

**풀이:** $\nabla f = (\cos x \cos y, -\sin x \sin y)$, $\nabla f(\pi/4, \pi/4) = (1/2, -1/2)$.

$$D_u f = \left(\frac{1}{2}, -\frac{1}{2}\right) \cdot (\cos\theta, \sin\theta) = \frac{1}{2}(\cos\theta - \sin\theta) = 0$$

$\cos\theta = \sin\theta$이므로 $\theta = \pi/4 + n\pi$이다. $\theta = \pi/4$ 방향은 $f$의 등고선의 접선 방향이다.

**예제 4:** $f(x, y) = \sqrt{x^2 + y^2}$의 $(0, 0)$에서 방향 도함수를 조사하라.

**풀이:** $D_u f(0, 0) = \lim_{t \to 0} \frac{\sqrt{(t u_1)^2 + (t u_2)^2}}{t} = \lim_{t \to 0} \frac{|t|}{t} \sqrt{u_1^2 + u_2^2} = \lim_{t \to 0} \frac{|t|}{t}$

$\lim_{t \to 0} \frac{|t|}{t}$는 존재하지 않으므로(좌극한 $-1$, 우극한 $1$), $f$는 $(0, 0)$에서 어떤 방향으로도 방향 도함수를 가지지 않는다. $f(x, y) = \sqrt{x^2 + y^2}$의 그래프는 원뿔(cone)이며, 꼭짓점에서 날카롭기 때문이다.

**예제 5:** $f(x, y) = x^2 e^y$의 점 $(2, 0)$에서 방향 $v = (3, 4)$의 방향 도함수를 구하고, $f$가 가장 빠르게 증가하는 방향과 그 값을 구하라.

**풀이:** $\nabla f = (2x e^y, x^2 e^y)$, $\nabla f(2, 0) = (4, 4)$.

방향 $v$의 방향 도함수: $D_v f = \nabla f \cdot v = (4, 4) \cdot (3, 4) = 12 + 16 = 28$.

최대 증가 방향: $u = \frac{\nabla f}{\|\nabla f\|} = \frac{(4, 4)}{\sqrt{32}} = \left(\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}\right)$.

최대 증가율: $\|\nabla f(2, 0)\| = \sqrt{32} = 4\sqrt{2}$.

**예제 6 (온도장):** 어떤 공간의 온도 분포가 $T(x, y, z) = 100 - x^2 - 2y^2 - 3z^2$일 때, 점 $(2, 1, 1)$에서 온도가 가장 빨리 감소하는 방향과 그 변화율을 구하라. 또한 $(1, 1, 0)$ 방향의 온도 변화율을 구하라.

**풀이:** $\nabla T = (-2x, -4y, -6z)$, $\nabla T(2, 1, 1) = (-4, -4, -6)$.

온도가 가장 빨리 감소하는 방향은 $-\nabla T = (4, 4, 6)$의 방향. 즉, 열이 가장 빨리 확산되는 방향이다(푸리에 법칙, Fourier's law).

변화율: $\|\nabla T(2, 1, 1)\| = \sqrt{16 + 16 + 36} = \sqrt{68} = 2\sqrt{17} \approx 8.25$.

$(1, 1, 0)$ 방향의 단위벡터: $u = (1/\sqrt{2}, 1/\sqrt{2}, 0)$.

$$D_u T = \nabla T \cdot u = (-4, -4, -6) \cdot (1/\sqrt{2}, 1/\sqrt{2}, 0) = -\frac{8}{\sqrt{2}} = -4\sqrt{2} \approx -5.66$$

**예제 7 (방향 도함수의 물리적 의미):** $T(x, y) = 50 - x^2 - 2y^2$가 평면의 온도 분포라 할 때, 개미가 점 $(3, 2)$에서 $(4, 1)$ 방향으로 움직일 때의 온도 변화율을 구하고, 가장 빠르게 더워지는 방향을 구하라.

**풀이:** $\nabla T = (-2x, -4y)$, $\nabla T(3, 2) = (-6, -8)$.

이동 방향 $v = (4, 1) - (3, 2) = (1, -1)$. $\|v\| = \sqrt{2}$.

$D_v T(3, 2) = \nabla T \cdot v = (-6, -8) \cdot (1, -1) = -6 + 8 = 2$.

개미는 이 방향으로 움직일 때 온도가 2씩 증가한다(단위 거리당 변화는 $D_u T = 2/\sqrt{2} = \sqrt{2}$).

가장 빠르게 더워지는 방향(온도 증가 최대): $\nabla T(3, 2) = (-6, -8)$의 방향, 즉 $u = (-3/5, -4/5)$. 이 방향의 온도 변화율은 $\|\nabla T\| = 10$.

**예제 8 (등고선과의 관계):** $f(x, y) = \ln(x^2 + y^2 + 1)$의 점 $(1, 1)$에서 방향 도함수가 최대가 되는 방향과 등고선의 접선 방향을 구하라.

**풀이:** $\nabla f = \left(\frac{2x}{x^2+y^2+1}, \frac{2y}{x^2+y^2+1}\right)$, $\nabla f(1, 1) = (2/3, 2/3)$.

최대 증가 방향: $u = \left(\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}\right)$, 최대 증가율 $= \frac{2\sqrt{2}}{3}$.

등고선 접선 방향: $\nabla f$에 수직인 $(-1, 1)$ 방향. 이 방향의 방향 도함수는 $0$이다.

**예제 9 (최대 방향 도함수의 기하):** $f(x, y) = x^2 - y^2$의 점 $(1, 0)$에서 방향 도함수의 최댓값과 그 방향, 그리고 도함수가 0이 되는 방향을 구하라.

**풀이:** $\nabla f = (2x, -2y)$, $\nabla f(1, 0) = (2, 0)$.

최댓값 $2$, 방향 $u = (1, 0)$ ($x$축 방향, 함수 증가 방향).

최솟값 $-2$, 방향 $u = (-1, 0)$ ($-x$축 방향, 함수 감소 방향).

도함수가 0이 되는 방향: $\nabla f \cdot u = 2u_1 = 0$, 즉 $u_1 = 0$인 방향 $u = (0, \pm 1)$($y$축 방향). 이는 $f$의 등고선 $x^2 - y^2 = c$가 $(1, 0)$에서 $y$축 방향으로 향함을 의미한다.

## 연결

- **[내적·노름·코사인 유사도](inner-product-norm.html)** : $D_u f = \nabla f \cdot u$는 내적의 기하학적 의미(투영)로 이해할 수 있다.
- **[편도함수·기울기 벡터](partial-derivatives.html)** : 방향 도함수의 특수한 경우가 편도함수($u = e_i$)다.
- **[등고선과 그래디언트](gradient-geometry.html)** : $D_u f = 0$인 $u$가 등고선의 접선 방향이다.
- **[다변수 연쇄법칙](multivar-chain-rule.html)** : $D_u f = \nabla f \cdot u$의 증명은 연쇄법칙을 사용한다.
