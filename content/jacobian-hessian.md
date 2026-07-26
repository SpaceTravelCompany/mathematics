---
title: 야코비안·헤시안
slug: jacobian-hessian
---

## 직관적 설명

**야코비안 행렬(Jacobian matrix)**은 다변수 벡터 함수 $f: \mathbb{R}^n \to \mathbb{R}^m$의 "전체 기울기 행렬"이다. 스칼라 함수의 그래디언트가 각 입력 변수에 대한 변화율을 벡터로 모은 것이라면, 야코비안은 출력의 각 성분 $f_i$에 대한 변화율을 행렬로 모은 것이다. $J_f$의 $(i,j)$ 성분은 $i$번째 출력이 $j$번째 입력에 의해 얼마나 민감하게 변하는지를 나타낸다.

**헤시안 행렬(Hessian matrix)**은 스칼라 함수 $f: \mathbb{R}^n \to \mathbb{R}$의 "곡률 행렬"이다. 헤시안 $H_f$의 $(i,j)$ 성분은 $\partial^2 f / \partial x_i \partial x_j$로, 함수의 2차 변화율을 측정한다. 헤시안은 그래디언트의 그래디언트, 즉 $\nabla f$의 야코비안으로 이해할 수 있다.

야코비안은 좌표 변환, 최적화, 로봇 공학(조작기의 속도 관계), 유체 역학(변형률)에서 필수적이다. 헤시안은 최적점의 분류(최소/최대/안장점), 뉴턴 방법(Newton's method)의 2차 최적화, 테일러 전개의 2차 항에서 핵심적인 역할을 한다.

## 정의

**야코비안 행렬 (Jacobian matrix):** 함수 $f: \mathbb{R}^n \to \mathbb{R}^m$이 $f(x) = (f_1(x), f_2(x), \ldots, f_m(x))^T$로 주어질 때, $x \in \mathbb{R}^n$에서의 야코비안 $J_f(x)$는 $m \times n$ 행렬이다:

$$J_f(x) = \frac{\partial f}{\partial x^T} = \begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\[4pt]
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \cdots & \frac{\partial f_2}{\partial x_n} \\[4pt]
\vdots & \vdots & \ddots & \vdots \\[4pt]
\frac{\partial f_m}{\partial x_1} & \frac{\partial f_m}{\partial x_2} & \cdots & \frac{\partial f_m}{\partial x_n}
\end{pmatrix}$$

간단히 $(J_f(x))_{ij} = \frac{\partial f_i}{\partial x_j}$로 쓴다.

**야코비안 행렬식 (Jacobian determinant):** $m = n$인 정사각형의 경우, $\det(J_f(x))$를 **야코비안**이라 부르기도 한다. 이는 $f$가 $x$ 근처에서 부피를 얼마나 확대·축소하는지를 나타낸다.

**헤시안 행렬 (Hessian matrix):** 함수 $f: \mathbb{R}^n \to \mathbb{R}$가 두 번 미분 가능할 때, $x \in \mathbb{R}^n$에서의 헤시안 $H_f(x)$는 $n \times n$ 행렬이다:

$$H_f(x) = \nabla^2 f(x) = \begin{pmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\[4pt]
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\[4pt]
\vdots & \vdots & \ddots & \vdots \\[4pt]
\frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{pmatrix}$$

간단히 $(H_f(x))_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}$.

**선형화 (linearization):** $f$의 1차 테일러 근사는 야코비안으로 표현된다:

$$f(x + \Delta x) \approx f(x) + J_f(x) \Delta x$$

이는 $f$를 $x$ 근처에서 선형 함수로 근사한 것이다.

**2차 근사 (quadratic approximation):** 스칼라 함수 $f$의 2차 테일러 근사는 헤시안을 포함한다:

$$f(x + \Delta x) \approx f(x) + \nabla f(x)^T \Delta x + \frac{1}{2} \Delta x^T H_f(x) \Delta x$$

헤시안 $H_f(x)$는 이 2차 항의 곡률을 결정한다.

## 주요 정리와 증명

### 정리 1: 헤시안의 대칭성 — 클레로 정리 (Clairaut's Theorem)

$f: \mathbb{R}^n \to \mathbb{R}$가 $C^2$ 함수(모든 2계 편도함수가 연속)이면, 혼합 편미분의 순서는 결과에 영향을 주지 않는다:

$$\frac{\partial^2 f}{\partial x_i \partial x_j} = \frac{\partial^2 f}{\partial x_j \partial x_i}$$

즉, 헤시안 $H_f(x)$는 대칭행렬(symmetric matrix)이다: $H_f^T = H_f$.

**증명:** $n = 2$인 경우를 증명한다 (일반 $n$은 성분별로 동일). $f: \mathbb{R}^2 \to \mathbb{R}$, $(x,y) \mapsto f(x,y)$에 대해 다음을 보이면 된다:

$$\frac{\partial^2 f}{\partial x \partial y} = \frac{\partial^2 f}{\partial y \partial x}$$

고정된 점 $(a,b)$에서 증명한다. 충분히 작은 $h, k \neq 0$에 대해 **2차 차분(second difference)** 을 정의한다:

$$\Delta(h,k) = f(a+h, b+k) - f(a+h, b) - f(a, b+k) + f(a, b)$$

이 $\Delta(h,k)$를 두 가지 방식으로 인수분해한다.

**방법 1:** $g(x) = f(x, b+k) - f(x, b)$라 정의하면:
$$\Delta(h,k) = g(a+h) - g(a)$$

평균값 정리(Mean Value Theorem)에 의해, 어떤 $\xi_1 \in (a, a+h)$가 존재하여:
$$\Delta(h,k) = g'(\xi_1) h = \left[ \frac{\partial f}{\partial x}(\xi_1, b+k) - \frac{\partial f}{\partial x}(\xi_1, b) \right] h$$

다시 평균값 정리를 $y$에 대해 적용하면, 어떤 $\eta_1 \in (b, b+k)$가 존재하여:
$$\Delta(h,k) = \frac{\partial^2 f}{\partial y \partial x}(\xi_1, \eta_1) \cdot hk$$

**방법 2:** $\tilde{g}(y) = f(a+h, y) - f(a, y)$라 정의하면 같은 과정을 통해 어떤 $(\xi_2, \eta_2)$에 대해:
$$\Delta(h,k) = \frac{\partial^2 f}{\partial x \partial y}(\xi_2, \eta_2) \cdot hk$$

두 표현이 같으므로:
$$\frac{\partial^2 f}{\partial y \partial x}(\xi_1, \eta_1) = \frac{\partial^2 f}{\partial x \partial y}(\xi_2, \eta_2)$$

$(h,k) \to (0,0)$의 극한을 취하면 $(\xi_1, \eta_1) \to (a,b)$, $(\xi_2, \eta_2) \to (a,b)$이다. 2계 편도함수의 연속성($C^2$ 가정)에 의해 극한이 존재하고 서로 같으므로:

$$\frac{\partial^2 f}{\partial y \partial x}(a,b) = \frac{\partial^2 f}{\partial x \partial y}(a,b)$$

$C^2$ 가정이 필수적임을 보이는 반례: $f(x,y) = \begin{cases} \frac{xy(x^2 - y^2)}{x^2 + y^2} & (x,y) \neq (0,0) \\ 0 & (x,y) = (0,0) \end{cases}$에서 $\frac{\partial^2 f}{\partial x \partial y}(0,0) = 1$, $\frac{\partial^2 f}{\partial y \partial x}(0,0) = -1$로 두 값이 다르다. 이 함수는 $(0,0)$에서 2계 편도함수가 불연속이다.

### 정리 2: 야코비안의 연쇄법칙 (Chain Rule for Jacobians)

$f: \mathbb{R}^n \to \mathbb{R}^m$이 $x \in \mathbb{R}^n$에서 미분 가능하고, $g: \mathbb{R}^m \to \mathbb{R}^p$가 $f(x) \in \mathbb{R}^m$에서 미분 가능할 때, 합성함수 $h = g \circ f: \mathbb{R}^n \to \mathbb{R}^p$의 야코비안은:

$$J_{g \circ f}(x) = J_g(f(x)) \cdot J_f(x)$$

즉, 야코비안의 곱으로 합성 함수의 전체 변화율을 구할 수 있다.

**증명:** $h_i(x) = g_i(f_1(x), \ldots, f_m(x))$라 하자. 연쇄법칙에 의해:

$$\frac{\partial h_i}{\partial x_j} = \sum_{k=1}^m \frac{\partial g_i}{\partial f_k} \cdot \frac{\partial f_k}{\partial x_j}$$

이는 $h_i$의 변화가 각 중간 변수 $f_k$를 통해 $x_j$로부터 전파됨을 의미한다. 행렬 형태로 쓰면:

$$(J_h(x))_{ij} = \sum_{k=1}^m (J_g(f(x)))_{ik} \cdot (J_f(x))_{kj}$$

이는 행렬곱 $J_g \cdot J_f$의 $(i,j)$ 성분과 정확히 일치한다.

**따름정리 (1차원 연쇄법칙 특수화):** $f: \mathbb{R}^n \to \mathbb{R}$, $g: \mathbb{R} \to \mathbb{R}$이면:
$$\nabla (g \circ f)(x) = g'(f(x)) \cdot \nabla f(x)$$

**따름정리 (변수 변환):** $\varphi: \mathbb{R}^n \to \mathbb{R}^n$이 가역 미분가능할 때:
$$\int_{D} f(x) \, dx = \int_{\varphi^{-1}(D)} f(\varphi(u)) \, |\det J_\varphi(u)| \, du$$

야코비안 행렬식은 이 변수 변환 공식(change of variables formula)에서 부피 확대율을 결정한다.

### 정리 3: 야코비안 행렬식과 부피 확대율

$f: \mathbb{R}^n \to \mathbb{R}^n$이 $C^1$ 함수이고 $x$에서 $J_f(x)$가 가역이면, $x$ 근처의 작은 영역의 부피는 $|\det J_f(x)|$배로 변환된다.

**서술:** $f$가 $x$에서 국소적 선형변환 $f(x + \Delta x) \approx f(x) + J_f(x) \Delta x$로 근사된다. 평행육면체(parallelepiped) $P = \{x + \sum_i t_i v_i \mid t_i \in [0,1]\}$의 상(image) $f(P)$의 부피는:
$$\text{vol}(f(P)) \approx |\det J_f(x)| \cdot \text{vol}(P)$$

이는 선형변환 $T(v) = J_f(x) v$가 단위 정육면체의 부피를 $|\det J_f(x)|$배로 변환한다는 사실에서 유도된다. 행렬식의 기하학적 의미가 야코비안 행렬식으로 자연스럽게 확장된 것이다.

**참고 (미분형식과의 연결):** 미분형식(differential form) 이론에서 야코비안은 $n$차 형식의 변환을 결정한다:
$$dy_1 \wedge \cdots \wedge dy_n = (\det J_f) \, dx_1 \wedge \cdots \wedge dx_n$$

이는 야코비안이 좌표 변환에서 부피 형식(volume form)을 어떻게 변환하는지를 나타낸다.

## 예제

**예제 1 (극좌표 변환의 야코비안):** 극좌표 변환 $T: (r, \theta) \mapsto (x, y)$를 $x = r\cos\theta$, $y = r\sin\theta$로 정의할 때 야코비안 행렬과 행렬식을 구하라.

**풀이:** 야코비안 행렬:
$$J_T(r, \theta) = \begin{pmatrix}
\frac{\partial x}{\partial r} & \frac{\partial x}{\partial \theta} \\[4pt]
\frac{\partial y}{\partial r} & \frac{\partial y}{\partial \theta}
\end{pmatrix} = \begin{pmatrix}
\cos\theta & -r\sin\theta \\
\sin\theta & r\cos\theta
\end{pmatrix}$$

야코비안 행렬식:
$$\det J_T = \cos\theta \cdot r\cos\theta - (-r\sin\theta) \cdot \sin\theta = r(\cos^2\theta + \sin^2\theta) = r$$

따라서 중적분의 변수 변환 공식에 의해 $dx\,dy = r\,dr\,d\theta$이다. 이는 극좌표에서 면적 요소가 $r$배 커짐을 의미한다.

**예제 2:** $f(x,y) = x^2 y + e^{xy}$의 헤시안을 구하라.

**풀이:** 먼저 1계 편도함수(그래디언트)를 계산한다:
$$\frac{\partial f}{\partial x} = 2xy + ye^{xy}, \quad \frac{\partial f}{\partial y} = x^2 + xe^{xy}$$

이제 2계 편도함수를 구한다:
$$\frac{\partial^2 f}{\partial x^2} = 2y + y^2 e^{xy}, \quad \frac{\partial^2 f}{\partial y^2} = x^2 e^{xy}$$
$$\frac{\partial^2 f}{\partial x \partial y} = 2x + e^{xy} + xye^{xy} = 2x + (1 + xy)e^{xy}$$
$$\frac{\partial^2 f}{\partial y \partial x} = 2x + e^{xy} + xye^{xy} = 2x + (1 + xy)e^{xy}$$

혼합 편도함수가 같음을 확인할 수 있다 ($C^\infty$ 함수이므로 클레로 정리 자동 만족). 헤시안:
$$H_f(x,y) = \begin{pmatrix}
2y + y^2 e^{xy} & 2x + (1 + xy)e^{xy} \\[4pt]
2x + (1 + xy)e^{xy} & x^2 e^{xy}
\end{pmatrix}$$

**예제 3 (2차 근사):** $f(x,y) = e^x \cos y$의 $(0,0)$에서 2차 테일러 근사를 구하라.

**풀이:** $f(0,0) = 1$. 그래디언트: $\nabla f = (e^x \cos y, -e^x \sin y)$, $\nabla f(0,0) = (1, 0)$.

헤시안:
$$H_f(x,y) = \begin{pmatrix}
e^x \cos y & -e^x \sin y \\
-e^x \sin y & -e^x \cos y
\end{pmatrix}, \quad H_f(0,0) = \begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}$$

