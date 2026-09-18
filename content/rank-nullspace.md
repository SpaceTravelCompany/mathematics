---
title: rank·열공간·널공간
slug: rank-nullspace
---

> 학습 순서 14 / 75 · [처음부터 읽기](math-language.html)

## 작은 예제로 시작하기

**앞에서 가져올 것:** span은 만들 수 있는 결과 전체이고, 소거의 피보트는 독립적인 제약의 자리다.

$A=\left(\begin{smallmatrix}1&0\\0&0\end{smallmatrix}\right)$를 적용하면 $(x,y)$가 $(x,0)$으로 바뀐다. 출력은 가로축 위에만 놓인다. 이 출력 집합이 열공간이며 그 차원인 rank는 1이다. 한편 $(0,y)$는 모두 $(0,0)$으로 바뀐다. 영벡터로 가는 입력의 집합이 널공간이고 그 차원도 1이다.

입력 공간은 2차원인데, 남는 방향 1개와 사라지는 방향 1개로 나뉜다. 이것이 $\operatorname{rank}(A)+\operatorname{nullity}(A)=\text{열의 수}$라는 식의 뜻이다. 행의 수가 아니라 **입력 성분 수**를 더해 얻는다는 점에 주의하자.

$Ax=(3,0)^T$는 입력 $(3,t)$라면 무엇이든 가능하지만, $Ax=(3,1)^T$는 불가능하다. 출력 공간에 목표 $b$가 있느냐가 해의 존재를 결정한다. 해 하나 $x_0$를 찾았을 때 널공간의 벡터 $z$를 더해도 $A(x_0+z)=b+0=b$이므로 또 다른 해가 된다.

**증명으로 이어 읽기:** rank-nullity 증명은 먼저 사라지는 방향의 기저를 고르고, 입력 전체의 기저가 되도록 나머지 방향을 보태는 방식이다. 보탠 방향의 출력들이 열공간의 기저가 되어 두 개수가 합쳐진다.

---

## 직관적 설명

선형변환 $T: V \to W$가 주어졌을 때, $V$의 모든 벡터는 $T$에 의해 $W$의 어떤 벡터로 옮겨간다. 이때 변환 후 **살아남는 차원**과 **사라지는 차원**이 있다. 살아남는 차원이 **rank(계수)**이고, 사라져서 영벡터가 되는 벡터들의 집합이 **널공간(nullspace, kernel)**이다.

선형변환 $T(x,y,z)=(x,y)$를 생각하자. 3차원 공간 전체를 평면으로 보내며 높이 성분 $z$를 버린다. 출력 공간의 차원인 rank는 2이고, 널공간은 $(0,0,z)$ 꼴의 벡터들로 이루어진 1차원 공간이다. 실제 지구의 지도 투영은 일반적으로 이런 선형변환과 다르다. rank와 널공간의 차원을 더하면 항상 원래 공간의 차원이 된다. 이것이 **rank-nullity 정리**이다.

이 개념은 연립방정식 $Ax = b$의 해의 존재 여부 판정에 직접 사용된다. $b$가 $A$의 열공간(column space)에 속하면 해가 존재하고, 속하지 않으면 해가 없다. 이미지 압축에서는 rank가 낮은 행렬이 압축률이 높은 행렬임을 의미한다. 제어공학에서는 시스템의 상태가 제어 가능한지를 판정하는 데 rank가 사용된다.

---
## 정의

**열공간(column space):** $m \times n$ 행렬 $A$의 열벡터들의 모든 선형결합의 집합을 **열공간**이라 하고 $\text{Col}(A)$로 표기한다.

$$\text{Col}(A) = \text{span}\{a_{*1}, a_{*2}, \dots, a_{*n}\} \subseteq \mathbb{R}^m$$

여기서 $a_{*j}$는 $A$의 $j$번째 열벡터이다.

**행공간(row space):** $A$의 행벡터들의 모든 선형결합의 집합을 **행공간**이라 하고 $\text{Row}(A)$로 표기한다.

$$\text{Row}(A) = \text{span}\{a_{1*}, a_{2*}, \dots, a_{m*}\} \subseteq \mathbb{R}^n$$

**널공간(nullspace, kernel):** $Ax = 0$을 만족하는 모든 $x \in \mathbb{R}^n$의 집합을 **널공간**이라 하고 $\text{Null}(A)$ 또는 $\ker(A)$로 표기한다.

$$\text{Null}(A) = \{x \in \mathbb{R}^n \mid Ax = 0\} \subseteq \mathbb{R}^n$$

**Rank(계수):** 행렬 $A$의 **rank** $\text{rank}(A)$는 열공간의 차원이다:

$$\text{rank}(A) = \dim(\text{Col}(A))$$

**Nullity:** 행렬 $A$의 **nullity** $\text{nullity}(A)$는 널공간의 차원이다:

$$\text{nullity}(A) = \dim(\text{Null}(A))$$

**기본 정리:** 행렬 $A$의 행공간과 열공간의 차원은 같다: $\dim(\text{Row}(A)) = \dim(\text{Col}(A)) = \text{rank}(A)$.

