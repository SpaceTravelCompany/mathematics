---
title: 양정치 행렬
slug: positive-definite
---

## 직관적 설명

**양정치(positive definite)** 행렬은 "모든 방향에서 양수인 곡률"을 가진 변환이다. 기하학적으로 $x^T A x = 1$은 타원체(ellipsoid)를 정의하며, $A$의 고유벡터 방향이 타원체의 주축 방향, 고유값이 각 축의 길이를 결정한다.

물리적으로 양정치 행렬은 안정적인 시스템을 나타낸다: 스프링의 위치에너지 $E = \frac12 k x^2$에서 $k > 0$이면 평형이 안정적이다. 고차원에서 $x^T A x$는 일반화된 에너지 함수이고, $A$가 양정치이면 원점이 안정적 극소점이다.

공분산 행렬(covariance matrix)은 항상 양반정치(positive semidefinite)다 — 분산은 음수가 될 수 없기 때문이다. 마찬가지로 $A^T A$ 형태의 행렬(그람 행렬, Gram matrix)은 항상 양반정치이며, $A$의 열이 일차독립이면 양정치가 된다. 이는 최소제곱법에서 $A^T A$의 가역성을 보장하는 조건이기도 하다.

## 정의

**양정치 (positive definite):** 대칭행렬 $A \in \mathbb{R}^{n \times n}$이 모든 $x \neq 0$에 대해
$$x^T A x > 0$$
을 만족하면 $A$를 양정치라 하고 $A \succ 0$으로 표기한다.

**양반정치 (positive semidefinite):** 모든 $x$에 대해 $x^T A x \geq 0$이면 양반정치라 하고 $A \succeq 0$으로 표기한다.

**음정치 (negative definite):** $x^T A x < 0$ (모든 $x \neq 0$)이면 음정치.

**주소행렬식 (principal minor):** $A$의 $k$번째 주소행렬식 $\Delta_k$는 $A$의 $1, \ldots, k$번째 행과 열로 이루어진 $k \times k$ 부분행렬의 행렬식이다.

**촐레스키 분해 (Cholesky decomposition):** 양정치 행렬 $A$는 유일하게 $A = LL^T$로 분해된다. 여기서 $L$은 하삼각행렬(lower triangular)이며 대각 성분이 양수다.

**동치 조건:** 대칭행렬 $A$에 대해 다음은 모두 동치다.
1. $A$는 양정치이다.
2. 모든 고유값이 양수이다.
3. 모든 피보트(pivot)가 양수이다. (가우스 소거 중)
4. $A = B^T B$를 만족하는 가역행렬 $B$가 존재한다.
5. 모든 주소행렬식이 양수이다. (실베스터 판정법)
6. 촐레스키 분해 $A = LL^T$가 존재한다.

## 주요 정리와 증명

### 정리 1: 양정치 ⟺ 모든 고유값 > 0

대칭행렬 $A$가 양정치일 필요충분조건은 $A$의 모든 고유값이 양수인 것이다.

**증명:** 스펙트럼 정리에 의해 $A = Q \Lambda Q^T$ ($Q$ 직교, $\Lambda = \text{diag}(\lambda_1, \ldots, \lambda_n)$). $y = Q^T x$로 변수변환하면 $\|y\| = \|x\|$이고
$$x^T A x = x^T Q \Lambda Q^T x = y^T \Lambda y = \sum_{i=1}^n \lambda_i y_i^2$$

($\Rightarrow$) $A$가 양정치라 가정하자. $i$번째 고유벡터 $q_i$ ($Q$의 $i$번째 열)에 대해
$$q_i^T A q_i = \lambda_i \|q_i\|^2 = \lambda_i > 0$$
따라서 $\lambda_i > 0$이다.

($\Leftarrow$) 모든 $\lambda_i > 0$이라 가정하자. $x \neq 0$이면 $y = Q^T x \neq 0$이고
$$x^T A x = \sum \lambda_i y_i^2 \geq (\min \lambda_i) \|y\|^2 = (\min \lambda_i) \|x\|^2 > 0$$
따라서 $A$는 양정치이다.

