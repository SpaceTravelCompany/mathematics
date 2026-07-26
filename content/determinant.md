---
title: 행렬식의 기하학
slug: determinant
---

## 직관적 설명

행렬식(determinant)은 정사각행렬이 공간을 변환할 때 **부피가 몇 배로 늘어나는지**를 나타내는 값이다. 2차원에서는 넓이의 확대율, 3차원에서는 부피의 확대율이다. 행렬식이 0이라면 변환이 공간을 납작하게 만든다는 뜻이다 — 예를 들어 3차원 공간을 2차원 평면으로 눌러 버리면 부피가 0이 된다.

행렬식이 음수라면 변환이 **방향(orientation)을 뒤집었다**는 의미다. 왼손 좌표계가 오른손 좌표계로 바뀌는 것이다. 행렬식의 절대값이 2라면 단위 정육면체의 부피가 2배가 된 정육면체(또는 평행육면체)로 변환되었음을 뜻한다.

행렬식은 적분에서 변수 변환(야코비안, Jacobian determinant)으로 등장하며, 물리에서는 위상 공간의 부피 변화를 계산하는 데 사용된다. 3D 모델링에서는 법선 벡터의 변환에 행렬식이 관여한다. 무엇보다 $\det A = 0$은 $A$가 가역(invertible)이 아님(역행렬이 존재하지 않음)을 판정하는 가장 빠른 지표다.

## 정의

**행렬식(determinant):** $n \times n$ 정사각행렬 $A$의 행렬식 $\det(A)$는 다음 세 공리를 만족하는 유일한 함수 $\det: \mathbb{R}^{n \times n} \to \mathbb{R}$로 정의된다.

1. **다중선형성(multilinearity):** 각 열에 대해 선형이다. 즉,
   $$\det(a_1, \dots, a_{i-1}, \alpha u + \beta v, a_{i+1}, \dots, a_n) = \alpha \det(a_1, \dots, u, \dots, a_n) + \beta \det(a_1, \dots, v, \dots, a_n)$$

2. **교대성(alternating):** 두 열을 교환하면 부호가 바뀐다.
   $$\det(\dots, a_i, \dots, a_j, \dots) = -\det(\dots, a_j, \dots, a_i, \dots)$$

3. **정규화(normalization):** 단위행렬 $I_n$의 행렬식은 1이다.
   $$\det(I_n) = 1$$

**$2 \times 2$ 행렬식:**

$$\det\begin{pmatrix} a & b \\ c & d \end{pmatrix} = ad - bc$$

