---
title: 내적·노름·코사인 유사도
slug: inner-product-norm
---

## 직관적 설명

**내적(inner product, dot product)**은 두 벡터가 얼마나 같은 방향을 향하는지를 하나의 숫자로 요약한다. 한 벡터를 다른 벡터에 비추었을 때 생기는 "그림자의 길이"라고 생각할 수 있다. 그림자가 길수록 두 벡터의 방향이 비슷하고, 0이면 수직이다.

**노름(norm)**은 벡터의 길이, 즉 크기(magnitude)다. 내적을 이용하면 길이를 정의할 수 있다: $\|v\| = \sqrt{\langle v, v \rangle}$. 내적이 있으면 길이와 각도, 거리라는 기하학적 개념을 추상적 벡터공간에서도 사용할 수 있다.

**코사인 유사도(cosine similarity)**는 두 벡터 사이의 각도의 코사인값이다. 방향만 비교하고 크기는 무시한다. 문서 분류, 추천 시스템 등에서 "두 데이터 포인트가 얼마나 비슷한가"를 측정하는 표준 도구로 사용된다.

내적공간(inner product space)은 유클리드 공간 $\mathbb{R}^n$의 기하학 — 길이, 각도, 직교성 — 을 일반적인 벡터공간으로 확장한다. 다항식, 함수, 신호도 내적공간의 원소가 될 수 있다.

---
## 정의

**내적 (inner product):** 실벡터공간 $V$ 위의 내적 $\langle \cdot, \cdot \rangle : V \times V \to \mathbb{R}$은 다음 공리를 만족하는 함수다.

1. **대칭성 (symmetry):** $\langle u, v \rangle = \langle v, u \rangle$ (실수), $\langle u, v \rangle = \overline{\langle v, u \rangle}$ (복소수, 에르미트 대칭)
2. **선형성 (linearity in the second argument):** $\langle u, \alpha v + \beta w \rangle = \alpha \langle u, v \rangle + \beta \langle u, w \rangle$
3. **양정부호 (positive definiteness):** $\langle v, v \rangle \geq 0$, 등호는 $v = 0$일 때만

**표준 내적 (Euclidean inner product):** $\mathbb{R}^n$에서
$$\langle u, v \rangle = u_1 v_1 + u_2 v_2 + \cdots + u_n v_n = \sum_{i=1}^n u_i v_i$$

**복소 내적:** $\mathbb{C}^n$에서
$$\langle u, v \rangle = \sum_{i=1}^n \bar{u}_i v_i$$
공액(conjugate)을 취하는 이유는 $\langle v, v \rangle = \sum |v_i|^2 \geq 0$을 보장하기 위해서다.

**유도 노름 (induced norm):** 내적에서 유도되는 노름
$$\|v\| = \sqrt{\langle v, v \rangle}$$

이는 다음 노름 공리를 만족한다.
1. **양정부호:** $\|v\| \geq 0$, $\|v\| = 0 \iff v = 0$
2. **절대 동차성:** $\|\alpha v\| = |\alpha| \|v\|$
3. **삼각부등식:** $\|u + v\| \leq \|u\| + \|v\|$

**코사인 유사도 (cosine similarity):** 두 벡터 $u, v \neq 0$ 사이의 각 $\theta$에 대해
$$\cos\theta = \frac{\langle u, v \rangle}{\|u\|\|v\|}$$

**거리 (distance/metric):** 내적에서 유도되는 거리
$$d(u, v) = \|u - v\|$$

**함수공간에서의 내적:** 구간 $[a, b]$에서 연속인 함수들의 공간 $C[a, b]$에서
$$\langle f, g \rangle = \int_a^b f(x) g(x) \, dx$$

$L^2$ 노름은 $\|f\|_2 = \left( \int_a^b |f(x)|^2 \, dx \right)^{1/2}$이다.

---
## 주요 정리와 증명

### 정리 1: 코시-슈바르츠 부등식 (Cauchy-Schwarz Inequality)

