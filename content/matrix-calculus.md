---
title: 행렬 미분
slug: matrix-calculus
---

## 직관적 설명

**행렬 미분(matrix calculus)**은 스칼라 함수를 벡터나 행렬로 미분하는 체계적인 표기법이다. 가장 흔한 상황은 손실 함수(loss function) $L$이 모델 파라미터 $\theta \in \mathbb{R}^n$의 함수로 주어질 때, $L$의 각 파라미터에 대한 변화율을 한꺼번에 표현하는 것이다.

스칼라 $f: \mathbb{R}^n \to \mathbb{R}$의 그래디언트(gradient) $\nabla f$는 $n$차원 벡터로, $i$번째 성분이 $\partial f / \partial x_i$이다. 이 벡터는 $x$에서 함수가 가장 가파르게 증가하는 방향을 가리킨다. 함수의 입력이 행렬 $W \in \mathbb{R}^{m \times n}$이라면 그래디언트도 같은 크기의 행렬이 된다.

행렬 미분의 핵심은 "스칼라 출력"을 다룬다는 점이다. 출력이 스칼라이므로 모든 입력 변수에 대한 편미분을 모으면 입력과 같은 크기의 배열이 나온다. 이 덕분에 연쇄법칙(chain rule)과 같은 친숙한 미분 규칙이 행렬 영역으로 자연스럽게 확장된다.

행렬 미분은 최소제곱법, 선형 회귀, 물리 시뮬레이션, 최적화 이론에서 핵심 도구로 사용된다. 정규방정식(normal equation)의 유도, 그래디언트 기반 최적화 알고리즘의 설계 모두 행렬 미분 없이는 불가능하다.

---
## 정의

**스칼라-대-벡터 미분 (gradient):** 함수 $f: \mathbb{R}^n \to \mathbb{R}$가 주어졌을 때, $x \in \mathbb{R}^n$에서의 **그래디언트**는 열벡터(column vector) 규약을 따라 다음과 같이 정의된다:

$$\nabla f(x) = \frac{\partial f}{\partial x} = \begin{pmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{pmatrix} \in \mathbb{R}^n$$

이때 $\left(\frac{\partial f}{\partial x}\right)_i = \frac{\partial f}{\partial x_i}$이다.

**스칼라-대-행렬 미분:** 함수 $f: \mathbb{R}^{m \times n} \to \mathbb{R}$에 대해 $W \in \mathbb{R}^{m \times n}$에서의 미분은 같은 크기의 행렬이며, $(i,j)$ 성분은 다음과 같다:

$$\left(\frac{\partial f}{\partial W}\right)_{ij} = \frac{\partial f}{\partial W_{ij}} \in \mathbb{R}^{m \times n}$$

**벡터-대-벡터 미분 (야코비안, 도입):** 함수 $f: \mathbb{R}^n \to \mathbb{R}^m$의 경우, $f$의 각 출력 성분 $f_i$를 각 입력 $x_j$로 미분하여 $m \times n$ **야코비안 행렬(Jacobian matrix)** 을 얻는다:

$$J_f(x) = \frac{\partial f}{\partial x^T} = \begin{pmatrix} \frac{\partial f_1}{\partial x_1} & \cdots & \frac{\partial f_1}{\partial x_n} \\ \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n} \end{pmatrix}$$

(야코비안은 [야코비안·헤시안](jacobian-hessian.html)에서 자세히 다룬다.)

**기본 미분 규칙:** $a, b \in \mathbb{R}^n$, $A \in \mathbb{R}^{n \times n}$일 때:

$$\frac{\partial}{\partial x}(a^T x) = a$$

$$\frac{\partial}{\partial x}(x^T A x) = (A + A^T)x$$

**행렬 미분의 기본 규칙:**

$$\frac{\partial}{\partial W}\text{tr}(AW) = A^T$$

$$\frac{\partial}{\partial W}\text{tr}(W^T W) = 2W$$