**$3 \times 3$ 행렬식 (사루스 법칙, Sarrus' rule):**

$$\det\begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{pmatrix} = a_{11}a_{22}a_{33} + a_{12}a_{23}a_{31} + a_{13}a_{21}a_{32} - a_{13}a_{22}a_{31} - a_{11}a_{23}a_{32} - a_{12}a_{21}a_{33}$$

**라플라스 전개(Laplace expansion):** $n \times n$ 행렬 $A$의 행렬식은 어떤 행(또는 열)을 따라 전개하여 계산할 수 있다. $i$번째 행을 따라 전개하면:

$$\det(A) = \sum_{j=1}^{n} (-1)^{i+j} a_{ij} \det(A_{ij})$$

여기서 $A_{ij}$는 $A$에서 $i$번째 행과 $j$번째 열을 제거한 $(n-1) \times (n-1)$ **소행렬(minor)** 이고, $C_{ij} = (-1)^{i+j} \det(A_{ij})$를 **여인수(cofactor)**라 한다.

## 주요 정리와 증명

### 정리 1: $\det(AB) = \det(A) \det(B)$

$n \times n$ 정사각행렬 $A, B$에 대해

$$\det(AB) = \det(A) \det(B)$$

**증명:** $B$를 고정하고 함수 $f(A) = \det(AB)$를 정의하자. 행렬곱의 정의에 의해 $AB$의 $j$번째 열은 $A(b_{*j})$, 즉 $A$와 $B$의 $j$번째 열의 선형결합이다. $f$가 행렬식의 세 공리를 만족함을 보인다.

1. **다중선형성:** $AB$의 각 열은 $A$의 열들의 선형결합이므로 $f$는 각 열에 대해 선형이다.
2. **교대성:** $B$의 두 열을 교환하면 $AB$의 두 열이 교환되므로 $f$의 부호가 바뀐다.
3. **정규화:** $f(I) = \det(IB) = \det(B)$.

행렬식의 유일성에 의해 $f(A) = \det(A) f(I) = \det(A) \det(B)$이 성립한다.

**따름정리:** $\det(A^{-1}) = 1/\det(A)$ ($A$가 가역일 때). $AA^{-1} = I$에 행렬식을 취하면 $\det(A)\det(A^{-1}) = \det(I) = 1$이므로 성립한다.

### 정리 2: 행렬식의 기하학적 해석

$n \times n$ 행렬 $A$의 행렬식 $\det(A)$의 절대값은 $A$의 열벡터들이 이루는 **평행육면체(parallelotope)의 $n$차원 부피**와 같다.

**증명 (개요):** 단위 정육면체(단위행렬 $I$의 열벡터들이 이루는 도형)의 부피는 1이다. $A$를 선형변환으로 볼 때, $A$는 단위 정육면체를 $A$의 열벡터들이 이루는 평행육면체로 변환한다. 선형변환에 의한 부피 변화율이 $\det(A)$임을 보일 수 있다.

구체적으로 축소된 행렬식(reduced determinant)의 성질을 이용하거나, 그람-슈미트 직교화 과정에서 부피 변화가 행렬식의 곱으로 표현됨을 보임으로써 증명할 수 있다.

### 정리 3: $\det A \neq 0$일 필요충분조건

$n \times n$ 행렬 $A$에 대해 다음은 모두 동치(equivalent)이다.

1. $\det A \neq 0$
2. $A$는 가역(invertible)이다.
3. $A$의 열들은 일차독립이다.
4. $A$의 행들은 일차독립이다.
5. $\text{rank}(A) = n$
6. $\text{Null}(A) = \{0\}$
7. $Ax = b$는 모든 $b$에 대해 유일해를 가진다.

**증명:** 위 동치 관계 중 일부를 증명한다.

($1 \Rightarrow 2$) $\det A \neq 0$이면 $A$가 가역임을 보인다. 여인수 행렬(cofactor matrix) $C$ ($C_{ij} = (-1)^{i+j} \det(A_{ji})$)를 이용하면 $A^{-1} = \frac{1}{\det A} C^T$임을 확인할 수 있다.

($2 \Rightarrow 3$) $A$가 가역이면 $Ax = 0$에 $A^{-1}$을 곱해 $x = 0$을 얻는다. 따라서 $\text{Null}(A) = \{0\}$이고, $A$의 열들은 일차독립이다.

($3 \Rightarrow 1$) 열들이 일차독립이면 $A$의 RREF는 $I_n$이다. 가우스 소거 과정에서 각 초등 행 연산에 대응하는 기본행렬 $E$에 대해 $\det(EA) = \det(E)\det(A)$이고, $\det(E) \neq 0$이다. $A$를 $I_n$으로 변환하는 기본행렬들의 곱을 $E$라 하면 $\det(E)\det(A) = \det(I) = 1$이므로 $\det(A) \neq 0$이다.

### 정리 4: 기본 행 연산과 행렬식

기본 행 연산이 행렬식에 미치는 영향:

1. **행 교환:** $\det$의 부호가 바뀐다. $\det(R_i \leftrightarrow R_j) = -\det(A)$
2. **행 스케일링:** $\det(R_i \leftarrow c R_i) = c \det(A)$
3. **행 더하기:** $\det(R_i \leftarrow R_i + c R_j) = \det(A)$ (행렬식 변화 없음)

### 정리 5: 전치 행렬의 행렬식

$\det(A^T) = \det(A)$

**증명:** $A = LU$ 분해(하삼각×상삼각, 적절한 행 교환 포함)를 이용하거나, 라플라스 전개에서 행과 열의 대칭성을 관찰하면 증명할 수 있다.

## 예제

**예제 1:** $\det\begin{pmatrix} 3 & 1 \\ 2 & -4 \end{pmatrix}$를 계산하라.

**풀이:** $\det = (3)(-4) - (1)(2) = -12 - 2 = -14$.

**예제 2:** $\det\begin{pmatrix} 1 & 0 & 2 \\ -1 & 3 & 1 \\ 2 & 1 & -2 \end{pmatrix}$를 사루스 법칙으로 계산하라.

**풀이:** 사루스 법칙에 의해

$$\det = 1\cdot3\cdot(-2) + 0\cdot1\cdot2 + 2\cdot(-1)\cdot1 - 2\cdot3\cdot2 - 1\cdot1\cdot1 - 0\cdot(-1)\cdot(-2)$$

$$= -6 + 0 + (-2) - 12 - 1 - 0 = -21$$

**예제 3:** $A = \begin{pmatrix} 2 & 1 & 0 \\ 1 & 3 & 1 \\ 0 & 1 & 2 \end{pmatrix}$의 행렬식을 라플라스 전개로 계산하라.

**풀이:** 1열을 따라 전개한다.

$$\det(A) = 2 \cdot \det\begin{pmatrix} 3 & 1 \\ 1 & 2 \end{pmatrix} - 1 \cdot \det\begin{pmatrix} 1 & 0 \\ 1 & 2 \end{pmatrix} + 0 \cdot \det\begin{pmatrix} 1 & 0 \\ 3 & 1 \end{pmatrix}$$

$$= 2(3\cdot2 - 1\cdot1) - 1(1\cdot2 - 0\cdot1) = 2(6-1) - 1(2-0) = 10 - 2 = 8$$

**예제 4:** $\det\begin{pmatrix} 1 & 2 & 3 & 4 \\ 0 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}$을 계산하라 (관찰로).

