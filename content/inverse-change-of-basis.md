---
title: 역행렬과 기저 변환
slug: inverse-change-of-basis
---

## 직관적 설명

어떤 변환을 **되돌리는** 것이 가능할까? 선형변환 $T$가 공간을 찌그러뜨리지 않고(즉, 차원을 줄이지 않고) 그대로 보존한다면, $T$를 되돌리는 역변환 $T^{-1}$이 존재한다. 행렬의 언어로는 $A^{-1}$이 **역행렬(inverse matrix)**이다. $A^{-1} A = I = A A^{-1}$이 성립하며, 이는 "변환 후 되돌리면 원래대로"라는 뜻이다.

기저 변환(change of basis)은 이와 별개로, **같은 현상을 다른 좌표계에서 바라보는** 방법이다. 3차원 공간의 한 점이 있다고 하자. 이 점의 좌표는 기준 좌표계(기저)에 따라 달라진다. 기저 변환 행렬 $P$는 한 기저로 표현된 벡터를 다른 기저로 변환한다. 두 개념은 밀접하게 연결되어 있다: 다른 기저에서 같은 선형변환을 표현하는 행렬은 $P^{-1} A P$의 형태가 된다.

이 개념의 실용적 예로는 GPS 좌표 변환(지구 중심 좌표계 ↔ 위경도), 카메라 캘리브레이션(월드 좌표계 ↔ 카메라 좌표계), 결정 구조 분석(단위세포의 기저 변경) 등이 있다. 기저 변환은 **관점의 변화**를 수학적으로 정밀하게 표현하는 도구다.

## 정의

**역행렬(inverse matrix):** $n \times n$ 정사각행렬 $A$에 대해

$$A A^{-1} = I_n = A^{-1} A$$

를 만족하는 $n \times n$ 행렬 $A^{-1}$이 존재할 때, $A$를 **가역(invertible)** 또는 **정칙(nonsingular)**이라 하고 $A^{-1}$을 $A$의 역행렬이라 한다.

**가역행렬의 동치 조건:** $n \times n$ 행렬 $A$에 대해 다음은 모두 동치이다.

- $A$는 가역이다.
- $\det A \neq 0$
- $\text{rank}(A) = n$
- $A$의 열(또는 행)들은 일차독립이다.
- $Ax = 0$의 유일해는 $x = 0$이다.
- $Ax = b$는 모든 $b \in \mathbb{R}^n$에 대해 유일해를 가진다.

**기저(basis):** 벡터공간 $V$의 기저 $\mathcal{B} = \{b_1, \dots, b_n\}$는 일차독립이고 $V$를 생성하는 벡터들의 집합이다. 모든 $v \in V$는 기저 벡터들의 선형결합으로 **유일하게** 표현된다:

$$v = \alpha_1 b_1 + \cdots + \alpha_n b_n$$

**좌표 벡터(coordinate vector):** $v$의 기저 $\mathcal{B}$에 대한 좌표벡터 $[v]_{\mathcal{B}}$는 위 표현의 계수들로 이루어진 열벡터 $(\alpha_1, \dots, \alpha_n)^T$이다.

**기저 변환 행렬(change-of-basis matrix):** $\mathcal{B} = \{b_1, \dots, b_n\}$과 $\mathcal{C} = \{c_1, \dots, c_n\}$이 $V$의 두 기저일 때, $\mathcal{C}$-좌표를 $\mathcal{B}$-좌표로 변환하는 행렬 $P_{\mathcal{C} \to \mathcal{B}}$는

$$P_{\mathcal{C} \to \mathcal{B}} = \begin{pmatrix} [c_1]_{\mathcal{B}} & [c_2]_{\mathcal{B}} & \cdots & [c_n]_{\mathcal{B}} \end{pmatrix}$$

즉, $\mathcal{C}$의 각 기저 벡터를 $\mathcal{B}$로 표현한 좌표벡터를 열로 하는 행렬이다. 임의의 벡터 $v$에 대해

$$[v]_{\mathcal{B}} = P_{\mathcal{C} \to \mathcal{B}} [v]_{\mathcal{C}}$$

**유사변환(similarity transformation):** 선형변환 $T: V \to V$가 기저 $\mathcal{B}$에 대해 행렬 $A$로 표현된다고 하자. 같은 변환을 기저 $\mathcal{C}$로 표현한 행렬 $B$는

$$B = P^{-1} A P$$

여기서 $P = P_{\mathcal{C} \to \mathcal{B}}$ (또는 $P = P_{\mathcal{B} \to \mathcal{C}}$, 정의에 따라 다를 수 있으므로 일관성이 중요하다).

## 주요 정리와 증명

### 정리 1: 역행렬의 유일성

역행렬이 존재하면 유일하다.

**증명:** $A$에 대해 두 개의 역행렬 $X$와 $Y$가 존재한다고 가정하자 ($AX = I = XA$, $AY = I = YA$). 그러면

$$X = XI = X(AY) = (XA)Y = IY = Y$$

따라서 $X = Y$이다.

### 정리 2: 가역성과 행렬식

$\det A \neq 0$일 필요충분조건은 $A$가 가역인 것이다. 가역일 때

