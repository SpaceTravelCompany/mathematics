---
title: 기저 변환
slug: change-of-basis
---

## 직관적 설명

같은 벡터라도 어떤 기준(기저, basis)으로 좌표를 읽느냐에 따라 다른 숫자들로 표현된다. **기저 변환(change of basis)**은 이렇게 다른 "관점" 사이의 좌표를 변환하는 방법이다.

예를 들어 2차원 평면에서 표준기저 $\{(1,0), (0,1)\}$로 $(3, 2)$인 점은, $45^\circ$ 회전된 기저로는 다른 좌표값을 가진다. 하지만 점의 위치 자체는 변하지 않는다 — 단지 좌표 표현만 바뀔 뿐이다.

**닮음 변환(similarity transformation)** $B = P^{-1}AP$는 이 아이디어를 선형변환으로 확장한다. $A$가 어떤 기저에서의 선형변환 행렬이라면, $P^{-1}AP$는 다른 기저에서 같은 변환을 표현한 행렬이다. 대각화(diagonalization)는 기저변환의 특수한 경우로, 고유벡터들로 이루어진 기저(즉 "본질적 축")를 찾아 행렬을 대각행렬로 단순화하는 과정이다.

기저 변환은 모든 행렬 연산의 기초에 깔려 있다. 좌표변환, 텐서 변환 법칙, 그래픽스에서의 모델-뷰-프로젝션 변환, 양자역학에서의 슈뢰딩거 묘사와 하이젠베르크 묘사의 관계까지 모두 기저 변환의 언어로 표현된다.

---
## 정의

**기저 (basis):** 벡터공간 $V$의 기저 $B = \{b_1, \ldots, b_n\}$는 일차독립이고 $V$를 생성하는(span) 벡터들의 집합이다. 모든 $v \in V$는 유일한 좌표계수 $\alpha_i$를 가져
$$v = \alpha_1 b_1 + \cdots + \alpha_n b_n$$

**좌표벡터 (coordinate vector):** 기저 $B$에 대한 $v$의 좌표벡터는
$$[v]_B = \begin{pmatrix} \alpha_1 \\ \vdots \\ \alpha_n \end{pmatrix}$$

**기저변환 행렬 (change-of-basis matrix):** $B = \{b_1, \ldots, b_n\}$에서 $C = \{c_1, \ldots, c_n\}$으로의 기저변환 행렬 $P_{C \leftarrow B}$는 $B$의 각 벡터를 $C$ 좌표로 표현하여 열로 배열한 행렬이다:
$$P_{C \leftarrow B} = [[b_1]_C \; [b_2]_C \; \cdots \; [b_n]_C]$$

이 행렬은 $[v]_C = P_{C \leftarrow B} [v]_B$를 만족한다.

**표준기저에서의 기저변환:** 표준기저 $E$에서 기저 $B$로의 변환은
$$P_{E \leftarrow B} = [b_1 \; b_2 \; \cdots \; b_n]$$
즉, 기저벡터들을 열로 배열한 행렬이다. 반대 방향은 $P_{B \leftarrow E} = P_{E \leftarrow B}^{-1}$이다.

**닮음 (similarity):** 두 행렬 $A$와 $B$가 $B = P^{-1} A P$를 만족하는 가역행렬 $P$가 존재할 때, $A$와 $B$는 닮음(similar)이라 하고 $A \sim B$로 표기한다.

**대각화 (diagonalization):** $A$가 $P^{-1} A P = D$ ($D$ 대각행렬)를 만족하면 $A$는 대각화 가능하다. $P$의 열은 $A$의 고유벡터이고 $D$의 대각 성분은 대응하는 고유값이다.

---
## 주요 정리와 증명

### 정리 1: 기저변환 행렬의 성질

$V$의 기저 $B$, $C$에 대해 $[v]_C = P_{C \leftarrow B} [v]_B$이며, $P_{C \leftarrow B}$는 가역행렬이고 $(P_{C \leftarrow B})^{-1} = P_{B \leftarrow C}$이다.

**증명:** $v = \sum \alpha_i b_i$라 하자. $[b_i]_C$를 $P_{C \leftarrow B}$의 $i$번째 열이라 하면
$$[v]_C = \left[ \sum_{i=1}^n \alpha_i b_i \right]_C = \sum_{i=1}^n \alpha_i [b_i]_C = P_{C \leftarrow B} [v]_B$$

