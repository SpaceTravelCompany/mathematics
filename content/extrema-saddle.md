---
title: 극값·안장점
slug: extrema-saddle
---

## 직관적 설명

**임계점(critical point)** 은 $\nabla f = 0$인 점으로, 기울기가 0인 평평한 지점이다. 1변수에서는 극대/극소/변곡점 중 하나였지만, 다변수에서는 **극대(local maximum)**, **극소(local minimum)**, **안장점(saddle point)** 이 가능하다.

안장점(saddle point)은 일부 방향으로는 극대, 다른 방향으로는 극소인 점이다. 말 안장(saddle) 모양을 생각하면 된다 — 말을 앞뒤로는 오르막이지만 좌우로는 내리막이다.

고차원($n$이 클수록)에서는 안장점이 극값보다 압도적으로 많다. $n$차원에서 임계점의 헤시안 고유값 부호 조합의 수는 $2^n$개인데, 이 중 극소는 모든 고유값이 양수인 1가지, 극대는 모든 고유값이 음수인 1가지뿐이다. 나머지 $2^n - 2$개는 안장점이다. 따라서 고차원 최적화에서는 극소보다 안장점을 만날 확률이 훨씬 높다.

## 정의

**임계점 (critical point):** $f: \mathbb{R}^n \to \mathbb{R}$의 점 $c$가 임계점(critical point)이라는 것은 $\nabla f(c) = 0$임을 뜻한다. 즉, 모든 편도함수가 0이다.

**극소 (local minimum):** $c$의 어떤 근방 $B(c, \delta)$가 존재하여 모든 $x \in B(c, \delta)$에 대해 $f(x) \geq f(c)$이면 $c$는 국소 최소(local minimum)다. 부등호가 $>$로 엄격하면 엄격 극소(strict local minimum)라 한다.

**극대 (local maximum):** $c$의 어떤 근방 $B(c, \delta)$가 존재하여 모든 $x \in B(c, \delta)$에 대해 $f(x) \leq f(c)$이면 $c$는 국소 최대(local maximum)다.

**안장점 (saddle point):** 임계점 $c$가 극대도 극소도 아닐 때, 즉 임의의 근방에 $f(x) > f(c)$인 점과 $f(x) < f(c)$인 점이 모두 존재할 때, $c$를 안장점이라 부른다.

**전역 최소 (global minimum):** 정의역 전체에서 $f(x) \geq f(c)$가 성립하면 $c$는 전역 최소(global minimum)다. 전역 최대(global maximum)도 동일하게 정의된다.

**볼록 함수 (convex function):** $f$가 볼록(convex)이면 모든 국소 최소는 전역 최소다(아래 정리 3).

**2계 판정법 (second derivative test) — 2변수:** $f: \mathbb{R}^2 \to \mathbb{R}$, $\nabla f(c) = 0$, $H(c) = \begin{pmatrix} f_{xx} & f_{xy} \\ f_{xy} & f_{yy} \end{pmatrix}$일 때:

$$\Delta = \det H(c) = f_{xx} f_{yy} - (f_{xy})^2$$

- $\Delta > 0$이고 $f_{xx} > 0$ → 극소
- $\Delta > 0$이고 $f_{xx} < 0$ → 극대
- $\Delta < 0$ → 안장점
- $\Delta = 0$ → 판정 불가

## 주요 정리와 증명

### 정리 1: 2계 판정법 (Second Derivative Test) — 완전 서술

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^2$이고 $\nabla f(c) = 0$일 때, 헤시안 $H(c)$의 고유값(eigenvalue) 부호에 따라 다음이 결정된다:

1. $H(c)$가 양정치(positive definite, 모든 고유값 $> 0$): $c$는 엄격 국소 최소
2. $H(c)$가 음정치(negative definite, 모든 고유값 $< 0$): $c$는 엄격 국소 최대
3. $H(c)$가 부정부호(indefinite, 양/음 고유값 모두 존재): $c$는 안장점
4. $H(c)$가 준정치(semidefinite, 0인 고유값 존재): 판정 불가 (고차 항 검사 필요)

**증명:** 2차 테일러 전개(Taylor expansion)를 사용한다. $f(c+h) = f(c) + \frac{1}{2} h^T H(c) h + o(\|h\|^2)$.

$H(c)$를 스펙트럼 정리(spectral theorem)로 대각화(diagonalize)한다. 직교행렬 $Q$가 존재하여 $Q^T H(c) Q = \text{diag}(\lambda_1, \ldots, \lambda_n)$이다. 좌표 변환 $h = Qy$에서:

$$h^T H(c) h = \sum_{i=1}^n \lambda_i y_i^2$$