### 정리 2: 양정치 ⟺ $A = B^T B$ (가역 $B$)

대칭행렬 $A$가 양정치일 필요충분조건은 $A = B^T B$를 만족하는 가역행렬 $B$가 존재하는 것이다.

**증명:** ($\Leftarrow$) $B$가 가역이면 $x \neq 0$일 때 $Bx \neq 0$이므로
$$x^T A x = x^T (B^T B) x = (Bx)^T (Bx) = \|Bx\|^2 > 0$$

($\Rightarrow$) $A$가 양정치이면 $A = Q \Lambda Q^T$ ($\lambda_i > 0$). $\sqrt{\Lambda} = \text{diag}(\sqrt{\lambda_1}, \ldots, \sqrt{\lambda_n})$라 하면
$$A = Q \sqrt{\Lambda} \sqrt{\Lambda} Q^T = (Q \sqrt{\Lambda})(Q \sqrt{\Lambda})^T = B^T B$$
여기서 $B = \sqrt{\Lambda} Q^T$ (또는 $B = Q \sqrt{\Lambda} Q^T$로 선택할 수도 있다). $B$는 가역이다.

### 정리 3: 실베스터 판정법 (Sylvester's Criterion)

대칭행렬 $A$가 양정치일 필요충분조건은 모든 주소행렬식(leading principal minor)이 양수인 것이다:
$$\Delta_1 = a_{11} > 0, \quad \Delta_2 = \det\begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} > 0, \quad \ldots, \quad \Delta_n = \det(A) > 0$$

**증명 ($2 \times 2$ 경우):** $A = \begin{pmatrix} a & b \\ b & c \end{pmatrix}$가 양정치라고 하자. $x = (1, 0)^T$를 대입하면 $a > 0$이다. $x = (0, 1)^T$를 대입하면 $c > 0$이다. 또한 고유값의 곱 $\det(A) = ac - b^2 = \lambda_1 \lambda_2 > 0$이므로 $\Delta_2 > 0$이다.

역으로 $a > 0$, $\det(A) = ac - b^2 > 0$이라 하자. 이차형식을 완전제곱 형태로 쓰면
$$x^T A x = ax_1^2 + 2bx_1x_2 + cx_2^2 = a\left(x_1 + \frac{b}{a}x_2\right)^2 + \frac{ac - b^2}{a} x_2^2$$
$a > 0$이고 $ac - b^2 > 0$이므로 $(x_1, x_2) \neq (0, 0)$일 때 $x^T A x > 0$이다. 따라서 $A$는 양정치다.

**일반 $n$에 대한 증명 개요:** 귀납법과 $A$의 마지막 행/열에 대한 Schur complement를 이용한다. $A$를 블록 형태 $A = \begin{pmatrix} A_{n-1} & b \\ b^T & c \end{pmatrix}$로 쓰면, $A$가 양정치일 필요충분조건은 $A_{n-1}$이 양정치이고 $c - b^T A_{n-1}^{-1} b > 0$이다. $A_{n-1}$의 양정치성은 귀납가설로 주소행렬식의 양수와 동치이고, $c - b^T A_{n-1}^{-1} b = \det(A)/\det(A_{n-1})$이므로 $\det(A) > 0$ 조건과 연결된다.

**참고:** 실베스터 판정법은 양반정치 판정에는 사용할 수 없다. 양반정치의 필요충분조건은 **모든** 주소행렬식(leading principal minors뿐 아니라 모든 principal minors)이 0 이상인 것이다.

### 정리 4: 촐레스키 분해 (Cholesky Decomposition)

양정치 행렬 $A$는 유일하게 $A = LL^T$로 분해된다. 여기서 $L$은 실수 하삼각행렬이고 대각 성분이 양수다.

**증명 (구성적):** 귀납법으로 $L$을 구성한다. $n = 1$: $A = [a_{11}]$, $L = [\sqrt{a_{11}}]$.

