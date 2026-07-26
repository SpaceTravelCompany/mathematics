---
title: 다중적분
slug: multiple-integrals
---

## 직관적 설명

**다중적분(multiple integral)** 은 1변수 리만 적분을 2차원·3차원으로 확장한 것이다. 2중적분(double integral) $\iint_D f\,dA$는 곡면 아래의 부피(volume)를 계산하고, 3중적분(triple integral) $\iiint_E f\,dV$는 밀도 함수 $f$가 주어진 3차원 물체의 질량(mass)을 구한다. $f = 1$로 두면 각각 영역 $D$의 면적과 $E$의 부피가 된다.

확률론에서 2중적분은 두 확률변수의 결합 확률밀도함수(joint PDF)를 적분하여 확률을 계산하는 데 사용된다: $P((X,Y) \in D) = \iint_D f(x,y)\,dA$.

좌표 변환(coordinate transformation)은 적분 영역을 더 간단한 형태로 바꾸거나 대칭성을 활용하기 위해 필수적이다. 극좌표(polar), 원통좌표(cylindrical), 구면좌표(spherical)로의 변환은 각각 원형·원통형·구형 대칭 문제에서 야코비안(Jacobian) 행렬식을 통해 부피 요소를 보정한다.

## 정의

**2중적분 (double integral):** 유계 영역 $D \subset \mathbb{R}^2$ 위에서 정의된 함수 $f: D \to \mathbb{R}$의 2중적분은 리만 합의 극한으로 정의된다. $D$를 작은 직사각형들로 분할하고 각각의 넓이 $\Delta A$와 함수값의 곱을 더한 뒤, 분할을 세밀하게 하는 극한이다:

$$\iint_D f(x,y)\,dA = \lim_{\|\Delta\| \to 0} \sum_{i=1}^n f(x_i^*, y_i^*) \Delta A_i$$

**반복적분 (iterated integral):** $D$가 $x$-단순 영역 $a \leq x \leq b$, $g_1(x) \leq y \leq g_2(x)$일 때 2중적분은 반복적분으로 계산된다:

$$\iint_D f(x,y)\,dA = \int_a^b \int_{g_1(x)}^{g_2(x)} f(x,y)\,dy\,dx$$

