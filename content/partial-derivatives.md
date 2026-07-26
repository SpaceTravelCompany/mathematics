---
title: 편도함수·기울기 벡터
slug: partial-derivatives
---

## 직관적 설명

**편도함수(partial derivative)** 는 다변수 함수에서 "한 변수만 바꾸고 나머지는 고정"한 채로 구한 변화율이다. $f(x, y)$가 지형의 높이라면, $\frac{\partial f}{\partial x}$는 동쪽 방향의 경사고 $\frac{\partial f}{\partial y}$는 북쪽 방향의 경사다. 각 변수에 대한 편도함수를 모아 벡터로 만든 것이 **기울기 벡터(gradient vector)** $\nabla f$다.

기울기 벡터 $\nabla f$는 모든 편도함수를 한데 묶어 "가장 가파른 상승 방향"을 가리킨다. 그 크기 $\|\nabla f\|$는 그 방향의 상승률이다. 이 사실 하나로 그래디언트는 최적화, 물리학, 기하학 전반에서 핵심적인 도구가 된다.

1변수 함수의 도함수 $f'(a)$가 "접선의 기울기"였다면, 다변수에서는 각 축 방향의 기울기를 따로따로 계산해야 한다. 편도함수는 이렇게 "한 방향씩" 미분하는 자연스러운 확장이다.

---
## 정의

**편도함수 (partial derivative):** 함수 $f: \mathbb{R}^n \to \mathbb{R}$가 주어질 때, $x = a \in \mathbb{R}^n$에서의 $x_i$에 대한 편도함수는 다음 극한이 존재할 때 정의된다:

$$\frac{\partial f}{\partial x_i}(a) = \lim_{h \to 0} \frac{f(a + h e_i) - f(a)}{h}$$

여기서 $e_i$는 $i$번째 표준기저벡터(standard basis vector)로, $i$번째 성분만 1이고 나머지는 0이다. 즉, $x_i$ 방향으로만 움직이며 변화율을 측정한다.

**표기법:** $f_{x_i}(a)$, $\partial_{x_i} f(a)$ 등으로도 쓴다. 2변수 함수 $f(x, y)$의 경우 $\frac{\partial f}{\partial x}$, $\frac{\partial f}{\partial y}$로 표기한다.

**기울기 벡터 (gradient vector):** $f$가 $a$에서 모든 편도함수를 가질 때, 이들을 모아 벡터로 만든다:

$$\nabla f(a) = \left( \frac{\partial f}{\partial x_1}(a), \frac{\partial f}{\partial x_2}(a), \ldots, \frac{\partial f}{\partial x_n}(a) \right)^T$$

$\nabla$는 "nabla"(나블라)라 읽는다.

**미분가능성 (differentiability):** 1변수와 달리, 다변수 함수에서 모든 편도함수가 존재한다고 해서 함수가 "매끄럽게" 행동한다고 보장할 수 없다. 진정한 미분가능성은 함수가 국소적으로 선형함수로 근사될 수 있음을 의미한다:

$$f(x + h) = f(x) + \nabla f(x)^T h + o(\|h\|) \quad \text{as } h \to 0$$

여기서 $o(\|h\|)$는 $\|h\|$보다 더 빨리 0으로 수렴하는 나머지항이다. 즉, $\lim_{h \to 0} \frac{|f(x+h) - f(x) - \nabla f(x)^T h|}{\|h\|} = 0$이 성립하는 $x$에서 $f$는 미분가능(differentiable)하다.

**전미분 (total differential):** 함수 $y = f(x_1, \ldots, x_n)$의 전미분 $dy$는 각 입력의 미소 변화 $dx_i$에 따른 출력의 변화를 합산한다:

$$df = \frac{\partial f}{\partial x_1} dx_1 + \frac{\partial f}{\partial x_2} dx_2 + \cdots + \frac{\partial f}{\partial x_n} dx_n$$

전미분은 오차 전파(error propagation), 열역학, 미분형식(differential form)의 기초가 된다.

**$C^1$ 함수 (continuously differentiable):** 모든 1계 편도함수가 존재하고 연속인 함수를 $C^1$ 함수라 한다. $C^1$이면 미분가능하다(아래 정리 2).

---
## 주요 정리와 증명

### 정리 1: 편도함수 존재 ≠ 미분가능 (Partial Derivatives Exist ≠ Differentiable)

편도함수가 모두 존재한다고 해서 함수가 미분가능한 것은 아니다. 다음 함수가 그 반례다:

$$f(x, y) = \begin{cases} \frac{xy}{x^2 + y^2}, & (x, y) \neq (0, 0) \\ 0, & (x, y) = (0, 0) \end{cases}$$