2차 근사:
$$f(x,y) \approx 1 + (1, 0) \begin{pmatrix} x \\ y \end{pmatrix} + \frac{1}{2} (x, y) \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = 1 + x + \frac{1}{2}x^2 - \frac{1}{2}y^2$$

헤시안의 고유값이 $1$과 $-1$이므로 $(0,0)$은 안장점(saddle point)이다.

**예제 4:** $f(x,y,z) = x^2 + y^2 + z^2 + xy$의 헤시안을 구하고 양정치(positive definite) 여부를 판별하라.

**풀이:** 그래디언트: $\nabla f = (2x + y, 2y + x, 2z)^T$.

헤시안:
$$H_f = \begin{pmatrix}
2 & 1 & 0 \\
1 & 2 & 0 \\
0 & 0 & 2
\end{pmatrix}$$

주소행렬식(principal minor)을 계산한다: $\Delta_1 = 2 > 0$, $\Delta_2 = 2 \cdot 2 - 1 \cdot 1 = 3 > 0$, $\Delta_3 = 2 \cdot 3 = 6 > 0$. 따라서 $H_f$는 양정치이고, $f$는 전역적 최소값을 가진다.

**예제 5:** 함수 $f: \mathbb{R}^3 \to \mathbb{R}^2$, $f(x,y,z) = (x^2 + y, yz + x)$의 야코비안을 구하라.

