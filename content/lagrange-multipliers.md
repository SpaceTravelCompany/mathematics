---
title: 라그랑주 승수법
slug: lagrange-multipliers
---

## 직관적 설명

**라그랑주 승수법(Lagrange multiplier method)** 은 제약 조건(constraint)이 있을 때 함수를 최적화하는 도구다. "언덕 위를 자유롭게 걸어다니며 최고점을 찾는 것"이 무제약 최적화라면, "산책로(제약 곡선)에서만 걸어다니며 가장 높은 지점을 찾는 것"이 제약 최적화다.

등산로에서 가장 높은 지점에서는 등산로의 방향과 등고선(level curve)이 접한다(tangent). 즉, 제약 곡선의 접선 방향으로는 함수값이 변하지 않는다. 이는 $\nabla f$가 제약 곡선에 수직임을 의미하고, 따라서 $\nabla f$는 $\nabla g$(제약 함수의 그래디언트)와 평행(parallel)하다:

$$\nabla f = \lambda \nabla g$$

여기서 $\lambda$가 **라그랑주 승수(Lagrange multiplier)** 다. 이 스칼라 $\lambda$는 제약이 최적값에 미치는 영향력, 즉 제약을 조금 완화했을 때 목적함수가 얼마나 변하는지를 나타낸다.

---
## 정의

**제약 최적화 문제 (constrained optimization problem):**

$$\min_{x \in \mathbb{R}^n} f(x) \quad \text{subject to} \quad g(x) = 0$$

여기서 $f: \mathbb{R}^n \to \mathbb{R}$는 목적함수(objective function), $g: \mathbb{R}^n \to \mathbb{R}$는 등식 제약(equality constraint)이다. $g(x) = 0$은 $n-1$차원 곡면을 정의한다.

**라그랑지안 (Lagrangian):**

$$\mathcal{L}(x, \lambda) = f(x) - \lambda g(x)$$

$\lambda \in \mathbb{R}$을 라그랑주 승수(Lagrange multiplier)라 부른다.

**1차 필요 조건 (first-order necessary condition):** 제약 최적점 $x^*$가 정규(regular, $\nabla g(x^*) \neq 0$)이면, 어떤 $\lambda^* \in \mathbb{R}$이 존재하여:

$$\nabla_x \mathcal{L}(x^*, \lambda^*) = 0 \quad \text{즉} \quad \nabla f(x^*) = \lambda^* \nabla g(x^*)$$

$$g(x^*) = 0$$

즉, $\mathcal{L}$의 정류점(stationary point)을 찾는 문제로 변환된다.

**2차 충분 조건 (second-order sufficient condition):** $\nabla f(x^*) = \lambda^* \nabla g(x^*)$, $g(x^*) = 0$이고, 제약 곡면의 접공간(tangent space) $T = \{v \mid \nabla g(x^*) \cdot v = 0\}$ 위에서 $v^T \nabla^2_{xx} \mathcal{L}(x^*, \lambda^*) v > 0$이면 $x^*$는 엄격한 국소 최소(strict local minimum)다. $< 0$이면 국소 최대다.

**다중 제약 (multiple constraints):** $g_i(x) = 0$, $i = 1, \ldots, m$인 경우:

$$\mathcal{L}(x, \lambda_1, \ldots, \lambda_m) = f(x) - \sum_{i=1}^m \lambda_i g_i(x)$$

1차 조건: $\nabla f(x) = \sum_{i=1}^m \lambda_i \nabla g_i(x)$.

---
## 주요 정리와 증명

### 정리 1: 라그랑주 승수 정리 (Lagrange Multiplier Theorem)

$f, g: \mathbb{R}^n \to \mathbb{R}$이 $C^1$ 함수이고, $x^*$가 $g(x) = 0$ 아래 $f$의 국소 극점(local extremum)이며 $\nabla g(x^*) \neq 0$이면, $\nabla f(x^*) = \lambda \nabla g(x^*)$를 만족하는 $\lambda \in \mathbb{R}$이 존재한다.

**증명:** $x^*$가 $g(x) = 0$ 위의 국소 극점이라 하자. $\gamma: (-\epsilon, \epsilon) \to \mathbb{R}^n$을 $\gamma(0) = x^*$이고 모든 $t$에서 $g(\gamma(t)) = 0$인 $C^1$ 곡선이라 하자(즉, 곡선이 제약 곡면 위에 있다).

