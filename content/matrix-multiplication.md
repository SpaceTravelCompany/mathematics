---
title: 행렬곱과 선형변환
slug: matrix-multiplication
---

## 직관적 설명

행렬(matrix)은 단순한 숫자의 직사각형 배열이 아니다. 행렬은 **공간을 변환(transform)하는 함수**다. $2 \times 2$ 행렬은 2차원 평면 위의 모든 점을 다른 점으로 보내며, $3 \times 3$ 행렬은 3차원 공간을 변환한다. 이 관점에서 행렬곱(matrix multiplication)은 두 변환의 **합성(composition)** 에 해당한다. 즉, "회전 행렬"과 "확대 행렬"을 곱하는 것은 "회전한 다음 확대하는 함수"를 만드는 것이다.

행렬곱이 교환 법칙(commutative law)을 따르지 않는다는 사실, 즉 $AB \neq BA$라는 사실은 이 해석에서 자연스럽게 이해된다. "회전 후 확대"와 "확대 후 회전"은 일반적으로 같은 결과를 주지 않기 때문이다. 이 비가환성(non-commutativity)이 선형대수학의 많은 흥미로운 현상의 근원이다.

행렬은 3D 그래픽스(회전·이동·확대 변환), 로봇 팔 제어(관절 변환의 합성), 양자역학(상태의 유니터리 변환), 경제학의 산업연관분석(레온티에프 투입-산출 모형), 구글의 페이지랭크(확률 행렬의 곱) 등 광범위한 분야에서 사용된다.

## 정의

**행렬(matrix):** $m \times n$ 행렬 $A$는 $m$개의 행(row)과 $n$개의 열(column)으로 배열된 수의 집합이다.