$n \geq 2$에 대해 $A$를 블록 형태로 분할하자:
$$A = \begin{pmatrix} a_{11} & w^T \\ w & A_{22} \end{pmatrix}$$

$a_{11} > 0$이므로 $l_{11} = \sqrt{a_{11}}$이다. $l = w / \sqrt{a_{11}}$이라 하고 $A_{22} - ll^T$를 계산한다. 이 행렬이 양정치임을 보일 수 있고(증명: Schur complement), 귀납가설에 의해 $L_{22}$로 분해된다. 따라서
$$L = \begin{pmatrix} l_{11} & 0 \\ l & L_{22} \end{pmatrix}$$

**촐레스키 알고리즘 ($i \geq j$):**
$$L_{jj} = \sqrt{A_{jj} - \sum_{k=1}^{j-1} L_{jk}^2}$$
$$L_{ij} = \frac{1}{L_{jj}} \left( A_{ij} - \sum_{k=1}^{j-1} L_{ik} L_{jk} \right) \quad (i > j)$$

### 정리 5: 공분산 행렬은 양반정치

확률벡터 $X = (X_1, \ldots, X_n)^T$의 공분산 행렬 $\Sigma = \mathbb{E}[(X - \mu)(X - \mu)^T]$ ($\mu = \mathbb{E}[X]$)는 양반정치다.

**증명:** 임의의 $c \in \mathbb{R}^n$에 대해
$$c^T \Sigma c = c^T \mathbb{E}[(X-\mu)(X-\mu)^T] c = \mathbb{E}[c^T (X-\mu)(X-\mu)^T c] = \mathbb{E}[((X-\mu)^T c)^2] \geq 0$$

$= 0$일 조건은 $c^T (X-\mu) = 0$ (확률 1), 즉 $X$의 성분들이 일차종속 관계에 있을 때다.

### 정리 6: 양정치 행렬과 에너지 노름

양정치 행렬 $A$는 **에너지 노름(energy norm)**을 정의한다:
$$\|x\|_A = \sqrt{x^T A x}$$

이 노름은 $A$가 생성하는 내적 $\langle x, y \rangle_A = x^T A y$에서 유도된다. 에너지 노름은 유한요소법(FEM)과 최적화에서 널리 사용된다.

## 예제

**예제 1:** $A = \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}$가 양정치임을 세 가지 방법으로 확인하라.

**풀이:**

방법 1 (고유값): $\det\begin{pmatrix} 2-\lambda & -1 \\ -1 & 2-\lambda \end{pmatrix} = (2-\lambda)^2 - 1 = \lambda^2 - 4\lambda + 3 = (\lambda-1)(\lambda-3)$.
$\lambda_1 = 1 > 0$, $\lambda_2 = 3 > 0$이므로 양정치.

방법 2 (실베스터 판정법): $\Delta_1 = 2 > 0$, $\Delta_2 = 2\cdot2 - (-1)(-1) = 3 > 0$. 따라서 양정치.

방법 3 (정의): $x^T A x = \begin{pmatrix} x & y \end{pmatrix} \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = 2x^2 - 2xy + 2y^2 = 2(x^2 - xy + y^2)$.
$x^2 - xy + y^2 = (x - y/2)^2 + 3y^2/4 \geq 0$이고 $(x, y) \neq (0, 0)$일 때 $> 0$이므로 양정치.

**예제 2:** $A = \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix}$는 양정치인가?

**풀이:** $\Delta_1 = 1 > 0$, $\Delta_2 = 1\cdot1 - 2\cdot2 = -3 < 0$. 따라서 양정치가 아니다. 고유값으로 확인: $\lambda^2 - 2\lambda - 3 = 0$, $\lambda = 3$과 $\lambda = -1$로 하나가 음수이므로 부정부정(indefinite)이다.

$x^T A x = x^2 + 4xy + y^2$는 $y = 0$, $x = 1$일 때 $1 > 0$이지만 $x = 1$, $y = -1$일 때 $1 - 4 + 1 = -2 < 0$이므로 부호가 바뀐다.

