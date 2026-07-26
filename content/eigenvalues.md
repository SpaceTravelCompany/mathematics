---
title: 고유값·고유벡터
slug: eigenvalues
---

## 직관적 설명

**고유값(eigenvalue)과 고유벡터(eigenvector)**는 선형변환의 "본질적인 축"과 그 축에서의 "늘어남 비율"을 나타낸다. $Av = \lambda v$는 행렬 $A$를 벡터 $v$에 적용해도 $v$의 방향은 변하지 않고 크기만 $\lambda$배가 된다는 뜻이다.

이 개념이 중요한 이유는 복잡한 선형변환도 고유벡터들로 분해하여 생각하면 각 축 방향의 단순한 스케일링으로 이해할 수 있기 때문이다. 예를 들어 3차원 회전 변환은 회전축 방향의 고유벡터(고유값 1)와 회전 평면 안의 복소 고유값으로 완전히 특징지어진다.

고유값은 진동 해석(고유진동수), 양자역학(에너지 준위), 주성분 분석(분산 방향), 페이지랭크(웹페이지 중요도), 미분방정식의 안정성 분석 등 과학과 공학 전반에서 가장 중요한 단일 개념이다. 거의 모든 행렬분해(SVD, 스펙트럼 정리, 대각화)의 출발점이기도 하다.

## 정의

**고유값과 고유벡터 (eigenvalue and eigenvector):** $n \times n$ 정사각행렬 $A$와 영벡터가 아닌 벡터 $v \in \mathbb{C}^n$에 대해
$$Av = \lambda v$$
를 만족하는 스칼라 $\lambda$를 $A$의 **고유값**, $v$를 $\lambda$에 대응하는 **고유벡터**라 한다.

**특성방정식 (characteristic equation):** $\lambda$가 고유값일 필요충분조건은 $\det(A - \lambda I) = 0$이다. 이는 $A - \lambda I$가 특이(singular) 행렬임을 의미한다.

**특성다항식 (characteristic polynomial):**
$$p(\lambda) = \det(A - \lambda I) = (-1)^n \lambda^n + c_{n-1} \lambda^{n-1} + \cdots + c_1 \lambda + c_0$$

$n$차 다항식이며, 계수 $c_k$는 $A$의 주소행렬식(principal minors)으로 표현된다.

**고유공간 (eigenspace):** 고유값 $\lambda$에 대응하는 모든 고유벡터와 영벡터의 집합
$$E_\lambda = \ker(A - \lambda I) = \{ v \in \mathbb{C}^n \mid (A - \lambda I)v = 0 \}$$

$E_\lambda$는 $\mathbb{C}^n$의 부분공간이다.

**대수적 중복도 (algebraic multiplicity):** 특성다항식에서 $(\lambda - \lambda_0)$ 인수의 차수. 즉, $\lambda_0$가 특성방정식의 근으로 나타나는 횟수.

**기하적 중복도 (geometric multiplicity):** 고유공간 $E_\lambda$의 차원. 즉, $\dim(\ker(A - \lambda I))$.

**고유값과 행렬의 불변량:**
$$\det(A) = \lambda_1 \lambda_2 \cdots \lambda_n \quad \text{(고유값들의 곱)}$$
$$\text{tr}(A) = \lambda_1 + \lambda_2 + \cdots + \lambda_n \quad \text{(고유값들의 합)}$$

**스펙트럼 (spectrum):** 행렬 $A$의 모든 고유값의 집합 $\sigma(A) = \{\lambda_1, \ldots, \lambda_n\}$.

## 주요 정리와 증명

### 정리 1: 고유값의 존재

복소수 위에서 모든 $n \times n$ 행렬은 적어도 하나의 고유값(복소수)을 가진다.