**풀이:** $f_1 = x^2 + y$, $f_2 = yz + x$:
$$J_f = \begin{pmatrix}
\frac{\partial f_1}{\partial x} & \frac{\partial f_1}{\partial y} & \frac{\partial f_1}{\partial z} \\[4pt]
\frac{\partial f_2}{\partial x} & \frac{\partial f_2}{\partial y} & \frac{\partial f_2}{\partial z}
\end{pmatrix} = \begin{pmatrix}
2x & 1 & 0 \\
1 & z & y
\end{pmatrix}$$

**예제 6 (야코비안 연쇄법칙):** $f(u,v) = (u^2 + v, uv)$와 $g(x,y) = (x+y, x-y)$에 대해 $h = g \circ f$의 야코비안을 $f$의 점 $(1,1)$에서 구하라.

**풀이:** $f(1,1) = (2, 1)$. 각 야코비안:
$$J_f(1,1) = \begin{pmatrix}
2u & 1 \\
v & u
\end{pmatrix}_{(1,1)} = \begin{pmatrix}
2 & 1 \\
1 & 1
\end{pmatrix}, \quad J_g(2,1) = \begin{pmatrix}
1 & 1 \\
1 & -1
\end{pmatrix}$$

연쇄법칙:
$$J_h(1,1) = J_g(f(1,1)) \cdot J_f(1,1) = \begin{pmatrix}
1 & 1 \\
1 & -1
\end{pmatrix} \begin{pmatrix}
2 & 1 \\
1 & 1
\end{pmatrix} = \begin{pmatrix}
3 & 2 \\
1 & 0
\end{pmatrix}$$