**예제 3:** $A = \begin{pmatrix} 4 & 2 & 0 \\ 2 & 5 & 3 \\ 0 & 3 & 6 \end{pmatrix}$를 실베스터 판정법으로 검사하라.

**풀이:** $\Delta_1 = 4 > 0$.
$\Delta_2 = \det\begin{pmatrix} 4 & 2 \\ 2 & 5 \end{pmatrix} = 20 - 4 = 16 > 0$.
$\Delta_3 = \det\begin{pmatrix} 4 & 2 & 0 \\ 2 & 5 & 3 \\ 0 & 3 & 6 \end{pmatrix}$를 계산:
$$= 4(5\cdot6 - 3\cdot3) - 2(2\cdot6 - 0\cdot3) + 0(2\cdot3 - 0\cdot5)$$
$$= 4(30 - 9) - 2(12 - 0) = 4\cdot21 - 24 = 84 - 24 = 60 > 0$$

모든 주소행렬식이 양수이므로 $A$는 양정치다.

**예제 4:** $A = \begin{pmatrix} 4 & 2 \\ 2 & 3 \end{pmatrix}$의 촐레스키 분해를 구하라.

**풀이:**
$L_{11} = \sqrt{a_{11}} = \sqrt{4} = 2$.
$L_{21} = a_{21} / L_{11} = 2 / 2 = 1$.
$L_{22} = \sqrt{a_{22} - L_{21}^2} = \sqrt{3 - 1^2} = \sqrt{2}$.

$$L = \begin{pmatrix} 2 & 0 \\ 1 & \sqrt{2} \end{pmatrix}, \quad LL^T = \begin{pmatrix} 2 & 0 \\ 1 & \sqrt{2} \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & \sqrt{2} \end{pmatrix} = \begin{pmatrix} 4 & 2 \\ 2 & 3 \end{pmatrix} = A$$

**예제 5:** $x^T A x = 1$이 정의하는 곡선을 그리시오. $A = \begin{pmatrix} 5 & 4 \\ 4 & 5 \end{pmatrix}$.

**풀이:** $A$의 고유값: $\lambda_1 = 1$, $\lambda_2 = 9$ (앞서 계산). 고유벡터: $q_1 = \frac{1}{\sqrt{2}}(1, -1)$, $q_2 = \frac{1}{\sqrt{2}}(1, 1)$.

$x^T A x = 1$은 $\frac{y_1^2}{1^2} + \frac{y_2^2}{(1/3)^2} = 1$로 변환된다. 이는 $q_1$ 방향(장축, 길이 1), $q_2$ 방향(단축, 길이 1/3)의 타원이다. $q_1$ 방향이 $y = -x$, $q_2$ 방향이 $y = x$이다.

