---
title: 함수
slug: functions
---

> 학습 순서 4 / 75 · [처음부터 읽기](math-language.html)

## 작은 예제로 시작하기

**앞에서 가져올 것:** 집합은 입력 후보나 출력 후보를 담는 모임이고, 문자는 숫자가 들어갈 자리다.

‘한 개에 2천 원인 물건 $x$개의 가격’을 $f(x)=2x$라고 쓰자. 단위를 천 원으로 잡았으므로 $f(3)=6$이다. $f$는 규칙의 이름, $x$는 입력, $f(x)$는 그 입력에 대응하는 출력이다. $f(x)$를 $f\times x$로 읽지 않는다.

자연수 개수만 살 수 있다면 정의역은 $\{0,1,2,\ldots\}$이다. 공역을 음이 아닌 실수로 정해도 실제 나오는 값인 치역은 $\{0,2,4,\ldots\}$다. 공역은 ‘출력이 들어가기로 정한 범위’, 치역은 ‘실제로 나오는 출력’이다. 서로 다른 입력이 같은 출력을 내도 함수다. 한 입력에 출력을 두 개 지정하면 함수가 아니다.

$f(x)=x+1$, $g(x)=2x$이면 $(g\circ f)(3)=g(4)=8$이다. 오른쪽 규칙부터 적용한다. 역함수는 출력을 보고 입력을 하나로 되찾는 규칙이다. $f(x)=x^2$에서 출력 4의 입력은 $2,-2$이므로 실수 전체에서는 역함수가 없다. 입력을 $x\ge0$으로 제한하면 $\sqrt{x}$로 되찾을 수 있다.

**증명으로 이어 읽기:** 단사는 ‘출력이 같으면 입력도 같다’, 전사는 ‘공역의 모든 값이 실제로 나온다’다. 둘을 합친 전단사에서만 모든 공역 원소를 입력 하나로 되돌릴 수 있다. 합성의 결합법칙은 괄호 위치를 바꿔도 입력이 거치는 규칙의 순서는 같다는 뜻이다.

---

## 직관적 설명

함수(function)는 단순한 "입력-출력 기계"가 아니다. 두 집합 사이의 **대응 규칙** 중 특별한 성질을 만족하는 것이다: 정의역(domain)의 각 원소에 대해 공역(codomain)의 **오직 하나**의 원소를 대응시킨다. 이 대응이 수학 전반에서 구조를 보존하고 변환하는 기본 단위가 된다. 선형변환(linear transformation)은 벡터공간 사이의 함수이고, 확률변수(random variable)는 표본공간에서 실수로 가는 함수이며, 미분(differentiation)은 함수를 그 도함수로 보내는 연산자(operator)이다. 함수를 받아 숫자를 내놓는 범함수(functional)와 구별한다. 함수를 이해하는 것은 수학의 가장 보편적인 렌즈를 얻는 일이다.

---
## 정의

**함수(function)** $f: A \to B$는 집합 $A$의 각 원소 $x$에 집합 $B$의 **유일한(unique)** 원소 $f(x)$를 대응시키는 규칙이다.

- $A$를 **정의역(domain)**, $B$를 **공역(codomain)**이라 부른다.
- $f(A) = \{f(x) \mid x \in A\} \subseteq B$를 **치역(range 또는 image)**이라 부른다.
- $x$를 **독립변수(independent variable)**, $y = f(x)$를 **종속변수(dependent variable)**라 한다.

**단사(injection, one-to-one):** $\forall x_1, x_2 \in A,\; x_1 \neq x_2 \Rightarrow f(x_1) \neq f(x_2)$. 즉, 서로 다른 입력이 같은 출력을 내지 않는다. 동치 조건은 $f(x_1) = f(x_2) \Rightarrow x_1 = x_2$이다.

**전사(surjection, onto):** $\forall y \in B,\; \exists x \in A : f(x) = y$. 즉, 공역의 모든 원소가 어떤 입력의 출력으로 나타난다. 치역이 공역과 같다.

**전단사(bijection):** 단사이면서 동시에 전사인 함수. 정의역과 공역의 원소가 일대일로 대응된다.

**합성함수(composition):** $f: A \to B$, $g: B \to C$에 대해 $(g \circ f)(x) = g(f(x))$로 정의된다.

**항등함수(identity function):** $\text{id}_A : A \to A$, $\text{id}_A(x) = x$.

**역함수(inverse function):** $f: A \to B$가 전단사일 때, $f^{-1}: B \to A$가 존재하여 $f^{-1}(y) = x \iff f(x) = y$를 만족한다. 이때 $f^{-1} \circ f = \text{id}_A$, $f \circ f^{-1} = \text{id}_B$이다.

---
## 주요 정리와 증명

### 정리 1: 전단사와 역함수의 동치

$f: A \to B$에 대해, $f$가 전단사(bijection)일 필요충분조건은 $f$의 역함수 $f^{-1}: B \to A$가 존재하는 것이다.

**증명:** 두 방향을 각각 증명한다.