**예제 7 (구면좌표):** 구면좌표 $(r, \theta, \phi) \to (x,y,z)$: $x = r\sin\theta\cos\phi$, $y = r\sin\theta\sin\phi$, $z = r\cos\theta$의 야코비안 행렬식을 구하라.

**풀이:** 야코비안 행렬:
$$J = \begin{pmatrix}
\sin\theta\cos\phi & r\cos\theta\cos\phi & -r\sin\theta\sin\phi \\
\sin\theta\sin\phi & r\cos\theta\sin\phi & r\sin\theta\cos\phi \\
\cos\theta & -r\sin\theta & 0
\end{pmatrix}$$

행렬식 계산:
$$\det J = r^2 \sin\theta$$

따라서 $dx\,dy\,dz = r^2 \sin\theta \, dr \, d\theta \, d\phi$이다.

## 연결

- **[행렬 미분](topics/matrix-calculus.html)** : 그래디언트는 야코비안의 특수한 경우($m=1$), 행렬 미분의 규칙들은 야코비안 연쇄법칙의 기초다.
- **[테일러 전개](topics/taylor-expansion.html)** : 헤시안은 2차 테일러 전개의 핵심이며, 1차 근사는 야코비안으로 표현된다.
- **[2계 도함수·헤시안·곡률](topics/second-derivatives.html)** : 헤시안의 고유값이 함수의 곡률과 극값 분류를 결정한다.
- **[다변수 연쇄법칙](topics/multivar-chain-rule.html)** : 야코비안 연쇄법칙은 스칼라 연쇄법칙의 다변수 일반화다.