$P_{B \leftarrow C} P_{C \leftarrow B} = I$임을 보이면 된다. $w \in V$에 대해 $[w]_B = P_{B \leftarrow C} [w]_C$이므로
$$P_{B \leftarrow C} P_{C \leftarrow B} [v]_B = P_{B \leftarrow C} [v]_C = [v]_B$$
$[v]_B$는 임의의 벡터이므로 $P_{B \leftarrow C} P_{C \leftarrow B} = I$이다. 따라서 $P_{C \leftarrow B}$는 가역이고 역행렬은 $P_{B \leftarrow C}$다.

### 정리 2: 닮음 변환은 같은 선형변환을 표현한다

$T: V \to V$가 선형변환이고 $B$, $C$가 $V$의 두 기저라 하자. $T$의 $B$에 대한 행렬 표현을 $[T]_B$, $C$에 대한 표현을 $[T]_C$라 하면
$$[T]_C = P_{C \leftarrow B} [T]_B P_{B \leftarrow C} = P_{C \leftarrow B} [T]_B (P_{C \leftarrow B})^{-1}$$

즉, $[T]_C$와 $[T]_B$는 닮음 관계다.

**증명:** 임의의 $v \in V$에 대해 $[T(v)]_B = [T]_B [v]_B$이다. $[T(v)]_C = P_{C \leftarrow B} [T(v)]_B$이므로
$$[T(v)]_C = P_{C \leftarrow B} [T]_B [v]_B = P_{C \leftarrow B} [T]_B P_{B \leftarrow C} [v]_C$$

그런데 $[T(v)]_C = [T]_C [v]_C$이기도 하므로, $[v]_C$의 임의성에 의해 $[T]_C = P_{C \leftarrow B} [T]_B P_{B \leftarrow C}$가 성립한다.

### 정리 3: 닮음 불변량 (Similarity Invariants)

닮음 행렬 $A \sim B = P^{-1}AP$는 다음을 공유한다:
1. **행렬식:** $\det(B) = \det(A)$
2. **대각합:** $\text{tr}(B) = \text{tr}(A)$
3. **rank:** $\text{rank}(B) = \text{rank}(A)$
4. **특성다항식:** $p_B(\lambda) = p_A(\lambda)$
5. **고유값:** $\sigma(B) = \sigma(A)$ (중복도 포함)
6. **고유값의 대수적 중복도**

**증명 (행렬식):**
$$\det(B) = \det(P^{-1}AP) = \det(P^{-1})\det(A)\det(P) = \det(P)^{-1}\det(A)\det(P) = \det(A)$$

**증명 (대각합):** $\text{tr}(P^{-1}AP) = \text{tr}(APP^{-1}) = \text{tr}(A)$. (순환성: $\text{tr}(XY) = \text{tr}(YX)$)

**증명 (특성다항식):**
$$\det(B - \lambda I) = \det(P^{-1}AP - \lambda I) = \det(P^{-1}(A - \lambda I)P) = \det(A - \lambda I)$$

**증명 (rank):** $P$가 가역이므로 $P^{-1}$와 $P$는 전단사(bijection) 선형변환이다. rank는 가역변환에 의해 보존된다.

**참고:** 고유값이 같다고 해서 행렬이 닮음인 것은 아니다. 예를 들어 $\begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$와 $\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$는 모두 고유값 1을 가지지만 닮음이 아니다(조르당 표준형이 다름).

### 정리 4: 대각화는 기저변환의 특수한 경우

$n \times n$ 행렬 $A$가 대각화 가능하면 $A = PDP^{-1}$이다. 여기서 $D$는 $A$의 고유벡터로 이루어진 기저에서 $A$를 표현한 행렬이다.

**증명:** $P = [v_1 \; \cdots \; v_n]$을 $A$의 일차독립 고유벡터들을 열로 하는 행렬이라 하자. $B = \{v_1, \ldots, v_n\}$은 $\mathbb{R}^n$의 기저이다. $A$를 선형변환 $T(x) = Ax$로 볼 때, 표준기저 $E$에서 $T$의 행렬은 $A$ 자체다. 기저 $B$에서 $T$의 행렬을 $D$라 하면
$$D = P_{B \leftarrow E}^{-1} A P_{E \leftarrow B} = P^{-1} A P$$
$T(v_i) = \lambda_i v_i$이므로 $B$에서의 행렬 $D$는 대각행렬 $\text{diag}(\lambda_1, \ldots, \lambda_n)$이다. 따라서 $A = PDP^{-1}$.