($\Rightarrow$) $f$가 전단사라고 가정하자. 임의의 $y \in B$에 대해, 전사성에 의해 $f(x) = y$인 $x \in A$가 존재한다. 이러한 $x$는 단사성에 의해 유일하다. 따라서 $g(y) = x$로 함수 $g: B \to A$를 정의할 수 있다. 그러면 $g(f(x)) = x$이고 $f(g(y)) = y$이므로 $g$가 $f$의 역함수이다.

($\Leftarrow$) $f^{-1}: B \to A$가 존재한다고 가정하자.
- **단사성:** $f(x_1) = f(x_2)$라 하자. 양변에 $f^{-1}$을 적용하면 $x_1 = f^{-1}(f(x_1)) = f^{-1}(f(x_2)) = x_2$이다.
- **전사성:** 임의의 $y \in B$에 대해 $x = f^{-1}(y)$라 두면 $f(x) = f(f^{-1}(y)) = y$이다.

따라서 $f$는 전단사이다.

### 정리 2: 합성의 결합법칙

함수 $f: A \to B$, $g: B \to C$, $h: C \to D$에 대해 다음이 성립한다.

$$(h \circ g) \circ f = h \circ (g \circ f)$$

**증명:** 두 함수의 정의역이 모두 $A$이고, 공역이 모두 $D$임을 확인한다. 임의의 $x \in A$에 대해

$$((h \circ g) \circ f)(x) = (h \circ g)(f(x)) = h(g(f(x)))$$

한편,

$$(h \circ (g \circ f))(x) = h((g \circ f)(x)) = h(g(f(x)))$$

따라서 모든 $x$에 대해 두 값이 같으므로 두 함수는 동일하다.

### 정리 3: 항등함수와의 관계

$f: A \to B$에 대해 다음이 성립한다.

$$f \circ \text{id}_A = f = \text{id}_B \circ f$$

**증명:** 임의의 $x \in A$에 대해 $(f \circ \text{id}_A)(x) = f(\text{id}_A(x)) = f(x)$이고, 임의의 $y \in B$에 대해 $(\text{id}_B \circ f)(y) = \text{id}_B(f(y)) = f(y)$. 따라서 성립한다.

---
## 예제

**예제 1:** $f: \mathbb{R} \to \mathbb{R}$, $f(x) = x^2$과 $g: \mathbb{R} \to \mathbb{R}$, $g(x) = 2x + 1$에 대해 단사(injectivity)와 전사(surjectivity)를 판정하라.

**풀이:**
- $f(x) = x^2$: $f(1) = 1 = f(-1)$이므로 단사가 아니다. 또한 $y < 0$인 $y$에 대해 $f(x) = y$를 만족하는 실수 $x$가 없으므로 전사도 아니다.
- $g(x) = 2x + 1$: $g(x_1) = g(x_2) \Rightarrow 2x_1 + 1 = 2x_2 + 1 \Rightarrow x_1 = x_2$이므로 단사이다. 임의의 $y \in \mathbb{R}$에 대해 $x = (y-1)/2$를 대입하면 $g(x) = y$이므로 전사이다. 따라서 $g$는 전단사이다.

**예제 2:** $f(x) = 2x + 1$, $g(x) = x^2$일 때 $f \circ g$와 $g \circ f$를 각각 구하라.

**풀이:**
$$(f \circ g)(x) = f(g(x)) = f(x^2) = 2x^2 + 1$$
$$(g \circ f)(x) = g(f(x)) = g(2x + 1) = (2x + 1)^2 = 4x^2 + 4x + 1$$

두 결과가 다름에 주목하라. 합성함수는 일반적으로 교환법칙이 성립하지 않는다.

**예제 3:** $f(x) = \frac{x}{x-1}$ ($x \neq 1$)의 역함수를 구하라.

**풀이:** $y = \frac{x}{x-1}$이라 두고 $x$에 대해 푼다.
$$y(x-1) = x \;\Rightarrow\; yx - y = x \;\Rightarrow\; yx - x = y \;\Rightarrow\; x(y-1) = y \;\Rightarrow\; x = \frac{y}{y-1}$$
따라서 $f^{-1}(y) = \frac{y}{y-1}$ ($y \neq 1$)이다. $f^{-1}$의 정의역이 $f$의 치역과 일치함을 확인할 수 있다.

---
## 연결

- **[집합과 논리](sets-and-logic.html)** : 함수는 집합 사이의 대응으로 정의되며, 집합론의 용어(정의역, 공역, 치역)를 사용한다.
- **[행렬과 선형변환](matrix-multiplication.html)** : 행렬은 선형함수(linear map)를 유한차원에서 표현한 것이다.
- **[극한과 도함수](limits-derivatives.html)** : 미분계수 $f'(a)$는 함수의 국소적 선형근사로, 함수의 개념 위에 세워진다.

---

[← 이전: 다항식·방정식·부등식](polynomials-equations.html) · [다음: 지수와 로그 →](exponentials-logarithms.html)
