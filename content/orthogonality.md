---
title: 직교성·직교투영·그람-슈미트
slug: orthogonality
---

## 직관적 설명

두 벡터가 **직교(orthogonal)**한다는 것은 "서로 수직"이라는 뜻이다. $\mathbb{R}^2$에서 두 벡터가 직교하면 내적이 0이다. 이 성질을 추상적 내적공간으로 확장하면, 벡터들을 서로 간섭하지 않는 성분들로 분해할 수 있다.

**직교투영(orthogonal projection)**은 한 벡터를 주어진 부분공간에 "수직으로 비추는" 연산이다. 벡터 $v$를 부분공간 $W$ 위로 투영하면, $v$는 $W$ 안에 있는 성분 $\text{proj}_W(v)$와 $W$에 수직인 성분 $v - \text{proj}_W(v)$으로 분해된다. 이 분해는 유일하며, 두 성분은 서로 직교한다.

**그람-슈미트 과정(Gram-Schmidt process)**은 임의의 일차독립 집합이 주어졌을 때, 같은 공간을 생성하는 정규직교기저(orthonormal basis)를 구성하는 알고리즘이다. 각 벡터를 이전 벡터들로 이루어진 부분공간에 투영한 뒤, 그 수직 성분만을 취하는 과정을 반복한다.

이 개념들의 응용 범위는 넓다. 직교분해는 푸리에 급수에서 신호를 정현파 성분들로 분해하는 기초이며, 최소제곱법은 직교투영의 형태로 이해할 수 있다. QR 분해는 그람-슈미트 과정의 행렬 형태다.

## 정의

**직교 (orthogonality):** 내적공간 $V$의 두 벡터 $u, v$가
$$\langle u, v \rangle = 0$$
일 때 $u \perp v$라 쓰고 직교한다고 말한다. 영벡터는 모든 벡터와 직교한다.

**직교집합 (orthogonal set):** 집합 $\{v_1, \ldots, v_k\}$의 모든 벡터가 쌍으로 직교할 때, 즉 $i \neq j$이면 $\langle v_i, v_j \rangle = 0$일 때 직교집합이라 한다.

**정규직교집합 (orthonormal set):** 직교집합이면서 각 벡터의 노름이 1인 집합. 즉,
$$\langle v_i, v_j \rangle = \delta_{ij} = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases}$$

**직교보완 (orthogonal complement):** 부분공간 $W \subseteq V$에 대해
$$W^\perp = \{ v \in V \mid \forall w \in W, \langle v, w \rangle = 0 \}$$
$W^\perp$는 $V$의 부분공간이며, $W \cap W^\perp = \{0\}$이다.

**직교투영 (orthogonal projection):** $V$의 부분공간 $W$와 정규직교기저 $\{e_1, \ldots, e_k\}$에 대해
$$\text{proj}_W(v) = \sum_{i=1}^k \langle v, e_i \rangle e_i$$

일반적인(정규직교가 아닌) 직교기저 $\{u_1, \ldots, u_k\}$에 대해서는
$$\text{proj}_W(v) = \sum_{i=1}^k \frac{\langle v, u_i \rangle}{\langle u_i, u_i \rangle} u_i$$

**직교행렬 (orthogonal matrix):** $Q^T Q = Q Q^T = I$를 만족하는 정사각행렬 $Q$. 직교행렬의 열(또는 행)들은 정규직교집합을 이룬다. 직교행렬은 내적을 보존한다: $\langle Qx, Qy \rangle = \langle x, y \rangle$.

## 주요 정리와 증명

### 정리 1: 피타고라스 정리 (Pythagorean Theorem)

내적공간에서 $u \perp v$이면
$$\|u + v\|^2 = \|u\|^2 + \|v\|^2$$

**증명:**
$$\|u + v\|^2 = \langle u+v, u+v \rangle = \|u\|^2 + \|v\|^2 + 2\langle u, v \rangle$$
$\langle u, v \rangle = 0$이므로 교차항이 사라진다.

