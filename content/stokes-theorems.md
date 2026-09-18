---
title: 그린·스토크스·가우스 정리
slug: stokes-theorems
---

> 학습 순서 47 / 75 · [처음부터 읽기](math-language.html)

## 작은 예제로 시작하기

**앞에서 가져올 것:** 선적분은 경로를 따라, 플럭스 적분은 표면을 가로질러 흐름을 더한다. 회전과 발산은 그 흐름의 국소적인 변화다.

바둑판의 각 작은 칸을 반시계 방향으로 한 바퀴 돌며 흐름을 더한다고 생각하자. 이웃 두 칸이 공유하는 변에서는 한쪽이 위로, 다른 쪽이 아래로 지나가므로 기여가 상쇄된다. 모든 칸을 합치면 바깥 테두리만 남는다. 이것이 내부의 회전과 경계의 순환을 연결하는 그린·스토크스 정리의 직관이다.

$F=(-y/2,x/2)$는 2차원 회전이 1이다. 단위원 내부에 대해 회전을 적분하면 넓이인 $\pi$다. 경계를 $r(t)=(\cos t,\sin t)$로 쓰면 $F(r(t))\cdot r'(t)=1/2$이고, $0$부터 $2\pi$까지 적분해도 $\pi$다.

가우스 정리에서는 상자들을 붙인다. 공유 면으로 한 상자에서 나간 흐름은 다른 상자로 들어간 흐름이므로 상쇄된다. 전체 내부의 발산을 더하면 바깥 표면의 순 유출량만 남는다.

**증명으로 이어 읽기:** 바깥 경계를 반시계로 돌면 내부가 왼쪽에 오도록 하는 식으로 방향을 일관되게 정해야 한다. 구멍의 안쪽 경계는 반대로 돈다. 장 안에 특이점이 있거나 필요한 미분이 존재하지 않으면 정리를 그대로 적용할 수 없으며, 먼저 정리의 영역과 매끄러움 조건을 읽는다.

---

## 직관적 설명

**그린 정리(Green's theorem), 스토크스 정리(Stokes' theorem), 가우스 발산 정리(Gauss divergence theorem)** 는 벡터 미적분의 세 거대한 정리들이다. 이들은 모두 하나의 통일된 원리를 표현한다: **"경계(boundary)에서의 적분 = 내부(interior)에서의 미분의 적분"**.

- **그린 정리:** 평면 영역 $D$의 경계 곡선 $\partial D$에서의 선적분 = $D$ 내부에서의 회전(2차원)의 2중적분.
- **스토크스 정리:** 곡면 $S$의 경계 곡선 $\partial S$에서의 선적분 = $S$ 위에서의 회전(3차원)의 면적분.
- **가우스 정리:** 입체 $V$의 경계 곡면 $\partial V$에서의 플럭스(면적분) = $V$ 내부에서의 발산의 3중적분.