---
## 주요 정리와 증명

### 정리 1: Rank-Nullity 정리

$m \times n$ 행렬 $A$에 대해

$$\text{rank}(A) + \text{nullity}(A) = n$$

**증명:** $A$를 선형변환 $T_A: \mathbb{R}^n \to \mathbb{R}^m$, $T_A(x) = Ax$로 해석하자. $\text{Null}(A)$의 기저를 $\{u_1, \dots, u_k\}$라 하면 $k = \text{nullity}(A)$이다. 이 기저를 $\mathbb{R}^n$의 기저로 확장하자. 확장 정리에 의해 $\mathbb{R}^n$의 기저 $\{u_1, \dots, u_k, w_1, \dots, w_{n-k}\}$가 존재한다.

이제 $\{T_A(w_1), \dots, T_A(w_{n-k})\}$가 $\text{Col}(A)$의 기저임을 보이자.

**1. 생성(spanning):** 임의의 $x \in \mathbb{R}^n$을 기저로 표현하면

$$x = \sum_{i=1}^{k} \alpha_i u_i + \sum_{j=1}^{n-k} \beta_j w_j$$

$$T_A(x) = \sum_{i=1}^{k} \alpha_i T_A(u_i) + \sum_{j=1}^{n-k} \beta_j T_A(w_j) = \sum_{j=1}^{n-k} \beta_j T_A(w_j)$$

( $T_A(u_i) = 0$이므로 ). 따라서 $\text{Col}(A) = \text{span}\{T_A(w_1), \dots, T_A(w_{n-k})\}$.

**2. 일차독립:** $\sum_{j=1}^{n-k} c_j T_A(w_j) = 0$이라 하자.

$$T_A\!\left(\sum_{j=1}^{n-k} c_j w_j\right) = 0 \;\Rightarrow\; \sum_{j=1}^{n-k} c_j w_j \in \text{Null}(A)$$

따라서 $\sum_{j=1}^{n-k} c_j w_j = \sum_{i=1}^{k} d_i u_i$ (널공간의 기저 표현). 그런데 $\{u_1, \dots, u_k, w_1, \dots, w_{n-k}\}$는 $\mathbb{R}^n$의 기저이므로 일차독립이고, 따라서 모든 $c_j = 0$이고 모든 $d_i = 0$이다. 즉 $\{T_A(w_j)\}$는 일차독립이다.

1과 2에 의해 $\{T_A(w_1), \dots, T_A(w_{n-k})\}$는 $\text{Col}(A)$의 기저이므로 $\text{rank}(A) = n - k = n - \text{nullity}(A)$.

$$\therefore \text{rank}(A) + \text{nullity}(A) = n$$

### 정리 2: 연립방정식 $Ax = b$의 해의 존재

$b \in \mathbb{R}^m$에 대해 $Ax = b$가 해를 가질 필요충분조건은 $b \in \text{Col}(A)$이다.

**증명:** $Ax = b$는 $A$의 열벡터들의 선형결합으로 $b$를 표현하는 것과 같다:

$$Ax = x_1 a_{*1} + \cdots + x_n a_{*n} = b$$

따라서 $b$가 $A$의 열들의 선형결합, 즉 $\text{Col}(A)$에 속할 때에만 해가 존재한다.

### 정리 3: Rank와 행동치

$A$에 기본 행 연산(elementary row operation)을 적용해 얻은 행렬 $B$에 대해 $\text{Row}(A) = \text{Row}(B)$이고 $\text{rank}(A) = \text{rank}(B)$이다.

**증명:** 각 기본 행 연산(행 교환, 행 스케일링, 한 행의 배수를 다른 행에 더하기)은 행공간을 보존한다. 따라서 행동치인 행렬들은 같은 행공간을 가지며, rank는 행공간의 차원이므로 보존된다.

### 정리 4: 열공간과 행공간의 차원 일치

$\dim(\text{Col}(A)) = \dim(\text{Row}(A))$이다.

**증명:** $A$를 RREF(reduced row echelon form) $R$로 변환하면, $R$의 **pivot(선행 1)** 이 있는 열들이 $\text{Col}(A)$의 기저를 결정하고, pivot이 있는 행들이 $\text{Row}(A)$의 기저를 결정한다. pivot의 개수는 열공간과 행공간에서 동일하므로 두 차원은 같다.

---
## 예제