**일반화:** $\{v_1, \ldots, v_k\}$가 직교집합이면
$$\|v_1 + \cdots + v_k\|^2 = \|v_1\|^2 + \cdots + \|v_k\|^2$$

### 정리 2: 정규직교집합은 일차독립

영벡터를 포함하지 않는 정규직교집합 $\{e_1, \ldots, e_k\}$은 일차독립이다.

**증명:** 일차결합 $\sum_{i=1}^k \alpha_i e_i = 0$이라 가정하자. $e_j$와의 내적을 취하면
$$\left\langle \sum_{i=1}^k \alpha_i e_i, e_j \right\rangle = \sum_{i=1}^k \alpha_i \langle e_i, e_j \rangle = \alpha_j \|e_j\|^2 = \alpha_j = 0$$
$\|e_j\| = 1$이므로 $\alpha_j = 0$이다. 따라서 모든 계수가 0이므로 일차독립이다.

### 정리 3: 그람-슈미트 과정 (Gram-Schmidt Process)

$V$의 일차독립 집합 $\{v_1, \ldots, v_n\}$이 주어졌을 때, 다음 알고리즘으로 정규직교기저 $\{e_1, \ldots, e_n\}$를 구성할 수 있다.

**알고리즘:**

1. $u_1 = v_1$, $e_1 = \frac{u_1}{\|u_1\|}$
2. $k = 2, \ldots, n$에 대해:
   $$u_k = v_k - \sum_{i=1}^{k-1} \frac{\langle v_k, u_i \rangle}{\langle u_i, u_i \rangle} u_i, \quad e_k = \frac{u_k}{\|u_k\|}$$

**증명 (귀납법):** $k$번째 단계에서 $\{u_1, \ldots, u_k\}$가 직교집합임을 보인다.

$k = 1$: $\{u_1\}$은 자명하게 직교집합이다.

$k - 1$까지 $\{u_1, \ldots, u_{k-1}\}$이 직교집합이라 가정하자. $u_k$와 $u_j$ ($j < k$)의 내적을 계산하면
$$\langle u_k, u_j \rangle = \left\langle v_k - \sum_{i=1}^{k-1} \frac{\langle v_k, u_i \rangle}{\|u_i\|^2} u_i, \; u_j \right\rangle$$
$$= \langle v_k, u_j \rangle - \sum_{i=1}^{k-1} \frac{\langle v_k, u_i \rangle}{\|u_i\|^2} \langle u_i, u_j \rangle$$

귀납가설에 의해 $i \neq j$일 때 $\langle u_i, u_j \rangle = 0$이므로 합에서 $i = j$ 항만 남는다:
$$\langle u_k, u_j \rangle = \langle v_k, u_j \rangle - \frac{\langle v_k, u_j \rangle}{\|u_j\|^2} \|u_j\|^2 = \langle v_k, u_j \rangle - \langle v_k, u_j \rangle = 0$$

따라서 $u_k \perp u_j$가 성립하고, $\{u_1, \ldots, u_k\}$는 직교집합이다.

$v_k$는 $\{v_1, \ldots, v_{k-1}\}$과 일차독립이므로 $u_k \neq 0$이다(그렇지 않다면 $v_k$가 선행 벡터들의 선형결합이 되어 일차독립에 위배). 따라서 정규화하여 $e_k$를 얻을 수 있다.

### 정리 4: 직교분해 (Orthogonal Decomposition)

$V$가 유한차원 내적공간이고 $W$가 $V$의 부분공간이면
$$V = W \oplus W^\perp$$
즉, 모든 $v \in V$는 유일하게 $v = w + w^\perp$ ($w \in W$, $w^\perp \in W^\perp$)로 분해된다.