$h(t) = f(\gamma(t))$는 $t = 0$에서 국소 극값을 가지므로 $h'(0) = 0$이다. 연쇄법칙(chain rule)에 의해:

$$h'(0) = \nabla f(x^*) \cdot \gamma'(0) = 0$$

$\gamma'(0)$은 $x^*$에서 제약 곡면에 접하는 임의의 접선벡터다. 따라서 $\nabla f(x^*)$는 제약 곡면의 모든 접선벡터와 직교한다.

$\nabla g(x^*)$는 $g(x) = 0$의 법선벡터다(그래디언트가 등위면에 수직). 따라서 1차원 법선공간(normal space)은 $\text{span}\{\nabla g(x^*)\}$이고, $\nabla f(x^*)$는 이 공간에 속한다. 즉:

$$\nabla f(x^*) = \lambda \nabla g(x^*)$$

$\square$

**기하학적 해석:** $x^*$에서 $f$의 등고선 $f = c$와 제약 곡면 $g = 0$이 접한다(tangent). 접하는 점에서는 두 곡면의 법선벡터가 평행하다.

### 정리 2: 라그랑주 승수의 의미 (Interpretation of Lagrange Multiplier)

$f^*(c) = \min\{f(x) \mid g(x) = c\}$라 정의할 때, $x^*(c)$가 대응하는 최적점이면:

$$\frac{df^*}{dc}(0) = \lambda^*$$

즉, $\lambda^*$는 제약을 완화했을 때(우변을 $0$에서 $c$로 변경했을 때) 목적함수의 최적값이 변하는 비율이다.

**증명:** $x^*(c)$가 $\min f(x)$ subject to $g(x) = c$의 해라 하자. $c = 0$에서 $\mathcal{L} = f(x) - \lambda(g(x) - c)$.

$$\frac{df^*}{dc} = \nabla f(x^*(c)) \cdot \frac{dx^*}{dc} = \lambda \nabla g(x^*(c)) \cdot \frac{dx^*}{dc} = \lambda \frac{d}{dc}(g(x^*(c))) = \lambda \cdot 1 = \lambda$$

$\square$

**경제학 해석:** $f$를 비용, $g$를 생산량 제약이라 하면 $\lambda$는 한계 비용(marginal cost) — 제약을 한 단위 완화할 때 비용의 증가분이다.

### 정리 3: 대칭행렬의 레일리 몫 (Rayleigh Quotient)

$A$가 $n \times n$ 대칭행렬일 때, $f(x) = x^T A x$의 $\|x\| = 1$에서의 최적화는 라그랑주 승수법으로 해결된다.

**문제:** $\min/\max x^T A x$ subject to $\|x\|^2 = 1$.

**라그랑지안:** $\mathcal{L} = x^T A x - \lambda(x^T x - 1)$.

**1차 조건:** $\nabla \mathcal{L} = 2Ax - 2\lambda x = 0$ → $Ax = \lambda x$.

따라서 최적점은 $A$의 고유벡터(eigenvector)이며, $\lambda$는 고유값(eigenvalue)이다. 최대/최소값은 각각 최대/최소 고유값이다. 이는 스펙트럼 정리(spectral theorem)의 핵심 내용이다.

---
## 예제

**예제 1:** $x^2 + y^2 = 1$ 위에서 $f(x, y) = x + y$의 최댓값과 최솟값을 구하라.

**풀이:** $g(x, y) = x^2 + y^2 - 1 = 0$.

라그랑지안: $\mathcal{L} = x + y - \lambda(x^2 + y^2 - 1)$.

1차 조건:

$$\frac{\partial \mathcal{L}}{\partial x} = 1 - 2\lambda x = 0 \quad \Rightarrow \quad x = \frac{1}{2\lambda}$$

$$\frac{\partial \mathcal{L}}{\partial y} = 1 - 2\lambda y = 0 \quad \Rightarrow \quad y = \frac{1}{2\lambda}$$

$$g = x^2 + y^2 - 1 = \frac{1}{2\lambda^2} - 1 = 0 \quad \Rightarrow \quad \lambda = \pm \frac{1}{\sqrt{2}}$$