$$A = \begin{pmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \cdots & a_{mn} \end{pmatrix}$$

$a_{ij}$는 $i$번째 행, $j$번째 열의 원소(entry)이다.

**행렬곱(matrix multiplication):** $m \times n$ 행렬 $A$와 $n \times p$ 행렬 $B$의 곱 $C = AB$는 $m \times p$ 행렬이며, 그 $(i,j)$ 원소는

$$(AB)_{ij} = \sum_{k=1}^{n} a_{ik} b_{kj}$$

로 정의된다. 즉, $A$의 $i$번째 행과 $B$의 $j$번째 열의 **내적(dot product)** 이다.

**중요:** $AB$가 정의되려면 $A$의 열 수와 $B$의 행 수가 같아야 한다. 일반적으로 $AB \neq BA$이며, 한쪽이 정의되어도 다른 쪽이 정의되지 않을 수 있다.

**선형변환(linear transformation):** 함수 $T: \mathbb{R}^n \to \mathbb{R}^m$이 다음 두 조건을 만족하면 **선형변환**이라 한다.

1. **가산성(additivity):** $T(u + v) = T(u) + T(v)$ for all $u, v \in \mathbb{R}^n$
2. **동차성(homogeneity):** $T(\alpha u) = \alpha T(u)$ for all $\alpha \in \mathbb{R}, u \in \mathbb{R}^n$

이 두 조건을 합쳐 $T(\alpha u + \beta v) = \alpha T(u) + \beta T(v)$로 쓸 수 있다.

**행렬의 선형변환:** $m \times n$ 행렬 $A$는 자연스럽게 선형변환 $T_A: \mathbb{R}^n \to \mathbb{R}^m$을 정의한다:

$$T_A(x) = A x$$

여기서 $x \in \mathbb{R}^n$은 열벡터(column vector)이고, $Ax$는 행렬-벡터 곱이다.

**행렬-벡터 곱:** $A$를 $m \times n$ 행렬, $x \in \mathbb{R}^n$이라 할 때,

$$Ax = \begin{pmatrix} a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n \\ a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n \\ \vdots \\ a_{m1}x_1 + a_{m2}x_2 + \cdots + a_{mn}x_n \end{pmatrix}$$

이는 $A$의 열벡터들의 선형결합으로도 해석할 수 있다:

$$Ax = x_1 \begin{pmatrix} a_{11} \\ a_{21} \\ \vdots \\ a_{m1} \end{pmatrix} + x_2 \begin{pmatrix} a_{12} \\ a_{22} \\ \vdots \\ a_{m2} \end{pmatrix} + \cdots + x_n \begin{pmatrix} a_{1n} \\ a_{2n} \\ \vdots \\ a_{mn} \end{pmatrix}$$

## 주요 정리와 증명

### 정리 1: 행렬 ↔ 선형변환의 일대일대응

모든 $m \times n$ 행렬 $A$는 선형변환 $T_A: \mathbb{R}^n \to \mathbb{R}^m$을 결정하고, 역으로 모든 선형변환 $T: \mathbb{R}^n \to \mathbb{R}^m$은 유일한 $m \times n$ 행렬 $A$에 의해 $T = T_A$로 표현된다. 즉, 행렬과 선형변환 사이에는 **일대일대응(bijection)** 이 존재한다.

**증명:** ($\Rightarrow$) $A$가 주어졌을 때 $T_A(x) = Ax$를 정의하자. 행렬-벡터 곱의 성질에 의해

$$T_A(\alpha u + \beta v) = A(\alpha u + \beta v) = \alpha Au + \beta Av = \alpha T_A(u) + \beta T_A(v)$$

이므로 $T_A$는 선형변환이다.

($\Leftarrow$) 선형변환 $T: \mathbb{R}^n \to \mathbb{R}^m$이 주어졌다고 하자. $\mathbb{R}^n$의 표준기저(standard basis) $e_1, \dots, e_n$을 고려하자. 여기서 $e_j$는 $j$번째 성분만 1이고 나머지는 0인 벡터이다. 각 $T(e_j) \in \mathbb{R}^m$을 열벡터로 하는 $m \times n$ 행렬 $A$를 구성하자:

$$A = \begin{pmatrix} T(e_1) & T(e_2) & \cdots & T(e_n) \end{pmatrix}$$

이제 임의의 $x = \sum_{j=1}^{n} x_j e_j \in \mathbb{R}^n$에 대해,

$$T(x) = T\!\left(\sum_{j=1}^{n} x_j e_j\right) = \sum_{j=1}^{n} x_j T(e_j) = A x = T_A(x)$$

첫 번째 등호는 기저 표현, 두 번째 등호는 선형성, 세 번째 등호는 행렬-벡터 곱의 정의에 의한다. 따라서 $T = T_A$이다.

유일성(unicity)은 표준기저의 상(image)이 $A$의 열벡터를 결정하므로 자명하다.

### 정리 2: 행렬곱의 결합법칙

$(AB)C = A(BC)$ (단, 곱이 정의되는 크기일 때).

**증명:** $(AB)C$의 $(i,j)$ 원소를 계산하자.

$$((AB)C)_{ij} = \sum_{k} (AB)_{ik} c_{kj} = \sum_{k} \left( \sum_{l} a_{il} b_{lk} \right) c_{kj} = \sum_{k} \sum_{l} a_{il} b_{lk} c_{kj}$$

한편 $A(BC)$의 $(i,j)$ 원소는

$$(A(BC))_{ij} = \sum_{l} a_{il} (BC)_{lj} = \sum_{l} a_{il} \left( \sum_{k} b_{lk} c_{kj} \right) = \sum_{l} \sum_{k} a_{il} b_{lk} c_{kj}$$

두 이중합은 같으므로 결합법칙이 성립한다.

### 정리 3: 행렬곱의 비가환성 — 반례

$AB = BA$가 일반적으로 성립하지 않음을 보이는 반례:

$$A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}, \quad B = \begin{pmatrix} 1 & 0 \\ 1 & 1 \end{pmatrix}$$

$$AB = \begin{pmatrix} 1\cdot1+1\cdot1 & 1\cdot0+1\cdot1 \\ 0\cdot1+1\cdot1 & 0\cdot0+1\cdot1 \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix}$$

$$BA = \begin{pmatrix} 1\cdot1+0\cdot0 & 1\cdot1+0\cdot1 \\ 1\cdot1+1\cdot0 & 1\cdot1+1\cdot1 \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 2 \end{pmatrix}$$

$AB \neq BA$이다.

### 정리 4: 행렬곱의 전치

$(AB)^T = B^T A^T$

**증명:** $(AB)^T$의 $(i,j)$ 원소는 $(AB)_{ji} = \sum_k a_{jk} b_{ki}$이다. 한편 $(B^T A^T)_{ij} = \sum_k (B^T)_{ik} (A^T)_{kj} = \sum_k b_{ki} a_{jk}$로 같다.