### 정리 5: 기저변환과 선형변환의 합성

$S, T: V \to V$가 선형변환이고 $B$가 기저일 때
$$[S \circ T]_B = [S]_B [T]_B$$

서로 다른 기저 $B, C$에서는
$$[S \circ T]_C = P_{C \leftarrow B} [S]_B [T]_B P_{B \leftarrow C}$$

**증명:** $(S \circ T)(v) = S(T(v))$이므로, 기저 $B$에서 $[S \circ T]_B [v]_B = [S]_B [T(v)]_B = [S]_B [T]_B [v]_B$이다. 따라서 $[S \circ T]_B = [S]_B [T]_B$.

### 정리 6: 직교 기저변환

$B$와 $C$가 모두 정규직교기저(orthonormal basis)이면 $P = P_{C \leftarrow B}$는 직교행렬이다. 즉, $P^T P = I$이고 $P^{-1} = P^T$이다.

**증명:** 정규직교기저 $B = \{b_1, \ldots, b_n\}$, $C = \{c_1, \ldots, c_n\}$라 하자. $P$의 $j$번째 열은 $[b_j]_C$이며, 그 $i$번째 성분은 $\langle b_j, c_i \rangle$이다($C$가 정규직교이므로). 따라서
$$(P^T P)_{jk} = \sum_i \langle b_j, c_i \rangle \langle c_i, b_k \rangle = \langle b_j, b_k \rangle = \delta_{jk}$$
즉, $P^T P = I$이다. 따라서 $P$는 직교행렬이며 $P^{-1} = P^T$이다.

---
## 예제

**예제 1:** $v = (3, 2)$를 $B = \{(1, 1), (1, -1)\}$ 기저로 표현하라.

**풀이:** $[v]_B = (\alpha, \beta)$라 하면
$$v = \alpha(1, 1) + \beta(1, -1) = (\alpha + \beta, \alpha - \beta)$$
$$(\alpha + \beta, \alpha - \beta) = (3, 2)$$
$\alpha + \beta = 3$, $\alpha - \beta = 2$ → $\alpha = 5/2$, $\beta = 1/2$.
$$[v]_B = \begin{pmatrix} 5/2 \\ 1/2 \end{pmatrix}$$

**기저변환 행렬:** $P_{E \leftarrow B} = \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$.
$$[v]_B = P_{E \leftarrow B}^{-1} [v]_E = \frac{1}{-2} \begin{pmatrix} -1 & -1 \\ -1 & 1 \end{pmatrix} \begin{pmatrix} 3 \\ 2 \end{pmatrix} = \frac12 \begin{pmatrix} 5 \\ 1 \end{pmatrix}$$

**예제 2:** $A = \begin{pmatrix} 4 & -2 \\ 1 & 1 \end{pmatrix}$를 대각화하고 $A^n$을 계산하라.

**풀이:** 앞서 구한 고유값: $\lambda_1 = 2$, $\lambda_2 = 3$.
$v_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$, $v_2 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$.
$P = \begin{pmatrix} 1 & 2 \\ 1 & 1 \end{pmatrix}$, $D = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix}$, $P^{-1} = \begin{pmatrix} -1 & 2 \\ 1 & -1 \end{pmatrix}$.

$A^n = P D^n P^{-1} = \begin{pmatrix} 1 & 2 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 2^n & 0 \\ 0 & 3^n \end{pmatrix} \begin{pmatrix} -1 & 2 \\ 1 & -1 \end{pmatrix}$
$$= \begin{pmatrix} 2^n & 2\cdot3^n \\ 2^n & 3^n \end{pmatrix} \begin{pmatrix} -1 & 2 \\ 1 & -1 \end{pmatrix} = \begin{pmatrix} -2^n + 2\cdot3^n & 2^{n+1} - 2\cdot3^n \\ -2^n + 3^n & 2^{n+1} - 3^n \end{pmatrix}$$