**증명:** 먼저 $(0,0)$에서 편도함수를 계산한다.

$$\frac{\partial f}{\partial x}(0,0) = \lim_{h \to 0} \frac{f(h, 0) - f(0,0)}{h} = \lim_{h \to 0} \frac{\frac{h \cdot 0}{h^2 + 0^2} - 0}{h} = \lim_{h \to 0} \frac{0}{h} = 0$$

같은 방법으로 $\frac{\partial f}{\partial y}(0,0) = 0$이다. 따라서 편도함수는 $(0,0)$에 존재한다.

그러나 $f$는 $(0,0)$에서 불연속이다. $y = mx$를 따라 $(0,0)$에 접근하면:

$$\lim_{x \to 0} f(x, mx) = \lim_{x \to 0} \frac{x(mx)}{x^2 + (mx)^2} = \lim_{x \to 0} \frac{mx^2}{x^2(1+m^2)} = \frac{m}{1+m^2}$$

이 값은 $m$에 따라 달라진다. 예를 들어 $m = 0$이면 0, $m = 1$이면 $1/2$다. 따라서 극한이 존재하지 않고 $f$는 $(0,0)$에서 불연속이다. 불연속 함수는 미분가능할 수 없으므로 (미분가능 ⇒ 연속), 편도함수는 존재하지만 $f$는 미분가능하지 않다.

$\square$

### 정리 2: $C^1$이면 미분가능 ($C^1$ Implies Differentiability)

$f: \mathbb{R}^n \to \mathbb{R}$이 $a$의 근방에서 모든 1계 편도함수를 가지며, 이 편도함수들이 $a$에서 연속이면, $f$는 $a$에서 미분가능하다.

**증명 (2변수 경우):** $f(x, y)$가 $(a, b)$ 근방에서 $C^1$이라 하자. 차분 $f(a+h, b+k) - f(a, b)$를 분석한다.

$$f(a+h, b+k) - f(a, b) = [f(a+h, b+k) - f(a, b+k)] + [f(a, b+k) - f(a, b)]$$

첫 번째 항에 1변수 평균값 정리(Mean Value Theorem)를 $x$에 대해 적용하면, 어떤 $\xi \in (a, a+h)$가 존재하여:

$$f(a+h, b+k) - f(a, b+k) = \frac{\partial f}{\partial x}(\xi, b+k) \cdot h$$

두 번째 항에 1변수 평균값 정리를 $y$에 대해 적용하면, 어떤 $\eta \in (b, b+k)$가 존재하여:

$$f(a, b+k) - f(a, b) = \frac{\partial f}{\partial y}(a, \eta) \cdot k$$

따라서:

$$f(a+h, b+k) - f(a, b) = \frac{\partial f}{\partial x}(\xi, b+k) \cdot h + \frac{\partial f}{\partial y}(a, \eta) \cdot k$$

$\frac{\partial f}{\partial x}$와 $\frac{\partial f}{\partial y}$가 $(a, b)$에서 연속이므로, $(h,k) \to (0,0)$일 때 $\frac{\partial f}{\partial x}(\xi, b+k) \to \frac{\partial f}{\partial x}(a, b)$이고 $\frac{\partial f}{\partial y}(a, \eta) \to \frac{\partial f}{\partial y}(a, b)$이다. 따라서:

$$f(a+h, b+k) - f(a, b) = \frac{\partial f}{\partial x}(a, b) \cdot h + \frac{\partial f}{\partial y}(a, b) \cdot k + o(\sqrt{h^2 + k^2})$$

즉, $f$는 $(a, b)$에서 미분가능하며 $\nabla f(a, b) = (\frac{\partial f}{\partial x}(a, b), \frac{\partial f}{\partial y}(a, b))$이다. 일반 $n$변수에 대해서도 동일한 논법으로 증명된다.

$\square$

### 정리 3: 그래디언트는 최대 증가 방향 (Gradient Points to Steepest Ascent)

$f: \mathbb{R}^n \to \mathbb{R}$이 $a$에서 미분가능하고 $\nabla f(a) \neq 0$이라 하자. 단위벡터 $u$ ($\|u\| = 1$) 방향으로의 방향 도함수 $D_u f(a) = \nabla f(a) \cdot u$가 최대가 되는 $u$는 $\nabla f(a)$ 방향이며, 그 최대값은 $\|\nabla f(a)\|$이다.

**증명:** 코시-슈바르츠 부등식(Cauchy-Schwarz inequality)에 의해:

$$D_u f(a) = \nabla f(a) \cdot u \leq \|\nabla f(a)\| \cdot \|u\| = \|\nabla f(a)\|$$

