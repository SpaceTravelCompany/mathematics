---
title: 다항식·방정식·부등식
slug: polynomials-equations
---

## 직관적 설명

**다항식(polynomial)** 은 가장 단순하면서도 가장 강력한 함수 형태다. 오직 덧셈과 곱셈, 그리고 자연수 거듭제곱만으로 구성되지만, 이 간단한 구조로도 놀라울 정도로 다양한 현상을 표현할 수 있다. **방정식(equation)** 은 "두 표현이 언제 같아지는가"라는 질문이고, **부등식(inequality)** 은 "언데 한쪽이 더 큰가"라는 질문이다. 이 두 질문은 수학의 모든 분야에서 반복해서 등장한다. 다항방정식의 해를 찾는 인수분해(factorization)는 선형대수의 특성방정식(characteristic equation)으로 이어지고, 부등식의 해집합은 최적화(optimization) 문제의 출발점이다.

## 정의

**다항식(polynomial):** 변수 $x$에 대한 다항식은 다음과 같은 유한합 형태로 표현된다.

$$P(x) = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_1 x + a_0$$

여기서 $a_i$는 계수(coefficient)이며, $a_n \neq 0$일 때 $n$을 **차수(degree)**라 하고 $\deg(P) = n$으로 표기한다. $a_n$을 **최고차항 계수(leading coefficient)**라 한다.

**인수분해(factorization):** 다항식을 더 낮은 차수의 다항식들의 곱으로 표현하는 것. 예: $x^2 - 5x + 6 = (x-2)(x-3)$.

**방정식(equation):** $P(x) = 0$의 형태로 주어지며, 이를 만족하는 $x$를 **근(root)** 또는 **해(solution)**라 한다.

**이차방정식(quadratic equation):** $ax^2 + bx + c = 0$ ($a \neq 0$)의 해는 **근의 공식(quadratic formula)** 으로 주어진다.

$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

**판별식(discriminant):** $D = b^2 - 4ac$로 정의된다.
- $D > 0$: 서로 다른 두 실근
- $D = 0$: 중근(double root)
- $D < 0$: 두 허근(complex conjugate roots)

**부등식(inequality):** 두 표현 사이의 대소 관계 $P(x) > 0$, $P(x) \geq 0$ 등을 말한다.

**절댓값 부등식(absolute value inequality):** $|x - a| < r$는 $a - r < x < a + r$과 동치이다. 일반적으로 $|x - a|$는 수직선 위에서 $x$와 $a$ 사이의 거리를 의미한다.

**항등식(identity):** 모든 $x$에 대해 성립하는 등식. 예: $(x+1)^2 = x^2 + 2x + 1$은 항등식이다.

## 주요 정리와 증명

### 정리 1: 근의 공식 유도

이차방정식 $ax^2 + bx + c = 0$ ($a \neq 0$)의 해는 $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$이다.

**증명 (완전제곱식 만들기, completing the square):**

양변을 $a$로 나눈다.

$$x^2 + \frac{b}{a}x + \frac{c}{a} = 0$$

$x$ 항의 계수의 절반의 제곱 $\left(\frac{b}{2a}\right)^2$을 양변에 더한다.

$$x^2 + \frac{b}{a}x + \left(\frac{b}{2a}\right)^2 = \left(\frac{b}{2a}\right)^2 - \frac{c}{a}$$

좌변은 완전제곱식이다.

$$\left(x + \frac{b}{2a}\right)^2 = \frac{b^2}{4a^2} - \frac{c}{a} = \frac{b^2 - 4ac}{4a^2}$$

양변에 제곱근을 취한다.

$$x + \frac{b}{2a} = \pm \sqrt{\frac{b^2 - 4ac}{4a^2}} = \pm \frac{\sqrt{b^2 - 4ac}}{2a}$$

따라서

$$x = -\frac{b}{2a} \pm \frac{\sqrt{b^2 - 4ac}}{2a} = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

### 정리 2: 인수정리 (Factor Theorem)

$f(x)$가 다항식일 때, $f(a) = 0$일 필요충분조건은 $(x-a)$가 $f(x)$의 인수인 것이다. 즉 $f(x) = (x-a)Q(x)$를 만족하는 다항식 $Q(x)$가 존재한다.

**증명:** 다항식의 나눗셈 정리(division algorithm)에 의해, $f(x)$를 $(x-a)$로 나누면