**증명:** $W$의 정규직교기저 $\{e_1, \ldots, e_k\}$를 잡자. $w = \text{proj}_W(v) = \sum \langle v, e_i \rangle e_i$라 하면 $w \in W$이다. $w^\perp = v - w$가 $W^\perp$에 속함을 보인다. 모든 $e_j$에 대해
$$\langle w^\perp, e_j \rangle = \langle v - \sum \langle v, e_i \rangle e_i, e_j \rangle = \langle v, e_j \rangle - \langle v, e_j \rangle = 0$$

$W$의 임의의 원소는 $\{e_i\}$의 선형결합이므로 $w^\perp$는 $W$의 모든 원소와 직교한다. 따라서 $w^\perp \in W^\perp$. 분해의 유일성은 $W \cap W^\perp = \{0\}$에서 따라온다.

### 정리 5: 최적 근사 정리 (Best Approximation Theorem)

$W$가 내적공간 $V$의 부분공간이고 $v \in V$라 하자. $w \in W$ 중에서 $v$에 가장 가까운(즉 $\|v - w\|$를 최소화하는) 유일한 벡터는 $\text{proj}_W(v)$이다.

**증명:** 임의의 $w \in W$에 대해
$$\|v - w\|^2 = \|(v - \text{proj}_W(v)) + (\text{proj}_W(v) - w)\|^2$$

$v - \text{proj}_W(v) \in W^\perp$이고 $\text{proj}_W(v) - w \in W$이므로 두 벡터는 직교한다. 피타고라스 정리에 의해
$$\|v - w\|^2 = \|v - \text{proj}_W(v)\|^2 + \|\text{proj}_W(v) - w\|^2$$

우변의 둘째 항은 $w = \text{proj}_W(v)$일 때만 0이 되고 그 외에는 양수다. 따라서 $\|v - w\|$는 $w = \text{proj}_W(v)$일 때 최소가 된다. 유일성: $\|v - w_1\| = \|v - w_2\|$가 최소이면 $w_1 = w_2$임을 위 분해로 보일 수 있다.

### 정리 6: 직교투영의 선형성과 멱등성

$\text{proj}_W: V \to W$는 선형변환이며 $\text{proj}_W \circ \text{proj}_W = \text{proj}_W$ (멱등성, idempotence)를 만족한다.

**증명:** 정규직교기저 표현 $\text{proj}_W(v) = \sum \langle v, e_i \rangle e_i$에서, 각 항은 $v$에 대해 선형이므로 합도 선형이다. $w \in W$에 대해 $\text{proj}_W(w) = w$이므로 $\text{proj}_W(\text{proj}_W(v)) = \text{proj}_W(v)$가 성립한다.

### 정리 7: 베셀 부등식 (Bessel's Inequality)

$\{e_1, \ldots, e_k\}$가 내적공간 $V$의 정규직교집합이면 모든 $v \in V$에 대해
$$\sum_{i=1}^k |\langle v, e_i \rangle|^2 \leq \|v\|^2$$

**증명:** $w = \sum_{i=1}^k \langle v, e_i \rangle e_i$라 하자. $w$는 $\{e_i\}$의 span 위로의 $v$의 직교투영이다. $v = w + (v - w)$에서 $w \perp (v - w)$이므로
$$\|v\|^2 = \|w\|^2 + \|v - w\|^2 \geq \|w\|^2 = \sum_{i=1}^k |\langle v, e_i \rangle|^2$$