$$A^{-1} = \frac{1}{\det A} C^T$$

여기서 $C$는 여인수 행렬(cofactor matrix)로 $C_{ij} = (-1)^{i+j} \det(A_{ij})$이고, $C^T$는 **수반행렬(adjugate matrix)**이라 한다.

**증명:** 행렬 $A$와 그 여인수 행렬 $C^T$의 곱을 계산하면

$$(A \cdot C^T)_{ik} = \sum_{j=1}^{n} a_{ij} (C^T)_{jk} = \sum_{j=1}^{n} a_{ij} C_{kj}$$

$i = k$인 경우 이 값은 $\det(A)$가 되고, $i \neq k$인 경우 (다른 행의 여인수 전개) 0이 된다. 따라서

$$A \cdot C^T = \det(A) I_n$$

$\det(A) \neq 0$이면 $A^{-1} = \frac{1}{\det A} C^T$가 성립한다.

역으로 $A^{-1}$이 존재하면 $AA^{-1} = I$에 행렬식을 취해 $\det(A) \det(A^{-1}) = 1$이므로 $\det(A) \neq 0$이다.

### 정리 3: 가우스-조르단으로 역행렬 구하기

첨가행렬 $(A | I)$에 가우스-조르단 소거를 적용하여 $(I | A^{-1})$를 얻을 수 있다.

**증명:** 초등 행 연산은 기본행렬(elementary matrix) $E$를 왼쪽에 곱하는 것과 같다. $A$를 $I$로 변환하는 기본행렬들의 곱을 $E = E_k \cdots E_2 E_1$이라 하면

$$E A = I \;\Rightarrow\; E = A^{-1}$$

동일한 연산을 $I$에 적용하면 $E I = E = A^{-1}$이 된다.

### 정리 4: $(AB)^{-1} = B^{-1} A^{-1}$

$A, B$가 모두 가역일 때 $(AB)^{-1} = B^{-1} A^{-1}$이다.

**증명:** $(AB)(B^{-1} A^{-1}) = A(B B^{-1}) A^{-1} = A I A^{-1} = A A^{-1} = I$. 따라서 $B^{-1} A^{-1}$은 $AB$의 역행렬이며, 유일성에 의해 $(AB)^{-1} = B^{-1} A^{-1}$이다.

### 정리 5: 기저 변환의 성질

벡터공간 $V$의 두 기저 $\mathcal{B}$와 $\mathcal{C}$에 대해, 기저 변환 행렬 $P = P_{\mathcal{C} \to \mathcal{B}}$는 가역이며 $P^{-1} = P_{\mathcal{B} \to \mathcal{C}}$이다.

**증명:** $P$는 $\mathcal{C}$의 각 기저 벡터를 $\mathcal{B}$의 선형결합으로 표현한 열들로 구성된다. $\mathcal{C}$의 벡터들은 일차독립이므로 $P$의 열들도 일차독립이다. 따라서 $\det P \neq 0$이고 $P$는 가역이다.

$P^{-1}$의 열들은 $\mathcal{B}$의 각 기저 벡터를 $\mathcal{C}$로 표현한 좌표이므로 $P^{-1} = P_{\mathcal{B} \to \mathcal{C}}$이다.

### 정리 6: 유사변환

$A$가 기저 $\mathcal{B}$에 대한 선형변환 $T$의 행렬 표현이라면, 기저 $\mathcal{C}$에 대한 $T$의 행렬 표현은

$$A' = P^{-1} A P$$

여기서 $P = P_{\mathcal{C} \to \mathcal{B}}$이다. 즉, $P$는 $\mathcal{C}$-좌표를 $\mathcal{B}$-좌표로 변환한다.

**증명:** 임의의 $v \in V$에 대해 $w = T(v)$라 하자. $[w]_{\mathcal{B}} = A [v]_{\mathcal{B}}$이다. $P[v]_{\mathcal{C}} = [v]_{\mathcal{B}}$이므로

$$[w]_{\mathcal{B}} = A P [v]_{\mathcal{C}}$$

한편 $[w]_{\mathcal{C}} = P^{-1} [w]_{\mathcal{B}}$이므로

$$[w]_{\mathcal{C}} = P^{-1} A P [v]_{\mathcal{C}}$$

따라서 $\mathcal{C}$에 대한 $T$의 행렬은 $P^{-1} A P$이다.

## 예제

**예제 1:** $A = \begin{pmatrix} 2 & 1 \\ 5 & 3 \end{pmatrix}$의 역행렬을 구하라.

**풀이:** $\det A = 2\cdot3 - 1\cdot5 = 6 - 5 = 1 \neq 0$이므로 가역이다.

$$A^{-1} = \frac{1}{1} \begin{pmatrix} 3 & -1 \\ -5 & 2 \end{pmatrix} = \begin{pmatrix} 3 & -1 \\ -5 & 2 \end{pmatrix}$$

검증: $AA^{-1} = \begin{pmatrix} 2 & 1 \\ 5 & 3 \end{pmatrix} \begin{pmatrix} 3 & -1 \\ -5 & 2 \end{pmatrix} = \begin{pmatrix} 6-5 & -2+2 \\ 15-15 & -5+6 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$.

