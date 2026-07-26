---
title: 선적분·면적분
slug: line-surface-integrals
---

## 직관적 설명

**선적분(line integral)** 은 곡선(curve)을 따라 함수를 적분하는 것이다. 스칼라 선적분 $\int_C f\,ds$는 곡선을 따라 밀도가 $f$인 선의 질량을 구한다. 벡터 선적분 $\int_C F \cdot dr$은 힘 $F$가 물체를 곡선 $C$를 따라 이동시킬 때 한 일(work)을 계산한다. 핵심은 "곡선을 따라 쪼개서 더한다"는 발상이며, 적분 구간이 직선이 아니라 곡선이라는 점이 1변수 적분과의 차이다.

**면적분(surface integral)** 은 곡면(surface)을 통과하는 플럭스(flux)를 계산한다. $\iint_S F \cdot dS$는 유체 속도장 $F$가 곡면 $S$를 통과하는 초당 유량(volume per unit time)을 나타낸다. 벡터장이 곡면에 수직으로 뚫고 나가는 정도를 측정하는 것이다.

**보존장(conservative field)** $F = \nabla f$에서는 선적분이 경로에 무관(path-independent)하며, 시작점과 끝점만으로 결정된다. 이는 중력장이나 정전기장에서 한 일이 경로와 무관하다는 물리적 사실을 반영한다.

---
## 정의

**매개변수화된 곡선 (parametrized curve):** $r(t) = (x(t), y(t), z(t))$, $a \leq t \leq b$. 곡선 $C$의 접선 벡터는 $r'(t) = (x'(t), y'(t), z'(t))$이고, 호의 길이 미분(arc length differential)은 $ds = \|r'(t)\|\,dt$이다.

**스칼라 선적분 (scalar line integral):** $f: \mathbb{R}^3 \to \mathbb{R}$의 곡선 $C$에 대한 선적분:

$$\int_C f\,ds = \int_a^b f(r(t)) \|r'(t)\|\,dt$$

$f = 1$이면 $\int_C 1\,ds = \int_a^b \|r'(t)\|\,dt$는 곡선의 길이(length)가 된다.

**벡터 선적분 (vector line integral, 일):** 벡터장 $F: \mathbb{R}^3 \to \mathbb{R}^3$의 곡선 $C$에 대한 선적분:

$$\int_C F \cdot dr = \int_a^b F(r(t)) \cdot r'(t)\,dt$$

$F$를 힘으로 해석하면, $F(r(t)) \cdot r'(t)$는 접선 방향의 힘 성분이고, $dt$를 곱해 적분하면 총 일(work)이 된다.

**닫힌 경로 선적분:** 곡선 $C$가 닫힌 곡선(시작점 = 끝점)일 때 $\oint_C F \cdot dr$로 표기한다.

**곡면의 매개변수화 (parametrized surface):** $r(u,v) = (x(u,v), y(u,v), z(u,v))$, $(u,v) \in D$. 편도함수 $r_u = \partial r/\partial u$, $r_v = \partial r/\partial v$는 곡면의 접평면을 생성한다.

**면적 요소 (surface area element):** $dS = \|r_u \times r_v\|\,du\,dv$. 이는 $r_u$와 $r_v$가 이루는 평행사변형의 넓이이며, 곡면의 국소적 확대율을 나타낸다.

**스칼라 면적분 (scalar surface integral):**

$$\iint_S f\,dS = \iint_D f(r(u,v)) \|r_u \times r_v\|\,du\,dv$$

$f = 1$이면 $\iint_S 1\,dS$는 곡면의 면적이 된다.

**벡터 면적분 (vector surface integral, 플럭스):**

$$\iint_S F \cdot dS = \iint_D F(r(u,v)) \cdot (r_u \times r_v)\,du\,dv$$

방향 $r_u \times r_v$는 곡면의 법선 벡터(normal vector)이며, $F \cdot (r_u \times r_v)$는 $F$가 곡면을 수직으로 뚫고 나가는 성분이다.

---
## 주요 정리와 증명

### 정리 1: 보존장의 경로 무관성 (Path Independence)