**분모 표기법 vs 분자 표기법 (Denominator vs Numerator Layout):** 본 장에서는 **분모 표기법(denominator layout)** 을 사용한다. 즉, $\partial f / \partial x$는 $x$와 같은 크기의 열벡터이다. 이는 그래디언트 기반 최적화에 자연스럽다.

---
## 주요 정리와 증명

### 정리 1: $\nabla_x (x^T A x) = (A + A^T)x$

**증명 (성분 전개):** $x \in \mathbb{R}^n$, $A \in \mathbb{R}^{n \times n}$이라 하자. 이차형식(quadratic form)을 성분으로 전개하면:

$$x^T A x = \sum_{i=1}^n \sum_{j=1}^n x_i A_{ij} x_j$$

$k$번째 성분 $\partial (x^T A x) / \partial x_k$를 계산하자. $x_k$가 포함된 항만 골라내기 위해 $i=k$ 또는 $j=k$인 경우를 분리한다:

$$\frac{\partial}{\partial x_k} \left( \sum_{i=1}^n \sum_{j=1}^n x_i A_{ij} x_j \right) = \frac{\partial}{\partial x_k} \left( \sum_{j=1}^n x_k A_{kj} x_j + \sum_{i=1}^n x_i A_{ik} x_k - x_k A_{kk} x_k \right)$$

(단, $i=k, j=k$인 항이 두 번 더해졌으므로 $x_k A_{kk} x_k$를 한 번 빼준다.)

각 항을 미분하면:
$$\sum_{j=1}^n A_{kj} x_j + \sum_{i=1}^n x_i A_{ik} - 2A_{kk} x_k + 2A_{kk} x_k$$

첫 번째 합은 $(Ax)_k$, 두 번째 합은 $(A^T x)_k$이므로:

$$\frac{\partial}{\partial x_k} (x^T A x) = (Ax)_k + (A^T x)_k$$

모든 $k$에 대해 벡터 형태로 쓰면:

$$\nabla_x (x^T A x) = Ax + A^T x = (A + A^T)x$$

$A$가 대칭행렬이면 $A^T = A$이므로 $\nabla_x (x^T A x) = 2Ax$가 된다.

### 정리 2: $\nabla_W \text{tr}(AW) = A^T$

**증명:** $A, W \in \mathbb{R}^{m \times n}$이라 하자. $AW$의 대각합(trace)을 전개하면:

$$\text{tr}(AW) = \sum_{i=1}^m (AW)_{ii} = \sum_{i=1}^m \sum_{j=1}^n A_{ij} W_{ji}$$

$(p,q)$ 성분 $W_{pq}$로 미분하면, $W_{pq}$가 포함된 항은 $i=p, j=q$일 때뿐이다:

$$\frac{\partial}{\partial W_{pq}} \text{tr}(AW) = \frac{\partial}{\partial W_{pq}} \sum_i \sum_j A_{ij} W_{ji} = A_{qp}$$

따라서 $\partial \text{tr}(AW) / \partial W$의 $(p,q)$ 성분은 $A_{qp}$이므로, 행렬 형태로 쓰면 $A^T$이다:

$$\frac{\partial}{\partial W} \text{tr}(AW) = A^T$$

**따름정리:** $\frac{\partial}{\partial W} \text{tr}(W^T W) = 2W$ (위 정리에서 $A = W^T$로 두고 연쇄법칙 적용)

### 정리 3: $\nabla_x \|Ax - b\|^2 = 2A^T(Ax - b)$

**증명 (직접 전개):** $A \in \mathbb{R}^{m \times n}$, $x \in \mathbb{R}^n$, $b \in \mathbb{R}^m$이라 하자. 잔차 제곱합을 전개한다:

$$\begin{aligned}
\|Ax - b\|^2 &= (Ax - b)^T (Ax - b) \\
&= (x^T A^T - b^T)(Ax - b) \\
&= x^T A^T A x - x^T A^T b - b^T A x + b^T b \\
&= x^T (A^T A) x - 2b^T A x + b^T b
\end{aligned}$$