**의미:** 베셀 부등식은 부분적인 정규직교집합으로 $v$의 "에너지"($\|v\|^2$)의 일부만 포착할 수 있음을 나타낸다. 완전한 정규직교기저(complete orthonormal basis)에서는 등호가 성립하며, 이는 파르세발 항등식(Parseval's identity)으로 알려져 있다.

### 정리 8: QR 분해

$m \times n$ 행렬 $A$ ($m \geq n$)의 열들이 일차독립이면 $A = QR$로 분해된다. 여기서 $Q$는 $m \times n$ 직교열 행렬(orthonormal columns)이고 $R$은 $n \times n$ 상삼각행렬(upper triangular)이며 $R$의 대각 성분은 양수다.

**증명 (그람-슈미트 과정의 행렬 형태):** $A$의 열을 $\{a_1, \ldots, a_n\}$이라 하자. 그람-슈미트 과정으로 정규직교벡터 $\{q_1, \ldots, q_n\}$을 얻는다. 각 $a_k$는
$$a_k = \sum_{i=1}^k \langle a_k, q_i \rangle q_i$$

로 표현된다. $r_{ik} = \langle a_k, q_i \rangle$ ($i \leq k$)라 정의하면 $A = QR$이 성립한다. $R$은 $i > k$일 때 $r_{ik} = 0$이므로 상삼각행렬이다. $r_{kk} = \|u_k\| > 0$이므로 대각 성분은 양수다.

## 예제

**예제 1:** $\{(1, 1, 0), (1, 0, 1), (0, 1, 1)\}$을 그람-슈미트 과정으로 정규직교기저로 변환하라.

**풀이:** $v_1 = (1, 1, 0)$, $v_2 = (1, 0, 1)$, $v_3 = (0, 1, 1)$.

1단계: $u_1 = v_1 = (1, 1, 0)$, $\|u_1\| = \sqrt{2}$, $e_1 = \frac{1}{\sqrt{2}}(1, 1, 0)$.

2단계: $\langle v_2, u_1 \rangle = 1\cdot1 + 0\cdot1 + 1\cdot0 = 1$, $\|u_1\|^2 = 2$.
$$u_2 = v_2 - \frac{1}{2} u_1 = (1, 0, 1) - \frac{1}{2}(1, 1, 0) = \left(\frac12, -\frac12, 1\right)$$
$$\|u_2\| = \sqrt{\frac14 + \frac14 + 1} = \sqrt{\frac32} = \frac{\sqrt{6}}{2}$$
$$e_2 = \frac{1}{\sqrt{6}}(1, -1, 2)$$

3단계: $\langle v_3, u_1 \rangle = 0\cdot1 + 1\cdot1 + 1\cdot0 = 1$, $\langle v_3, u_2 \rangle = 0\cdot\frac12 + 1\cdot(-\frac12) + 1\cdot1 = \frac12$.
$$u_3 = v_3 - \frac{1}{2} u_1 - \frac{1/2}{3/2} u_2 = (0, 1, 1) - \frac12(1, 1, 0) - \frac13\left(\frac12, -\frac12, 1\right)$$
$$= (0, 1, 1) - \left(\frac12, \frac12, 0\right) - \left(\frac16, -\frac16, \frac13\right) = \left(-\frac23, \frac23, \frac23\right)$$
$$\|u_3\| = \sqrt{\frac{4}{9} + \frac{4}{9} + \frac{4}{9}} = \frac{2}{\sqrt{3}}$$
$$e_3 = \frac{1}{\sqrt{3}}(-1, 1, 1)$$

정규직교기저: $\left\{ \frac{1}{\sqrt{2}}(1, 1, 0), \frac{1}{\sqrt{6}}(1, -1, 2), \frac{1}{\sqrt{3}}(-1, 1, 1) \right\}$.

**예제 2:** $\mathbb{R}^3$에서 $v = (2, 3, 1)$을 부분공간 $W = \text{span}\{(1, 0, 1), (0, 1, 0)\}$ 위로 투영하라.

**풀이:** 두 기저벡터가 이미 직교하므로($\langle (1, 0, 1), (0, 1, 0) \rangle = 0$), 정규화만 하면 된다.
$e_1 = \frac{1}{\sqrt{2}}(1, 0, 1)$, $e_2 = (0, 1, 0)$.
$$\text{proj}_W(v) = \langle v, e_1 \rangle e_1 + \langle v, e_2 \rangle e_2$$
$$\langle v, e_1 \rangle = \frac{2+1}{\sqrt{2}} = \frac{3}{\sqrt{2}}, \quad \langle v, e_2 \rangle = 3$$
$$\text{proj}_W(v) = \frac{3}{\sqrt{2}} \cdot \frac{1}{\sqrt{2}}(1, 0, 1) + 3(0, 1, 0) = \frac32(1, 0, 1) + (0, 3, 0) = \left(\frac32, 3, \frac32\right)$$

수직 성분: $v - \text{proj}_W(v) = (2, 3, 1) - (1.5, 3, 1.5) = (0.5, 0, -0.5)$.
확인: $\langle (0.5, 0, -0.5), (1, 0, 1) \rangle = 0.5 - 0.5 = 0$, $\langle (0.5, 0, -0.5), (0, 1, 0) \rangle = 0$.

**예제 3:** $f(x) = x(1-x)$를 구간 $[0, 1]$에서 $\{1, x\}$로 생성되는 부분공간 위로 $L^2$ 투영하라.

**풀이:** $\{1, x\}$에 그람-슈미트를 적용하자.
$u_1 = 1$, $\|u_1\|^2 = \int_0^1 1^2 dx = 1$, $e_1 = 1$.
$\langle x, 1 \rangle = \int_0^1 x dx = \frac12$.
$$u_2 = x - \frac12 \cdot 1 = x - \frac12$$
$\|u_2\|^2 = \int_0^1 (x - \frac12)^2 dx = \int_0^1 (x^2 - x + \frac14) dx = \frac13 - \frac12 + \frac14 = \frac{1}{12}$.
$e_2 = \sqrt{12}(x - \frac12) = 2\sqrt{3}(x - \frac12)$.

이제 $f$를 투영:
$$\langle f, e_1 \rangle = \int_0^1 x(1-x) dx = \int_0^1 (x - x^2) dx = \frac12 - \frac13 = \frac16$$
$$\langle f, e_2 \rangle = 2\sqrt{3} \int_0^1 x(1-x)(x - \tfrac12) dx = 2\sqrt{3} \int_0^1 (-x^3 + \tfrac32 x^2 - \tfrac12 x) dx$$
$$= 2\sqrt{3} \left[ -\frac14 + \frac12 - \frac14 \right] = 2\sqrt{3} \cdot 0 = 0$$

따라서 $\text{proj}_W(f) = \frac16 \cdot 1 = \frac16$, 즉 $f$의 최적 근사는 상수함수 $\frac16$이다.

**예제 4 (투영 행렬의 성질):** $W = \text{span}\{(1, 0, 1), (0, 1, 0)\}$ 위로의 투영 행렬을 구하고 멱등성을 확인하라.

**풀이:** 정규직교기저: $e_1 = \frac{1}{\sqrt{2}}(1, 0, 1)$, $e_2 = (0, 1, 0)$.
투영 행렬 $P = e_1 e_1^T + e_2 e_2^T$:
$$P = \frac12\begin{pmatrix} 1 \\ 0 \\ 1 \end{pmatrix}\begin{pmatrix} 1 & 0 & 1 \end{pmatrix} + \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}\begin{pmatrix} 0 & 1 & 0 \end{pmatrix}$$
$$= \frac12\begin{pmatrix} 1 & 0 & 1 \\ 0 & 0 & 0 \\ 1 & 0 & 1 \end{pmatrix} + \begin{pmatrix} 0 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 0 \end{pmatrix} = \begin{pmatrix} 1/2 & 0 & 1/2 \\ 0 & 1 & 0 \\ 1/2 & 0 & 1/2 \end{pmatrix}$$