**예제 3:** 표준기저 $E$에서 $B = \{(1, 0), (0, 2)\}$로의 기저변환 행렬을 구하고, $A = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix}$의 $B$ 표현을 구하라.

**풀이:** $P_{E \leftarrow B} = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$, $P_{B \leftarrow E} = \begin{pmatrix} 1 & 0 \\ 0 & 1/2 \end{pmatrix}$.
$$[T]_B = P_{B \leftarrow E} [T]_E P_{E \leftarrow B} = \begin{pmatrix} 1 & 0 \\ 0 & 1/2 \end{pmatrix} \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$$
$$= \begin{pmatrix} 1 & 0 \\ 0 & 1/2 \end{pmatrix} \begin{pmatrix} 1 & 4 \\ 3 & 8 \end{pmatrix} = \begin{pmatrix} 1 & 4 \\ 3/2 & 4 \end{pmatrix}$$

확인: $T(1, 0) = (1, 3)$은 표준기저로 $(1, 3)$이고 $B$로는 $(1, 3/2)$다 — $[T]_B$의 첫 열과 일치.

**예제 4 (직교 기저변환):** $B = \{(1, 0), (0, 1)\}$ (표준기저), $C = \{(1/\sqrt{2}, 1/\sqrt{2}), (-1/\sqrt{2}, 1/\sqrt{2})\}$ ($45^\circ$ 회전) 사이의 기저변환.

**풀이:** $P_{E \leftarrow C} = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & -1 \\ 1 & 1 \end{pmatrix}$. $P_{C \leftarrow E} = P_{E \leftarrow C}^{-1} = P_{E \leftarrow C}^T$ (직교행렬이므로) $= \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}$.

벡터 $v = (3, 2)$의 $C$ 좌표:
$$[v]_C = P_{C \leftarrow E} [v]_E = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix} \begin{pmatrix} 3 \\ 2 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 5 \\ -1 \end{pmatrix}$$

즉, 회전된 기저에서 $v$의 좌표는 $(5/\sqrt{2}, -1/\sqrt{2})$다.

**예제 5:** 행렬 $A = \begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}$ ($90^\circ$ 회전)의 고유값을 이용해 대각화 가능한지 판정하라.

**풀이:** 특성방정식: $\det(A - \lambda I) = \det\begin{pmatrix} -\lambda & 1 \\ -1 & -\lambda \end{pmatrix} = \lambda^2 + 1 = 0$.
고유값: $\lambda = \pm i$ (복소수). 복소수 위에서는 고유벡터가 존재하므로 대각화 가능:
$$P = \begin{pmatrix} 1 & 1 \\ i & -i \end{pmatrix}, \quad D = \begin{pmatrix} i & 0 \\ 0 & -i \end{pmatrix}$$
실수 위에서는 대각화 불가능하지만, SVD는 실수에서도 존재한다.

**예제 6 (닮음 불변량 확인):** $A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$의 대각화 $D = \begin{pmatrix} 3 & 0 \\ 0 & 1 \end{pmatrix}$와 닮음 불변량을 확인하라.

**풀이:** $P = \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$, $P^{-1} = \frac12 \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$.
$\det(A) = 4 - 1 = 3$, $\det(D) = 3\cdot1 = 3$ ✓
$\text{tr}(A) = 2 + 2 = 4$, $\text{tr}(D) = 3 + 1 = 4$ ✓
고유값: $\sigma(A) = \{3, 1\} = \sigma(D)$ ✓

**예제 7 (기저변환의 합성):** 세 기저 $A$, $B$, $C$가 있을 때 $P_{C \leftarrow A} = P_{C \leftarrow B} P_{B \leftarrow A}$임을 확인하라. $\mathbb{R}^2$에서 $B = \{(1, 1), (1, -1)\}$, $C = \{(1, 0), (0, 2)\}$로 두고 검산하라.

**풀이:** $P_{E \leftarrow B} = \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$, $P_{B \leftarrow E} = \frac12 \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$.
$P_{E \leftarrow C} = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$, $P_{C \leftarrow E} = \begin{pmatrix} 1 & 0 \\ 0 & 1/2 \end{pmatrix}$.

$P_{C \leftarrow B} = P_{C \leftarrow E} P_{E \leftarrow B} = \begin{pmatrix} 1 & 0 \\ 0 & 1/2 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1/2 & -1/2 \end{pmatrix}$.