**증명:** 특성다항식 $p(\lambda) = \det(A - \lambda I)$는 $\lambda$에 대한 $n$차 다항식이다. 대수학의 기본정리(Fundamental Theorem of Algebra)에 의해 복소수 체 위에서 $n$차 다항식은 중복을 포함해 정확히 $n$개의 근을 가진다. 각 근 $\lambda$에 대해 $\det(A - \lambda I) = 0$이므로 $A - \lambda I$는 특이행렬이고, $\ker(A - \lambda I) \neq \{0\}$이므로 영 아닌 고유벡터가 존재한다.

**참고:** 실수 위에서는 항상 고유값이 존재한다고 보장할 수 없다. 예를 들어 회전 행렬 $R = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$는 실수 고유값을 가지지 않는다(특성다항식 $\lambda^2 + 1 = 0$).

### 정리 2: 서로 다른 고유값의 고유벡터는 일차독립

$\lambda_1, \ldots, \lambda_k$가 $A$의 서로 다른 고유값이고 $v_1, \ldots, v_k$가 각각에 대응하는 고유벡터이면 $\{v_1, \ldots, v_k\}$는 일차독립이다.

**증명 (귀납법):** $k = 1$일 때 $v_1 \neq 0$이므로 자명하게 일차독립이다.

$k - 1$개의 고유벡터가 일차독립이라 가정하고 $k$개에 대해 증명하자. 일차결합
$$c_1 v_1 + \cdots + c_k v_k = 0$$
을 고려한다. 양변에 $A$를 곱하면
$$c_1 \lambda_1 v_1 + \cdots + c_k \lambda_k v_k = 0$$

한편 첫 식에 $\lambda_k$를 곱하면
$$c_1 \lambda_k v_1 + \cdots + c_k \lambda_k v_k = 0$$

두 식을 빼면
$$c_1 (\lambda_1 - \lambda_k) v_1 + \cdots + c_{k-1} (\lambda_{k-1} - \lambda_k) v_{k-1} = 0$$

귀납가설에 의해 $\{v_1, \ldots, v_{k-1}\}$이 일차독립이므로 모든 $i = 1, \ldots, k-1$에 대해 $c_i (\lambda_i - \lambda_k) = 0$이다. $\lambda_i \neq \lambda_k$이므로 $c_i = 0$이다. 첫 식에 대입하면 $c_k v_k = 0$이고 $v_k \neq 0$이므로 $c_k = 0$이다. 따라서 $\{v_1, \ldots, v_k\}$는 일차독립이다.

**따름정리:** $n \times n$ 행렬이 $n$개의 서로 다른 고유값을 가지면 $n$개의 일차독립 고유벡터가 존재하므로 대각화 가능하다.

### 정리 3: 대각화 (Diagonalization)

$n \times n$ 행렬 $A$가 대각화 가능할 필요충분조건은 $n$개의 일차독립인 고유벡터가 존재하는 것이다. 이때
$$A = PDP^{-1}$$
여기서 $P$의 열은 고유벡터이고 $D$는 대각행렬로 $D_{ii} = \lambda_i$($\lambda_i$는 $P$의 $i$번째 열에 대응하는 고유값)이다.

**증명:** ($\Leftarrow$) $n$개의 일차독립 고유벡터 $v_1, \ldots, v_n$이 존재한다고 가정하자. $P = [v_1 \; v_2 \; \cdots \; v_n]$이라 하면 $P$는 가역이다. $AP$를 계산하면
$$AP = [Av_1 \; Av_2 \; \cdots \; Av_n] = [\lambda_1 v_1 \; \lambda_2 v_2 \; \cdots \; \lambda_n v_n] = PD$$

따라서 $AP = PD$, 양변에 $P^{-1}$을 곱하면 $A = PDP^{-1}$이다.

($\Rightarrow$) $A = PDP^{-1}$ ($D$ 대각행렬)이라 하자. $P$의 열을 $v_1, \ldots, v_n$이라 하면 $Av_i = \lambda_i v_i$이므로 각 $v_i$는 고유벡터이다. $P$가 가역이므로 $v_i$들은 일차독립이다.