멱등성 확인: $P^2 = P$를 계산하면
$$P^2 = \begin{pmatrix} 1/2 & 0 & 1/2 \\ 0 & 1 & 0 \\ 1/2 & 0 & 1/2 \end{pmatrix} \begin{pmatrix} 1/2 & 0 & 1/2 \\ 0 & 1 & 0 \\ 1/2 & 0 & 1/2 \end{pmatrix} = \begin{pmatrix} 1/4+1/4 & 0 & 1/4+1/4 \\ 0 & 1 & 0 \\ 1/4+1/4 & 0 & 1/4+1/4 \end{pmatrix} = \begin{pmatrix} 1/2 & 0 & 1/2 \\ 0 & 1 & 0 \\ 1/2 & 0 & 1/2 \end{pmatrix} = P$$

$v = (2, 3, 1)$에 적용: $Pv = (1.5, 3, 1.5)$로 앞서 구한 $\text{proj}_W(v)$와 일치.

**예제 5 (최적 근사):** $v = (1, 2, 3)$을 $W = \text{span}\{(1, 1, 0), (0, 1, 1)\}$에서 가장 가까운 벡터로 근사하라.

**풀이:** 먼저 그람-슈미트로 $W$의 정규직교기저를 구한다.
$u_1 = (1, 1, 0)$, $e_1 = \frac{1}{\sqrt{2}}(1, 1, 0)$.
$\langle u_2, u_1 \rangle = 0\cdot1 + 1\cdot1 + 1\cdot0 = 1$, $\|u_1\|^2 = 2$.
$u_2' = (0, 1, 1) - \frac12(1, 1, 0) = (-\frac12, \frac12, 1)$.
$\|u_2'\| = \sqrt{1/4 + 1/4 + 1} = \sqrt{3/2} = \sqrt{6}/2$.
$e_2 = \frac{1}{\sqrt{6}}(-1, 1, 2)$.

