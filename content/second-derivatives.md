---
title: 2계 도함수·헤시안·곡률
slug: second-derivatives
---

## 직관적 설명

**2계 도함수(second derivative)** 는 "도함수의 도함수"로, 함수의 변화율 자체가 어떻게 변하는지를 측정한다. 1변수에서 $f''(a) > 0$은 함수가 $a$ 근처에서 아래로 볼록(convex, ∪ 모양)함을, $f''(a) < 0$은 위로 볼록(concave, ∩ 모양)함을 의미한다.

다변수에서는 **헤시안 행렬(Hessian matrix)** $H$가 이 역할을 한다. $H_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}$는 함수의 2차 변화율을 모든 방향에 대해 기록한 곡률 행렬(curvature matrix)이다. 헤시안이 양정치(positive definite)이면 함수는 그 점에서 극소, 음정치(negative definite)이면 극대, 부정부호(indefinite)이면 안장점(saddle point)이다.

1변수 함수 $f(x) = x^2$은 $f''(x) = 2 > 0$으로 항상 볼록하다. 2변수 함수 $f(x, y) = x^2 - y^2$는 $x$ 방향으로는 볼록하지만 $y$ 방향으로는 오목하며, 그 헤시안은 $\begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$로 부정부호이다 — 이것이 안장점의 전형이다.

---
## 정의

**2계 편도함수 (second-order partial derivative):** $f: \mathbb{R}^n \to \mathbb{R}$의 2계 편도함수:

$$\frac{\partial^2 f}{\partial x_i \partial x_j}(a) = \frac{\partial}{\partial x_i}\left(\frac{\partial f}{\partial x_j}\right)(a)$$

$i = j$일 때 $\frac{\partial^2 f}{\partial x_i^2}$(순수 2계 도함수), $i \neq j$일 때 $\frac{\partial^2 f}{\partial x_i \partial x_j}$(혼합 편도함수, mixed partial derivative)라 부른다.

**헤시안 행렬 (Hessian matrix):** $f: \mathbb{R}^n \to \mathbb{R}$이 $C^2$($2$계 편도함수가 모두 연속)이면, 점 $a$에서의 헤시안 $H_f(a)$는 $n \times n$ 행렬이다:

$$H_f(a) = \begin{pmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\[4pt]
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\[4pt]
\vdots & \vdots & \ddots & \vdots \\[4pt]
\frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{pmatrix}$$

$C^2$ 조건에서 헤시안은 대칭행렬이다: $H_{ij} = H_{ji}$ (클레로 정리, Clairaut's theorem).

**테일러 전개의 2차 항 (quadratic form in Taylor expansion):** $f(a+h) = f(a) + \nabla f(a)^T h + \frac{1}{2} h^T H(a) h + O(\|h\|^3)$

2차 항 $\frac{1}{2} h^T H h$가 곡률을 결정한다. $h$ 방향의 곡률(2계 방향 도함수)은:

$$\frac{d^2}{dt^2}\bigg|_{t=0} f(a + th) = h^T H(a) h$$

**볼록성 (convexity):** $f$가 $\mathbb{R}^n$의 볼록집합 $\Omega$에서 $C^2$일 때, $f$가 $\Omega$에서 볼록(convex)할 필요충분조건은 모든 $x \in \Omega$에서 $H(x) \succeq 0$(헤시안이 양반정치, positive semidefinite)인 것이다.

---
## 주요 정리와 증명

### 정리 1: 2계 도함수 판정법 (1변수) (Second Derivative Test, 1D)

$f: \mathbb{R} \to \mathbb{R}$이 $C^2$이고 $f'(c) = 0$($c$가 임계점)이라 하자.
- $f''(c) > 0$이면 $c$에서 극소(local minimum)
- $f''(c) < 0$이면 $c$에서 극대(local maximum)
- $f''(c) = 0$이면 판정 불가(inconclusive)

**증명 (테일러 전개):** $f$를 $c$에서 2차 테일러 전개한다:

$$f(c + h) = f(c) + f'(c)h + \frac{1}{2}f''(c)h^2 + o(h^2)$$

$f'(c) = 0$이므로:

$$f(c + h) - f(c) = \frac{1}{2}f''(c)h^2 + o(h^2) = h^2\left(\frac{1}{2}f''(c) + \frac{o(h^2)}{h^2}\right)$$

$h \to 0$일 때 $o(h^2)/h^2 \to 0$이므로, 충분히 작은 $h$에 대해 $\frac{1}{2}f''(c) + \frac{o(h^2)}{h^2}$의 부호는 $f''(c)$의 부호와 같다. $h^2 > 0$이므로:

- $f''(c) > 0$이면 $f(c+h) - f(c) > 0$ → 극소
- $f''(c) < 0$이면 $f(c+h) - f(c) < 0$ → 극대

$f''(c) = 0$이면 $h^4$ 이상의 차수에 의해 부호가 결정되므로 더 높은 차수의 도함수를 검사해야 한다.

$\square$

### 정리 2: 다변수 2계 판정법 (Second Derivative Test, Multivariate)

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^2$이고 $\nabla f(c) = 0$($c$가 임계점)이라 하자. 헤시안 $H(c)$에 대해:
- $H(c)$가 양정치(positive definite, 모든 고유값 $> 0$) → $c$에서 극소
- $H(c)$가 음정치(negative definite, 모든 고유값 $< 0$) → $c$에서 극대
- $H(c)$가 부정부호(indefinite, 양/음 고유값 모두 존재) → $c$에서 안장점(saddle point)
- $H(c)$가 준정치(semidefinite, 0인 고유값 존재) → 판정 불가

**증명:** $c$에서 2차 테일러 전개($\nabla f(c) = 0$이므로 1차 항 소멸):

$$f(c + h) = f(c) + \frac{1}{2} h^T H(c) h + o(\|h\|^2)$$

$H(c)$가 양정치이면, 스펙트럼 정리(spectral theorem)에 의해 $H(c)$의 최소 고유값 $\lambda_{\min} > 0$이 존재하고:

$$h^T H(c) h \geq \lambda_{\min} \|h\|^2 > 0 \quad (\forall h \neq 0)$$

따라서 충분히 작은 $\|h\|$에 대해 $f(c+h) - f(c) \geq \frac{1}{2}\lambda_{\min}\|h\|^2 + o(\|h\|^2) > 0$이므로 $c$는 극소점이다.

음정치의 경우 $H(c)$ 대신 $-H(c)$를 고려하면 동일한 논증으로 극대임을 보일 수 있다.

부정부호이면 $h^T H(c) h$가 $h$의 방향에 따라 양수도 음수도 될 수 있다. $H(c)$의 양의 고유벡터 방향으로 움직이면 $f$가 증가하고, 음의 고유벡터 방향으로 움직이면 $f$가 감소하므로 $c$는 안장점이다.

$\square$

**2변수 특수 경우:** $\det H = f_{xx}f_{yy} - (f_{xy})^2$와 $f_{xx}$의 부호로 판정할 수 있다:

- $\det H > 0$이고 $f_{xx} > 0$ → 극소
- $\det H > 0$이고 $f_{xx} < 0$ → 극대
- $\det H < 0$ → 안장점
- $\det H = 0$ → 판정 불가

### 정리 3: 볼록성과 헤시안 (Convexity and Hessian)

$C^2$ 함수 $f: \mathbb{R}^n \to \mathbb{R}$가 볼록(convex)일 필요충분조건은 모든 $x$에서 $H(x) \succeq 0$(양반정치)인 것이다.

**증명:** ($\Rightarrow$) $f$가 볼록하면 임의의 $x$와 $v$에 대해, $g(t) = f(x + tv)$로 정의하면 $g$는 1변수 볼록함수이고 $g''(0) \geq 0$이다. $g''(0) = v^T H(x) v$이므로 $H(x) \succeq 0$이다.

($\Leftarrow$) 모든 $x$에서 $H(x) \succeq 0$이라 하자. 평균값 정리의 2변수 버전을 사용하면 임의의 $x, y$에 대해 어떤 $\xi$가 존재하여:

$$f(y) - f(x) - \nabla f(x)^T (y-x) = \frac{1}{2} (y-x)^T H(\xi) (y-x) \geq 0$$

이는 $f$의 볼록성 정의($f(y) \geq f(x) + \nabla f(x)^T (y-x)$)와 정확히 일치한다.

$\square$

### 정리 4: 라플라시안 (Laplacian)

$f: \mathbb{R}^n \to \mathbb{R}$의 라플라시안 $\Delta f$는 헤시안의 대각합(trace)이다:

$$\Delta f = \nabla^2 f = \sum_{i=1}^n \frac{\partial^2 f}{\partial x_i^2} = \text{tr}(H_f)$$

라플라시안은 함수의 "평균 곡률"을 나타내며, $\Delta f = 0$인 함수를 조화함수(harmonic function)라 부른다. 조화함수는 극대/극소가 없으며(최대 원리, maximum principle), 물리학에서 정상 상태(steady state)의 온도 분포, 전위(electric potential) 등을 기술한다.

---
## 예제

**예제 1:** $f(x, y) = x^3 - 3xy + y^3$의 임계점을 찾고 2계 판정법으로 분류하라.

**풀이:** $\nabla f = (3x^2 - 3y, -3x + 3y^2)$.

임계점: $3x^2 - 3y = 0$, $-3x + 3y^2 = 0$ → $y = x^2$, $x = y^2$.

$x = y^2 = (x^2)^2 = x^4$ → $x^4 - x = 0$ → $x(x^3 - 1) = 0$ → $x = 0$ 또는 $x = 1$.

- $(x, y) = (0, 0)$: $y = 0^2 = 0$
- $(x, y) = (1, 1)$: $y = 1^2 = 1$

헤시안: $H(x, y) = \begin{pmatrix} 6x & -3 \\ -3 & 6y \end{pmatrix}$.

**$(0, 0)$에서:** $H(0, 0) = \begin{pmatrix} 0 & -3 \\ -3 & 0 \end{pmatrix}$, $\det H = -9 < 0$ → 안장점.

**$(1, 1)$에서:** $H(1, 1) = \begin{pmatrix} 6 & -3 \\ -3 & 6 \end{pmatrix}$, $\det H = 36 - 9 = 27 > 0$, $f_{xx} = 6 > 0$ → 극소.

$f(1, 1) = 1 - 3 + 1 = -1$ (극소값).

**예제 2:** $f(x, y) = x^2 + xy + y^2$의 헤시안을 구하고 함수의 볼록성을 판정하라.

**풀이:** $\nabla f = (2x + y, x + 2y)$.

$$H = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$$

고유값: $\det\begin{pmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{pmatrix} = (2-\lambda)^2 - 1 = \lambda^2 - 4\lambda + 3 = 0$ → $\lambda = 1, 3$.

모든 고유값 $> 0$이므로 $H$는 양정치(positive definite)이다. 따라서 $f$는 전역적으로 엄격 볼록(strictly convex)하다. 실제로 $f(x, y) = \frac{1}{2}(x+y)^2 + \frac{1}{2}(x^2 + y^2)$로 쓸 수 있으며, 두 항 모두 볼록하다.

**예제 3:** $f(x, y) = x^2 - y^2$의 $(0, 0)$을 분류하라.

**풀이:** $\nabla f = (2x, -2y)$, $\nabla f(0, 0) = 0$. $H = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$.

고유값: $2$와 $-2$ — 부정부호(indefinite). 따라서 $(0, 0)$은 안장점이다. $x$ 방향($h = (t, 0)$)으로 $f(t, 0) = t^2$ (볼록), $y$ 방향($h = (0, t)$)으로 $f(0, t) = -t^2$ (오목).

**예제 4:** $f(x, y) = x^4 + y^4 - 2x^2 - 2y^2 + 4xy$의 임계점을 분류하라.

**풀이:** $\nabla f = (4x^3 - 4x + 4y, 4y^3 - 4y + 4x)$.

임계점 조건: $4x^3 - 4x + 4y = 0$, $4y^3 - 4y + 4x = 0$.
$x^3 - x + y = 0$, $y^3 - y + x = 0$. 두 식을 빼면 $x^3 - y^3 - (x - y) - (x - y) = (x-y)(x^2 + xy + y^2 - 2) = 0$.

$x = y$이면 $x^3 - x + x = x^3 = 0$ → $x = 0$. $(0, 0)$.

$x \neq y$이면 $x^2 + xy + y^2 = 2$을 만족하는 해가 존재한다. $x = -y$를 대입: $(-y)^2 + (-y)y + y^2 = y^2 = 2$ → $y = \pm\sqrt{2}$, $x = \mp\sqrt{2}$. 점 $(\sqrt{2}, -\sqrt{2})$, $(-\sqrt{2}, \sqrt{2})$.

헤시안: $H = \begin{pmatrix} 12x^2 - 4 & 4 \\ 4 & 12y^2 - 4 \end{pmatrix}$.

**$(0, 0)$:** $H = \begin{pmatrix} -4 & 4 \\ 4 & -4 \end{pmatrix}$, $\det H = 16 - 16 = 0$ — 판정 불가. 더 높은 차수를 검사해야 한다.

실제로 $f(x, y) = (x^2 - 1)^2 + (y^2 - 1)^2 + 4xy - 2$로 쓸 수 있으며, $(0, 0)$ 근처 $y = x$ 방향: $f(x, x) = 2x^4$ → $0$에서 극소; $y = -x$ 방향: $f(x, -x) = 2x^4 - 8x^2$ → $0$에서 극대. 따라서 $(0, 0)$은 안장점.

**$(\sqrt{2}, -\sqrt{2})$:** $H = \begin{pmatrix} 20 & 4 \\ 4 & 20 \end{pmatrix}$, $\det H = 400 - 16 = 384 > 0$, $f_{xx} = 20 > 0$ → 극소.

**$(-\sqrt{2}, \sqrt{2})$:** $H = \begin{pmatrix} 20 & 4 \\ 4 & 20 \end{pmatrix}$, 극소.

**예제 5:** $f(x, y) = e^{x^2 - y^2}$의 임계점을 분류하라.

**풀이:** $\nabla f = (2x e^{x^2 - y^2}, -2y e^{x^2 - y^2})$.

$\nabla f = 0$ → $x = 0$, $y = 0$. $(0, 0)$이 유일한 임계점.

헤시안: $\frac{\partial^2 f}{\partial x^2} = (2 + 4x^2) e^{x^2 - y^2}$, $\frac{\partial^2 f}{\partial y^2} = (-2 + 4y^2) e^{x^2 - y^2}$, $\frac{\partial^2 f}{\partial x \partial y} = -4xy e^{x^2 - y^2}$.

$(0, 0)$에서 $H = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$, $\det H = -4 < 0$ → 안장점.

$f(x, y) = e^{x^2 - y^2}$는 $x$ 방향으로는 아래로 볼록, $y$ 방향으로는 위로 볼록한 함수다.

**예제 6 (라플라시안):** $f(x, y, z) = \frac{1}{\sqrt{x^2 + y^2 + z^2}}$ (전위, electric potential)의 라플라시안을 구하라($(x, y, z) \neq (0, 0, 0)$).

**풀이:** $r = \sqrt{x^2 + y^2 + z^2}$라 하면 $f = 1/r$이다.

$$\frac{\partial f}{\partial x} = -\frac{x}{r^3}, \quad \frac{\partial^2 f}{\partial x^2} = -\frac{1}{r^3} + \frac{3x^2}{r^5}$$

$$\Delta f = \sum_{i=1}^3 \frac{\partial^2 f}{\partial x_i^2} = -\frac{3}{r^3} + \frac{3(x^2 + y^2 + z^2)}{r^5} = -\frac{3}{r^3} + \frac{3r^2}{r^5} = 0$$

따라서 $\Delta(1/r) = 0$ (원점 제외). $1/r$은 조화함수(harmonic function)이며, 이는 전기장이 없는 진공에서 전위가 라플라스 방정식 $\Delta \phi = 0$을 만족함을 의미한다.

---
## 연결

- **[야코비안·헤시안](jacobian-hessian.html)** : 헤시안의 정의와 대칭성(클레로 정리)을 자세히 다룬다.
- **[테일러 전개](taylor-expansion.html)** : 헤시안은 2차 테일러 전개의 핵심 항이다.
- **[극값·안장점](extrema-saddle.html)** : 2계 판정법으로 임계점을 분류하는 방법을 더 확장한다.
- **[양정치 행렬](positive-definite.html)** : 헤시안의 양정치성과 고유값 판정을 연결한다.