**예제 2:** $A = \begin{pmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 0 & 0 & 1 \end{pmatrix}$의 역행렬을 가우스-조르단 소거로 구하라.

**풀이:** 첨가행렬 $(A|I)$:

$$\left(\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 4 & 0 & 1 & 0 \\
0 & 0 & 1 & 0 & 0 & 1
\end{array}\right)$$

$R_2 \leftarrow R_2 - 4R_3$:

$$\left(\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 0 & 0 & 1 & -4 \\
0 & 0 & 1 & 0 & 0 & 1
\end{array}\right)$$

$R_1 \leftarrow R_1 - 2R_2 - 3R_3$:

$$\left(\begin{array}{ccc|ccc}
1 & 0 & 0 & 1 & -2 & 5 \\
0 & 1 & 0 & 0 & 1 & -4 \\
0 & 0 & 1 & 0 & 0 & 1
\end{array}\right)$$

따라서 $A^{-1} = \begin{pmatrix} 1 & -2 & 5 \\ 0 & 1 & -4 \\ 0 & 0 & 1 \end{pmatrix}$.

**예제 3:** $\mathbb{R}^2$에서 표준기저 $\mathcal{S} = \{e_1 = (1,0), e_2 = (0,1)\}$와 다른 기저 $\mathcal{B} = \{b_1 = (1,1), b_2 = (1,-1)\}$를 고려하자. $v = (3, 1)$의 $\mathcal{B}$-좌표를 구하라.

**풀이:** $P_{\mathcal{B} \to \mathcal{S}} = \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$ (즉, $\mathcal{B}$의 벡터들을 표준기저로 표현한 열들). $[v]_{\mathcal{S}} = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$.

$$[v]_{\mathcal{B}} = P_{\mathcal{B} \to \mathcal{S}}^{-1} [v]_{\mathcal{S}}$$

$P^{-1}$를 구한다: $\det P = 1\cdot(-1) - 1\cdot1 = -2$, $P^{-1} = -\frac{1}{2} \begin{pmatrix} -1 & -1 \\ -1 & 1 \end{pmatrix} = \begin{pmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & -\frac{1}{2} \end{pmatrix}$.

$$[v]_{\mathcal{B}} = \begin{pmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & -\frac{1}{2} \end{pmatrix} \begin{pmatrix} 3 \\ 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$$

검증: $2b_1 + 1b_2 = 2(1,1) + 1(1,-1) = (3,1) = v$. 따라서 $\mathcal{B}$-좌표는 $(2, 1)^T$이다.

**예제 4:** $\mathbb{R}^2$에서 반시계 $90^\circ$ 회전 변환 $T$가 표준기저에서 $A = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$로 표현된다. 기저 $\mathcal{B} = \{b_1 = (1,1), b_2 = (1,-1)\}$에서 $T$의 행렬 표현 $A'$을 구하라.

**풀이:** $P = P_{\mathcal{B} \to \mathcal{S}} = \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$ ($\mathcal{B}$-좌표를 표준좌표로 변환). $P^{-1}$은 예제 3에서 구한 대로 $\begin{pmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & -\frac{1}{2} \end{pmatrix}$.

$$A' = P^{-1} A P = \begin{pmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & -\frac{1}{2} \end{pmatrix} \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

먼저 $AP$: $\begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} = \begin{pmatrix} -1 & 1 \\ 1 & 1 \end{pmatrix}$

$P^{-1}(AP)$: $\begin{pmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & -\frac{1}{2} \end{pmatrix} \begin{pmatrix} -1 & 1 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} \frac{-1+1}{2} & \frac{1+1}{2} \\ \frac{-1-1}{2} & \frac{1-1}{2} \end{pmatrix} = \begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}$

$\mathcal{B}$-기저에서 회전 변환은 $\begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}$로 표현된다. 이는 표준기저에서의 표현과 같은 형태(반시계 $90^\circ$)이지만, 기저가 다르므로 같은 행렬이 아님에 주의하라.

## 연결

- **[행렬식의 기하학](determinant.html)** : $\det A \neq 0$이 역행렬 존재의 필요충분조건이며, $A^{-1} = \frac{1}{\det A} C^T$로 계산된다.
- **[가우스 소거와 RREF](gaussian-elimination.html)** : 가우스-조르단 소거는 역행렬을 계산하는 실용적인 알고리즘이다.
- **[행렬곱과 선형변환](matrix-multiplication.html)** : 행렬과 선형변환의 관계는 기저 변환의 개념적 기초다.
- **[rank·열공간·널공간](rank-nullspace.html)** : $A$가 가역일 때 $\text{rank}(A) = n$이고 $\text{Null}(A) = \{0\}$이다.
- **[고유값·고유벡터](eigenvalues.html)** : $P^{-1}AP$를 대각행렬로 만드는 기저 변환을 대각화(diagonalization)라고 한다.
- **[SVD](svd.html)** : 특이값 분해는 서로 다른 두 기저(입력/출력)에서의 변환을 대각화한다.