$\lambda = 1/\sqrt{2}$: $x = y = 1/\sqrt{2}$, $f = \sqrt{2}$ (최댓값).

$\lambda = -1/\sqrt{2}$: $x = y = -1/\sqrt{2}$, $f = -\sqrt{2}$ (최솟값).

기하학: 원 위에서 $x + y$를 최대화하는 점은 직선 $x + y = c$이 원에 접하는 점이다.

**예제 2 (원기둥 부피 최대):** 표면적이 $S$로 고정된 원기둥 중 부피가 최대인 것을 구하라.

**풀이:** 반지름 $r$, 높이 $h$인 원기둥의 부피 $V = \pi r^2 h$, 표면적 $S = 2\pi r^2 + 2\pi rh$가 일정하다.

제약: $g(r, h) = 2\pi r^2 + 2\pi rh - S = 0$.

라그랑지안: $\mathcal{L} = \pi r^2 h - \lambda(2\pi r^2 + 2\pi rh - S)$.

1차 조건:

$$\frac{\partial \mathcal{L}}{\partial r} = 2\pi r h - \lambda(4\pi r + 2\pi h) = 0 \quad \Rightarrow \quad 2\pi r h = \lambda(4\pi r + 2\pi h)$$

$$\frac{\partial \mathcal{L}}{\partial h} = \pi r^2 - \lambda(2\pi r) = 0 \quad \Rightarrow \quad \pi r^2 = 2\pi \lambda r \quad \Rightarrow \quad \lambda = \frac{r}{2}$$

$\lambda = r/2$를 첫 번째 식에 대입:

$$2\pi r h = \frac{r}{2}(4\pi r + 2\pi h) = 2\pi r^2 + \pi r h$$

$$2\pi r h - \pi r h = 2\pi r^2 \quad \Rightarrow \quad \pi r h = 2\pi r^2 \quad \Rightarrow \quad h = 2r$$

따라서 최적 원기둥은 높이 = 지름($h = 2r$)일 때로, 전형적인 참치 캔 비율이다. 최대 부피: $V = \pi r^2(2r) = 2\pi r^3$.

**예제 3 (최소 거리):** 원 $x^2 + y^2 = 1$에서 점 $(2, 0)$까지의 최소 거리를 구하라.

**풀이:** 거리의 제곱 $f(x, y) = (x-2)^2 + y^2$를 최소화한다(제곱근을 피하기 위해). 제약: $g(x, y) = x^2 + y^2 - 1 = 0$.

라그랑지안: $\mathcal{L} = (x-2)^2 + y^2 - \lambda(x^2 + y^2 - 1)$.

1차 조건:

$$\frac{\partial \mathcal{L}}{\partial x} = 2(x-2) - 2\lambda x = 0 \quad \Rightarrow \quad x(1-\lambda) = 2 \quad \Rightarrow \quad x = \frac{2}{1-\lambda}$$

$$\frac{\partial \mathcal{L}}{\partial y} = 2y - 2\lambda y = 2y(1-\lambda) = 0$$

두 번째 식: $y = 0$ 또는 $\lambda = 1$.

$\lambda \neq 1$이면 $y = 0$이고, 제약에서 $x^2 = 1$, $x = \pm 1$.

- $(1, 0)$: $f = (1-2)^2 + 0 = 1$, 거리 $1$.
- $(-1, 0)$: $f = (-1-2)^2 + 0 = 9$, 거리 $3$.

따라서 최소 거리는 $1$ (점 $(1, 0)$). 직관적으로 원 위에서 $(2, 0)$에 가장 가까운 점은 $(1, 0)$이다.

$\lambda = 1$인 경우 첫 번째 식이 $0 = 2$로 모순이므로 해가 아니다.

**예제 4 (다중 제약):** $f(x, y, z) = x + y + z$를 $g_1(x, y, z) = x^2 + y^2 = 1$, $g_2(x, y, z) = z = 1$ 아래 최적화하라.

**풀이:** 라그랑지안: $\mathcal{L} = x + y + z - \lambda_1(x^2 + y^2 - 1) - \lambda_2(z - 1)$.

1차 조건:

$$\frac{\partial \mathcal{L}}{\partial x} = 1 - 2\lambda_1 x = 0 \quad \Rightarrow \quad x = \frac{1}{2\lambda_1}$$

$$\frac{\partial \mathcal{L}}{\partial y} = 1 - 2\lambda_1 y = 0 \quad \Rightarrow \quad y = \frac{1}{2\lambda_1}$$

$$\frac{\partial \mathcal{L}}{\partial z} = 1 - \lambda_2 = 0 \quad \Rightarrow \quad \lambda_2 = 1$$

$$x^2 + y^2 = 1 \quad \Rightarrow \quad \frac{1}{2\lambda_1^2} = 1 \quad \Rightarrow \quad \lambda_1 = \pm \frac{1}{\sqrt{2}}$$

$\lambda_1 = 1/\sqrt{2}$: $x = y = 1/\sqrt{2}$, $f = \sqrt{2} + 1$ (최댓값).

$\lambda_1 = -1/\sqrt{2}$: $x = y = -1/\sqrt{2}$, $f = -\sqrt{2} + 1$ (최솟값).

**예제 5 (코시-슈바르츠 부등식의 증명):** 라그랑주 승수법으로 코시-슈바르츠 부등식(Cauchy-Schwarz inequality)을 증명하라.

**풀이:** $a, b \in \mathbb{R}^n$이 주어졌을 때, $\max_{x \neq 0} \frac{(a^T x)^2}{\|x\|^2}$을 고려한다(레일리 몫, Rayleigh quotient). $\|x\|^2 = 1$에서 제약하면 $\max (a^T x)^2$ subject to $\|x\|^2 = 1$이다.

라그랑지안: $\mathcal{L} = (a^T x)^2 - \lambda(x^T x - 1)$.

1차 조건: $\nabla \mathcal{L} = 2(a^T x)a - 2\lambda x = 0$ → $(a^T x)a = \lambda x$.

$x$가 $a$에 평행할 때 성립: $x = \pm a/\|a\|$. $\lambda = \|a\|^2$.

최댓값: $(a^T (\pm a/\|a\|))^2 = (\pm \|a\|)^2 = \|a\|^2$.

따라서 모든 단위벡터 $x$에 대해 $(a^T x)^2 \leq \|a\|^2 = \|a\|^2 \|x\|^2$.

이제 $b$를 $x = b/\|b\|$로 놓으면 $(a^T b)^2 \leq \|a\|^2 \|b\|^2$, 즉 $|a^T b| \leq \|a\|\|b\|$를 얻는다.

**예제 6 (엔트로피 최대 — 균등분포):** $p_1 + \cdots + p_n = 1$, $p_i \geq 0$ 아래 $H(p) = -\sum p_i \ln p_i$를 최대화하라.

**풀이:** $g(p) = \sum p_i - 1 = 0$.

라그랑지안: $\mathcal{L} = -\sum p_i \ln p_i - \lambda(\sum p_i - 1)$.

1차 조건: $\frac{\partial \mathcal{L}}{\partial p_i} = -\ln p_i - 1 - \lambda = 0$ → $\ln p_i = -1 - \lambda$ → $p_i = e^{-1-\lambda}$.

모든 $p_i$가 같으므로 $p_i = 1/n$. 제약 조건 확인: $\sum p_i = n \cdot 1/n = 1$.

최대 엔트로피: $H = -\sum (1/n) \ln(1/n) = \ln n$. 균등분포(uniform distribution)가 엔트로피를 최대화함을 보여준다.

---
## 연결

- **[양정치 행렬](positive-definite.html)** : 2차 충분 조건에서 헤시안의 제약 접공간 위 양정치성을 이해하는 데 필요하다.
- **[극값·안장점](extrema-saddle.html)** : 제약이 없는 극값 판정과 제약이 있는 경우의 차이를 비교한다.
- **[테일러 전개](taylor-expansion.html)** : 2차 충분 조건의 증명에 테일러 전개가 사용된다.
- **[스펙트럼 정리](spectral-theorem.html)** : 레일리 몫과 고유값 문제와 라그랑주 승수법의 연결을 보여준다.
- **[등고선과 그래디언트](gradient-geometry.html)** : $\nabla f \parallel \nabla g$의 기하학적 의미를 등고선 접점으로 이해한다.