(마지막 줄: $b^T A x$는 스칼라이므로 $b^T A x = (b^T A x)^T = x^T A^T b$이다. 따라서 $x^T A^T b + b^T A x = 2b^T A x$.)

이제 정리 1과 선형 항의 미분 규칙을 적용한다:

$$\begin{aligned}
\nabla_x \|Ax - b\|^2 &= \nabla_x \big( x^T (A^T A) x \big) - 2 \nabla_x (b^T A x) + 0 \\
&= (A^T A + (A^T A)^T)x - 2A^T b \\
&= 2A^T A x - 2A^T b \\
&= 2A^T (A x - b)
\end{aligned}$$

$A^T A$는 대칭행렬이므로 $A^T A + (A^T A)^T = 2A^T A$가 사용되었다.

**연쇄법칙을 통한 증명 (대안):** $f(x) = \|g(x)\|^2$, $g(x) = Ax - b$로 보면:

$$\nabla_x f = 2 J_g(x)^T g(x)$$

여기서 $J_g(x) = A$이므로 $\nabla_x f = 2 A^T (Ax - b)$로 동일한 결과를 얻는다. 이는 행렬 미분에서 연쇄법칙의 전형적인 예시다.

### 정리 4: 행렬 미분의 연쇄법칙 구조

스칼라 함수 $f: \mathbb{R}^{m \times n} \to \mathbb{R}$와 행렬 함수 $G: \mathbb{R}^{p \times q} \to \mathbb{R}^{m \times n}$의 합성 $h(W) = f(G(W))$에 대해:

$$\frac{\partial h}{\partial W_{kl}} = \sum_{i=1}^m \sum_{j=1}^n \frac{\partial f}{\partial G_{ij}} \cdot \frac{\partial G_{ij}}{\partial W_{kl}}$$

이는 스칼라 연쇄법칙의 직접적인 일반화이다. 행렬 형태로 깔끔하게 쓰기는 어렵지만, 특수한 경우 단순화된다.

**특수 사례 — 선형 변환 후 스칼라 함수:** $g(x) = f(Ax)$일 때:

$$\nabla_x g(x) = A^T \nabla f(Ax)$$

이는 위 정리 3의 대안 증명에서 이미 사용되었다.

**증명:** $y = Ax$라 하자. $g(x) = f(y)$, $y_i = \sum_j A_{ij} x_j$. 연쇄법칙:

$$\frac{\partial g}{\partial x_j} = \sum_i \frac{\partial f}{\partial y_i} \frac{\partial y_i}{\partial x_j} = \sum_i \frac{\partial f}{\partial y_i} A_{ij}$$

벡터 형태: $\nabla_x g = A^T \nabla_y f$.

---
## 예제

**예제 1:** $f(x) = x^T A x + b^T x$의 그래디언트를 구하라 ($A \in \mathbb{R}^{n \times n}$, $b \in \mathbb{R}^n$).

**풀이:** 각 항에 미분 규칙을 적용한다:
$$\nabla f(x) = \nabla (x^T A x) + \nabla (b^T x) = (A + A^T)x + b$$

$A$가 대칭이면 $\nabla f(x) = 2Ax + b$이다.

**예제 2:** 최소제곱 문제 $\min_x \|Ax - b\|^2$의 최적해(정규방정식)를 행렬 미분으로 유도하라.

**풀이:** 목적함수 $f(x) = \|Ax - b\|^2$의 그래디언트는 정리 3에서 구했다:
$$\nabla f(x) = 2A^T(Ax - b)$$

최적 조건 $\nabla f(x) = 0$에서:
$$2A^T(Ax - b) = 0 \quad \Longrightarrow \quad A^T A x = A^T b$$

이는 **정규방정식(normal equation)** 이다. $A^T A$가 가역이면 유일해 $x^* = (A^T A)^{-1} A^T b$를 얻는다.

**예제 3:** $f(X) = \text{tr}(X^T X)$를 미분하라, $X \in \mathbb{R}^{m \times n}$.

