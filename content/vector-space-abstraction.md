---
title: 벡터공간 추상화
slug: vector-space-abstraction
---

## 직관적 설명

지금까지 우리가 다룬 벡터는 $\mathbb{R}^n$의 원소, 즉 숫자 $n$개의 순서쌍이었다. 하지만 "더하고 스칼라배할 수 있는" 대상은 이것만이 아니다. **함수(function)**도 더할 수 있고 상수배할 수 있다. **다항식(polynomial)**도, **신호(signal)**도, **미분방정식의 해(solution)**도 마찬가지다. 이 모든 대상이 "벡터"라는 하나의 개념으로 포괄된다는 것이 벡터공간 추상화의 핵심이다.

벡터공간(vector space)은 "덧셈과 스칼라배라는 두 연산이 정의된 집합"으로, 단 여덟 개의 공리(axiom)를 만족해야 한다. 이 추상화의 힘은, $\mathbb{R}^n$에서 증명한 정리가 함수공간에서도 똑같이 성립한다는 데 있다. 예를 들어 $\mathbb{R}^n$에서의 기저와 차원 개념은 그대로 함수공간에 적용할 수 있다. 푸리에 해석은 바로 이 관점의 결정체다 — 함수 $\sin(nx)$와 $\cos(nx)$는 함수공간의 기저이며, 푸리에 급수는 함수를 이 기저들의 선형결합으로 표현하는 것이다.

양자역학에서 파동함수는 무한차원 벡터공간(힐베르트 공간)의 벡터이며, 신호 처리에서 신호는 함수공간의 원소다. 미분방정식의 해의 집합이 벡터공간을 이룬다는 사실(중첩 원리, superposition principle)은 선형 미분방정식 이론의 출발점이다.

## 정의

**벡터공간(vector space):** 집합 $V$와 체(field) $\mathbb{R}$ (실수)에 대해, 다음 두 연산이 정의되고 여덟 개의 공리를 만족하면 $V$를 $\mathbb{R}$-벡터공간(또는 실벡터공간)이라 한다.

- **덧셈(addition):** $V \times V \to V$, $(u, v) \mapsto u + v$
- **스칼라배(scalar multiplication):** $\mathbb{R} \times V \to V$, $(\alpha, v) \mapsto \alpha v$

**공리 (모든 $u, v, w \in V$, $\alpha, \beta \in \mathbb{R}$에 대해):**

1. **덧셈의 결합법칙:** $(u + v) + w = u + (v + w)$
2. **덧셈의 교환법칙:** $u + v = v + u$
3. **덧셈의 항등원:** $u + 0 = u$를 만족하는 $0 \in V$가 존재한다 (**영벡터**)
4. **덧셈의 역원:** 각 $u \in V$에 대해 $u + (-u) = 0$을 만족하는 $-u \in V$가 존재한다
5. **스칼라배의 결합법칙:** $\alpha(\beta u) = (\alpha\beta) u$
6. **스칼라배의 항등원:** $1 \cdot u = u$
7. **분배법칙 1:** $\alpha(u + v) = \alpha u + \alpha v$
8. **분배법칙 2:** $(\alpha + \beta) u = \alpha u + \beta u$

**부분공간(subspace):** $V$의 부분집합 $W \subseteq V$가 $V$의 연산에 대해 스스로 벡터공간을 이루면 $W$를 **부분공간**이라 한다. $W$가 부분공간일 필요충분조건은:

1. $0 \in W$
2. $u, v \in W \Rightarrow u + v \in W$ (덧셈에 닫힘)
3. $u \in W, \alpha \in \mathbb{R} \Rightarrow \alpha u \in W$ (스칼라배에 닫힘)

**선형변환(linear transformation):** 두 벡터공간 $V, W$ 사이의 함수 $T: V \to W$가 다음을 만족하면 선형변환이다:
$$T(\alpha u + \beta v) = \alpha T(u) + \beta T(v) \quad \forall u, v \in V,\; \forall \alpha, \beta \in \mathbb{R}$$

**선형범함수(linear functional):** $V$에서 $\mathbb{R}$로 가는 선형변환 $f: V \to \mathbb{R}$을 선형범함수라 한다.