$F$가 영역 $D \subset \mathbb{R}^3$에서 연속인 벡터장이고 $F = \nabla f$($f$는 스칼라 퍼텐셜)이면, $D$ 내의 임의의 곡선 $C$ (시작점 $A$, 끝점 $B$)에 대해

$$\int_C F \cdot dr = f(B) - f(A)$$

즉, 선적분은 경로 $C$에 무관하고 오직 끝점에만 의존한다.

**증명:** $r(t)$, $a \leq t \leq b$가 $C$의 매개변수화이고 $r(a) = A$, $r(b) = B$라 하자. $F = \nabla f$이므로

$$
\begin{aligned}
\int_C F \cdot dr &= \int_a^b \nabla f(r(t)) \cdot r'(t)\,dt \\
&= \int_a^b \left( \frac{\partial f}{\partial x} \frac{dx}{dt} + \frac{\partial f}{\partial y} \frac{dy}{dt} + \frac{\partial f}{\partial z} \frac{dz}{dt} \right) dt
\end{aligned}
$$

이는 연쇄법칙에 의해 $\frac{d}{dt} f(r(t))$와 같다:

$$\int_C F \cdot dr = \int_a^b \frac{d}{dt} f(r(t))\,dt = f(r(b)) - f(r(a)) = f(B) - f(A)$$

마지막 등식은 미적분학의 기본정리(FTC)에 의한다. $\square$

이 정리는 중력장에서 물체를 어떤 경로로 이동시키든 한 일이 같다는 물리 법칙의 수학적 표현이다.

### 정리 2: 닫힌 경로에서 보존장의 선적분

$F$가 보존장($F = \nabla f$)이면 임의의 닫힌 곡선 $C$에 대해

$$\oint_C F \cdot dr = 0$$

**증명:** 닫힌 곡선은 $A = B$이므로 정리 1에 의해 $\oint_C F \cdot dr = f(A) - f(A) = 0$. $\square$

역으로, 단연결 영역에서 $\oint_C F \cdot dr = 0$이 모든 닫힌 곡선에 대해 성립하면 $F$는 보존장이다. 이는 $\nabla \times F = 0$과 동치이다(div-curl의 정리 3 참조).

### 정리 3: 면적 요소 $\|r_u \times r_v\|\,du\,dv$의 유도

곡면 $S$가 $r(u,v)$로 매개변수화될 때, $S$ 위의 작은 곡선 사각형의 면적은 $\|r_u \times r_v\|\,\Delta u\,\Delta v$로 근사된다.

**증명:** $(u_0, v_0)$에서 $u$ 방향과 $v$ 방향으로 각각 $\Delta u$, $\Delta v$만큼 변화했을 때의 점을 생각한다:

$$r(u_0 + \Delta u, v_0) \approx r(u_0, v_0) + r_u(u_0, v_0) \Delta u$$

$$r(u_0, v_0 + \Delta v) \approx r(u_0, v_0) + r_v(u_0, v_0) \Delta v$$

곡면 위의 곡선 사각형의 변은 각각 $r_u \Delta u$와 $r_v \Delta v$로 근사된다. 이 두 벡터가 이루는 평행사변형의 넓이는 외적의 크기와 같다:

$$\text{Area} \approx \|(r_u \Delta u) \times (r_v \Delta v)\| = \|r_u \times r_v\| \,\Delta u \,\Delta v$$

극한 $\Delta u, \Delta v \to 0$에서 면적 요소 $dS = \|r_u \times r_v\|\,du\,dv$를 얻는다. $\square$

**면적분의 방향:** 법선 벡터 $n = r_u \times r_v$의 방향이 곡면의 방향(orientation)을 결정한다. 폐곡면(closed surface)에서는 $n$이 바깥쪽을 가리키도록 표준화한다.

### 정리 4: 선적분의 기본 성질

선적분은 선형성(linearity)과 가법성(additivity)을 만족한다.

**선형성:** 상수 $\alpha, \beta$와 곡선 $C$에 대해

$$\int_C (\alpha F + \beta G) \cdot dr = \alpha \int_C F \cdot dr + \beta \int_C G \cdot dr$$

**곡선의 합 (additivity):** $C = C_1 \cup C_2$($C_1$의 끝점 = $C_2$의 시작점)이면