## 예제

**예제 1:** $A = \begin{pmatrix} 2 & -1 \\ 0 & 3 \end{pmatrix}$, $B = \begin{pmatrix} 1 & 4 \\ -2 & 1 \end{pmatrix}$에 대해 $AB$와 $BA$를 각각 계산하라.

**풀이:**

$$AB = \begin{pmatrix} 2\cdot1 + (-1)\cdot(-2) & 2\cdot4 + (-1)\cdot1 \\ 0\cdot1 + 3\cdot(-2) & 0\cdot4 + 3\cdot1 \end{pmatrix} = \begin{pmatrix} 2+2 & 8-1 \\ 0-6 & 0+3 \end{pmatrix} = \begin{pmatrix} 4 & 7 \\ -6 & 3 \end{pmatrix}$$

$$BA = \begin{pmatrix} 1\cdot2 + 4\cdot0 & 1\cdot(-1) + 4\cdot3 \\ (-2)\cdot2 + 1\cdot0 & (-2)\cdot(-1) + 1\cdot3 \end{pmatrix} = \begin{pmatrix} 2 & -1+12 \\ -4 & 2+3 \end{pmatrix} = \begin{pmatrix} 2 & 11 \\ -4 & 5 \end{pmatrix}$$

$AB \neq BA$임을 확인할 수 있다.

**예제 2:** 선형변환 $T: \mathbb{R}^2 \to \mathbb{R}^2$가 $T(e_1) = (2, 1)$, $T(e_2) = (-1, 3)$일 때 $T$의 행렬을 구하고, $T(4, -2)$를 계산하라.

**풀이:** $T(e_1), T(e_2)$를 열로 하는 행렬은

$$A = \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix}$$

$$T(4, -2) = A \begin{pmatrix} 4 \\ -2 \end{pmatrix} = \begin{pmatrix} 2\cdot4 + (-1)\cdot(-2) \\ 1\cdot4 + 3\cdot(-2) \end{pmatrix} = \begin{pmatrix} 8+2 \\ 4-6 \end{pmatrix} = \begin{pmatrix} 10 \\ -2 \end{pmatrix}$$

**예제 3:** 반시계 방향 $90^\circ$ 회전 행렬 $R = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$과 $x$축 방향 2배 확대 행렬 $S = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix}$에 대해 $RS$와 $SR$을 구하고, 결과를 기하학적으로 해석하라.

**풀이:**

$$RS = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 0\cdot2 + (-1)\cdot0 & 0\cdot0 + (-1)\cdot1 \\ 1\cdot2 + 0\cdot0 & 1\cdot0 + 0\cdot1 \end{pmatrix} = \begin{pmatrix} 0 & -1 \\ 2 & 0 \end{pmatrix}$$

$$SR = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 2\cdot0 + 0\cdot1 & 2\cdot(-1) + 0\cdot0 \\ 0\cdot0 + 1\cdot1 & 0\cdot(-1) + 1\cdot0 \end{pmatrix} = \begin{pmatrix} 0 & -2 \\ 1 & 0 \end{pmatrix}$$

$RS$는 "먼저 $x$축으로 2배 확대한 후 회전"이고, $SR$은 "먼저 회전한 후 $x$축으로 2배 확대"이다. 이 둘은 결과가 다르다. $RS$는 $y$축 방향으로만 2배 확대한 후 회전한 효과가 나타난다.

## 연결

- **[선형결합·span·일차독립](topics/span-independence.html)** : 행렬의 열공간은 열벡터들의 span이며, 행렬의 rank는 일차독립인 열의 개수와 같다.
- **[rank·열공간·널공간](topics/rank-nullspace.html)** : 행렬이 정의하는 선형변환의 핵(kernel)과 상(image)의 차원 관계를 다룬다.
- **[행렬식의 기하학](topics/determinant.html)** : 정사각행렬이 공간의 부피를 얼마나 늘리는지 측정하며, $\det A = 0$은 변환이 공간을 납작하게 만듦을 의미한다.
- **[역행렬과 기저 변환](topics/inverse-change-of-basis.html)** : 행렬의 역행렬은 변환을 되돌리는 선형변환에 해당한다.
- **[평면벡터 기초](topics/plane-vectors.html)** : 벡터의 연산과 기하학적 해석은 행렬 이론의 기초가 된다.
