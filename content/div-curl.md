---
title: 발산·회전
slug: div-curl
---

## 직관적 설명

**벡터장(vector field)** $F: \mathbb{R}^3 \to \mathbb{R}^3$은 공간의 각 점에 벡터를 할당한다. 바람의 속도장, 유체의 흐름, 전자기장 등이 물리적 예시다.

**발산(divergence)** $\nabla \cdot F$는 한 점에서 벡터장이 "퍼져나가는(diverging)" 정도를 측정하는 스칼라 값이다. 양수면(source, 유체가 생겨남), 음수면(sink, 유체가 사라짐), 0이면 비압축(incompressible)이다. 발산은 각 방향으로의 변화율의 합이므로, 한 점 주변의 작은 부피에서 순 유출량(net outflow)을 나타낸다.

**회전(curl)** $\nabla \times F$는 벡터장의 "소용돌이(circulation)" 정도를 측정하는 벡터 값이다. 회전 벡터의 방향은 회전축, 크기는 회전 강도를 나타낸다. 예를 들어 $F = (-y, x, 0)$는 원점 주변을 반시계 방향으로 회전시키며, $\nabla \times F = (0, 0, 2)$로 $z$축 방향의 회전을 가리킨다.

두 연산자는 벡터 미적분의 기본 구성 요소이며, 그린-스토크스-가우스 정리들을 통해 적분과 연결된다.

---
## 정의

**벡터장 (vector field):** $F: \mathbb{R}^n \to \mathbb{R}^n$은 각 점에 벡터를 대응시키는 함수이다. 3차원에서 $F(x,y,z) = (P(x,y,z), Q(x,y,z), R(x,y,z))$로 표현한다.

**발산 (divergence):** 벡터장 $F = (P, Q, R)$의 발산은 나블라 연산자 $\nabla = (\partial/\partial x, \partial/\partial y, \partial/\partial z)$와 $F$의 내적(dot product)이다:

$$\nabla \cdot F = \frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y} + \frac{\partial R}{\partial z}$$

$F: \mathbb{R}^n \to \mathbb{R}^n$으로 일반화하면 $\nabla \cdot F = \sum_{i=1}^n \frac{\partial F_i}{\partial x_i}$.

**회전 (curl):** 3차원 벡터장 $F = (P, Q, R)$의 회전은 $\nabla$와 $F$의 외적(cross product)이다:

$$\nabla \times F = \left( \frac{\partial R}{\partial y} - \frac{\partial Q}{\partial z}, \; \frac{\partial P}{\partial z} - \frac{\partial R}{\partial x}, \; \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right)$$

행렬식 형태:

$$\nabla \times F = \det \begin{pmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ P & Q & R \end{pmatrix}$$

2차원 벡터장 $F = (P, Q)$의 회전은 스칼라 $\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}$로 정의되며 (그린 정리에서 등장), 이는 3차원 회전의 $z$-성분에 해당한다.

**라플라시안 (Laplacian):** 스칼라 함수 $f$의 라플라시안은 기울기의 발산이다:

$$\nabla^2 f = \nabla \cdot (\nabla f) = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} + \frac{\partial^2 f}{\partial z^2}$$

**벡터 라플라시안:** $\nabla^2 F = (\nabla^2 P, \nabla^2 Q, \nabla^2 R)$.

---
## 주요 정리와 증명

### 정리 1: $\nabla \cdot (\nabla \times F) = 0$

$F$가 $C^2$급(2계 편도함수가 연속)이면 발산의 회전은 항상 0이다.

**증명:** $F = (P, Q, R)$에 대해 직접 계산한다:

$$
\begin{aligned}
\nabla \cdot (\nabla \times F) &= \frac{\partial}{\partial x}\left(\frac{\partial R}{\partial y} - \frac{\partial Q}{\partial z}\right) + \frac{\partial}{\partial y}\left(\frac{\partial P}{\partial z} - \frac{\partial R}{\partial x}\right) + \frac{\partial}{\partial z}\left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right) \\
&= \frac{\partial^2 R}{\partial x \partial y} - \frac{\partial^2 Q}{\partial x \partial z} + \frac{\partial^2 P}{\partial y \partial z} - \frac{\partial^2 R}{\partial y \partial x} + \frac{\partial^2 Q}{\partial z \partial x} - \frac{\partial^2 P}{\partial z \partial y}
\end{aligned}
$$