$$\int_C F \cdot dr = \int_{C_1} F \cdot dr + \int_{C_2} F \cdot dr$$

**방향 반전 (orientation reversal):** $-C$가 $C$의 역방향(reverse orientation) 곡선일 때

$$\int_{-C} F \cdot dr = -\int_C F \cdot dr$$

이 성질들은 정의와 리만 합의 선형성에서 직접 유도된다.

---
## 예제

**예제 1 (선적분 — 일 계산):** $F(x,y) = (y, x)$를 $C$: 원 $x^2 + y^2 = 1$의 상반부(반시계 방향)를 따라 적분하라.

**풀이:** $r(t) = (\cos t, \sin t)$, $0 \leq t \leq \pi$로 매개변수화한다.

$r'(t) = (-\sin t, \cos t)$, $F(r(t)) = (\sin t, \cos t)$.

$$F \cdot r' = (\sin t)(-\sin t) + (\cos t)(\cos t) = -\sin^2 t + \cos^2 t = \cos 2t$$

$$\int_C F \cdot dr = \int_0^{\pi} \cos 2t\,dt = \left[ \frac{\sin 2t}{2} \right]_0^{\pi} = 0$$

$\square$

$F = (y, x)$는 $F = \nabla(xy)$이므로 보존장이다. 따라서 닫힌 경로에서 적분이 0임이 정리 2와 일치한다.

**예제 2 (선적분 — 보존장 확인과 퍼텐셜):** $F(x,y) = (2xy, x^2 + 1)$이 보존장인지 확인하고, 보존장이면 퍼텐셜 함수를 구하라.

**풀이:** $\nabla \times F$의 $z$성분(2차원 회전)을 계산한다:

$$\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = \frac{\partial}{\partial x}(x^2 + 1) - \frac{\partial}{\partial y}(2xy) = 2x - 2x = 0$$

$\mathbb{R}^2$는 단연결이므로 $F$는 보존장이다. 퍼텐셜 $f$를 찾는다:

$\partial f/\partial x = 2xy$이므로 $f(x,y) = \int 2xy\,dx = x^2 y + g(y)$.

$\partial f/\partial y = x^2 + g'(y) = x^2 + 1$이므로 $g'(y) = 1$, $g(y) = y + C$.

따라서 $F = \nabla f$ where $f(x,y) = x^2 y + y + C$.

검증: $\partial f/\partial x = 2xy$, $\partial f/\partial y = x^2 + 1$. $\square$

**예제 3 (면적분 — 포물면 위 플럭스):** $F(x,y,z) = (0, 0, -z)$의 포물면 $S: z = x^2 + y^2$, $0 \leq z \leq 1$ 위로의 플럭스(상향)를 구하라.

**풀이:** $r(x,y) = (x, y, x^2 + y^2)$, $(x,y) \in D: x^2 + y^2 \leq 1$.

$$r_x = (1, 0, 2x), \quad r_y = (0, 1, 2y)$$

$$r_x \times r_y = \det \begin{pmatrix} i & j & k \\ 1 & 0 & 2x \\ 0 & 1 & 2y \end{pmatrix} = (-2x, -2y, 1)$$

상향 법선 벡터는 $z$성분이 양수인 $n = (-2x, -2y, 1)$이다.

$$F(r(x,y)) = (0, 0, -(x^2 + y^2))$$

$$F \cdot (r_x \times r_y) = 0 \cdot (-2x) + 0 \cdot (-2y) + (-(x^2+y^2)) \cdot 1 = -(x^2 + y^2)$$

플럭스:

$$\iint_S F \cdot dS = \iint_D -(x^2 + y^2)\,dx\,dy$$

극좌표 변환: $x = r\cos\theta$, $y = r\sin\theta$, $dx\,dy = r\,dr\,d\theta$:

$$= \int_0^{2\pi} \int_0^1 -(r^2) \cdot r\,dr\,d\theta = -2\pi \int_0^1 r^3\,dr = -2\pi \cdot \frac{1}{4} = -\frac{\pi}{2}$$

$\square$

플럭스가 음수이므로 $F$가 곡면을 아래에서 위로 통과하는 방향과 반대(즉, 아래 방향으로 더 많이 흐름)임을 의미한다.