내적공간 $V$의 모든 $u, v$에 대해
$$|\langle u, v \rangle| \leq \|u\|\|v\|$$

등호는 $u$와 $v$가 일차종속(즉, $u = \alpha v$ 또는 $v = 0$)일 때 성립한다.

**증명:** $v = 0$이면 양변이 0이므로 자명하다. $v \neq 0$이라 가정하자. 실수 $t$에 대한 함수
$$f(t) = \langle u + tv, u + tv \rangle = \|u + tv\|^2 \geq 0$$

를 전개하면
$$f(t) = \langle u, u \rangle + t\langle u, v \rangle + t\langle v, u \rangle + t^2 \langle v, v \rangle$$

실내적공간에서는 $\langle v, u \rangle = \langle u, v \rangle$이므로
$$f(t) = \|u\|^2 + 2t \langle u, v \rangle + t^2 \|v\|^2$$

$f(t) \geq 0$가 모든 실수 $t$에 대해 성립하므로, 이 이차식의 판별식은 0 이하다:
$$D = (2\langle u, v \rangle)^2 - 4\|u\|^2\|v\|^2 \leq 0$$

따라서
$$|\langle u, v \rangle| \leq \|u\|\|v\|$$

등호 조건 $D = 0$은 $f(t) = \|u + tv\|^2 = 0$인 $t$가 존재함을 의미하며, 이는 $u + tv = 0$, 즉 $u = -tv$로 $u$와 $v$가 일차종속임을 뜻한다.

**복소 내적공간에서의 증명:** $\langle v, u \rangle = \overline{\langle u, v \rangle}$이므로
$$f(t) = \|u\|^2 + 2\,\text{Re}(t\langle u, v \rangle) + |t|^2\|v\|^2$$

$t = -\langle u, v \rangle / \|v\|^2$로 선택하면(실수일 필요 없음)
$$0 \leq \|u\|^2 - \frac{|\langle u, v \rangle|^2}{\|v\|^2}$$

를 얻고, 따라서 $|\langle u, v \rangle| \leq \|u\|\|v\|$가 성립한다.

### 정리 2: 삼각부등식 (Triangle Inequality)

$$\|u + v\| \leq \|u\| + \|v\|$$

**증명:** 양변을 제곱하여 코시-슈바르츠 부등식을 적용한다.
$$\|u + v\|^2 = \langle u+v, u+v \rangle = \|u\|^2 + 2\langle u, v \rangle + \|v\|^2$$
$$\leq \|u\|^2 + 2\|u\|\|v\| + \|v\|^2 = (\|u\| + \|v\|)^2$$

양변에 제곱근을 취하면 원하는 부등식을 얻는다.

### 정리 3: 평행사변형 법칙 (Parallelogram Law)

$$\|u + v\|^2 + \|u - v\|^2 = 2\|u\|^2 + 2\|v\|^2$$

**증명:** 직접 전개한다.
$$\|u + v\|^2 = \|u\|^2 + 2\langle u, v \rangle + \|v\|^2$$
$$\|u - v\|^2 = \|u\|^2 - 2\langle u, v \rangle + \|v\|^2$$

두 식을 더하면 교차항이 소거되어
$$\|u + v\|^2 + \|u - v\|^2 = 2\|u\|^2 + 2\|v\|^2$$

**의미:** 평행사변형의 두 대각선 길이의 제곱합은 네 변의 길이의 제곱합과 같다. 이 법칙은 노름이 내적에서 유도되었는지를 판정하는 필요충분조건이다(조르단-폰 노이만 정리).

### 정리 4: 코사인 법칙과 내적

벡터 $u, v$ 사이의 각 $\theta$에 대해
$$\|u - v\|^2 = \|u\|^2 + \|v\|^2 - 2\|u\|\|v\|\cos\theta$$

**증명:**
$$\|u - v\|^2 = \langle u-v, u-v \rangle = \|u\|^2 + \|v\|^2 - 2\langle u, v \rangle$$