각 경우:
- 모든 $\lambda_i > 0$이면 $\sum \lambda_i y_i^2 \geq \lambda_{\min}\|y\|^2 = \lambda_{\min}\|h\|^2$이므로 $f(c+h) > f(c)$ (극소)
- 모든 $\lambda_i < 0$이면 $\sum \lambda_i y_i^2 \leq -\lambda_{\max}\|h\|^2$이므로 $f(c+h) < f(c)$ (극대)
- 양수와 음수 고유값이 모두 있으면 $y$ 방향에 따라 $f(c+h) > f(c)$도 $< f(c)$도 가능 (안장점)

$\square$

### 정리 2: 고차원에서 안장점이 지배적인 이유 (Why Saddle Points Dominate in High Dimensions)

$n$차원에서 $C^2$ 함수의 임계점 $c$에서 $\det H(c) \neq 0$인 경우(비퇴화, non-degenerate), 고유값 부호의 가능한 조합은 $2^n$가지다. 이 중:

- 국소 최소: 모든 $n$개 고유값이 양수 — 1가지
- 국소 최대: 모든 $n$개 고유값이 음수 — 1가지
- 안장점: 나머지 $2^n - 2$가지

$n$이 커질수록 안장점의 비율 $\frac{2^n - 2}{2^n} = 1 - 2^{1-n}$이 1에 수렴한다.

예를 들어 $n = 2$면 안장점 비율 $1/2$, $n = 10$이면 $1 - 2^{-9} \approx 0.998$, $n = 100$이면 사실상 1이다. 따라서 고차원에서는 거의 모든 임계점이 안장점이다.

### 정리 3: 볼록 함수의 국소 최소 = 전역 최소 (Local Minima Are Global for Convex Functions)

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^2$ 볼록 함수(즉, $H(x) \succeq 0$ for all $x$)이면, $c$가 국소 최소일 필요충분조건은 $c$가 전역 최소(global minimum)인 것이다.

**증명:** ($\Leftarrow$) 전역 최소는 당연히 국소 최소다.

($\Rightarrow$) $c$가 국소 최소라 하자. $\nabla f(c) = 0$임을 보인다. 만약 $\nabla f(c) \neq 0$이면, $-\nabla f(c)$ 방향으로 충분히 작게 이동하면 $f$가 감소하므로 $c$는 국소 최소가 아니다. 따라서 $\nabla f(c) = 0$이다.

이제 임의의 $x \in \mathbb{R}^n$에 대해, 볼록 함수의 성질에 의해:

$$f(x) \geq f(c) + \nabla f(c)^T (x - c) = f(c)$$

따라서 $c$는 전역 최소다.

$\square$

**볼록성이 아닌 함수의 경우 (비볼록 최적화, non-convex optimization):** 국소 최소는 여러 개일 수 있으며, 그중 가장 작은 값을 전역 최소라 부른다. 이러한 문제를 전역 최적화(global optimization)라 하며, 일반적으로 NP-hard다.

### 정리 4: 페르마 정리 (Fermat's Theorem, 다변수)

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^1$이고 $c$가 내부점(interior point)에서 국소 극점이면 $\nabla f(c) = 0$이다.

**증명:** 임의의 방향 $v$에 대해 $g(t) = f(c + tv)$를 고려하자. $c$가 국소 극점이므로 $g$는 $t = 0$에서 국소 극값을 가진다. 1변수 페르마 정리에 의해 $g'(0) = 0$이다. $g'(0) = \nabla f(c) \cdot v$이므로 모든 방향 $v$에 대해 $\nabla f(c) \cdot v = 0$이고, 따라서 $\nabla f(c) = 0$이다.

$\square$

**역은 성립하지 않는다:** $\nabla f(c) = 0$이라고 $c$가 극점인 것은 아니다(안장점이 반례).

### 정리 5: 비퇴화 임계점의 분류 정리 (Classification of Non-Degenerate Critical Points)

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^2$이고 $c$가 비퇴화 임계점(non-degenerate critical point, $\det H(c) \neq 0$)이면, $c$ 근처에서 $f$의 국소적 형태는 헤시안의 고유값 부호에 의해 완전히 결정된다(모스 정리, Morse lemma).

**모스 정리 (Morse Lemma):** $c$가 비퇴화 임계점이면, $c$의 근방에서 정의된 좌표 변환 $\phi$가 존재하여:

$$f(\phi^{-1}(y)) = f(c) - y_1^2 - \cdots - y_k^2 + y_{k+1}^2 + \cdots + y_n^2$$

여기서 $k$는 헤시안 $H(c)$의 음의 고유값 개수(모스 지수, Morse index)다. 즉, 임계점 근처에서 함수는 단순한 이차형식(quadratic form)과 동등하게 행동한다.