투영: $\langle v, e_1 \rangle = \frac{1+2}{\sqrt{2}} = \frac{3}{\sqrt{2}}$, $\langle v, e_2 \rangle = \frac{-1+2+6}{\sqrt{6}} = \frac{7}{\sqrt{6}}$.
$$\text{proj}_W(v) = \frac{3}{\sqrt{2}}e_1 + \frac{7}{\sqrt{6}}e_2 = \frac32(1, 1, 0) + \frac76(-1, 1, 2)$$
$$= \left(\frac32 - \frac76,\; \frac32 + \frac76,\; \frac{14}{6}\right) = \left(\frac{1}{3},\; \frac{8}{3},\; \frac{7}{3}\right)$$

거리: $\|v - \text{proj}_W(v)\| = \left\| \left(\frac23, -\frac23, \frac23\right) \right\| = \frac{2}{\sqrt{3}}$.

**예제 6:** $A = \begin{pmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{pmatrix}$의 QR 분해를 구하라.

**풀이:** $a_1 = (1, 1, 1)$, $a_2 = (0, 1, 2)$.
$u_1 = (1, 1, 1)$, $\|u_1\| = \sqrt{3}$, $q_1 = \frac{1}{\sqrt{3}}(1, 1, 1)$.
$\langle a_2, q_1 \rangle = \frac{1}{\sqrt{3}}(0+1+2) = \sqrt{3}$.
$u_2 = a_2 - \sqrt{3} q_1 = (0, 1, 2) - (1, 1, 1) = (-1, 0, 1)$.
$\|u_2\| = \sqrt{2}$, $q_2 = \frac{1}{\sqrt{2}}(-1, 0, 1)$.
$r_{11} = \sqrt{3}$, $r_{12} = \sqrt{3}$, $r_{22} = \sqrt{2}$.

$$Q = \begin{pmatrix} 1/\sqrt{3} & -1/\sqrt{2} \\ 1/\sqrt{3} & 0 \\ 1/\sqrt{3} & 1/\sqrt{2} \end{pmatrix}, \quad R = \begin{pmatrix} \sqrt{3} & \sqrt{3} \\ 0 & \sqrt{2} \end{pmatrix}$$

## 연결

- **[내적·노름·코사인 유사도](topics/inner-product-norm.html)** : 내적공간의 정의와 기본 성질을 학습한다.
- **[최소제곱법](topics/least-squares.html)** : 직교투영이 최소제곱 문제의 기하학적 해석을 제공한다.
- **[가우스 소거와 RREF](topics/gaussian-elimination.html)** : QR 분해는 가우스 소거를 직교 변환으로 대체하는 수치적으로 안정적인 방법이다.