**따름정리:** $A^k = PD^k P^{-1}$이다. 즉, $A$의 거듭제곱은 고유값의 거듭제곱으로 쉽게 계산된다.

### 정리 4: 케일리-해밀턴 정리 (Cayley-Hamilton Theorem)

모든 정사각행렬 $A$는 자신의 특성다항식을 만족한다. 즉, $p(\lambda) = \det(A - \lambda I)$에 대해 $p(A) = 0$이다.

**서술:** 특성다항식 $p(\lambda) = (-1)^n \lambda^n + c_{n-1} \lambda^{n-1} + \cdots + c_0$에 대해
$$p(A) = (-1)^n A^n + c_{n-1} A^{n-1} + \cdots + c_1 A + c_0 I = 0$$

**예시 ($2 \times 2$):** $A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$의 특성다항식은 $p(\lambda) = \lambda^2 - (a+d)\lambda + (ad - bc)$이다. 케일리-해밀턴 정리에 의해
$$A^2 - (a+d)A + (ad - bc)I = 0$$
이를 이용하면 $A^2$를 $A$와 $I$의 선형결합으로 표현할 수 있고, 고차 거듭제곱도 반복적으로 계산 가능하다.

**참고:** 케일리-해밀턴 정리는 $A^{-1}$을 $A$의 다항식으로 표현하는 데 사용된다. $p(A) = 0$에서 $A$의 최고차항을 이항하면 $A^{-1}$을 얻을 수 있다($\det A \neq 0$일 때).

### 정리 5: 고유값의 기하학적 의미 — 행렬식과 대각합

$n \times n$ 행렬 $A$의 고유값 $\lambda_1, \ldots, \lambda_n$ (중복 포함)에 대해
$$\det(A) = \prod_{i=1}^n \lambda_i, \quad \text{tr}(A) = \sum_{i=1}^n \lambda_i$$

**증명:** 특성다항식 $p(\lambda) = \det(A - \lambda I)$를 전개하면
$$p(\lambda) = (-\lambda)^n + (-\lambda)^{n-1} \text{tr}(A) + \cdots + \det(A)$$

한편 $p(\lambda) = \prod_{i=1}^n (\lambda_i - \lambda)$로 인수분해되므로 상수항과 $\lambda^{n-1}$의 계수를 비교하면 위 관계를 얻는다.

### 정리 6: 닮음 변환과 고유값

$A$와 $B = P^{-1}AP$ (닮음, similar)는 같은 고유값을 가진다.

**증명:** $B$의 특성다항식을 계산하면
$$\det(B - \lambda I) = \det(P^{-1}AP - \lambda I) = \det(P^{-1}(A - \lambda I)P)$$
$$= \det(P^{-1})\det(A - \lambda I)\det(P) = \det(A - \lambda I)$$

따라서 특성다항식이 같고, 고유값도 같다.

## 예제

**예제 1:** $A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$의 고유값과 고유벡터를 구하라.

**풀이:** 특성방정식:
$$\det(A - \lambda I) = \det\begin{pmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{pmatrix} = (2-\lambda)^2 - 1 = \lambda^2 - 4\lambda + 3 = 0$$

$\lambda^2 - 4\lambda + 3 = (\lambda - 1)(\lambda - 3) = 0$이므로 $\lambda_1 = 1$, $\lambda_2 = 3$.

$\lambda_1 = 1$에 대해: $(A - I)v = 0$
$$\begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} \;\Longrightarrow\; x + y = 0$$
$v_1 = \begin{pmatrix} 1 \\ -1 \end{pmatrix}$ (또는 스칼라배).

$\lambda_2 = 3$에 대해: $(A - 3I)v = 0$
$$\begin{pmatrix} -1 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} \;\Longrightarrow\; -x + y = 0$$
$v_2 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$.

대각화: $P = \begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}$, $D = \begin{pmatrix} 1 & 0 \\ 0 & 3 \end{pmatrix}$, $A = P D P^{-1}$.