**증명 개요:** 스펙트럼 정리로 $H(c)$를 대각화한 후, $f$의 2차 테일러 전개로부터 시작하여 점진적인 좌표 변환(모스의 완성제곱법, completing the square의 다변수 일반화)을 통해 이차형식을 표준형으로 변환한다.

**의미:** 비퇴화 임계점은 항상 "국소적으로 이차형식처럼" 행동한다. 이는 고차항이 국소적 형태에 영향을 주지 않음을 의미한다(정리 1에서 $o(\|h\|^2)$ 항이 극값 판정에 영향을 주지 않는 이유).

## 예제

**예제 1:** $f(x, y) = x^2 - y^2$의 $(0, 0)$을 분류하라.

**풀이:** $\nabla f = (2x, -2y)$, $\nabla f(0, 0) = (0, 0)$. $H = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$.

$\det H = -4 < 0$ → 안장점(saddle point).

$x$ 방향($y = 0$ 고정): $f(x, 0) = x^2$ → 아래로 볼록(극소). $y$ 방향($x = 0$ 고정): $f(0, y) = -y^2$ → 위로 볼록(극대). 이중성(duality)이 안장점의 특징이다.

**예제 2 (원숭이 안장, Monkey Saddle):** $f(x, y) = x^3 - 3xy^2$의 $(0, 0)$을 분류하라.

**풀이:** $\nabla f = (3x^2 - 3y^2, -6xy)$, $\nabla f(0, 0) = (0, 0)$.

$$H = \begin{pmatrix} 6x & -6y \\ -6y & -6x \end{pmatrix}, \quad H(0, 0) = \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix}$$

$\det H = 0$ → 판정 불가. 고차 항을 검사해야 한다.

극좌표 $x = r\cos\theta$, $y = r\sin\theta$에서:

$$f(r\cos\theta, r\sin\theta) = r^3(\cos^3\theta - 3\cos\theta\sin^2\theta) = r^3 \cos 3\theta$$

$\cos 3\theta$는 $3$번 부호를 바꾼다. 따라서 $(0, 0)$ 근처에서 $f$는 양수도 음수도 될 수 있다 → 안장점. "원숭이 안장"이라는 이름은 원숭이의 꼬리를 위한 세 번째 방향(두 다리 + 꼬리)이 있어 $z = x^3 - 3xy^2$가 3개의 "다리"를 가진 안장 모양이기 때문이다.

**예제 3:** $f(x, y, z) = x^2 + y^2 - z^2$의 $(0, 0, 0)$을 분류하라.

**풀이:** $\nabla f = (2x, 2y, -2z)$, $\nabla f(0, 0, 0) = 0$.

$$H = \begin{pmatrix} 2 & 0 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & -2 \end{pmatrix}$$

고유값: $2, 2, -2$. 양수 2개, 음수 1개 → 안장점. $(x, y)$ 평면 방향으로는 극소, $z$ 방향으로는 극대.

3차원 안장점의 예시로, $f(x, y, z) = \|x\|^2 - \|z\|^2$ 꼴이면 $(x, z)$가 혼합된 더 복잡한 안장점도 가능하다.

**예제 4:** $f(x, y) = x^4 + y^4 - 4xy + 2$의 임계점을 분류하라.

**풀이:** $\nabla f = (4x^3 - 4y, 4y^3 - 4x)$. $4x^3 = 4y$, $4y^3 = 4x$ → $y = x^3$, $x = y^3$.

$x = (x^3)^3 = x^9$ → $x^9 - x = x(x^8 - 1) = 0$ → $x = 0, \pm 1$.

임계점: $(0, 0)$, $(1, 1)$, $(-1, -1)$.

헤시안: $H = \begin{pmatrix} 12x^2 & -4 \\ -4 & 12y^2 \end{pmatrix}$.

**$(0, 0)$:** $H = \begin{pmatrix} 0 & -4 \\ -4 & 0 \end{pmatrix}$, $\det H = -16 < 0$ → 안장점.

**$(1, 1)$:** $H = \begin{pmatrix} 12 & -4 \\ -4 & 12 \end{pmatrix}$, $\det H = 144 - 16 = 128 > 0$, $f_{xx} = 12 > 0$ → 극소. $f(1, 1) = 1 + 1 - 4 + 2 = 0$.

**$(-1, -1)$:** $H = \begin{pmatrix} 12 & -4 \\ -4 & 12 \end{pmatrix}$, 극소. $f(-1, -1) = 1 + 1 - 4 + 2 = 0$.

**예제 5 (볼록 함수 — 전역 최소):** $f(x, y) = (x - 1)^2 + (y + 2)^2$의 모든 임계점을 찾고 분류하라.