**예제 1:** $A = \begin{pmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \\ 1 & 1 & 2 \end{pmatrix}$의 rank, nullity, 열공간, 널공간을 구하라.

**풀이:** 먼저 RREF를 구한다.

$$\begin{pmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \\ 1 & 1 & 2 \end{pmatrix} \xrightarrow{R_2 \leftarrow R_2 - 2R_1} \begin{pmatrix} 1 & 2 & 3 \\ 0 & 0 & 0 \\ 1 & 1 & 2 \end{pmatrix} \xrightarrow{R_3 \leftarrow R_3 - R_1} \begin{pmatrix} 1 & 2 & 3 \\ 0 & 0 & 0 \\ 0 & -1 & -1 \end{pmatrix}$$

$$\xrightarrow{R_2 \leftrightarrow R_3} \begin{pmatrix} 1 & 2 & 3 \\ 0 & -1 & -1 \\ 0 & 0 & 0 \end{pmatrix} \xrightarrow{R_2 \leftarrow -R_2} \begin{pmatrix} 1 & 2 & 3 \\ 0 & 1 & 1 \\ 0 & 0 & 0 \end{pmatrix} \xrightarrow{R_1 \leftarrow R_1 - 2R_2} \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 0 \end{pmatrix}$$

Pivot이 2개(1열, 2열)이므로 $\text{rank}(A) = 2$이다. $n = 3$이므로 $\text{nullity}(A) = 3 - 2 = 1$이다.

**열공간:** Pivot 열에 대응하는 원래 행렬의 열들이 기저가 된다. $\text{Col}(A) = \text{span}\{(1, 2, 1), (2, 4, 1)\}$이다.

**널공간:** $Ax = 0$을 풀자. RREF에서 $x_1 + x_3 = 0$, $x_2 + x_3 = 0$이므로 $x_1 = -x_3$, $x_2 = -x_3$. 따라서

$$\text{Null}(A) = \left\{ t \begin{pmatrix} -1 \\ -1 \\ 1 \end{pmatrix} \;\middle|\; t \in \mathbb{R} \right\}$$

$\dim(\text{Null}(A)) = 1$이고, $\text{rank} + \text{nullity} = 2 + 1 = 3 = n$이 성립한다.

**예제 2:** $A = \begin{pmatrix} 1 & 0 & 2 \\ 0 & 1 & -1 \end{pmatrix}$에 대해 $b = (3, 1)$이 열공간에 속하는지 판정하고, 속한다면 해를 구하라.

**풀이:** $\text{Col}(A) = \text{span}\{(1, 0), (0, 1), (2, -1)\}$이다. $(1, 0)$과 $(0, 1)$이 $\mathbb{R}^2$ 전체를 생성하므로 $\text{Col}(A) = \mathbb{R}^2$이고 $b = (3, 1)$은 열공간에 속한다.

$Ax = b$를 풀면 $x_1 + 2x_3 = 3$, $x_2 - x_3 = 1$이다. 자유변수(free variable)는 $x_3$이므로

$$x = \begin{pmatrix} 3 - 2t \\ 1 + t \\ t \end{pmatrix} = \begin{pmatrix} 3 \\ 1 \\ 0 \end{pmatrix} + t \begin{pmatrix} -2 \\ 1 \\ 1 \end{pmatrix}, \quad t \in \mathbb{R}$$

**예제 3:** 행렬 $A = \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 1 & 0 & 1 \end{pmatrix}$의 rank를 구하고, rank-nullity 정리를 검증하라.

**풀이:** RREF를 구한다.

$$\begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 1 & 0 & 1 \end{pmatrix} \xrightarrow{R_3 \leftarrow R_3 - R_1} \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 0 & -1 & 1 \end{pmatrix} \xrightarrow{R_3 \leftarrow R_3 + R_2} \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 0 & 0 & 2 \end{pmatrix}$$

$$\xrightarrow{R_3 \leftarrow \frac{1}{2}R_3} \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{pmatrix} \xrightarrow{R_2 \leftarrow R_2 - R_3} \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \xrightarrow{R_1 \leftarrow R_1 - R_2} \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

RREF가 $I_3$이므로 $\text{rank}(A) = 3$이다. $n = 3$이므로 $\text{nullity}(A) = 0$이다. $Ax = 0$의 유일해는 $x = 0$뿐이며, 이는 $A$의 열들이 일차독립임을 의미한다. $\text{rank} + \text{nullity} = 3 = n$이 성립한다.

---
## 연결

- **[선형결합·span·일차독립](span-independence.html)** : rank는 일차독립인 열(또는 행)의 개수이며, span의 차원 개념을 구체화한다.
- **[행렬곱과 선형변환](matrix-multiplication.html)** : 행렬을 선형변환으로 해석할 때, rank는 상(image)의 차원이고 nullity는 핵(kernel)의 차원이다.
- **[가우스 소거와 RREF](gaussian-elimination.html)** : RREF는 rank와 널공간의 기저를 계산하는 실질적인 알고리즘이다.
- **[행렬식의 기하학](determinant.html)** : 정사각행렬이 최대 rank($=n$)를 가질 필요충분조건은 $\det A \neq 0$이다.
- **[역행렬과 기저 변환](inverse-change-of-basis.html)** : $A$가 가역일 필요충분조건은 $\text{rank}(A) = n$ (full rank)이다.
- **[최소제곱법](least-squares.html)** : $Ax = b$의 해가 존재하지 않을 때, 열공간으로의 직교투영을 통해 최적해를 구한다.

---

[← 이전: Ax = b·가우스 소거·RREF](gaussian-elimination.html) · [다음: 행렬식의 기하학 →](determinant.html)
