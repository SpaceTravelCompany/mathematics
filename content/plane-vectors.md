---
title: 평면벡터 기초
slug: plane-vectors
---

## 직관적 설명

**벡터(vector)** 는 "어디로 얼마나"라는 정보를 담은 객체다. 위치와 관계없이 방향(direction)과 크기(magnitude)만 같으면 같은 벡터로 본다. 이것은 벡터가 좌표에 묶여 있지 않은 자유로운 기하학적 객체임을 의미한다. 벡터는 힘, 속도, 변위 등 방향성을 가진 물리량을 표현하는 자연스러운 도구이며, 수학적으로는 벡터공간(vector space)이라는 추상 구조의 원형(prototype)이 된다. 두 벡터의 **내적(inner product, dot product)** 은 "두 벡터가 얼마나 같은 방향인가"를 수량화하며, 이 개념은 고차원 공간에서의 유사도(similarity)와 직교성(orthogonality)의 출발점이다.

---
## 정의

**벡터(vector):** 평면 위의 벡터 $\vec{v}$는 순서쌍 $(v_1, v_2)$으로 표현된다. 여기서 $v_1$을 $x$-성분(component), $v_2$를 $y$-성분이라 한다.

**시점과 종점:** 두 점 $A(a_1, a_2)$, $B(b_1, b_2)$에 대해 벡터 $\overrightarrow{AB} = (b_1 - a_1, b_2 - a_2)$이다.

**크기(magnitude, norm):** $\|\vec{v}\| = \sqrt{v_1^2 + v_2^2}$.

**영벡터(zero vector):** $\vec{0} = (0, 0)$. 크기가 0이고 방향이 정의되지 않는다.

**단위벡터(unit vector):** 크기가 1인 벡터. $\hat{v} = \frac{\vec{v}}{\|\vec{v}\|}$ ($\vec{v} \neq \vec{0}$).

**기본단위벡터(standard basis vectors):** $\hat{i} = (1, 0)$, $\hat{j} = (0, 1)$. 임의의 벡터는 $\vec{v} = v_1 \hat{i} + v_2 \hat{j}$로 표현된다.

**벡터의 덧셈:** $\vec{a} + \vec{b} = (a_1 + b_1, a_2 + b_2)$. 기하학적으로는 평행사변형 법칙(parallelogram law)을 따른다.

**스칼라배(scalar multiplication):** $c\vec{v} = (cv_1, cv_2)$ ($c \in \mathbb{R}$).

**내적(dot product):** $\vec{a} \cdot \vec{b} = a_1 b_1 + a_2 b_2 = \|\vec{a}\| \|\vec{b}\| \cos\theta$.

여기서 $\theta$는 두 벡터 사이의 각(angle)이다 ($0 \leq \theta \leq \pi$).

---
## 주요 정리와 증명

### 정리 1: 코시-슈바르츠 부등식 (Cauchy-Schwarz Inequality)

평면 위의 두 벡터 $\vec{a}, \vec{b}$에 대해 다음이 성립한다.

$$|\vec{a} \cdot \vec{b}| \leq \|\vec{a}\| \|\vec{b}\|$$

등호는 $\vec{a}$와 $\vec{b}$가 평행(즉, 하나가 다른 것의 스칼라배)일 때 성립한다.

**증명 (판별식 방법):** 실수 $t$에 대해 함수 $f(t) = \| \vec{a} + t\vec{b} \|^2$를 고려하자. 노름의 제곱이므로 $f(t) \geq 0$이다. 이를 전개하면

$$f(t) = (\vec{a} + t\vec{b}) \cdot (\vec{a} + t\vec{b}) = \vec{a} \cdot \vec{a} + 2t(\vec{a} \cdot \vec{b}) + t^2 (\vec{b} \cdot \vec{b})$$

$$= \|\vec{a}\|^2 + 2t(\vec{a} \cdot \vec{b}) + t^2 \|\vec{b}\|^2$$

이것은 $t$에 대한 이차식이다. $f(t) \geq 0$이 모든 실수 $t$에 대해 성립하므로, 이 이차식의 판별식 $D$는 0 이하여야 한다.

$$D = (2\vec{a} \cdot \vec{b})^2 - 4 \|\vec{a}\|^2 \|\vec{b}\|^2 \leq 0$$

$$4(\vec{a} \cdot \vec{b})^2 - 4 \|\vec{a}\|^2 \|\vec{b}\|^2 \leq 0$$

$$(\vec{a} \cdot \vec{b})^2 \leq \|\vec{a}\|^2 \|\vec{b}\|^2$$

양변에 제곱근을 취하면 $|\vec{a} \cdot \vec{b}| \leq \|\vec{a}\| \|\vec{b}\|$을 얻는다. 등호 조건 $D = 0$은 이차식이 완전제곱일 때, 즉 $\vec{a} + t\vec{b} = \vec{0}$인 $t$가 존재할 때(벡터가 평행할 때) 성립한다.

### 정리 2: 내적과 직교 (Orthogonality)