**풀이:** 두 번째 행이 영행이므로 행렬식은 0이다. 영행이 포함된 행렬은 항상 행렬식이 0이다 (다중선형성에서 스칼라 0을 곱한 것으로 볼 수 있으므로).

**예제 5:** $A = \begin{pmatrix} 2 & 0 & 0 \\ 0 & -3 & 0 \\ 0 & 0 & 5 \end{pmatrix}$의 행렬식을 구하라.

**풀이:** 대각행렬(diagonal matrix)의 행렬식은 대각 원소의 곱이다. $\det(A) = 2 \cdot (-3) \cdot 5 = -30$. 이는 각 축 방향의 확대율이 각각 2, -3, 5이므로 부피 변화율이 $2 \times (-3) \times 5 = -30$임을 의미한다 (방향이 한 번 뒤집혔으므로 음수).

## 연결

- **[역행렬과 기저 변환](topics/inverse-change-of-basis.html)** : $\det A = 0$은 역행렬이 존재하지 않을 조건이며, $\det A \neq 0$일 때 $A^{-1} = \frac{1}{\det A} C^T$로 구한다.
- **[선형결합·span·일차독립](topics/span-independence.html)** : $\det A \neq 0$은 열(또는 행)들이 일차독립임을 의미한다.
- **[rank·열공간·널공간](topics/rank-nullspace.html)** : $\det A \neq 0$일 때 $\text{rank}(A) = n$ (full rank)이다.
- **[행렬곱과 선형변환](topics/matrix-multiplication.html)** : 행렬식은 선형변환의 부피 확대율로, $\det(AB) = \det A \det B$는 합성변환의 부피 변화율이 각각의 곱임을 의미한다.
- **[고유값·고유벡터](topics/eigenvalues.html)** : $\det(A - \lambda I) = 0$이 특성방정식이며, 행렬식은 모든 고유값의 곱과 같다.
- **[야코비안·헤시안](topics/jacobian-hessian.html)** : 다변수 적분에서 변수 변환 시 야코비 행렬식이 부피 변화율을 결정한다.