### 중요한 예시

**$\mathbb{R}^n$:** $n$-튜플 $(x_1, \dots, x_n)$의 집합. 성분별 덧셈과 스칼라배. $\dim(\mathbb{R}^n) = n$.

**행렬공간 $\mathbb{R}^{m \times n}$:** $m \times n$ 행렬의 집합. 행렬 덧셈과 스칼라배. $\dim(\mathbb{R}^{m \times n}) = mn$.

**다항식공간 $\mathcal{P}_n$:** 차수가 $n$ 이하인 실계수 다항식의 집합. $\dim(\mathcal{P}_n) = n+1$이며, 기저로 $\{1, x, x^2, \dots, x^n\}$을 가진다.

**함수공간 $C[a,b]$:** 닫힌 구간 $[a,b]$에서 연속인 모든 실함수의 집합. $\dim(C[a,b]) = \infty$ (무한차원).

**수열공간 $\ell^2$:** 제곱합이 수렴하는 실수열 $(a_n)_{n=1}^{\infty}$의 집합. $\sum_{n=1}^{\infty} a_n^2 < \infty$. 무한차원이며, 내적이 정의되는 힐베르트 공간의 예시이다.

## 주요 정리와 증명

### 정리 1: 부분공간 판정 정리

$V$의 부분집합 $W$가 부분공간일 필요충분조건은 $W$가 덧셈과 스칼라배에 대해 닫혀 있고 $0 \in W$인 것이다.

**증명:** ($\Rightarrow$) $W$가 부분공간이면 정의에 의해 $0 \in W$이고 연산에 닫혀 있다.

($\Leftarrow$) $W$가 $0$을 포함하고 덧셈과 스칼라배에 닫혀 있다고 하자. $V$의 공리 1, 2, 5, 6, 7, 8은 $W$의 원소에 대해서도 $V$에서와 같이 성립하므로 $W$에서도 성립한다. 덧셈의 역원의 존재: $u \in W$에 대해 $(-1)u \in W$ (스칼라배에 닫힘)이고 $u + (-1)u = 1\cdot u + (-1)\cdot u = (1 + (-1))u = 0 \cdot u = 0$이므로 $(-1)u = -u \in W$이다. 따라서 $W$는 모든 공리를 만족하여 부분공간이다.

### 정리 2: 연속함수공간 $C[a,b]$는 벡터공간이다

구간 $[a,b]$에서 연속인 함수들의 집합 $C[a,b]$는 실벡터공간이다.

**증명:** 두 연속함수 $f, g \in C[a,b]$와 $\alpha \in \mathbb{R}$에 대해:

- $(f + g)(x) = f(x) + g(x)$로 정의하면, 연속함수의 합은 연속이므로 $f + g \in C[a,b]$.
- $(\alpha f)(x) = \alpha f(x)$로 정의하면, 연속함수의 상수배는 연속이므로 $\alpha f \in C[a,b]$.
- 영함수 $0(x) = 0$은 연속이고 $0 \in C[a,b]$.
- $(-f)(x) = -f(x)$는 연속이고 $f + (-f) = 0$.

여덟 개의 공리는 함수값의 실수 연산에서 유도되므로 $C[a,b]$는 벡터공간이다.

### 정리 3: $n$차 다항식공간 $\mathcal{P}_n$의 차원

$\mathcal{P}_n = \{a_0 + a_1 x + \cdots + a_n x^n \mid a_i \in \mathbb{R}\}$의 차원은 $n+1$이다.

**증명:** $\mathcal{B} = \{1, x, x^2, \dots, x^n\}$이 기저임을 보인다.

1. **생성:** 임의의 $p(x) = \sum_{i=0}^{n} a_i x^i \in \mathcal{P}_n$는 $\mathcal{B}$의 선형결합이다.
2. **일차독립:** $\sum_{i=0}^{n} c_i x^i = 0$ (영함수)라 하자. 대수학의 기본정리에 의해 차수가 $n$ 이하인 다항식이 모든 $x$에 대해 0이 되려면 모든 계수가 0이어야 한다. 따라서 $c_0 = c_1 = \cdots = c_n = 0$이다.