$\vec{a} \perp \vec{b}$ (두 벡터가 직교)일 필요충분조건은 $\vec{a} \cdot \vec{b} = 0$이다 ($\vec{a}, \vec{b}$가 모두 영벡터가 아닐 때).

**증명:** 내적의 정의 $\vec{a} \cdot \vec{b} = \|\vec{a}\| \|\vec{b}\| \cos\theta$에서, $\|\vec{a}\| > 0$, $\|\vec{b}\| > 0$이므로 $\vec{a} \cdot \vec{b} = 0 \iff \cos\theta = 0 \iff \theta = \pi/2$ (또는 $90^\circ$)이다. 이는 정확히 두 벡터가 수직인 조건이다.

**참고:** 영벡터는 모든 벡터와의 내적이 0이므로 형식적으로 모든 벡터와 직교한다고 간주하기도 한다.

### 정리 3: 투영 벡터 (Vector Projection)

벡터 $\vec{a}$의 $\vec{b}$ 방향으로의 **정사영(projection)** 은

$$\text{proj}_{\vec{b}} \vec{a} = \frac{\vec{a} \cdot \vec{b}}{\|\vec{b}\|^2} \vec{b}$$

이고, 이에 수직인 성분은 $\vec{a} - \text{proj}_{\vec{b}} \vec{a}$이다.

**증명:** $\text{proj}_{\vec{b}} \vec{a} = t\vec{b}$의 형태를 가져야 한다 (같은 방향). 잔차(residual) $\vec{a} - t\vec{b}$가 $\vec{b}$와 직교해야 하므로

$$(\vec{a} - t\vec{b}) \cdot \vec{b} = 0 \;\Longrightarrow\; \vec{a} \cdot \vec{b} - t \|\vec{b}\|^2 = 0 \;\Longrightarrow\; t = \frac{\vec{a} \cdot \vec{b}}{\|\vec{b}\|^2}$$

**스칼라 투영(scalar projection):** $\text{comp}_{\vec{b}} \vec{a} = \|\vec{a}\| \cos\theta = \frac{\vec{a} \cdot \vec{b}}{\|\vec{b}\|}$는 투영 벡터의 길이(부호 포함)이다.

---
## 예제

**예제 1:** $\vec{a} = (3, -1)$, $\vec{b} = (2, 4)$에 대해 다음을 구하라.
(a) $\vec{a} \cdot \vec{b}$ \quad (b) $\|\vec{a}\|$, $\|\vec{b}\|$ \quad (c) 두 벡터 사이의 각 $\theta$

**풀이:**
(a) $\vec{a} \cdot \vec{b} = 3\cdot2 + (-1)\cdot4 = 6 - 4 = 2$
(b) $\|\vec{a}\| = \sqrt{3^2 + (-1)^2} = \sqrt{10}$, $\|\vec{b}\| = \sqrt{2^2 + 4^2} = \sqrt{20} = 2\sqrt{5}$
(c) $\cos\theta = \frac{\vec{a} \cdot \vec{b}}{\|\vec{a}\| \|\vec{b}\|} = \frac{2}{\sqrt{10} \cdot 2\sqrt{5}} = \frac{2}{2\sqrt{50}} = \frac{1}{\sqrt{50}} = \frac{1}{5\sqrt{2}}$
따라서 $\theta = \cos^{-1}(1/(5\sqrt{2})) \approx 81.87^\circ$.

**예제 2:** $\vec{a} = (4, 3)$을 $\vec{b} = (1, 2)$ 방향으로 투영하라.

**풀이:**
$\vec{a} \cdot \vec{b} = 4\cdot1 + 3\cdot2 = 10$, $\|\vec{b}\|^2 = 1^2 + 2^2 = 5$.
$$\text{proj}_{\vec{b}} \vec{a} = \frac{10}{5}(1, 2) = 2(1, 2) = (2, 4)$$
수직 성분: $\vec{a} - \text{proj}_{\vec{b}} \vec{a} = (4, 3) - (2, 4) = (2, -1)$. 확인: $(2, -1) \cdot (1, 2) = 2 - 2 = 0$이므로 직교한다.

**예제 3:** 세 점 $A(1, 1)$, $B(4, 2)$, $C(3, 5)$가 이루는 평행사변형의 넓이를 구하라.

**풀이:** $\overrightarrow{AB} = (3, 1)$, $\overrightarrow{AC} = (2, 4)$라 하자. 평행사변형의 넓이는 $|\overrightarrow{AB} \times \overrightarrow{AC}|$ (2차원에서는 외적의 크기 = $|a_1 b_2 - a_2 b_1|$)와 같다.

$$\text{넓이} = |3 \cdot 4 - 1 \cdot 2| = |12 - 2| = 10$$

---
## 연결

- **[내적과 노름](inner-product-norm.html)** : 평면벡터의 내적과 노름을 고차원 벡터공간으로 일반화한다.
- **[행렬곱과 선형변환](matrix-multiplication.html)** : 행렬은 벡터를 다른 벡터로 보내는 선형함수이고, 행렬곱은 합성함수에 해당한다.
- **[좌표기하와 이차곡선](coordinate-geometry.html)** : 벡터의 좌표 표현은 해석기하학의 기본 언어이다.