등호는 $u$가 $\nabla f(a)$와 같은 방향일 때 성립한다. 즉 $u = \nabla f(a) / \|\nabla f(a)\|$일 때 $D_u f(a) = \|\nabla f(a)\|$가 최대가 된다. 반대 방향 $u = -\nabla f(a) / \|\nabla f(a)\|$에서는 $-\|\nabla f(a)\|$로 가장 급격히 감소한다.

$\square$

이 정리는 그래디언트 상승법(gradient ascent)과 하강법(gradient descent)의 수학적 근거가 된다. 함수를 최대화하려면 $\nabla f$ 방향으로, 최소화하려면 $-\nabla f$ 방향으로 이동해야 한다.

### 정리 4: 미분가능 함수의 국소적 선형성 (Local Linear Approximation)

$f$가 $a$에서 미분가능하면, 다음이 성립한다:

$$f(a+h) - f(a) = \nabla f(a)^T h + \epsilon(h)\|h\|, \quad \epsilon(h) \to 0 \text{ as } h \to 0$$

이는 $h \to 0$일 때 $f$가 $\nabla f(a)^T h$에 의해 지배됨을 의미한다. 특히:

$$\lim_{h \to 0} \frac{|f(a+h) - f(a) - \nabla f(a)^T h|}{\|h\|} = 0$$