푸비니 정리(Fubini's theorem)는 $f$가 연속일 때 적분 순서를 바꿔도 결과가 같음을 보장한다:

$$\iint_D f(x,y)\,dA = \int_a^b \int_{g_1(x)}^{g_2(x)} f(x,y)\,dy\,dx = \int_c^d \int_{h_1(y)}^{h_2(y)} f(x,y)\,dx\,dy$$

**3중적분 (triple integral):** 3차원 영역 $E \subset \mathbb{R}^3$에서의 적분:

$$\iiint_E f(x,y,z)\,dV = \int_{x=a}^b \int_{y=g_1(x)}^{g_2(x)} \int_{z=h_1(x,y)}^{h_2(x,y)} f(x,y,z)\,dz\,dy\,dx$$

**극좌표 변환 (polar coordinates):** $x = r\cos\theta$, $y = r\sin\theta$일 때 면적 요소는

$$dA = dx\,dy = r\,dr\,d\theta$$

따라서

$$\iint_D f(x,y)\,dA = \iint_{D'} f(r\cos\theta, r\sin\theta)\, r\,dr\,d\theta$$

**원통좌표 변환 (cylindrical coordinates):** $x = r\cos\theta$, $y = r\sin\theta$, $z = z$일 때

$$dV = dx\,dy\,dz = r\,dr\,d\theta\,dz$$

**구면좌표 변환 (spherical coordinates):** $x = \rho\sin\phi\cos\theta$, $y = \rho\sin\phi\sin\theta$, $z = \rho\cos\phi$ ($\rho \geq 0$, $0 \leq \phi \leq \pi$, $0 \leq \theta < 2\pi$)일 때

$$dV = \rho^2\sin\phi\,d\rho\,d\phi\,d\theta$$

**야코비안 (Jacobian):** 일반 변환 $T: (u,v) \mapsto (x(u,v), y(u,v))$에 대해, 야코비안 행렬식은 부피 요소의 변환율이다:

$$J = \left|\frac{\partial(x,y)}{\partial(u,v)}\right| = \left| \det \begin{pmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \end{pmatrix} \right|$$

$$dx\,dy = |J|\,du\,dv$$

3차원에서는 $dx\,dy\,dz = |J|\,du\,dv\,dw$이며

$$J = \left|\frac{\partial(x,y,z)}{\partial(u,v,w)}\right| = \left| \det \begin{pmatrix} x_u & x_v & x_w \\ y_u & y_v & y_w \\ z_u & z_v & z_w \end{pmatrix} \right|$$

## 주요 정리와 증명

### 정리 1: 푸비니 정리 (Fubini's Theorem)

$f$가 직사각형 $R = [a,b] \times [c,d]$에서 연속이면

$$\iint_R f(x,y)\,dA = \int_a^b \int_c^d f(x,y)\,dy\,dx = \int_c^d \int_a^b f(x,y)\,dx\,dy$$

**증명 (개요):** 고정된 $x$에 대해 $A(x) = \int_c^d f(x,y)\,dy$를 정의하자. $A(x)$는 $x$의 연속함수이며 $x$ 단면의 면적을 나타낸다. $A(x)$를 $[a,b]$에서 적분하면

$$\iint_R f(x,y)\,dA = \int_a^b A(x)\,dx = \int_a^b \left( \int_c^d f(x,y)\,dy \right) dx$$

같은 논리를 $y$에 대해 반복하면 적분 순서 교환이 가능하다. 완전한 증명은 리만 합의 이중 극한과 균등연속성(uniform continuity)을 사용한다. $\square$

푸비니 정리는 적분 영역이 직사각형이 아닌 일반 영역에서도 성립하며, 이 경우 반복적분의 적분 구간이 변수의 함수가 된다. $f$의 연속성은 충분조건이며, 유계 불연속 집합이 영측도(null set)이면 여전히 성립한다.

### 정리 2: 극좌표 변환의 야코비안

변환 $T: (r,\theta) \mapsto (x,y) = (r\cos\theta, r\sin\theta)$의 야코비안 행렬식은 $r$이다.

**증명:** 야코비안 행렬은

$$\frac{\partial(x,y)}{\partial(r,\theta)} = \begin{pmatrix} \frac{\partial x}{\partial r} & \frac{\partial x}{\partial \theta} \\ \frac{\partial y}{\partial r} & \frac{\partial y}{\partial \theta} \end{pmatrix} = \begin{pmatrix} \cos\theta & -r\sin\theta \\ \sin\theta & r\cos\theta \end{pmatrix}$$

행렬식은

$$\det = (\cos\theta)(r\cos\theta) - (-r\sin\theta)(\sin\theta) = r\cos^2\theta + r\sin^2\theta = r(\cos^2\theta + \sin^2\theta) = r$$

야코비안은 절댓값 $|J| = |r| = r$ ($r \geq 0$)이다. 따라서 $dA = |J|\,dr\,d\theta = r\,dr\,d\theta$. $\square$

기하학적 해석: 극좌표에서 $dr$와 $d\theta$ 변화에 따른 면적 요소는 반지름 $r$의 호(arc)의 길이 $r\,d\theta$와 반경 방향 $dr$의 곱이므로 $r\,dr\,d\theta$가 된다.

### 정리 3: 구면좌표 변환의 야코비안

변환 $T: (\rho,\phi,\theta) \mapsto (x,y,z) = (\rho\sin\phi\cos\theta, \rho\sin\phi\sin\theta, \rho\cos\phi)$의 야코비안 행렬식은 $\rho^2\sin\phi$이다.

**증명:** 편도함수를 계산한다:

$$
\begin{aligned}
x_\rho &= \sin\phi\cos\theta, & x_\phi &= \rho\cos\phi\cos\theta, & x_\theta &= -\rho\sin\phi\sin\theta \\
y_\rho &= \sin\phi\sin\theta, & y_\phi &= \rho\cos\phi\sin\theta, & y_\theta &= \rho\sin\phi\cos\theta \\
z_\rho &= \cos\phi, & z_\phi &= -\rho\sin\phi, & z_\theta &= 0
\end{aligned}
$$

야코비안 행렬식:

$$
\begin{aligned}
\frac{\partial(x,y,z)}{\partial(\rho,\phi,\theta)} &=
\det \begin{pmatrix}
\sin\phi\cos\theta & \rho\cos\phi\cos\theta & -\rho\sin\phi\sin\theta \\
\sin\phi\sin\theta & \rho\cos\phi\sin\theta & \rho\sin\phi\cos\theta \\
\cos\phi & -\rho\sin\phi & 0
\end{pmatrix}
\end{aligned}
$$

3열에 대해 여인수 전개(cofactor expansion)한다:

$$
\begin{aligned}
&= (-\rho\sin\phi\sin\theta) \cdot \det\begin{pmatrix}\sin\phi\sin\theta & \rho\cos\phi\sin\theta \\ \cos\phi & -\rho\sin\phi\end{pmatrix} \\
&\qquad - (\rho\sin\phi\cos\theta) \cdot \det\begin{pmatrix}\sin\phi\cos\theta & \rho\cos\phi\cos\theta \\ \cos\phi & -\rho\sin\phi\end{pmatrix} \\
&\qquad + 0
\end{aligned}
$$

첫 번째 항:

$$(-\rho\sin\phi\sin\theta)[(\sin\phi\sin\theta)(-\rho\sin\phi) - (\rho\cos\phi\sin\theta)(\cos\phi)]$$
$$= (-\rho\sin\phi\sin\theta)[-\rho\sin^2\phi\sin\theta - \rho\cos^2\phi\sin\theta]$$
$$= (-\rho\sin\phi\sin\theta)[-\rho\sin\theta(\sin^2\phi + \cos^2\phi)]$$
$$= (-\rho\sin\phi\sin\theta)(-\rho\sin\theta) = \rho^2\sin\phi\sin^2\theta$$

두 번째 항:

$$-(\rho\sin\phi\cos\theta)[(\sin\phi\cos\theta)(-\rho\sin\phi) - (\rho\cos\phi\cos\theta)(\cos\phi)]$$
$$= -(\rho\sin\phi\cos\theta)[-\rho\sin^2\phi\cos\theta - \rho\cos^2\phi\cos\theta]$$
$$= -(\rho\sin\phi\cos\theta)[-\rho\cos\theta] = \rho^2\sin\phi\cos^2\theta$$

합하면:

$$\det = \rho^2\sin\phi(\sin^2\theta + \cos^2\theta) = \rho^2\sin\phi$$

$\rho \geq 0$, $0 \leq \phi \leq \pi$에서 $\sin\phi \geq 0$이므로 $|J| = \rho^2\sin\phi$이고 $dV = \rho^2\sin\phi\,d\rho\,d\phi\,d\theta$. $\square$

### 정리 4: 일반 변수 변환 공식 (Change of Variables)

$T: D' \subset \mathbb{R}^2 \to D \subset \mathbb{R}^2$가 연속적으로 미분가능하고 일대일이며 야코비안 $J(u,v) \neq 0$인 변환이라 하자. $f$가 $D$에서 연속이면

$$\iint_D f(x,y)\,dx\,dy = \iint_{D'} f(x(u,v), y(u,v))\,|J(u,v)|\,du\,dv$$

**증명 (직관):** $D'$의 작은 직사각형 $[u, u+\Delta u] \times [v, v+\Delta v]$를 생각하자. $T$에 의해 이 영역은 $D$ 속의 곡선 사각형(cuvi-linear rectangle)으로 사상된다. $T$의 일차 근사(first-order approximation)를 사용하면, 이 곡선 사각형은 야코비안 행렬 $DT$로 근사된 평행사변형이 되며, 그 넓이는 $|\det(DT)|\,\Delta u\,\Delta v = |J(u,v)|\,\Delta u\,\Delta v$이다. 따라서 $f(x,y)\,dx\,dy \approx f(T(u,v))\,|J(u,v)|\,du\,dv$이고, 분할을 세밀하게 하면 위 적분 공식을 얻는다. $\square$

엄밀한 증명은 미분동형사상(diffeomorphism)의 역함수 정리와 리만 합의 변환을 사용한다.

### 정리 5: 3중적분에서 $f=1$일 때 부피

$$\text{Vol}(E) = \iiint_E 1\,dV$$

**증명:** $E$가 $x \in [a,b]$, $g_1(x) \leq y \leq g_2(x)$, $h_1(x,y) \leq z \leq h_2(x,y)$로 주어질 때

$$\iiint_E 1\,dV = \int_a^b \int_{g_1(x)}^{g_2(x)} \int_{h_1(x,y)}^{h_2(x,y)} 1\,dz\,dy\,dx$$

내부 적분: $\int_{h_1}^{h_2} 1\,dz = h_2(x,y) - h_1(x,y)$는 $(x,y)$에서의 수직 길이. $y$에 대해 적분하면 단면적 $A(x)$, $x$에 대해 적분하면 부피가 된다. $\square$

## 예제

**예제 1 (극좌표로 가우시안 적분):** $\int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}$임을 2중적분으로 증명하라.

**풀이:** $I = \int_{-\infty}^{\infty} e^{-x^2}\,dx$라 하자. $I^2$를 2중적분으로 나타낸다:

$$I^2 = \left(\int_{-\infty}^{\infty} e^{-x^2}\,dx\right)\left(\int_{-\infty}^{\infty} e^{-y^2}\,dy\right) = \iint_{\mathbb{R}^2} e^{-(x^2+y^2)}\,dx\,dy$$

극좌표로 변환한다: $x^2 + y^2 = r^2$, $dx\,dy = r\,dr\,d\theta$, 영역 $\mathbb{R}^2$는 $r \in [0, \infty)$, $\theta \in [0, 2\pi)$:

$$I^2 = \int_0^{2\pi} \int_0^{\infty} e^{-r^2} \cdot r\,dr\,d\theta$$

내부 적분: $u = r^2$, $du = 2r\,dr$로 치환하면 $\int_0^{\infty} r e^{-r^2}\,dr = \frac{1}{2}\int_0^{\infty} e^{-u}\,du = \frac{1}{2}$.

따라서 $I^2 = \int_0^{2\pi} \frac{1}{2}\,d\theta = \pi$이고, $I = \sqrt{\pi}$ (양수이므로). $\square$

이 증명은 극좌표 변환과 야코비안 없이는 어렵다. $e^{-x^2}$의 부정적분이 초등함수로 표현되지 않기 때문이다.

**예제 2 (구면좌표로 구의 부피):** 반지름 $R$인 구의 부피를 구면좌표 변환으로 계산하라.

**풀이:** 구 $E = \{ (x,y,z) \mid x^2 + y^2 + z^2 \leq R^2 \}$의 부피:

$$V = \iiint_E 1\,dV = \int_0^{2\pi} \int_0^{\pi} \int_0^R \rho^2\sin\phi\,d\rho\,d\phi\,d\theta$$

$\rho$ 적분: $\int_0^R \rho^2\,d\rho = \frac{R^3}{3}$.

$\phi$ 적분: $\int_0^{\pi} \sin\phi\,d\phi = [-\cos\phi]_0^{\pi} = -(-1) - (-1) = 2$.

$\theta$ 적분: $\int_0^{2\pi} d\theta = 2\pi$.

$$V = \frac{R^3}{3} \cdot 2 \cdot 2\pi = \frac{4\pi R^3}{3}$$

$\square$

**예제 3 (타원 영역 위 2중적분):** 타원 $\frac{x^2}{a^2} + \frac{y^2}{b^2} \leq 1$의 면적을 구하라.

**풀이:** 변수 변환 $x = a u$, $y = b v$를 적용한다. 이 변환의 야코비안:

$$J = \left|\frac{\partial(x,y)}{\partial(u,v)}\right| = \left| \det \begin{pmatrix} a & 0 \\ 0 & b \end{pmatrix} \right| = ab$$

영역은 단위원 $u^2 + v^2 \leq 1$이 된다:

$$A = \iint_D 1\,dx\,dy = \iint_{u^2+v^2 \leq 1} ab\,du\,dv = ab \cdot \text{Area}(u^2+v^2 \leq 1) = ab \cdot \pi = \pi ab$$

$\square$

일반적인 접근법: 타원을 선형변환으로 원으로 바꾸고, 단위원의 넓이 $\pi$를 곱한다. 야코비안 $ab$는 선형변환이 면적을 $ab$배 확대함을 의미한다.

**예제 4 (3중적분 — 사면체의 질량):** 밀도 $f(x,y,z) = xyz$인 사면체 $x \geq 0$, $y \geq 0$, $z \geq 0$, $x + y + z \leq 1$의 질량을 구하라.

**풀이:**

$$M = \iiint_E xyz\,dV = \int_{x=0}^1 \int_{y=0}^{1-x} \int_{z=0}^{1-x-y} xyz\,dz\,dy\,dx$$

$z$ 적분: $\int_0^{1-x-y} z\,dz = \frac{1}{2}(1-x-y)^2$.

$$M = \int_0^1 \int_0^{1-x} \frac{1}{2}xy(1-x-y)^2\,dy\,dx$$

$y$ 적분: $u = 1-x-y$, $du = -dy$로 치환하면 $y = 1-x-u$:

$$\frac{1}{2}x \int_{u=1-x}^{0} (1-x-u)u^2(-du) = \frac{1}{2}x \int_0^{1-x} [(1-x)u^2 - u^3]\,du$$

$$= \frac{1}{2}x\left[ (1-x)\frac{u^3}{3} - \frac{u^4}{4} \right]_0^{1-x} = \frac{1}{2}x\left[ \frac{(1-x)^4}{3} - \frac{(1-x)^4}{4} \right] = \frac{1}{2}x \cdot \frac{(1-x)^4}{12} = \frac{x(1-x)^4}{24}$$

$x$ 적분: $\int_0^1 \frac{x(1-x)^4}{24}\,dx$.

$t = 1-x$로 치환하면 $x = 1-t$, $dx = -dt$:

$$\frac{1}{24} \int_1^0 (1-t)t^4(-dt) = \frac{1}{24} \int_0^1 (t^4 - t^5)\,dt = \frac{1}{24}\left[ \frac{t^5}{5} - \frac{t^6}{6} \right]_0^1 = \frac{1}{24} \cdot \frac{1}{30} = \frac{1}{720}$$

$\square$

**예제 5 (원통좌표 활용):** 원기둥 $x^2 + y^2 \leq R^2$, $0 \leq z \leq H$의 부피를 원통좌표로 계산하라.

**풀이:** 원통좌표 $x = r\cos\theta$, $y = r\sin\theta$, $z = z$, $dV = r\,dr\,d\theta\,dz$:

$$V = \int_{z=0}^H \int_{\theta=0}^{2\pi} \int_{r=0}^R r\,dr\,d\theta\,dz = H \cdot 2\pi \cdot \frac{R^2}{2} = \pi R^2 H$$

$\square$

## 연결

- **[적분의 의미](integral-meaning.html)** : 1변수 리만 적분의 개념을 2차원·3차원으로 확장한 것이 다중적분이다. 미적분학의 기본정리는 선적분에서도 경로 무관성(path independence)의 형태로 일반화된다.
- **[야코비안·헤시안](jacobian-hessian.html)** : 변수 변환 공식에서 등장하는 야코비안 행렬식 $|J|$는 좌표 변환에 따른 부피 요소의 변화율이다. 야코비안 행렬 자체는 다변수 함수의 일차 근사(linear approximation)를 나타내며, 헤시안은 이차 근사를 담당한다.
- **[발산·회전](div-curl.html)** : 3중적분의 변수 변환과 야코비안은 벡터장의 발산(divergence)과 회전(curl)의 정의에서도 중요한 역할을 한다.