**풀이 1 (성분 접근):**
$$\text{tr}(X^T X) = \sum_{i=1}^n (X^T X)_{ii} = \sum_{i=1}^n \sum_{j=1}^m X_{ji} X_{ji} = \sum_{i=1}^n \sum_{j=1}^m X_{ji}^2$$

$(p,q)$ 성분 $X_{pq}$로 미분:
$$\frac{\partial}{\partial X_{pq}} \text{tr}(X^T X) = \frac{\partial}{\partial X_{pq}} \sum_{i,j} X_{ji}^2 = 2X_{pq}$$

따라서 $\partial f / \partial X = 2X$.

**풀이 2 (trace 미분 규칙 활용):** $\text{tr}(X^T X) = \text{tr}(X X^T)$이므로 정리 2의 따름정리를 직접 적용:
$$\frac{\partial}{\partial X} \text{tr}(X^T X) = 2X$$

**예제 4:** $g(W) = \|XW - Y\|_F^2$의 그래디언트를 구하라 ($X \in \mathbb{R}^{m \times n}$, $W \in \mathbb{R}^{n \times p}$, $Y \in \mathbb{R}^{m \times p}$).

**풀이:** 프로베니우스 노름(Frobenius norm)의 정의 $\|Z\|_F^2 = \text{tr}(Z^T Z)$를 사용한다:

$$\begin{aligned}
\|XW - Y\|_F^2 &= \text{tr}((XW - Y)^T (XW - Y)) \\
&= \text{tr}(W^T X^T X W) - 2\text{tr}(Y^T X W) + \text{tr}(Y^T Y)
\end{aligned}$$

이제 각 항을 미분한다. 첫째 항: trace 항등식 $\partial \text{tr}(W^T M W) / \partial W = (M + M^T)W$를 사용하면 ($M = X^T X$ 대칭): $\partial \text{tr}(W^T X^T X W) / \partial W = 2X^T X W$.

둘째 항: $\partial \text{tr}(Y^T X W) / \partial W = \partial \text{tr}(W Y^T X) / \partial W = X^T Y$ (정리 2).

따라서:
$$\frac{\partial}{\partial W} \|XW - Y\|_F^2 = 2X^T X W - 2X^T Y = 2X^T (XW - Y)$$

이는 선형 회귀의 다중 출력(multi-output) 일반화에 해당한다.

**예제 5:** $f(x) = \|x\|^3 = (x^T x)^{3/2}$의 그래디언트를 구하라.

**풀이:** $g(x) = x^T x$라 하면 $f(x) = (g(x))^{3/2}$. 연쇄법칙:
$$\nabla f(x) = \frac{3}{2} (x^T x)^{1/2} \cdot \nabla g(x) = \frac{3}{2} \|x\| \cdot 2x = 3\|x\| x$$

**예제 6:** $f(x) = (Ax + b)^T D (Ax + b)$의 그래디언트를 구하라 ($D$ 대칭).

**풀이:** $y = Ax + b$라 하면 $f = y^T D y$. $\nabla_y f = 2Dy$ (정리 1, $D$ 대칭). 선형 변환의 연쇄법칙:
$$\nabla_x f = A^T \nabla_y f = 2A^T D (Ax + b)$$

---
## 연결

- **[고유값·고유벡터](eigenvalues.html)** : $x^T A x$의 그래디언트는 $A$의 대칭 성분과 연결되며, 고유값은 이차형식의 최적화에서 중요한 역할을 한다.
- **[야코비안·헤시안](jacobian-hessian.html)** : 행렬 미분의 자연스러운 확장 — 야코비안은 벡터-대-벡터 미분, 헤시안은 2계 미분 행렬이다.
- **[최소제곱법](least-squares.html)** : 예제 2의 정규방정식 유도는 최소제곱법의 수학적 기초다.
- **[다변수 연쇄법칙](multivar-chain-rule.html)** : 행렬 미분의 연쇄법칙은 다변수 연쇄법칙의 행렬 표현이다.