**풀이:** $\nabla f = (2(x-1), 2(y+2)) = 0$ → $(1, -2)$가 유일한 임계점.

$$H = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$$

$\det H = 4 > 0$, $f_{xx} = 2 > 0$ → 극소. $H$가 모든 점에서 양정치이므로 $f$는 전역적으로 볼록(globally convex)하다. 따라서 $(1, -2)$는 전역 최소(global minimum)이며 $f(1, -2) = 0$이다.

**예제 6 (3차원 안장점):** $f(x, y, z) = xyz$의 $(0, 0, 0)$을 분류하라.

**풀이:** $\nabla f = (yz, xz, xy) = (0, 0, 0)$. $(0, 0, 0)$이 유일한 임계점.

$$H = \begin{pmatrix} 0 & z & y \\ z & 0 & x \\ y & x & 0 \end{pmatrix}, \quad H(0, 0, 0) = \begin{pmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$$

$\det H = 0$ → 판정 불가. 직접 조사:

- $f(t, 0, 0) = 0$ (일정)
- $f(t, t, t) = t^3$: $t > 0$에서 양, $t < 0$에서 음
- $f(t, t, -t) = -t^3$: $t > 0$에서 음, $t < 0$에서 양

따라서 $(0, 0, 0)$에서는 임의의 근방에 양수값과 음수값이 모두 존재하므로 안장점이다. 이는 3변수 함수에서 0인 고유값이 있어도 안장점이 될 수 있음을 보여준다.

**예제 7 (모스 지수 계산):** $f(x, y, z) = x^2 + y^2 - z^2$의 $(0, 0, 0)$에서 모스 지수(Morse index)를 구하라.

**풀이:** $H = \begin{pmatrix} 2 & 0 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & -2 \end{pmatrix}$, 고유값 $2, 2, -2$. 음의 고유값 개수 $= 1$($-2$ 하나). 따라서 모스 지수 $k = 1$.

모스 정리에 따르면 근처에서 $f$는 $-y_1^2 + y_2^2 + y_3^2$와 동등하며, 이는 $y_1$ 방향으로 오목(극대), $y_2, y_3$ 방향으로 볼록(극소)인 안장점임을 의미한다.

**예제 8 (판정 불가 — 고차 항의 영향):** $f(x, y) = x^4 + y^4$와 $g(x, y) = -x^4 - y^4$, $h(x, y) = x^4 - y^4$의 $(0, 0)$을 비교하라.

**풀이:** 세 함수 모두 $\nabla f(0, 0) = \nabla g(0, 0) = \nabla h(0, 0) = 0$이고, $H(0, 0) = \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix}$이다($\det H = 0$, 판정 불가).

- $f(x, y) = x^4 + y^4$: $(0, 0)$의 임의의 근방에서 $f(x, y) \geq 0 = f(0, 0)$이므로 극소.
- $g(x, y) = -x^4 - y^4$: $g(x, y) \leq 0 = g(0, 0)$이므로 극대.
- $h(x, y) = x^4 - y^4$: $(t, 0)$ 방향으로 $h(t, 0) = t^4 > 0$, $(0, t)$ 방향으로 $h(0, t) = -t^4 < 0$. 따라서 안장점.

헤시안이 0이면 4차 이상의 고차 항이 극값을 결정함을 보여준다.

**예제 9 (다중 극소 — 비볼록 함수):** $f(x) = \cos x$의 임계점을 분류하고 전역 최소 여부를 논하라.

**풀이:** $f'(x) = -\sin x = 0$ → $x = n\pi$ ($n \in \mathbb{Z}$). $f''(x) = -\cos x$.

- $n$이 짝수: $f''(n\pi) = -\cos(2k\pi) = -1 < 0$ → 극대
- $n$이 홀수: $f''(n\pi) = -\cos((2k+1)\pi) = 1 > 0$ → 극소

국소 최소는 무한히 많고, 모든 국소 최소값은 $-1$로 같다. 따라서 모두 전역 최소이기도 하다(비볼록 함수에서 여러 전역 최소가 공존하는 예).

## 연결

- **[스펙트럼 정리](topics/spectral-theorem.html)** : 헤시안의 고유값 부호가 극값 분류의 핵심이다.
- **[2계 도함수·헤시안·곡률](topics/second-derivatives.html)** : 헤시안 판정법의 상세한 조건을 다룬다.
- **[라그랑주 승수법](topics/lagrange-multipliers.html)** : 제약이 있는 경우의 극값 조건으로 확장한다.
- **[가우시안 과정](topics/gaussian-process.html)** : 볼록 함수의 성질이 최적화 이론에서 어떻게 활용되는지 안다.