**예제 2:** $A = \begin{pmatrix} 2 & -1 \\ 1 & 0 \end{pmatrix}$의 고유값과 고유벡터를 구하라.

**풀이:**
$$\det(A - \lambda I) = \det\begin{pmatrix} 2-\lambda & -1 \\ 1 & -\lambda \end{pmatrix} = (2-\lambda)(-\lambda) - (-1)(1) = \lambda^2 - 2\lambda + 1 = (\lambda - 1)^2$$

$\lambda = 1$ (중복도 2). 고유벡터를 구하면:
$$\begin{pmatrix} 1 & -1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} \;\Longrightarrow\; x - y = 0$$
$v = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$만 얻어진다. 기하적 중복도는 1, 대수적 중복도는 2이므로 이 행렬은 대각화 불가능하다. 이는 조르당 표준형(Jordan normal form)이 필요한 경우다.

**예제 3 (피보나치 수열):** 피보나치 수열 $F_{n+1} = F_n + F_{n-1}$ ($F_0 = 0$, $F_1 = 1$)을 행렬의 거듭제곱으로 표현하라.

**풀이:** $u_n = \begin{pmatrix} F_{n+1} \\ F_n \end{pmatrix}$라 하면
$$u_n = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} u_{n-1} = A u_{n-1}$$

$A$의 고유값을 구하면:
$$\det(A - \lambda I) = \det\begin{pmatrix} 1-\lambda & 1 \\ 1 & -\lambda \end{pmatrix} = \lambda^2 - \lambda - 1 = 0$$
$$\lambda_1 = \frac{1 + \sqrt{5}}{2}, \quad \lambda_2 = \frac{1 - \sqrt{5}}{2}$$

고유벡터:
$v_1 = \begin{pmatrix} \lambda_1 \\ 1 \end{pmatrix}$, $v_2 = \begin{pmatrix} \lambda_2 \\ 1 \end{pmatrix}$.

초기값 $u_0 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$를 고유벡터의 선형결합으로 표현:
$u_0 = c_1 v_1 + c_2 v_2$에서 $c_1 = \frac{1}{\sqrt{5}}$, $c_2 = -\frac{1}{\sqrt{5}}$.

따라서
$$F_n = \frac{1}{\sqrt{5}} \left( \lambda_1^n - \lambda_2^n \right) = \frac{1}{\sqrt{5}} \left( \left(\frac{1+\sqrt{5}}{2}\right)^n - \left(\frac{1-\sqrt{5}}{2}\right)^n \right)$$

이는 피보나치 수열의 **비네 공식(Binet's formula)**이다.

**예제 4:** $A = \begin{pmatrix} 4 & -2 \\ 1 & 1 \end{pmatrix}$에 대해 $A^5$를 계산하라 (대각화 활용).

**풀이:** 고유값: $\det\begin{pmatrix} 4-\lambda & -2 \\ 1 & 1-\lambda \end{pmatrix} = (4-\lambda)(1-\lambda) + 2 = \lambda^2 - 5\lambda + 6 = (\lambda - 2)(\lambda - 3) = 0$.
$\lambda_1 = 2$, $\lambda_2 = 3$.

$\lambda_1 = 2$: $(A-2I)v = \begin{pmatrix} 2 & -2 \\ 1 & -1 \end{pmatrix}v = 0$ → $v_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$.
$\lambda_2 = 3$: $(A-3I)v = \begin{pmatrix} 1 & -2 \\ 1 & -2 \end{pmatrix}v = 0$ → $v_2 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$.

$P = \begin{pmatrix} 1 & 2 \\ 1 & 1 \end{pmatrix}$, $P^{-1} = \begin{pmatrix} -1 & 2 \\ 1 & -1 \end{pmatrix}$, $D = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix}$.
$A^5 = P D^5 P^{-1} = \begin{pmatrix} 1 & 2 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 32 & 0 \\ 0 & 243 \end{pmatrix} \begin{pmatrix} -1 & 2 \\ 1 & -1 \end{pmatrix}$
$$= \begin{pmatrix} 32 & 486 \\ 32 & 243 \end{pmatrix} \begin{pmatrix} -1 & 2 \\ 1 & -1 \end{pmatrix} = \begin{pmatrix} -32 + 486 & 64 - 486 \\ -32 + 243 & 64 - 243 \end{pmatrix} = \begin{pmatrix} 454 & -422 \\ 211 & -179 \end{pmatrix}$$