이 통일성은 미분형식(differential form)의 언어에서 **일반화된 스토크스 정리(Generalized Stokes' theorem)** $\int_{\partial\Omega} \omega = \int_\Omega d\omega$로 완성된다. 여기서 $\omega$는 미분형식, $d\omega$는 외미분(exterior derivative), $\partial\Omega$는 $\Omega$의 경계다.

물리학에서 이 정리들은 전자기학의 맥스웰 방정식을 적분 형태와 미분 형태로 변환하는 데 핵심적이다. 유체역학, 열역학, 양자역학에도 응용된다.

---
## 정의

**그린 정리 (Green's Theorem):** $D \subset \mathbb{R}^2$가 단순 닫힌 곡선(simple closed curve) $C = \partial D$로 둘러싸인 영역이고, $P, Q: D \to \mathbb{R}$가 $C^1$급이면

$$\oint_{\partial D} (P\,dx + Q\,dy) = \iint_D \left( \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right) dA$$

$C$는 반시계 방향(counterclockwise)으로 향한다.

**스토크스 정리 (Stokes' Theorem):** $S \subset \mathbb{R}^3$가 방향이 지정된(oriented) 곡면이고 $C = \partial S$가 그 경계 곡선($S$의 방향과 일관된 방향)일 때, $C^1$급 벡터장 $F$에 대해

$$\oint_{\partial S} F \cdot dr = \iint_S (\nabla \times F) \cdot dS$$

즉, 경계에서의 선적분 = 곡면에서의 회전의 면적분.

**가우스 발산 정리 (Gauss Divergence Theorem):** $V \subset \mathbb{R}^3$가 유계 영역이고 $\partial V$가 그 경계 곡면(바깥쪽 방향)일 때, $C^1$급 벡터장 $F$에 대해

$$\oiint_{\partial V} F \cdot dS = \iiint_V \nabla \cdot F\,dV$$

즉, 폐곡면을 통한 플럭스 = 내부 발산의 3중적분.

**일반화된 스토크스 정리 (Generalized Stokes' Theorem):** $\Omega$가 방향이 지정된 $k$차원 다양체(manifold)이고 $\partial\Omega$가 그 경계($k-1$차원)일 때, $(k-1)$-미분형식 $\omega$에 대해

$$\int_{\partial\Omega} \omega = \int_\Omega d\omega$$

여기서 $d\omega$는 $\omega$의 외미분(exterior derivative)이다.

### 차원별 대응

| 정리 | 차원 | $\Omega$ | $\partial\Omega$ | $d\omega$ 대응 |
|------|------|----------|-----------------|----------------|
| 미적분학 기본정리 | 1 | $[a, b]$ | $\{a, b\}$ | $f'(x)\,dx$ |
| 그린 정리 | 2 | $D \subset \mathbb{R}^2$ | $\partial D$ (곡선) | $(\partial Q/\partial x - \partial P/\partial y)\,dA$ |
| 스토크스 정리 | 2(곡면) | $S \subset \mathbb{R}^3$ | $\partial S$ (곡선) | $(\nabla \times F) \cdot dS$ |
| 가우스 정리 | 3 | $V \subset \mathbb{R}^3$ | $\partial V$ (곡면) | $(\nabla \cdot F)\,dV$ |

---
## 주요 정리와 증명

### 정리 1: 그린 정리 (Green's Theorem) 증명

영역 $D$가 $x$-단순(type I)이면서 동시에 $y$-단순(type II)이라고 가정한다. 즉,

$$D = \{(x,y) : a \le x \le b,\; g_1(x) \le y \le g_2(x)\} = \{(x,y) : c \le y \le d,\; h_1(y) \le x \le h_2(y)\}$$

경계 $\partial D$는 반시계 방향(counterclockwise)으로 향한다. 다음 두 등식을 각각 증명하면 그린 정리가 완성된다.

$$\oint_{\partial D} Q\,dy = \iint_D \frac{\partial Q}{\partial x}\,dA, \qquad \oint_{\partial D} P\,dx = -\iint_D \frac{\partial P}{\partial y}\,dA$$

**$Q$ 부분 증명 ($x$-단순 영역):** $D$를 $x$-단순 영역으로 표현하자. 이중적분을 반복적분으로 바꾸고 미적분학의 기본정리(FTC)를 적용하면

$$\iint_D \frac{\partial Q}{\partial x}\,dA = \int_a^b \int_{g_1(x)}^{g_2(x)} \frac{\partial Q}{\partial x}(x,y)\,dy\,dx = \int_a^b \left[ Q(x, g_2(x)) - Q(x, g_1(x)) \right] dx$$

한편 경계 $\partial D$는 반시계 방향으로 다음 네 조각으로 나뉜다.

- $C_1$ (아래): $y = g_1(x)$, $x$가 $a \to b$
- $C_2$ (오른쪽): $x = b$, $y$가 $g_1(b) \to g_2(b)$
- $C_3$ (위): $y = g_2(x)$, $x$가 $b \to a$ (역방향)
- $C_4$ (왼쪽): $x = a$, $y$가 $g_2(a) \to g_1(a)$ (역방향)

$\oint_{\partial D} Q\,dy$를 각 조각에서 계산한다.

$$\oint_{\partial D} Q\,dy = \int_a^b Q(x, g_1(x)) g_1'(x)\,dx - \int_a^b Q(x, g_2(x)) g_2'(x)\,dx + \int_{g_1(b)}^{g_2(b)} Q(b,y)\,dy - \int_{g_1(a)}^{g_2(a)} Q(a,y)\,dy$$

이제 라이프니츠 적분 규칙(Leibniz integral rule)을 적용한다.

$$\frac{d}{dx}\int_{g_1(x)}^{g_2(x)} Q(x,y)\,dy = \int_{g_1(x)}^{g_2(x)} \frac{\partial Q}{\partial x}\,dy + Q(x, g_2(x)) g_2'(x) - Q(x, g_1(x)) g_1'(x)$$

양변을 $a$부터 $b$까지 적분하고 FTC를 쓰면

$$\int_{g_1(b)}^{g_2(b)} Q(b,y)\,dy - \int_{g_1(a)}^{g_2(a)} Q(a,y)\,dy = \iint_D \frac{\partial Q}{\partial x}\,dA + \int_a^b \left[ Q(x, g_2(x)) g_2'(x) - Q(x, g_1(x)) g_1'(x) \right] dx$$

항을 재배열하면

$$\iint_D \frac{\partial Q}{\partial x}\,dA = \int_a^b \left[ Q(x, g_1(x)) g_1'(x) - Q(x, g_2(x)) g_2'(x) \right] dx + \int_{g_1(b)}^{g_2(b)} Q(b,y)\,dy - \int_{g_1(a)}^{g_2(a)} Q(a,y)\,dy$$

우변은 위에서 구한 $\oint_{\partial D} Q\,dy$와 정확히 일치한다. 따라서 $\oint_{\partial D} Q\,dy = \iint_D \frac{\partial Q}{\partial x}\,dA$이다. ✓

**$P$ 부분 증명 ($y$-단순 영역):** 완전히 대칭적인 논법으로, $D$를 $y$-단순 영역 $c \le y \le d$, $h_1(y) \le x \le h_2(y)$로 표현한다. FTC에 의해

$$\iint_D \frac{\partial P}{\partial y}\,dA = \int_c^d \int_{h_1(y)}^{h_2(y)} \frac{\partial P}{\partial y}\,dx\,dy = \int_c^d \left[ P(h_2(y), y) - P(h_1(y), y) \right] dy$$

경계 $\partial D$를 반시계 방향으로 아래변($y=c$, $x$: $h_1(c)\to h_2(c)$), 오른변($x=h_2(y)$, $y$: $c\to d$), 위변($y=d$, $x$: $h_2(d)\to h_1(d)$), 왼변($x=h_1(y)$, $y$: $d\to c$)으로 나눈다. $\oint_{\partial D} P\,dx$를 계산하면

$$\oint_{\partial D} P\,dx = \int_{h_1(c)}^{h_2(c)} P(x,c)\,dx - \int_{h_1(d)}^{h_2(d)} P(x,d)\,dx + \int_c^d \left[ P(h_2(y), y) h_2'(y) - P(h_1(y), y) h_1'(y) \right] dy$$

라이프니츠 규칙을 $\frac{d}{dy}\int_{h_1(y)}^{h_2(y)} P(x,y)\,dx$에 적용하고 $Q$ 부분과 동일하게 정리하면

$$\oint_{\partial D} P\,dx = -\iint_D \frac{\partial P}{\partial y}\,dA$$

를 얻는다. ✓

두 결과를 더하면 그린 정리가 성립한다.

$$\oint_{\partial D} (P\,dx + Q\,dy) = \iint_D \left( \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right) dA$$

$\square$

그린 정리는 유한 개의 단순 영역의 합집합(경계가 유한 개의 조각으로 이루어진 영역)으로 확장할 수 있다. 인접 영역 사이의 공유 경계에서 선적분이 서로 상쇄되기 때문이다.

### 정리 2: 가우스 발산 정리 (Gauss Divergence Theorem)

직육면체 $V = [a_1, b_1] \times [a_2, b_2] \times [a_3, b_3]$에서 $F = (P, Q, R)$에 대해 증명한다. 일반 영역은 분할과 근사로 확장된다.

**증명 (직육면체):** 세 성분을 각각 증명한다.

$$\oiint_{\partial V} F \cdot dS = \oiint_{\partial V} (P, Q, R) \cdot dS = \oiint_{\partial V} P\,dy\,dz + \oiint_{\partial V} Q\,dz\,dx + \oiint_{\partial V} R\,dx\,dy$$

**$R$ 성분:** $\oiint_{\partial V} R\,dx\,dy$는 $V$의 윗면과 아랫면에서만 기여한다(측면에서는 $dS$의 $z$성분이 0).

- 윗면($z = b_3$): 법선 $(0,0,1)$, $dS = (0,0,dx\,dy)$, $\iint R(x,y,b_3)\,dx\,dy$
- 아랫면($z = a_3$): 법선 $(0,0,-1)$, $dS = (0,0,-dx\,dy)$, $-\iint R(x,y,a_3)\,dx\,dy$

$$\oiint_{\partial V} R\,dx\,dy = \iint_{[a_1,b_1]\times[a_2,b_2]} [R(x,y,b_3) - R(x,y,a_3)]\,dx\,dy$$

미적분학의 기본정리에 의해:

$$R(x,y,b_3) - R(x,y,a_3) = \int_{a_3}^{b_3} \frac{\partial R}{\partial z}(x,y,z)\,dz$$

따라서

$$\oiint_{\partial V} R\,dx\,dy = \iiint_V \frac{\partial R}{\partial z}\,dV$$

같은 방법으로 $P$ 성분은 $x$ 방향, $Q$ 성분은 $y$ 방향에 대해:

$$\oiint_{\partial V} P\,dy\,dz = \iiint_V \frac{\partial P}{\partial x}\,dV, \quad \oiint_{\partial V} Q\,dz\,dx = \iiint_V \frac{\partial Q}{\partial y}\,dV$$

세 결과를 합하면:

$$\oiint_{\partial V} F \cdot dS = \iiint_V \left( \frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y} + \frac{\partial R}{\partial z} \right) dV = \iiint_V \nabla \cdot F\,dV$$

$\square$

일반 영역으로의 확장은 영역을 작은 직육면체로 분할하고, 내부 경계면의 적분이 상쇄됨(cancellation)을 이용한다. 각 작은 직육면체에서 정리를 적용하고 합산하면, 내부 면에서의 플럭스가 서로 소멸하고 외부 경계면의 플럭스만 남는다.

### 정리 3: 스토크스 정리 — 그린 정리의 3차원 일반화

스토크스 정리는 그린 정리를 곡면으로 확장한 것이다. $F = (P, Q, R)$, 곡면 $S$가 $z = f(x,y)$로 주어졌을 때(간단한 경우) 스토크스 정리는 그린 정리로 환원됨을 보일 수 있다.

**증명 개요:** $S$가 함수 그래프 $z = f(x,y)$, $(x,y) \in D$이고 경계 $C = \partial S$가 $xy$-평면으로 사영된 곡선 $C' = \partial D$에 대응된다고 하자.

$\iint_S (\nabla \times F) \cdot dS$를 계산하여 $\oint_{\partial S} F \cdot dr$과 같음을 보인다.

$$\iint_S (\nabla \times F) \cdot dS = \iint_D (\nabla \times F) \cdot (-f_x, -f_y, 1)\,dx\,dy$$

이를 전개하면 그린 정리의 형태가 되어 $\oint_{\partial D} (P + R f_x)\,dx + (Q + R f_y)\,dy = \oint_{\partial S} F \cdot dr$와 일치함을 확인할 수 있다. $\square$

### 정리 4: 세 정리의 통일 구조

그린, 스토크스, 가우스 정리는 모두 다음 통일 원리의 특수한 경우다:

**"경계에서의 적분 = 내부에서의 미분의 적분"**

$$\int_{\partial\Omega} \omega = \int_\Omega d\omega$$

이것이 일반화된 스토크스 정리(Generalized Stokes' Theorem)이며, 미분형식(differential form)의 언어로 표현된다.

| 정리 | $\omega$ | $d\omega$ | 해석 |
|------|----------|-----------|------|
| FTC | $f$ (0-형식) | $f'\,dx$ (1-형식) | $\int_a^b f' = f(b) - f(a)$ |
| 그린 | $P\,dx + Q\,dy$ (1-형식) | $(\partial Q/\partial x - \partial P/\partial y)\,dx \wedge dy$ (2-형식) | $\oint P\,dx + Q\,dy = \iint (\partial Q/\partial x - \partial P/\partial y)\,dA$ |
| 스토크스 | $F \cdot dr$ (1-형식) | $(\nabla \times F) \cdot dS$ (2-형식) | $\oint F \cdot dr = \iint (\nabla \times F) \cdot dS$ |
| 가우스 | $F \cdot dS$ (2-형식) | $\nabla \cdot F\,dV$ (3-형식) | $\oiint F \cdot dS = \iiint \nabla \cdot F\,dV$ |

---
## 예제

**예제 1 (그린 정리로 타원 넓이):** 타원 $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$의 넓이를 그린 정리로 구하라.

**풀이:** 그린 정리에서 $P = -y/2$, $Q = x/2$로 두면

$$\iint_D \left( \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right) dA = \iint_D \left( \frac{1}{2} - \left(-\frac{1}{2}\right) \right) dA = \iint_D 1\,dA = \text{Area}(D)$$

한편 $\oint_{\partial D} P\,dx + Q\,dy = \frac{1}{2} \oint_{\partial D} (-y\,dx + x\,dy)$.

타원의 매개변수화: $x = a\cos t$, $y = b\sin t$, $0 \leq t \leq 2\pi$.

$dx = -a\sin t\,dt$, $dy = b\cos t\,dt$.

$$\begin{aligned}
\text{Area} &= \frac{1}{2} \oint (-y\,dx + x\,dy) \\
&= \frac{1}{2} \int_0^{2\pi} [-(b\sin t)(-a\sin t) + (a\cos t)(b\cos t)]\,dt \\
&= \frac{1}{2} \int_0^{2\pi} (ab\sin^2 t + ab\cos^2 t)\,dt = \frac{ab}{2} \int_0^{2\pi} dt = \pi ab
\end{aligned}$$

$\square$

이 접근법은 "플래니미터(planimeter)"라는 면적 측정 장치의 수학적 원리다.

**예제 2 (가우스 정리로 구 위 플럭스):** $F(x,y,z) = (x^3, y^3, z^3)$의 반지름 $R$인 구면 $S$를 통한 플럭스를 가우스 정리로 계산하라.

**풀이:** 발산을 계산한다:

$$\nabla \cdot F = 3x^2 + 3y^2 + 3z^2 = 3(x^2 + y^2 + z^2) = 3r^2$$

가우스 정리에 의해:

$$\oiint_S F \cdot dS = \iiint_V 3(x^2 + y^2 + z^2)\,dV = 3 \iiint_V r^2\,dV$$

구면좌표 변환: $dV = \rho^2\sin\phi\,d\rho\,d\phi\,d\theta$, $r^2 = \rho^2$:

$$
\begin{aligned}
&= 3 \int_0^{2\pi} \int_0^{\pi} \int_0^R \rho^2 \cdot \rho^2 \sin\phi\,d\rho\,d\phi\,d\theta \\
&= 3 \int_0^{2\pi} d\theta \int_0^{\pi} \sin\phi\,d\phi \int_0^R \rho^4\,d\rho \\
&= 3 \cdot 2\pi \cdot 2 \cdot \frac{R^5}{5} = \frac{12\pi R^5}{5}
\end{aligned}
$$

직접 면적분으로 계산하는 것보다 가우스 정리가 훨씬 간단하다. $\square$

**예제 3 (스토크스 정리 — 선적분 ↔ 면적분):** $F = (-y, x, z)$를 $z = 4 - x^2 - y^2$ ($z \geq 0$) 위의 곡면 $S$의 경계 $C$를 따라 적분하라. 스토크스 정리를 이용하라.

**풀이:** 스토크스 정리에 의해 $\oint_C F \cdot dr = \iint_S (\nabla \times F) \cdot dS$.

회전 계산:

$$\nabla \times F = \left( \frac{\partial}{\partial y}(z) - \frac{\partial}{\partial z}(x), \; \frac{\partial}{\partial z}(-y) - \frac{\partial}{\partial x}(z), \; \frac{\partial}{\partial x}(x) - \frac{\partial}{\partial y}(-y) \right) = (0 - 0, 0 - 0, 1 - (-1)) = (0, 0, 2)$$

곡면 $S$: $z = f(x,y) = 4 - x^2 - y^2$, $(x,y) \in D: x^2 + y^2 \leq 4$ (상향 방향).

상향 법선: $(-f_x, -f_y, 1) = (2x, 2y, 1)$ (상향, $z$성분 양수).

$$\iint_S (0, 0, 2) \cdot dS = \iint_D (0, 0, 2) \cdot (2x, 2y, 1)\,dx\,dy = \iint_D 2\,dx\,dy = 2 \cdot \text{Area}(D) = 2 \cdot 4\pi = 8\pi$$

$\square$

따라서 $\oint_C F \cdot dr = 8\pi$이다. 직접 선적분($C: x^2 + y^2 = 4$, $z = 0$)으로도 확인 가능하다: $r(t) = (2\cos t, 2\sin t, 0)$ → $F = (-2\sin t, 2\cos t, 0)$, $r' = (-2\sin t, 2\cos t, 0)$ → $F \cdot r' = 4\sin^2 t + 4\cos^2 t = 4$ → $\int_0^{2\pi} 4\,dt = 8\pi$.

**예제 4 (그린 정리 — 복잡한 경로의 선적분):** $\oint_C (y^2\,dx + 3xy\,dy)$를 계산하라. $C$는 $y = \sin x$와 $x$축이 $x \in [0, \pi]$에서 이루는 폐곡선(반시계 방향).

**풀이:** $P = y^2$, $Q = 3xy$. 그린 정리 적용:

$$\oint_C (y^2\,dx + 3xy\,dy) = \iint_D \left( \frac{\partial}{\partial x}(3xy) - \frac{\partial}{\partial y}(y^2) \right) dA = \iint_D (3y - 2y)\,dA = \iint_D y\,dA$$

$D$는 $0 \leq x \leq \pi$, $0 \leq y \leq \sin x$:

$$\iint_D y\,dA = \int_0^{\pi} \int_0^{\sin x} y\,dy\,dx = \int_0^{\pi} \left[ \frac{y^2}{2} \right]_0^{\sin x} dx = \frac{1}{2} \int_0^{\pi} \sin^2 x\,dx = \frac{1}{2} \cdot \frac{\pi}{2} = \frac{\pi}{4}$$

$\square$

그린 정리가 없다면 세 조각의 경로(아래 직선 + 위 곡선 + 양 끝 수직선)를 각각 적분해야 했을 것이다.

---
## 연결

- **[발산·회전](div-curl.html)** : 그린·스토크스·가우스 정리는 발산과 회전이라는 국소적 미분 연산자를 대역적 적분과 연결한다. $\nabla \cdot (\nabla \times F) = 0$과 $\nabla \times (\nabla f) = 0$은 $d^2 = 0$의 표현이며, 이 정리들의 일관성을 보장한다.
- **[선적분·면적분](line-surface-integrals.html)** : 이 정리들은 선적분과 면적분을 더 낮은 차원(또는 높은 차원)의 적분으로 변환하는 도구다. 보존장의 경로 무관성은 스토크스 정리의 직접적 결과다.
- **[다중적분](multiple-integrals.html)** : 가우스 정리의 증명에서 직육면체 분할과 3중적분이 사용된다. 그린 정리의 $x$-단순·$y$-단순 영역 분할은 2중적분의 반복적분 계산 방식과 동일하다.

---

[← 이전: 선적분·면적분](line-surface-integrals.html) · [다음: 상미분방정식 기초 →](ode-basics.html)