이 성질은 국소적 선형 근사의 정확도를 정량화하며, 뉴턴법(Newton's method), 테일러 전개(Taylor expansion), 최적화 알고리즘의 수렴 분석에서 핵심적인 역할을 한다.

### 정리 5: 미분가능성과 연속성 (Differentiability Implies Continuity)

$f$가 $a$에서 미분가능하면 $f$는 $a$에서 연속이다.

**증명:** 미분가능성의 정의에서:

$$f(a+h) = f(a) + \nabla f(a)^T h + o(\|h\|)$$

$h \to 0$일 때 $\nabla f(a)^T h \to 0$이고 $o(\|h\|) \to 0$이므로 $\lim_{h \to 0} f(a+h) = f(a)$이다. 따라서 $f$는 $a$에서 연속이다.

$\square$

---
## 예제

**예제 1:** $f(x, y) = x^2 y + e^{xy}$의 편도함수와 기울기 벡터를 구하라.

**풀이:** $y$를 상수로 보고 $x$에 대해 미분한다:

$$\frac{\partial f}{\partial x} = 2xy + y e^{xy}$$

$x$를 상수로 보고 $y$에 대해 미분한다:

$$\frac{\partial f}{\partial y} = x^2 + x e^{xy}$$

기울기 벡터:

$$\nabla f(x, y) = (2xy + y e^{xy}, \; x^2 + x e^{xy})$$

점 $(1, 0)$에서 $\nabla f(1, 0) = (0, 1)$이다. 이 점에서 함수는 북쪽 방향으로 가장 가파르게 증가한다.

**예제 2:** $f(x, y, z) = x \sin(yz) + z^2$의 편도함수를 구하라.

**풀이:**

$$\frac{\partial f}{\partial x} = \sin(yz)$$
$$\frac{\partial f}{\partial y} = xz \cos(yz)$$
$$\frac{\partial f}{\partial z} = xy \cos(yz) + 2z$$

**예제 3:** $f(x, y) = |x| + |y|$의 $(0,0)$에서 편도함수 존재 여부와 미분가능성을 판정하라.

**풀이:** $f(x, 0) = |x|$이므로:

$$\frac{\partial f}{\partial x}(0,0) = \lim_{h \to 0} \frac{|h| - 0}{h}$$

이 극한은 존재하지 않는다(좌극한 $-1$, 우극한 $1$). $\frac{\partial f}{\partial y}$도 마찬가지. 따라서 편도함수가 존재하지 않고, 미분가능하지도 않다.

**예제 4:** $f(x, y) = \begin{cases} \frac{x^2 y}{x^2 + y^2}, & (x, y) \neq (0, 0) \\ 0, & (0, 0) \end{cases}$의 $(0,0)$에서 미분가능성을 판정하라.

**풀이:** 편도함수를 계산한다:

$$\frac{\partial f}{\partial x}(0,0) = \lim_{h \to 0} \frac{h^2 \cdot 0 / (h^2 + 0) - 0}{h} = 0$$

$$\frac{\partial f}{\partial y}(0,0) = \lim_{h \to 0} \frac{0^2 \cdot h / (0 + h^2) - 0}{h} = 0$$

편도함수는 존재한다. 이제 미분가능성을 확인한다:

$$\lim_{(h,k) \to (0,0)} \frac{|f(h,k) - f(0,0) - 0 \cdot h - 0 \cdot k|}{\sqrt{h^2 + k^2}} = \lim_{(h,k) \to (0,0)} \frac{|h^2 k|}{(h^2 + k^2)^{3/2}}$$

$k = h$로 접근하면 $\frac{|h^3|}{(2h^2)^{3/2}} = \frac{|h|^3}{2^{3/2}|h|^3} = \frac{1}{2^{3/2}} \neq 0$. 따라서 극한이 0이 아니므로 $f$는 $(0,0)$에서 미분가능하지 않다.

**예제 5:** 원기둥의 부피 $V(r, h) = \pi r^2 h$에 대해 전미분 $dV$를 구하고, 반지름이 $10$ cm, 높이가 $20$ cm인 원기둥에서 반지름을 $0.1$ cm, 높이를 $0.2$ cm 늘릴 때 부피 변화의 근삿값을 구하라.

**풀이:**

$$\frac{\partial V}{\partial r} = 2\pi r h, \quad \frac{\partial V}{\partial h} = \pi r^2$$

$$dV = 2\pi r h \cdot dr + \pi r^2 \cdot dh = 2\pi(10)(20) \cdot 0.1 + \pi(10)^2 \cdot 0.2$$

$$= 40\pi \cdot 0.1 + 100\pi \cdot 0.2 = 4\pi + 20\pi = 24\pi \approx 75.4 \text{ cm}^3$$

실제 변화량과의 오차는 $o(\sqrt{dr^2 + dh^2})$ 차수로 작다.

**예제 6 (기울기 방향 계산):** $f(x, y) = x^2 + xy + y^2$의 점 $(1, 2)$에서 최대 증가 방향과 그 증가율을 구하라.

**풀이:** $\nabla f = (2x + y, x + 2y)$, $\nabla f(1, 2) = (4, 5)$. 최대 증가 방향은 $u = \frac{(4, 5)}{\sqrt{41}}$이고, 최대 증가율은 $\|\nabla f(1, 2)\| = \sqrt{41}$이다.

**예제 7 (함수 그래프의 접평면):** $z = f(x, y) = e^x \cos y$의 점 $(0, \pi/4)$에서 접평면의 방정식을 구하라.

**풀이:** $\nabla f = (e^x \cos y, -e^x \sin y)$, $\nabla f(0, \pi/4) = \left(\frac{1}{\sqrt{2}}, -\frac{1}{\sqrt{2}}\right)$.

$f(0, \pi/4) = e^0 \cos(\pi/4) = 1/\sqrt{2}$.

접평면: $z - \frac{1}{\sqrt{2}} = \frac{1}{\sqrt{2}}(x-0) - \frac{1}{\sqrt{2}}(y - \pi/4)$

정리: $z = \frac{1}{\sqrt{2}} + \frac{1}{\sqrt{2}}x - \frac{1}{\sqrt{2}}y + \frac{\pi}{4\sqrt{2}}$

**예제 8 (오차 전파, Error Propagation):** 삼각형의 두 변 $a, b$와 그 사이 각 $\theta$가 주어졌을 때, 넓이 $S = \frac{1}{2}ab\sin\theta$의 오차를 전미분으로 추정하라. $a = 10$, $b = 16$, $\theta = \pi/6$이고 측정 오차가 각각 $da = 0.1$, $db = 0.1$, $d\theta = 0.01$일 때 넓이 오차를 구하라.

**풀이:** $\frac{\partial S}{\partial a} = \frac{1}{2}b\sin\theta$, $\frac{\partial S}{\partial b} = \frac{1}{2}a\sin\theta$, $\frac{\partial S}{\partial \theta} = \frac{1}{2}ab\cos\theta$.

$$dS = \frac{\partial S}{\partial a}da + \frac{\partial S}{\partial b}db + \frac{\partial S}{\partial \theta}d\theta$$

$= \frac{1}{2} \cdot 16 \cdot \frac{1}{2} \cdot 0.1 + \frac{1}{2} \cdot 10 \cdot \frac{1}{2} \cdot 0.1 + \frac{1}{2} \cdot 10 \cdot 16 \cdot \frac{\sqrt{3}}{2} \cdot 0.01$

$= 0.4 + 0.25 + 0.4\sqrt{3} \approx 0.4 + 0.25 + 0.693 = 1.343$

---
## 연결

- **[극한·연속·도함수](limits-derivatives.html)** : 1변수 도함수의 정의와 극한 개념이 편도함수의 기초다.
- **[등고선과 그래디언트](gradient-geometry.html)** : $\nabla f$가 등고선에 수직임을 기하학적으로 해석한다.
- **[방향 도함수](directional-derivative.html)** : 편도함수를 임의의 방향으로 일반화한다.
- **[다변수 연쇄법칙](multivar-chain-rule.html)** : 편도함수들의 결합으로 합성함수의 변화율을 계산한다.