**예제 5 (삼각행렬의 고유값):** $A = \begin{pmatrix} 3 & -1 & 2 \\ 0 & 2 & 5 \\ 0 & 0 & -1 \end{pmatrix}$의 고유값을 구하라.

**풀이:** $A$가 상삼각행렬(upper triangular)이므로 고유값은 대각 성분이다. 즉, $\lambda_1 = 3$, $\lambda_2 = 2$, $\lambda_3 = -1$.
확인: $\det(A - \lambda I) = (3-\lambda)(2-\lambda)(-1-\lambda)$.

**예제 6 (고유값과 미분방정식):** $x'(t) = Ax(t)$, $A = \begin{pmatrix} -2 & 1 \\ 1 & -2 \end{pmatrix}$의 해를 고유값 분해로 구하라.

**풀이:** $A$의 고유값: $\det\begin{pmatrix} -2-\lambda & 1 \\ 1 & -2-\lambda \end{pmatrix} = (\lambda+2)^2 - 1 = \lambda^2 + 4\lambda + 3 = (\lambda+1)(\lambda+3)$.
$\lambda_1 = -1$, $\lambda_2 = -3$.

고유벡터: $\lambda_1 = -1$: $\begin{pmatrix} -1 & 1 \\ 1 & -1 \end{pmatrix}v = 0$ → $v_1 = (1, 1)$.
$\lambda_2 = -3$: $\begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}v = 0$ → $v_2 = (1, -1)$.

일반해: $x(t) = c_1 e^{-t} v_1 + c_2 e^{-3t} v_2$.
초기조건 $x(0) = (x_1(0), x_2(0))$가 주어지면 $c_1, c_2$를 결정한다. $\lambda_i < 0$이므로 해는 $t \to \infty$에서 0으로 수렴하며, $\lambda_1 = -1$ 모드($v_1$ 방향)가 가장 느리게 감쇠한다.

**예제 7 (고유공간의 차원):** $A = \begin{pmatrix} 2 & 0 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & 3 \end{pmatrix}$의 각 고유값의 대수적·기하적 중복도를 구하라.

**풀이:** $\lambda = 2$ (대수적 중복도 2), $\lambda = 3$ (대수적 중복도 1).
$\lambda = 2$에 대해 $(A - 2I) = \begin{pmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$의 rank는 1이므로 $\dim(E_2) = 3 - 1 = 2$. 기하적 중복도 = 2 = 대수적 중복도.
$\lambda = 3$에 대해 $(A - 3I) = \begin{pmatrix} -1 & 0 & 0 \\ 0 & -1 & 0 \\ 0 & 0 & 0 \end{pmatrix}$의 rank는 2이므로 $\dim(E_3) = 3 - 2 = 1$.
따라서 이 행렬은 대각화 가능하다(이미 대각행렬).

## 연결

- **[행렬식의 기하학](topics/determinant.html)** : 특성방정식 $\det(A - \lambda I) = 0$은 행렬식의 개념과 직접 연결된다.
- **[대칭행렬·스펙트럼 정리](topics/spectral-theorem.html)** : 대칭행렬은 항상 실수 고유값을 가지며 직교 대각화 가능하다 — 고유값 이론의 가장 아름다운 결과.
- **[SVD](topics/svd.html)** : SVD는 모든 행렬(직사각형 포함)로 고유값 개념을 확장한 최종 행렬분해다.