$$f(x) = (x-a)Q(x) + R$$

여기서 $Q(x)$는 몫(quotient), $R$은 나머지(remainder)이다. 나머지 $R$은 상수인데, 그 이유는 $(x-a)$가 1차식이므로 나머지는 차수가 0인 상수여야 하기 때문이다.

($\Rightarrow$) $f(a) = 0$이라 하자. $x = a$를 대입하면

$$f(a) = (a-a)Q(a) + R = 0 + R = R$$

따라서 $R = 0$이고, $f(x) = (x-a)Q(x)$이다.

($\Leftarrow$) $(x-a)$가 $f(x)$의 인수이면 $f(x) = (x-a)Q(x)$로 쓸 수 있다. $x = a$를 대입하면 $f(a) = (a-a)Q(a) = 0$이다.

**따름정리(Corollary):** 상수항이 $a_0$인 $n$차 다항식 $f(x)$가 서로 다른 $n$개의 실근 $\alpha_1, \ldots, \alpha_n$을 가지면

$$f(x) = a_n(x - \alpha_1)(x - \alpha_2)\cdots(x - \alpha_n)$$

으로 인수분해된다.

### 정리 3: 삼차방정식의 판별 조건 (개요)

삼차방정식 $ax^3 + bx^2 + cx + d = 0$ ($a \neq 0$)의 판별식 $\Delta$는 다음과 같다.

$$\Delta = 18abcd - 4b^3d + b^2c^2 - 4ac^3 - 27a^2d^2$$

- $\Delta > 0$: 서로 다른 세 실근
- $\Delta = 0$: 중근 발생 (적어도 두 근이 같음)
- $\Delta < 0$: 한 실근과 두 허근

이차방정식의 판별식과 달리 삼차 이상에서는 판별식이 더 복잡해지지만, 근의 성질을 결정한다는 역할은 동일하다.

## 예제

**예제 1:** 이차방정식 $2x^2 - 4x - 6 = 0$을 풀어라.

**풀이:** $a = 2$, $b = -4$, $c = -6$을 근의 공식에 대입한다.

$$x = \frac{-(-4) \pm \sqrt{(-4)^2 - 4 \cdot 2 \cdot (-6)}}{2 \cdot 2} = \frac{4 \pm \sqrt{16 + 48}}{4} = \frac{4 \pm \sqrt{64}}{4} = \frac{4 \pm 8}{4}$$

따라서 $x = \frac{4+8}{4} = 3$ 또는 $x = \frac{4-8}{4} = -1$이다.

인수분해로 확인: $2x^2 - 4x - 6 = 2(x^2 - 2x - 3) = 2(x-3)(x+1) = 0$이므로 $x = 3$ 또는 $x = -1$.

**예제 2:** 부등식 $|2x - 3| < 5$를 풀어라.

**풀이:** 절댓값 부등식 $|X| < a$ ($a > 0$)의 해는 $-a < X < a$이다. 여기에 대입하면

$$-5 < 2x - 3 < 5$$

각 변에 3을 더한다.

$$-2 < 2x < 8$$

각 변을 2로 나눈다.

$$-1 < x < 4$$

따라서 해집합은 $(-1, 4)$이다.

**예제 3:** 다항식 $P(x) = x^3 - 6x^2 + 11x - 6$의 근을 구하고 인수분해하라.

**풀이:** $P(1) = 1 - 6 + 11 - 6 = 0$이므로 인수정리에 의해 $(x-1)$이 인수이다. 조립제법(synthetic division)으로 나누면

$$P(x) = (x-1)(x^2 - 5x + 6)$$

이차식을 다시 인수분해하면 $x^2 - 5x + 6 = (x-2)(x-3)$이다.

따라서 $P(x) = (x-1)(x-2)(x-3)$이고, 근은 $x = 1, 2, 3$이다.

## 연결

- **[좌표기하와 이차곡선](topics/coordinate-geometry.html)** : 원뿔곡선의 방정식은 모두 이차방정식이다.
- **[고유값과 고유벡터](topics/eigenvalues.html)** : 특성방정식 $\det(A - \lambda I) = 0$은 다항방정식으로, 고유값을 찾는 핵심 도구이다.
- **[극한과 도함수](topics/limits-derivatives.html)** : 다항함수의 미분은 차수를 낮추는 간단한 연산이다.