내적의 기하학적 정의 $\langle u, v \rangle = \|u\|\|v\|\cos\theta$를 대입하면 코사인 법칙을 얻는다.

### 정리 5: 폴라 항등식 (Polarization Identity)

실내적공간에서 내적은 노름으로 완전히 복원된다:
$$\langle u, v \rangle = \frac{1}{4} \left( \|u+v\|^2 - \|u-v\|^2 \right)$$

복소내적공간에서는
$$\langle u, v \rangle = \frac{1}{4} \left( \|u+v\|^2 - \|u-v\|^2 + i\|u+iv\|^2 - i\|u-iv\|^2 \right)$$

**증명:** 실수 경우, $\|u+v\|^2 = \|u\|^2 + 2\langle u, v \rangle + \|v\|^2$와 $\|u-v\|^2 = \|u\|^2 - 2\langle u, v \rangle + \|v\|^2$를 빼면 $4\langle u, v \rangle$을 얻는다.

**의미:** 이 항등식은 노름이 평행사변형 법칙을 만족할 때만 내적에서 유도될 수 있음을 보여준다(조르단-폰 노이만 정리의 핵심).

### 정리 6: 내적의 연속성

내적은 각 인수에 대해 연속이다. 즉, $u_n \to u$, $v_n \to v$이면 $\langle u_n, v_n \rangle \to \langle u, v \rangle$이다.

**증명:** 코시-슈바르츠 부등식을 이용한다.
$$|\langle u_n, v_n \rangle - \langle u, v \rangle| = |\langle u_n - u, v_n \rangle + \langle u, v_n - v \rangle|$$
$$\leq \|u_n - u\|\|v_n\| + \|u\|\|v_n - v\| \to 0$$

---
## 예제

**예제 1:** $\mathbb{R}^4$에서 $u = (1, -2, 0, 3)$, $v = (2, 1, -1, 1)$에 대해 내적, 노름, 코사인 유사도를 구하라.

**풀이:**
$$\langle u, v \rangle = 1\cdot2 + (-2)\cdot1 + 0\cdot(-1) + 3\cdot1 = 2 - 2 + 0 + 3 = 3$$
$$\|u\| = \sqrt{1^2 + (-2)^2 + 0^2 + 3^2} = \sqrt{1 + 4 + 0 + 9} = \sqrt{14}$$
$$\|v\| = \sqrt{2^2 + 1^2 + (-1)^2 + 1^2} = \sqrt{4 + 1 + 1 + 1} = \sqrt{7}$$
$$\cos\theta = \frac{3}{\sqrt{14}\sqrt{7}} = \frac{3}{\sqrt{98}} = \frac{3}{7\sqrt{2}} \approx 0.303$$

**예제 2:** 구간 $[0, 1]$에서 $f(x) = x$, $g(x) = x^2$의 내적과 노름을 구하라.

**풀이:**
$$\langle f, g \rangle = \int_0^1 x \cdot x^2 \, dx = \int_0^1 x^3 \, dx = \left[ \frac{x^4}{4} \right]_0^1 = \frac{1}{4}$$
$$\|f\| = \left( \int_0^1 x^2 \, dx \right)^{1/2} = \left( \left[ \frac{x^3}{3} \right]_0^1 \right)^{1/2} = \frac{1}{\sqrt{3}}$$
$$\|g\| = \left( \int_0^1 x^4 \, dx \right)^{1/2} = \left( \left[ \frac{x^5}{5} \right]_0^1 \right)^{1/2} = \frac{1}{\sqrt{5}}$$
$$\cos\theta = \frac{1/4}{(1/\sqrt{3})(1/\sqrt{5})} = \frac{\sqrt{15}}{4} \approx 0.968$$

두 함수가 매우 비슷한 방향(매우 가까움)을 의미한다.

**예제 3:** $u = (3, 4)$, $v = (-4, 3)$의 코사인 유사도를 계산하고 해석하라.