$\mathcal{B}$가 기저이므로 $\dim(\mathcal{P}_n) = n+1$이다.

### 정리 4: 선형 상미분방정식의 해공간

2계 선형 동차 상미분방정식 $y'' + p(x)y' + q(x)y = 0$ (여기서 $p, q$는 연속함수)의 모든 해의 집합은 2차원 벡터공간이다.

**증명:** $S = \{y \in C^2[a,b] \mid y'' + p(x)y' + q(x)y = 0\}$라 하자.

1. $S$가 부분공간임을 확인한다:
   - 영함수 $y = 0$은 해이므로 $0 \in S$.
   - $y_1, y_2 \in S$이고 $\alpha, \beta \in \mathbb{R}$일 때, $y = \alpha y_1 + \beta y_2$에 대해
     $$y'' + p y' + q y = (\alpha y_1'' + \beta y_2'') + p(\alpha y_1' + \beta y_2') + q(\alpha y_1 + \beta y_2)$$
     $$= \alpha(y_1'' + p y_1' + q y_1) + \beta(y_2'' + p y_2' + q y_2) = \alpha \cdot 0 + \beta \cdot 0 = 0$$
     따라서 $y \in S$. 즉, $S$는 선형성을 가진다 (중첩 원리, superposition principle).

2. 초기조건 $y(x_0) = a$, $y'(x_0) = b$에 대한 해의 존재성과 유일성 정리에 의해, $S$는 2차원이다. 구체적으로, 기저는 $\{y_1, y_2\}$로 잡을 수 있는데, 여기서 $y_1$은 $y_1(x_0)=1, y_1'(x_0)=0$의 해이고 $y_2$는 $y_2(x_0)=0, y_2'(x_0)=1$의 해이다. 임의의 해는 이 두 기저해의 선형결합으로 유일하게 표현된다.

### 정리 5: 유한차원 벡터공간의 분류

차원이 $n$인 모든 유한차원 실벡터공간은 $\mathbb{R}^n$과 동형(isomorphic)이다. 즉, 차원이 같은 두 유한차원 벡터공간 사이에는 항상 가역 선형변환(동형사상, isomorphism)이 존재한다.

**증명:** $V$를 $\dim V = n$인 벡터공간이라 하고 $\mathcal{B} = \{b_1, \dots, b_n\}$을 $V$의 기저라 하자. 함수 $\phi: V \to \mathbb{R}^n$을

$$\phi(v) = [v]_{\mathcal{B}} = (\alpha_1, \dots, \alpha_n)^T$$

로 정의한다 (여기서 $v = \sum \alpha_i b_i$). $\phi$는 선형이고($\phi(\alpha u + \beta v) = \alpha \phi(u) + \beta \phi(v)$), 전단사(bijective)이므로 동형사상이다. 따라서 $V \cong \mathbb{R}^n$이다.

## 예제

**예제 1:** 다음 집합이 $\mathbb{R}^3$의 부분공간인지 판정하라.

(a) $W_1 = \{(x, y, z) \mid x + y + z = 0\}$
(b) $W_2 = \{(x, y, z) \mid x + y + z = 1\}$
(c) $W_3 = \{(x, y, z) \mid x^2 + y^2 = 0\}$

**풀이:**

(a) $W_1$은 부분공간이다. $0 = (0,0,0)$은 $0+0+0=0$이므로 속한다. $(x_1,y_1,z_1), (x_2,y_2,z_2) \in W_1$이면 $(x_1+x_2)+(y_1+y_2)+(z_1+z_2) = (x_1+y_1+z_1)+(x_2+y_2+z_2) = 0+0 = 0$이므로 합도 $W_1$에 속한다. 스칼라배도 마찬가지로 $W_1$에 속한다.

(b) $W_2$는 부분공간이 아니다. $0 = (0,0,0) \notin W_2$ ($0+0+0 \neq 1$)이므로.

(c) $W_3$는 부분공간이 아니다. $x^2 + y^2 = 0$이면 $x = 0$이고 $y = 0$이므로 $W_3 = \{(0,0,z)\}$이다. 이는 $z$축 전체이며, 부분공간 조건을 만족한다... 다시 생각해 보면 $W_3 = \{(0,0,z) \mid z \in \mathbb{R}\}$이므로 $0 \in W_3$, 덧셈과 스칼라배에 닫혀 있다. 따라서 $W_3$는 부분공간이다. (조건 $x^2 + y^2 = 0$이 실수에서는 $x=0, y=0$을 의미하므로.)

**예제 2:** 함수 $f(x) = e^x$, $g(x) = e^{2x}$가 $C[0,1]$에서 일차독립인가?

**풀이:** $\alpha e^x + \beta e^{2x} = 0$ (모든 $x \in [0,1]$에서)이라 가정하자. $x = 0$을 대입하면 $\alpha + \beta = 0$. $x = 1$을 대입하면 $\alpha e + \beta e^2 = 0$. 첫 식에서 $\beta = -\alpha$를 둘째에 대입: $\alpha e - \alpha e^2 = \alpha(e - e^2) = 0$. $e \neq e^2$이므로 $\alpha = 0$이고 따라서 $\beta = 0$이다. 따라서 일차독립이다.

**예제 3:** 다항식 $p_1(x) = 1 + x$, $p_2(x) = 1 - x$, $p_3(x) = 1 + x^2$가 $\mathcal{P}_2$의 기저를 이루는가?

**풀이:** $\mathcal{P}_2$의 차원은 3이므로, 세 다항식이 일차독립이면 기저가 된다. $\alpha p_1 + \beta p_2 + \gamma p_3 = 0$라 하면

$$\alpha(1+x) + \beta(1-x) + \gamma(1+x^2) = (\alpha + \beta + \gamma) + (\alpha - \beta)x + \gamma x^2 = 0$$

이 모든 $x$에 대해 성립하므로 각 차수의 계수가 0이어야 한다:

$$\alpha + \beta + \gamma = 0,\quad \alpha - \beta = 0,\quad \gamma = 0$$

$\gamma = 0$에서 $\alpha + \beta = 0$, $\alpha - \beta = 0$이므로 $\alpha = \beta = 0$. 따라서 일차독립이고, $\mathcal{P}_2$의 기저이다. $\{1+x, 1-x, 1+x^2\}$는 $\mathcal{P}_2$의 한 기저이다.

**예제 4:** $W = \{f \in C[0,1] \mid f(0) = 0\}$이 $C[0,1]$의 부분공간임을 보여라.

**풀이:** 1. 영함수 $0(x) = 0$에 대해 $0(0) = 0$이므로 $0 \in W$.
2. $f, g \in W$이면 $(f+g)(0) = f(0) + g(0) = 0 + 0 = 0$이므로 $f+g \in W$.
3. $f \in W$, $\alpha \in \mathbb{R}$이면 $(\alpha f)(0) = \alpha \cdot f(0) = \alpha \cdot 0 = 0$이므로 $\alpha f \in W$.

따라서 $W$는 부분공간이다.

## 연결

- **[내적과 노름](topics/inner-product-norm.html)** : 벡터공간에 내적이 추가되면 내적공간이 되고, 노름과 직교성의 개념을 추상공간으로 확장할 수 있다.
- **[직교성·직교투영·그람-슈미트](topics/orthogonality.html)** : 함수공간에서의 직교 기저(예: 푸리에 급수의 삼각함수 기저)는 중요한 응용이다.
- **[푸리에 급수·푸리에 변환](topics/fourier.html)** : 함수를 주파수 성분의 선형결합으로 분해하는 것은 벡터공간에서의 기저 전개로 이해할 수 있다.
- **[행렬곱과 선형변환](topics/matrix-multiplication.html)** : 유한차원 벡터공간 사이의 선형변환은 항상 행렬로 표현된다.
- **[rank·열공간·널공간](topics/rank-nullspace.html)** : rank-nullity 정리는 유한차원 벡터공간 사이의 모든 선형변환에 대해 성립한다.
- **[고유값·고유벡터](topics/eigenvalues.html)** : 무한차원 함수공간에서의 고유값 문제는 미분방정식과 양자역학의 핵심이다.
- **상미분방정식 기초** : 선형 미분방정식의 해공간이 벡터공간을 이룬다는 사실(중첩 원리)이 전체 이론의 기초다.