**예제 4 (스칼라 선적분 — 곡선의 질량):** 밀도 $f(x,y) = x + y$인 선분 $C: y = x^2$, $0 \leq x \leq 1$의 질량을 구하라.

**풀이:** $r(t) = (t, t^2)$, $0 \leq t \leq 1$. $r'(t) = (1, 2t)$, $\|r'(t)\| = \sqrt{1 + 4t^2}$.

$$\int_C (x + y)\,ds = \int_0^1 (t + t^2) \sqrt{1 + 4t^2}\,dt$$

이 적분은 치환 $u = 1 + 4t^2$ ($du = 8t\,dt$)으로 계산한다. 먼저 $t\sqrt{1+4t^2}$ 항과 $t^2\sqrt{1+4t^2}$ 항을 분리한다:

$$\int_0^1 t\sqrt{1+4t^2}\,dt = \frac{1}{8} \int_1^5 \sqrt{u}\,du = \frac{1}{8} \cdot \frac{2}{3}(5^{3/2} - 1) = \frac{1}{12}(5\sqrt{5} - 1)$$

$t^2\sqrt{1+4t^2}$ 항은 삼각치환 $2t = \tan\theta$로 계산 가능하다. $\square$

**예제 5 (면적분 — 곡면의 면적):** 구면 $x^2 + y^2 + z^2 = R^2$의 표면적을 면적분으로 유도하라.

**풀이:** 구면 매개변수화: $r(\phi,\theta) = (R\sin\phi\cos\theta, R\sin\phi\sin\theta, R\cos\phi)$, $\phi \in [0,\pi]$, $\theta \in [0, 2\pi)$.

$$r_\phi = (R\cos\phi\cos\theta, R\cos\phi\sin\theta, -R\sin\phi)$$
$$r_\theta = (-R\sin\phi\sin\theta, R\sin\phi\cos\theta, 0)$$

$$r_\phi \times r_\theta = \det \begin{pmatrix} i & j & k \\ R\cos\phi\cos\theta & R\cos\phi\sin\theta & -R\sin\phi \\ -R\sin\phi\sin\theta & R\sin\phi\cos\theta & 0 \end{pmatrix}$$

계산:

$$= (R^2\sin^2\phi\cos\theta, R^2\sin^2\phi\sin\theta, R^2\sin\phi\cos\phi)$$

크기:

$$\|r_\phi \times r_\theta\| = R^2\sqrt{\sin^4\phi(\cos^2\theta+\sin^2\theta) + \sin^2\phi\cos^2\phi} = R^2\sqrt{\sin^4\phi + \sin^2\phi\cos^2\phi}$$

$$= R^2\sqrt{\sin^2\phi(\sin^2\phi + \cos^2\phi)} = R^2\sqrt{\sin^2\phi} = R^2\sin\phi \quad (\phi \in [0,\pi], \sin\phi \geq 0)$$

면적:

$$A = \iint_S 1\,dS = \int_0^{2\pi} \int_0^{\pi} R^2\sin\phi\,d\phi\,d\theta = 2\pi R^2 [-\cos\phi]_0^{\pi} = 2\pi R^2(1+1) = 4\pi R^2$$

$\square$

---
## 연결

- **[그린·스토크스·가우스 정리](stokes-theorems.html)** : 선적분과 면적분은 각각 그린 정리, 스토크스 정리, 가우스 정리를 통해 2중적분·3중적분과 연결된다. 이 정리들은 곡선/곡면의 경계(boundary)에서의 적분을 내부 영역의 적분으로 변환한다.
- **[발산·회전](div-curl.html)** : 벡터 선적분 $\int_C F \cdot dr$은 회전 $\nabla \times F$와, 면적분 $\iint_S F \cdot dS$는 발산 $\nabla \cdot F$와 각각 대응된다. 이는 스토크스 정리와 가우스 정리의 핵심이다.
- **[다중적분](multiple-integrals.html)** : 면적분과 선적분은 각각 2중적분과 1변수 적분으로 변환되어 계산된다. 야코비안 $|J|$와 면적 요소 $\|r_u \times r_v\|$는 모두 좌표 변환에 따른 부피(면적) 요소의 변화율을 나타낸다는 공통점이 있다.