**풀이:**
$$\langle u, v \rangle = 3(-4) + 4\cdot3 = -12 + 12 = 0$$
$$\|u\| = 5, \|v\| = 5$$
$$\cos\theta = \frac{0}{5\cdot5} = 0$$

$\cos\theta = 0$이므로 $\theta = 90^\circ$다. 즉, 두 벡터는 직교(orthogonal)한다.

**예제 4 (폴라 항등식 확인):** $u = (1, 2)$, $v = (3, 1)$에 대해 폴라 항등식을 확인하라.

**풀이:**
$u+v = (4, 3)$, $u-v = (-2, 1)$
$$\|u+v\|^2 = 25, \quad \|u-v\|^2 = 5$$
$$\frac14(\|u+v\|^2 - \|u-v\|^2) = \frac14(25 - 5) = 5$$
직접 내적 계산: $\langle u, v \rangle = 1\cdot3 + 2\cdot1 = 5$. 일치한다.

**예제 5 ($\mathbb{R}^n$에서의 코사인 유사도):** 문서 A의 단어 빈도 벡터가 $u = (3, 1, 0, 2, 0)$, 문서 B가 $v = (1, 2, 1, 0, 1)$일 때 두 문서의 코사인 유사도를 구하라.

**풀이:**
$$\langle u, v \rangle = 3\cdot1 + 1\cdot2 + 0\cdot1 + 2\cdot0 + 0\cdot1 = 3 + 2 = 5$$
$$\|u\| = \sqrt{9 + 1 + 0 + 4 + 0} = \sqrt{14}, \quad \|v\| = \sqrt{1 + 4 + 1 + 0 + 1} = \sqrt{7}$$
$$\cos\theta = \frac{5}{\sqrt{14}\sqrt{7}} = \frac{5}{\sqrt{98}} \approx 0.505$$
두 문서는 중간 정도의 유사도를 가진다.

**예제 6 (복소 내적공간):** $\mathbb{C}^2$에서 $u = (1 + i, 2 - i)$, $v = (2, i)$의 내적과 노름을 구하라.

**풀이:**
$$\langle u, v \rangle = \overline{(1+i)}\cdot2 + \overline{(2-i)}\cdot i = (1-i)(2) + (2+i)(i)$$
$$= (2-2i) + (2i + i^2) = (2-2i) + (2i - 1) = 1$$
$$\|u\| = \sqrt{|1+i|^2 + |2-i|^2} = \sqrt{(1^2+1^2) + (2^2+1^2)} = \sqrt{2 + 5} = \sqrt{7}$$
$$\|v\| = \sqrt{|2|^2 + |i|^2} = \sqrt{4 + 1} = \sqrt{5}$$
$$\cos\theta\text{의 일반화: } |\langle u, v \rangle|/(\|u\|\|v\|) = 1/\sqrt{35} \approx 0.169$$

**예제 7 (평행사변형 법칙 확인):** $u = (1, 2)$, $v = (3, 1)$에 대해 평행사변형 법칙을 확인하라.

**풀이:**
$u + v = (4, 3)$, $u - v = (-2, 1)$
$$\|u + v\|^2 = 4^2 + 3^2 = 25, \quad \|u - v\|^2 = (-2)^2 + 1^2 = 5$$
$$\|u\|^2 = 5, \quad \|v\|^2 = 10$$
$$\|u + v\|^2 + \|u - v\|^2 = 25 + 5 = 30 = 2\cdot5 + 2\cdot10$$

---
## 연결

- **[평면벡터 기초](plane-vectors.html)** : 2차원 벡터의 내적과 기하학적 의미를 먼저 학습한다.
- **[직교성·직교투영·그람-슈미트](orthogonality.html)** : 내적이 0인 벡터들의 관계와 벡터 분해로 확장한다.
- **[SVD](svd.html)** : 특이값 분해는 내적공간의 기하를 행렬분해에 적용한 정점이다.