**예제 6 (그람 행렬):** $A = \begin{pmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{pmatrix}$에 대해 $A^T A$가 양정치임을 확인하라.

**풀이:** $A^T A = \begin{pmatrix} 3 & 3 \\ 3 & 5 \end{pmatrix}$.
$\Delta_1 = 3 > 0$, $\Delta_2 = 3\cdot5 - 3\cdot3 = 15 - 9 = 6 > 0$. 따라서 양정치.
참고: $A$의 열이 일차독립이므로 $A^T A$는 항상 양정치다.

**예제 7 (에너지 노름):** $A = \begin{pmatrix} 5 & 4 \\ 4 & 5 \end{pmatrix}$에 대해 $x = (1, 2)$의 에너지 노름을 구하라.

**풀이:** $\|x\|_A^2 = x^T A x = \begin{pmatrix} 1 & 2 \end{pmatrix} \begin{pmatrix} 5 & 4 \\ 4 & 5 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 1 & 2 \end{pmatrix} \begin{pmatrix} 13 \\ 14 \end{pmatrix} = 13 + 28 = 41$.
$\|x\|_A = \sqrt{41} \approx 6.40$. 유클리드 노름 $\|x\| = \sqrt{5} \approx 2.24$보다 크다 — $A$의 가장 큰 고유값($\lambda = 9$) 방향의 성분이 증폭되었기 때문이다.

**예제 8 (촐레스키 분해 — $3 \times 3$):** $A = \begin{pmatrix} 9 & 3 & 6 \\ 3 & 5 & 4 \\ 6 & 4 & 9 \end{pmatrix}$의 촐레스키 분해를 구하라.

**풀이:**
$L_{11} = \sqrt{9} = 3$.
$L_{21} = 3/3 = 1$.
$L_{31} = 6/3 = 2$.
$L_{22} = \sqrt{5 - 1^2} = \sqrt{4} = 2$.
$L_{32} = (4 - 1\cdot2)/2 = (4-2)/2 = 1$.
$L_{33} = \sqrt{9 - 2^2 - 1^2} = \sqrt{9 - 4 - 1} = \sqrt{4} = 2$.

$$L = \begin{pmatrix} 3 & 0 & 0 \\ 1 & 2 & 0 \\ 2 & 1 & 2 \end{pmatrix}, \quad LL^T = \begin{pmatrix} 9 & 3 & 6 \\ 3 & 5 & 4 \\ 6 & 4 & 9 \end{pmatrix} = A$$

**예제 9 (행렬 $A^T A$의 양정치성):** $A = \begin{pmatrix} 1 & 2 \\ 0 & 1 \\ 1 & 1 \end{pmatrix}$에 대해 $A^T A$가 양정치임을 확인하고, $A^T A$의 최소 고유값을 구하라.

**풀이:** $A^T A = \begin{pmatrix} 2 & 3 \\ 3 & 6 \end{pmatrix}$.
$\det\begin{pmatrix} 2-\lambda & 3 \\ 3 & 6-\lambda \end{pmatrix} = (2-\lambda)(6-\lambda) - 9 = \lambda^2 - 8\lambda + 3 = 0$.
$\lambda = \frac{8 \pm \sqrt{64-12}}{2} = 4 \pm \sqrt{13}$.
$\lambda_1 = 4 + \sqrt{13} \approx 7.61$, $\lambda_2 = 4 - \sqrt{13} \approx 0.39$.
두 고유값 모두 양수이므로 $A^T A$는 양정치다. 최소 고유값 $\lambda_{\min} = 4 - \sqrt{13} \approx 0.39$는 $A$의 열들이 "얼마나 일차독립에 가까운가"를 나타내는 척도(condition number와 관련)다.

**예제 10 (양반정치 판정):** $A = \begin{pmatrix} 1 & 1 & 1 \\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{pmatrix}$의 정부호를 판정하라.

**풀이:** $x^T A x = (x_1 + x_2 + x_3)^2 \geq 0$이므로 양반정치이다. $x = (1, -1, 0)^T$일 때 0이 되므로 양정치는 아니다. 고유값은 $\lambda_1 = 3$, $\lambda_2 = \lambda_3 = 0$이다.

**예제 11 (볼록성과 양정치 헤시안):** $f(x, y) = x^2 + 2xy + 2y^2$가 볼록함수(convex function)임을 보이라.

**풀이:** $f$의 헤시안 행렬: $H = \begin{pmatrix} 2 & 2 \\ 2 & 4 \end{pmatrix}$.
$\Delta_1 = 2 > 0$, $\Delta_2 = 2\cdot4 - 2\cdot2 = 4 > 0$이므로 $H$는 양정치다.
모든 점에서 헤시안이 양정치이므로 $f$는 (엄격) 볼록함수이며, 유일한 전역 최소점을 가진다.
$\nabla f = (2x + 2y, 2x + 4y) = 0$에서 유일한 임계점 $(x, y) = (0, 0)$을 얻고, $f(0, 0) = 0$이 전역 최소값이다.

## 연결

- **[대칭행렬·스펙트럼 정리](spectral-theorem.html)** : 양정치 판정의 핵심 도구는 스펙트럼 정리 — 고유값의 부호를 통해 이차형식을 분류한다.
- **[라그랑주 승수법](lagrange-multipliers.html)** : 제약 최적화에서 헤시안 행렬의 양정치성이 극값의 종류(극소/극대/안장)를 결정한다.