$C^2$급 가정($\frac{\partial^2}{\partial x \partial y} = \frac{\partial^2}{\partial y \partial x}$)에 의해 클레로 정리(Clairaut's theorem, 혼합 편도함수의 대칭성)가 성립한다:

$$\frac{\partial^2 R}{\partial x \partial y} - \frac{\partial^2 R}{\partial y \partial x} = 0, \quad \frac{\partial^2 P}{\partial y \partial z} - \frac{\partial^2 P}{\partial z \partial y} = 0, \quad \frac{\partial^2 Q}{\partial z \partial x} - \frac{\partial^2 Q}{\partial x \partial z} = 0$$

따라서 모든 항이 상쇄되어 $\nabla \cdot (\nabla \times F) = 0$. $\square$

물리적 의미: 자기장 $B$는 $\nabla \cdot B = 0$을 만족한다(자기 단극자(magnetic monopole)는 존재하지 않음). 즉 $B = \nabla \times A$로 표현될 수 있다($A$는 벡터 퍼텐셜).

### 정리 2: $\nabla \times (\nabla f) = 0$

스칼라 함수 $f$가 $C^2$급이면 기울기의 회전은 항상 0이다.

**증명:** $\nabla f = (\partial f/\partial x, \partial f/\partial y, \partial f/\partial z)$의 회전을 계산한다:

$$
\begin{aligned}
\nabla \times (\nabla f) &= \left( \frac{\partial}{\partial y}\left(\frac{\partial f}{\partial z}\right) - \frac{\partial}{\partial z}\left(\frac{\partial f}{\partial y}\right), \;
\frac{\partial}{\partial z}\left(\frac{\partial f}{\partial x}\right) - \frac{\partial}{\partial x}\left(\frac{\partial f}{\partial z}\right), \;
\frac{\partial}{\partial x}\left(\frac{\partial f}{\partial y}\right) - \frac{\partial}{\partial y}\left(\frac{\partial f}{\partial x}\right) \right) \\
&= \left( \frac{\partial^2 f}{\partial y \partial z} - \frac{\partial^2 f}{\partial z \partial y}, \;
\frac{\partial^2 f}{\partial z \partial x} - \frac{\partial^2 f}{\partial x \partial z}, \;
\frac{\partial^2 f}{\partial x \partial y} - \frac{\partial^2 f}{\partial y \partial x} \right)
\end{aligned}
$$

$f \in C^2$이므로 혼합 편도함수가 같아 각 성분이 0이 된다. $\square$

두 정리(1, 2)는 벡터 미적분의 기본 identity들이다. 이들은 "회전의 발산 = 0"과 "기울기의 회전 = 0"이라는 중요한 연쇄 구조를 보여준다: $\text{grad} \to \text{curl} \to \text{div}$를 적용하면 두 번 연속 적용 시 0이 된다. 이는 미분형식(differential form)의 $d^2 = 0$에 대응한다.

### 정리 3: 보존장 판정 (Conservative Field Test)

단연결 영역(simply connected region) $D \subset \mathbb{R}^3$에서 $C^1$ 벡터장 $F$가 보존장(conservative field, 즉 $F = \nabla f$인 스칼라 퍼텐셜 $f$가 존재)이기 위한 필요충분조건은 $\nabla \times F = 0$이다.

**증명 (필요조건):** $F = \nabla f$이면 정리 2에 의해 $\nabla \times F = \nabla \times (\nabla f) = 0$.

**증명 (충분조건, 개요):** $\nabla \times F = 0$일 때, $F$가 보존장임을 보이려면 퍼텐셜 함수 $f$를 직접 구성한다. 기준점 $x_0$를 고정하고 경로 $C$를 따라 선적분으로 정의한다:

$$f(x) = \int_C F \cdot dr$$

단연결성과 $\nabla \times F = 0$은 이 적분이 경로에 무관함을 보장한다(스토크스 정리에 의해 임의의 닫힌 경로에서 적분이 0). $f$의 편도함수를 계산하면 $\nabla f = F$임을 확인할 수 있다. $\square$

물리적 예: 중력장 $F = -\frac{GMm}{r^2} \hat{r}$은 $\nabla \times F = 0$이며 퍼텐셜 $f = -GMm/r$을 가진다. 반면 소용돌이장 $F = (-y, x, 0)$은 $\nabla \times F \neq 0$이므로 보존장이 아니다.

### 정리 4: 발산의 물리적 의미

$F$가 유체의 속도장(velocity field)이라고 할 때, 점 $p$에서의 발산 $\nabla \cdot F(p)$는 $p$를 포함하는 작은 부피 $V_\epsilon$의 경계면을 통한 순 유출량(net flux)을 부피로 나눈 극한이다:

$$\nabla \cdot F(p) = \lim_{\epsilon \to 0} \frac{1}{|V_\epsilon|} \oiint_{\partial V_\epsilon} F \cdot dS$$

**증명 (직관):** 가우스 발산 정리(Gauss divergence theorem)에 의해 $\oiint_{\partial V_\epsilon} F \cdot dS = \iiint_{V_\epsilon} \nabla \cdot F\,dV$. $V_\epsilon$이 충분히 작으면 $\nabla \cdot F$가 거의 상수이므로 $\iiint_{V_\epsilon} \nabla \cdot F\,dV \approx \nabla \cdot F(p) \cdot |V_\epsilon|$. 따라서 위 극한이 성립한다. $\square$

이 결과는 발산이 점별 단위 부피당 플럭스(flux density)임을 보여준다. $\nabla \cdot F = 0$인 벡터장을 비압축(incompressible) 또는 솔레노이드(solenoidal) 장이라 한다.

### 정리 5: 라플라시안의 물리적 해석

라플라시안 $\nabla^2 f$는 점 $p$에서 함수값과 그 주변 평균값의 차이를 측정한다:

$$\nabla^2 f(p) = \lim_{\epsilon \to 0} \frac{2n}{\epsilon^2} \left( \frac{1}{|\partial B_\epsilon(p)|} \int_{\partial B_\epsilon(p)} f\,dS - f(p) \right)$$

즉, $\nabla^2 f > 0$이면 $p$의 함수값이 주변 평균보다 작고(오목), $\nabla^2 f < 0$이면 크다(볼록). 열방정식 $u_t = \nabla^2 u$에서 라플라시안은 온도가 퍼져나가는 정도를 결정한다.

---
## 예제

**예제 1 (발산과 회전 계산):** $F(x,y,z) = (x^2, y^2, z^2)$의 발산과 회전을 구하라.

**풀이:** 발산:

$$\nabla \cdot F = \frac{\partial}{\partial x}(x^2) + \frac{\partial}{\partial y}(y^2) + \frac{\partial}{\partial z}(z^2) = 2x + 2y + 2z = 2(x + y + z)$$

회전:

$$\nabla \times F = \left( \frac{\partial}{\partial y}(z^2) - \frac{\partial}{\partial z}(y^2), \; \frac{\partial}{\partial z}(x^2) - \frac{\partial}{\partial x}(z^2), \; \frac{\partial}{\partial x}(y^2) - \frac{\partial}{\partial y}(x^2) \right) = (0 - 0, 0 - 0, 0 - 0) = \mathbf{0}$$

$F$는 $F = \nabla(\frac{x^3 + y^3 + z^3}{3})$이므로 보존장이며, 따라서 회전이 0이다. $\square$

**예제 2 (회전의 기하학적 의미):** $F(x,y,z) = (-y, x, 0)$의 회전을 계산하고 그 의미를 설명하라.

**풀이:**

$$\nabla \times F = \left( \frac{\partial}{\partial y}(0) - \frac{\partial}{\partial z}(x), \; \frac{\partial}{\partial z}(-y) - \frac{\partial}{\partial x}(0), \; \frac{\partial}{\partial x}(x) - \frac{\partial}{\partial y}(-y) \right) = (0 - 0, 0 - 0, 1 - (-1)) = (0, 0, 2)$$

$F$는 $z$축 주변을 반시계 방향으로 회전시키는 장이며, 회전 $(0,0,2)$는 $z$축 방향으로 크기 2의 회전을 나타낸다. $(x,y)$ 평면에서 $F = (-y, x)$의 선적분 $\oint F \cdot dr$이 원의 면적의 2배임을 확인할 수 있으며, 이는 스토크스 정리와 일치한다. $\square$

**예제 3 (라플라시안 계산):** $f(x,y,z) = \frac{1}{\sqrt{x^2 + y^2 + z^2}}$ ($r = \|(x,y,z)\|$, 원점 제외)의 라플라시안을 구하라.

**풀이:** $r = (x^2 + y^2 + z^2)^{1/2}$라 하면 $f = r^{-1}$.

$$\frac{\partial f}{\partial x} = -\frac{x}{r^3}, \quad \frac{\partial^2 f}{\partial x^2} = -\frac{1}{r^3} + \frac{3x^2}{r^5}$$

같은 방식으로 $y$, $z$에 대해:

$$\frac{\partial^2 f}{\partial y^2} = -\frac{1}{r^3} + \frac{3y^2}{r^5}, \quad \frac{\partial^2 f}{\partial z^2} = -\frac{1}{r^3} + \frac{3z^2}{r^5}$$

합하면:

$$\nabla^2 f = -\frac{3}{r^3} + \frac{3(x^2 + y^2 + z^2)}{r^5} = -\frac{3}{r^3} + \frac{3r^2}{r^5} = -\frac{3}{r^3} + \frac{3}{r^3} = 0$$

따라서 $f = 1/r$는 $\mathbb{R}^3 \setminus \{0\}$에서 조화 함수(harmonic function, $\nabla^2 f = 0$)이다. 이는 전기장의 퍼텐셜과 중력 퍼텐셜이 라플라스 방정식을 만족함을 의미한다. $\square$

**예제 4 (발산을 통한 비압축성 확인):** $F(x,y,z) = (y, -x, z)$가 비압축 유체인지 판별하라.

**풀이:** 발산을 계산한다:

$$\nabla \cdot F = \frac{\partial}{\partial x}(y) + \frac{\partial}{\partial y}(-x) + \frac{\partial}{\partial z}(z) = 0 + 0 + 1 = 1 \neq 0$$

$\nabla \cdot F \neq 0$이므로 비압축성이 아니다. $z$ 방향으로 유체가 생성(source)되고 있다. $\square$

**예제 5 (벡터 identity 활용):** $\nabla \times (\nabla \times F)$를 발산과 라플라시안으로 표현하라.

**풀이:** 벡터 삼중곱(vector triple product) 항등식 $A \times (B \times C) = B(A \cdot C) - C(A \cdot B)$를 나블라 연산자에 적용하면:

$$\nabla \times (\nabla \times F) = \nabla(\nabla \cdot F) - \nabla^2 F$$

이 항등식은 전자기학의 맥스웰 방정식에서 파동 방정식을 유도할 때 핵심적으로 사용된다. 예를 들어 진공에서 $\nabla \times B = \mu_0 \epsilon_0 \frac{\partial E}{\partial t}$에 회전을 취하면 $E$에 대한 파동 방정식을 얻는다. $\square$

**예제 6 ($\nabla \cdot (\nabla \times F) = 0$ 수치 확인):** $F = (xz, yz, xy)$에 대해 $\nabla \cdot (\nabla \times F) = 0$을 확인하라.

**풀이:** 먼저 회전:

$$\nabla \times F = \left( \frac{\partial}{\partial y}(xy) - \frac{\partial}{\partial z}(yz), \; \frac{\partial}{\partial z}(xz) - \frac{\partial}{\partial x}(xy), \; \frac{\partial}{\partial x}(yz) - \frac{\partial}{\partial y}(xz) \right)$$

$$= (x - y, \; x - y, \; 0 - 0) = (x - y, x - y, 0)$$

발산:

$$\nabla \cdot (\nabla \times F) = \frac{\partial}{\partial x}(x-y) + \frac{\partial}{\partial y}(x-y) + \frac{\partial}{\partial z}(0) = 1 - 1 + 0 = 0$$

$\square$

---
## 연결

- **[텐서 연산](tensor-operations.html)** : 발산 $\nabla \cdot F$와 회전 $\nabla \times F$는 각각 벡터장의 1계 미분 연산자이며, 텐서 미적분에서 미분형식(differential form)의 외미분(exterior derivative)으로 일반화된다. $d^2 = 0$은 $\nabla \times (\nabla f) = 0$과 $\nabla \cdot (\nabla \times F) = 0$의 통합이다.
- **[선적분·면적분](line-surface-integrals.html)** : 발산과 회전은 각각 면적분(플럭스)과 선적분(순환)의 국소적 밀도로 해석된다. 스토크스 정리와 가우스 정리가 이 연결을 수학적으로 완성한다.
- **[그린·스토크스·가우스 정리](stokes-theorems.html)** : 발산-회전의 적분 버전인 이 세 정리는 벡터장의 국소적 성질(미분)과 대역적 성질(적분)을 연결한다.