$P_{B \leftarrow C} = (P_{C \leftarrow B})^{-1} = \begin{pmatrix} 1/2 & 1 \\ 1/2 & -1 \end{pmatrix}$ (직접 확인).

$P_{C \leftarrow A}$와 $P_{C \leftarrow B} P_{B \leftarrow A}$가 같은지 확인할 수 있다: 어떤 기저 $A$에 대해서도 $P_{C \leftarrow A} = P_{C \leftarrow B} P_{B \leftarrow A}$가 성립하며, 이는 기저변환 행렬이 함수 합성처럼 작동함을 의미한다.

**예제 8 (고유값과 기저변환):** $A = \begin{pmatrix} 5 & -2 \\ -2 & 5 \end{pmatrix}$의 고유값과 고유벡터를 구하고, 고유벡터 기저에서 $A$의 표현이 대각행렬임을 확인하라.

**풀이:** $\det\begin{pmatrix} 5-\lambda & -2 \\ -2 & 5-\lambda \end{pmatrix} = (5-\lambda)^2 - 4 = \lambda^2 - 10\lambda + 21 = (\lambda-3)(\lambda-7)$.
$\lambda_1 = 3$, $\lambda_2 = 7$.

$\lambda_1 = 3$: $\begin{pmatrix} 2 & -2 \\ -2 & 2 \end{pmatrix}v = 0$ → $v_1 = \frac{1}{\sqrt{2}}(1, 1)$.
$\lambda_2 = 7$: $\begin{pmatrix} -2 & -2 \\ -2 & -2 \end{pmatrix}v = 0$ → $v_2 = \frac{1}{\sqrt{2}}(1, -1)$.

$P = [v_1 \; v_2]$라 하면 $P^T A P = \begin{pmatrix} 3 & 0 \\ 0 & 7 \end{pmatrix} = D$.

고유벡터 기저에서 $A$는 대각행렬 $D$로 표현된다. 즉, $A$의 작용은 $v_1$ 방향을 3배, $v_2$ 방향을 7배 늘리는 단순한 연산이 된다.

**예제 9 (동시에 두 번 기저변환):** $T: \mathbb{R}^2 \to \mathbb{R}^2$가 $T(x, y) = (2x + y, x - y)$로 정의될 때, $B = \{(1, 1), (1, -1)\}$에서 $T$의 행렬을 구하라.

**풀이:** 표준기저에서 $[T]_E = \begin{pmatrix} 2 & 1 \\ 1 & -1 \end{pmatrix}$.
$P_{E \leftarrow B} = \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$, $P_{B \leftarrow E} = \frac12 \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$ (직교행렬의 스케일 버전).

$$[T]_B = P_{B \leftarrow E} [T]_E P_{E \leftarrow B} = \frac12 \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$
먼저 $[T]_E P_{E \leftarrow B} = \begin{pmatrix} 2 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} = \begin{pmatrix} 3 & 1 \\ 0 & 2 \end{pmatrix}$.
$$[T]_B = \frac12 \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} 3 & 1 \\ 0 & 2 \end{pmatrix} = \frac12 \begin{pmatrix} 3 & 3 \\ 3 & -1 \end{pmatrix} = \begin{pmatrix} 3/2 & 3/2 \\ 3/2 & -1/2 \end{pmatrix}$$

**참고:** 기저변환의 관점은 선형대수의 통일된 언어를 제공한다. 행렬의 곱셈, 역행렬, 대각화, SVD, 스펙트럼 분해를 모두 "기저를 바꾼다"는 하나의 프레임워크로 이해할 수 있다. 이 통일성이 선형대수를 강력하게 만드는 핵심 요소다.

---
## 연결

- **[좌표기하와 이차곡선](coordinate-geometry.html)** : 기저 변환은 좌표계를 바꾸어 이차곡선의 표준형을 찾는 과정과 직접 연결된다.
- **[고유값·고유벡터](eigenvalues.html)** : 대각화는 기저변환을 통해 행렬을 가장 단순한 형태(대각행렬)로 만드는 과정이다.
- **[대칭행렬·스펙트럼 정리](spectral-theorem.html)** : 직교 기저변환은 대칭행렬의 직교 대각화와 동일하며, 내적을 보존하는 변환이다.
