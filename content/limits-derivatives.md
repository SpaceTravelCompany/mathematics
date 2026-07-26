---
title: 극한·연속·도함수
slug: limits-derivatives
---

## 직관적 설명

**극한(limit)** 은 "무한히 가까이 갈 때의 값"이다. $x$가 $a$에 한없이 가까워질 때 $f(x)$가 다가가는 값을 $\lim_{x \to a} f(x)$로 쓴다. 함수가 그 지점에서 정의되지 않아도 극한이 존재할 수 있다는 점이 중요하다. 예를 들어 $\lim_{x \to 0} \frac{\sin x}{x} = 1$은 $x = 0$에서 분모가 0이지만 극한이 존재하는 경우다.

**연속(continuity)** 은 "그래프가 끊어지지 않음"이다. $x = a$에서 극한값과 함수값이 일치하면 연속이다. 연속은 미분가능성(differentiability)보다 약한 조건으로, 미분가능하면 반드시 연속이지만 연속이라고 미분가능한 것은 아니다.

**도함수(derivative)** 는 "순간 변화율 = 접선의 기울기"다. 평균 변화율 $\frac{f(a+h) - f(a)}{h}$의 극한값이 도함수 $f'(a)$이다. 위치-시간 그래프에서 도함수는 순간 속도(instantaneous velocity)가 되고, 비용-생산량 그래프에서 도함수는 한계 비용(marginal cost)이 된다.

## 정의

**극한(limit):** $f$가 $x = a$ 근처(단 $a$ 제외)에서 정의되었다고 하자. $\lim_{x \to a} f(x) = L$은 다음을 의미한다: 임의의 $\epsilon > 0$에 대해 어떤 $\delta > 0$이 존재하여 $0 < |x - a| < \delta$이면 $|f(x) - L| < \epsilon$이다. 이것이 $\epsilon$-$\delta$ 정의(epsilon-delta definition)다.

**좌극한(left-hand limit)과 우극한(right-hand limit):**
- $\lim_{x \to a^-} f(x) = L$: $x < a$인 쪽에서만 접근
- $\lim_{x \to a^+} f(x) = L$: $x > a$인 쪽에서만 접근
- 극한이 존재할 필요충분조건은 좌극한과 우극한이 모두 존재하고 같을 것이다

**연속(continuity):** $f$가 $x = a$에서 연속이라는 것은 다음 세 조건이 모두 성립함을 뜻한다.
1. $f(a)$가 정의되어 있다
2. $\lim_{x \to a} f(x)$가 존재한다
3. $\lim_{x \to a} f(x) = f(a)$

$f$가 $[a, b]$의 모든 점에서 연속이면 **구간에서 연속**이라 한다. $f$가 $[a, b]$에서 연속이고 $(a, b)$에서 미분가능한 상황이 많은 정리들의 전제 조건이 된다.

**극한의 대수적 성질 (algebraic limit laws):** $\lim_{x \to a} f(x) = L$, $\lim_{x \to a} g(x) = M$일 때 다음이 성립한다.

1. **상수배:** $\lim_{x \to a} [c f(x)] = cL$
2. **합/차:** $\lim_{x \to a} [f(x) \pm g(x)] = L \pm M$
3. **곱:** $\lim_{x \to a} [f(x)g(x)] = LM$
4. **몫:** $\lim_{x \to a} [f(x)/g(x)] = L/M$ (단, $M \neq 0$)
5. **거듭제곱:** $\lim_{x \to a} [f(x)]^n = L^n$ ($n$은 양의 정수)

**조임 정리(Squeeze Theorem):** $x = a$ 근방에서(단 $a$ 제외) $g(x) \leq f(x) \leq h(x)$이고 $\lim_{x \to a} g(x) = \lim_{x \to a} h(x) = L$이면 $\lim_{x \to a} f(x) = L$이다.

**도함수(derivative):** 함수 $f: \mathbb{R} \to \mathbb{R}$의 $x = a$에서의 도함수는 다음 극한이 존재할 때 정의된다.

$$f'(a) = \lim_{h \to 0} \frac{f(a+h) - f(a)}{h}$$

동등한 표기로 $f'(a) = \lim_{x \to a} \frac{f(x) - f(a)}{x - a}$가 있다. 도함수 자체도 함수이며, $f': x \mapsto f'(x)$로 표기한다. 다른 표기법으로는 $\frac{df}{dx}$(라이프니츠 표기법, Leibniz notation), $\dot{f}$(뉴턴 표기법, Newton notation)가 있다.

**미분가능(differentiable):** $f$가 $x = a$에서 미분가능하다는 것은 위 극한이 유한한 값으로 존재함을 뜻한다. $f$가 열린구간 $(a, b)$의 모든 점에서 미분가능하면 $(a, b)$에서 미분가능하다고 한다.

**좌미분계수와 우미분계수(left and right derivatives):**

$$f'_-(a) = \lim_{h \to 0^-} \frac{f(a+h) - f(a)}{h}, \qquad f'_+(a) = \lim_{h \to 0^+} \frac{f(a+h) - f(a)}{h}$$

도함수가 존재할 필요충분조건은 좌미분계수와 우미분계수가 모두 존재하고 같을 것이다.

**고계 도함수(higher-order derivatives):** $f'(x)$의 도함수를 $f''(x)$(2계 도함수, second derivative), 일반적으로 $f^{(n)}(x)$(n계 도함수, nth derivative)로 표기한다. 2계 도함수는 곡률(curvature)과 볼록성(convexity)을 나타낸다.

## 주요 정리와 증명

### 정리 1: 극한의 유일성 (Uniqueness of Limits)

$\lim_{x \to a} f(x) = L$이고 $\lim_{x \to a} f(x) = M$이면 $L = M$이다.

**증명:** 귀류법(proof by contradiction)으로 증명한다. $L \neq M$이라 가정하자. $\epsilon = \frac{|L - M|}{2} > 0$이라 두자.

극한 정의에 의해 $\delta_1 > 0$이 존재하여 $0 < |x - a| < \delta_1$이면 $|f(x) - L| < \epsilon$이다. 또한 $\delta_2 > 0$이 존재하여 $0 < |x - a| < \delta_2$이면 $|f(x) - M| < \epsilon$이다.

$\delta = \min(\delta_1, \delta_2)$라 두고 $0 < |x - a| < \delta$인 $x$를 선택하면 다음이 성립한다.

$$|L - M| = |(L - f(x)) + (f(x) - M)| \leq |f(x) - L| + |f(x) - M| < \epsilon + \epsilon = 2\epsilon = |L - M|$$

이는 $|L - M| < |L - M|$이 되어 모순이다. 따라서 $L = M$이어야 한다.

### 정리 2: 미분가능하면 연속이다 (Differentiability Implies Continuity)

$f$가 $x = a$에서 미분가능하면 $f$는 $x = a$에서 연속이다.

**증명:** $f$가 $x = a$에서 미분가능하므로 $f'(a) = \lim_{h \to 0} \frac{f(a+h) - f(a)}{h}$가 유한하게 존재한다. 이제 $h \to 0$일 때 $f(a+h) - f(a)$의 극한을 계산하자.

$$\lim_{h \to 0} [f(a+h) - f(a)] = \lim_{h \to 0} \frac{f(a+h) - f(a)}{h} \cdot h = \lim_{h \to 0} \frac{f(a+h) - f(a)}{h} \cdot \lim_{h \to 0} h = f'(a) \cdot 0 = 0$$

따라서 $\lim_{h \to 0} f(a+h) = f(a)$, 즉 $\lim_{x \to a} f(x) = f(a)$이므로 $f$는 $x = a$에서 연속이다.

**역은 성립하지 않는다:** $f(x) = |x|$는 $x = 0$에서 연속이지만 $f'(0)$은 존재하지 않는다. 좌미분계수 $\lim_{h \to 0^-} \frac{|h|}{h} = -1$과 우미분계수 $\lim_{h \to 0^+} \frac{|h|}{h} = 1$이 다르기 때문이다.

### 정리 3: 중간값 정리 (Intermediate Value Theorem, IVT)

$f$가 닫힌구간 $[a, b]$에서 연속이고 $f(a) \neq f(b)$일 때, $f(a)$와 $f(b)$ 사이의 임의의 값 $k$에 대해 $f(c) = k$인 $c \in (a, b)$가 존재한다.

**증명:** 일반성을 잃지 않고 $f(a) < k < f(b)$라 하자. 집합 $S = \{x \in [a, b] \mid f(x) \leq k\}$를 정의한다. $S$는 공집합이 아니고($a \in S$) 위로 유계이므로(bounded above by $b$), 실수의 완비성 공리(completeness axiom)에 의해 $S$의 최소상계( supremum) $c = \sup S$가 존재한다.

$f$의 연속성을 이용해 $f(c) = k$임을 보인다. $f(c) < k$이면 $c < b$이고 $c$ 근방에서 $f(x) < k$인 구간이 존재하여 $c$가 최소상계라는 사실과 모순된다. $f(c) > k$이면 $c > a$이고 $c$ 근방에서 $f(x) > k$인 구간이 존재하여 $c$보다 작은 상계가 존재하게 된다. 따라서 $f(c) = k$이다.

IVT는 연속함수의 중요한 성질로, 방정식의 실근 존재 증명, 고정점 정리(fixed point theorem) 등에 활용된다.

### 정리 4: 평균값 정리 (Mean Value Theorem, MVT)

$f$가 $[a, b]$에서 연속이고 $(a, b)$에서 미분가능하면, $f'(c) = \frac{f(b) - f(a)}{b - a}$를 만족하는 $c \in (a, b)$가 존재한다.

먼저 롤 정리(Rolle's theorem)를 증명한 후 MVT를 유도한다.

**롤 정리:** $f$가 $[a, b]$에서 연속이고 $(a, b)$에서 미분가능하며 $f(a) = f(b)$이면 $f'(c) = 0$인 $c \in (a, b)$가 존재한다.

**증명 (롤 정리):** $f$가 $[a, b]$에서 연속이므로 최대최소 정리(Extreme Value Theorem)에 의해 최댓값 $M$과 최솟값 $m$을 갖는다. $f(a) = f(b)$이므로 두 가지 경우가 있다.

- $M = m$이면 $f$는 상수함수이므로 모든 $c \in (a, b)$에서 $f'(c) = 0$이다.
- $M > m$이면 $M$ 또는 $m$이 내부점에서 달성된다(양 끝점에서 동시에 달성될 수는 없는데, $f(a) = f(b)$이므로 두 값이 모두 끝점에서 달성되면 $M = m$이 되기 때문이다). 내부점 $c$에서 최댓값(또는 최솟값)이 달성된다고 하자. 페르마 정리(Fermat's theorem)에 의해 $f'(c) = 0$이다.

**증명 (평균값 정리):** 함수 $g(x) = f(x) - \frac{f(b) - f(a)}{b - a}(x - a)$를 정의하자. $g$는 $f$가 연속이므로 연속이고, 미분가능하므로 미분가능하다. 직접 계산하면 $g(a) = f(a)$, $g(b) = f(b) - (f(b) - f(a)) = f(a)$이므로 $g(a) = g(b)$이다.

롤 정리를 $g$에 적용하면 $g'(c) = 0$인 $c \in (a, b)$가 존재한다.

$$g'(x) = f'(x) - \frac{f(b) - f(a)}{b - a}$$

이므로 $g'(c) = 0$에서 $f'(c) = \frac{f(b) - f(a)}{b - a}$를 얻는다.

MVT는 미적분학의 가장 강력한 도구 중 하나로, 함수의 증가/감소 판정, 함수의 부등식 증명, 오차 추정 등에 광범위하게 사용된다.

### 정리 5: 최대최소 정리 (Extreme Value Theorem, EVT)

$f$가 닫힌구간 $[a, b]$에서 연속이면 $f$는 $[a, b]$에서 최댓값과 최솟값을 갖는다.

**증명 개요:** 실수의 완비성(completeness)에 기반한다. $M = \sup_{x \in [a, b]} f(x)$라 하자. $M$으로 수렴하는 수열 $\{f(x_n)\}$을 선택할 수 있다. $[a, b]$는 닫혀있으므로 $\{x_n\}$은 수렴하는 부분수열(subsequence) $\{x_{n_k}\}$를 가지며(볼차노-바이어슈트라스 정리, Bolzano-Weierstrass theorem), 그 극한 $c$는 $[a, b]$에 속한다. $f$의 연속성에 의해 $f(c) = \lim f(x_{n_k}) = M$이다. 최솟값에 대해서도 동일하게 증명된다.

EVT는 IVT 및 롤 정리와 함께 연속함수의 세 가지 기본 정리를 이룬다.

### 정리 6: 조임 정리 (Squeeze Theorem)

$x = a$ 근방(단 $a$ 제외)에서 $g(x) \leq f(x) \leq h(x)$이고 $\lim_{x \to a} g(x) = \lim_{x \to a} h(x) = L$이면 $\lim_{x \to a} f(x) = L$이다.

**증명:** 임의의 $\epsilon > 0$에 대해, $\delta_1 > 0$이 존재하여 $0 < |x - a| < \delta_1$이면 $|g(x) - L| < \epsilon$, 즉 $L - \epsilon < g(x) < L + \epsilon$이다. 또한 $\delta_2 > 0$이 존재하여 $0 < |x - a| < \delta_2$이면 $|h(x) - L| < \epsilon$, 즉 $L - \epsilon < h(x) < L + \epsilon$이다.

$\delta = \min(\delta_1, \delta_2)$라 하자. $0 < |x - a| < \delta$이면 $L - \epsilon < g(x) \leq f(x) \leq h(x) < L + \epsilon$이므로 $|f(x) - L| < \epsilon$이다. 따라서 $\lim_{x \to a} f(x) = L$이다.

조임 정리는 직접 계산하기 어려운 극한을 다룰 때 유용하다. 특히 $\lim_{x \to 0} \frac{\sin x}{x} = 1$의 증명이 대표적 예시다.

## 예제

**예제 1 ($\epsilon$-$\delta$ 증명):** $\lim_{x \to 2} (3x - 1) = 5$임을 $\epsilon$-$\delta$ 정의로 증명하라.

**풀이:** 임의의 $\epsilon > 0$에 대해, $|(3x - 1) - 5| = |3x - 6| = 3|x - 2| < \epsilon$이 되도록 하는 $\delta$를 찾아야 한다.

$$|3x - 6| = 3|x - 2| < \epsilon \iff |x - 2| < \frac{\epsilon}{3}$$

따라서 $\delta = \frac{\epsilon}{3}$으로 선택하면, $0 < |x - 2| < \delta$일 때

$$|(3x - 1) - 5| = 3|x - 2| < 3 \cdot \frac{\epsilon}{3} = \epsilon$$

이 성립한다. $\square$

**예제 2 (도함수를 정의로 계산):** $f(x) = x^2$의 도함수를 극한 정의로 구하라.

**풀이:** 도함수의 정의에 의해

$$f'(x) = \lim_{h \to 0} \frac{(x+h)^2 - x^2}{h} = \lim_{h \to 0} \frac{x^2 + 2xh + h^2 - x^2}{h} = \lim_{h \to 0} \frac{2xh + h^2}{h} = \lim_{h \to 0} (2x + h) = 2x$$

따라서 $f'(x) = 2x$이다. 특히 $x = 3$에서의 도함수는 $f'(3) = 6$이다.

**예제 3 (미분가능하지만 도함수가 불연속인 함수):** 함수

$$f(x) = \begin{cases} x^2 \sin\left(\frac{1}{x}\right), & x \neq 0 \\ 0, & x = 0 \end{cases}$$

을 고려하자. $x = 0$에서의 미분가능성과 도함수의 연속성을 조사하라.

**풀이:** $x = 0$에서 도함수를 극한 정의로 계산한다.

$$f'(0) = \lim_{h \to 0} \frac{h^2 \sin(1/h) - 0}{h} = \lim_{h \to 0} h \sin\left(\frac{1}{h}\right)$$

$|\sin(1/h)| \leq 1$이므로 $|h \sin(1/h)| \leq |h|$이고, 조임 정리(squeeze theorem)에 의해 $\lim_{h \to 0} h \sin(1/h) = 0$이다. 따라서 $f'(0) = 0$이고 $f$는 $x = 0$에서 미분가능하다.

$x \neq 0$에서는 기본 미분법으로

$$f'(x) = 2x \sin\left(\frac{1}{x}\right) - \cos\left(\frac{1}{x}\right)$$

이다. $\lim_{x \to 0} \cos(1/x)$는 진동하며 존재하지 않는다. 따라서 $\lim_{x \to 0} f'(x)$가 존재하지 않는 반면 $f'(0) = 0$이므로, $f'$는 $x = 0$에서 불연속이다. 이 예는 미분가능성이 도함수의 연속성을 보장하지 않음을 보여준다.

**예제 4 (조임 정리 활용):** $\lim_{x \to 0} x \sin\left(\frac{1}{x}\right) = 0$임을 조임 정리로 증명하라.

**풀이:** 모든 $x \neq 0$에 대해 $|\sin(1/x)| \leq 1$이므로

$$-|x| \leq x \sin\left(\frac{1}{x}\right) \leq |x|$$

이다. $\lim_{x \to 0} (-|x|) = 0$이고 $\lim_{x \to 0} |x| = 0$이므로 조임 정리에 의해

$$\lim_{x \to 0} x \sin\left(\frac{1}{x}\right) = 0$$

이다. 이 극한은 $\frac{0}{0}$ 꼴의 부정형(indeterminate form)이 아니라, 유계 함수와 0으로 수렴하는 함수의 곱의 극한이 0이 되는 전형적인 예시다.

**예제 5 (IVT로 방정식의 실근 존재 증명):** 방정식 $x^3 - x - 1 = 0$이 $(1, 2)$에 실근을 가짐을 보여라.

**풀이:** $f(x) = x^3 - x - 1$은 다항함수이므로 모든 점에서 연속이다.

$f(1) = 1 - 1 - 1 = -1 < 0$, $f(2) = 8 - 2 - 1 = 5 > 0$

IVT에 의해 $f(1) < 0 < f(2)$이므로 $f(c) = 0$인 $c \in (1, 2)$가 존재한다. $f$는 증가함수이므로 이 실근은 유일하다.

**예제 6 (MVT로 부등식 증명):** $a < b$일 때 $|\sin b - \sin a| \leq |b - a|$임을 평균값 정리로 증명하라.

**풀이:** $f(x) = \sin x$는 $[a, b]$에서 연속이고 $(a, b)$에서 미분가능하다. MVT에 의해

$$\frac{\sin b - \sin a}{b - a} = \sin' c = \cos c$$

인 $c \in (a, b)$가 존재한다. 양변에 절댓값을 취하면

$$\frac{|\sin b - \sin a|}{|b - a|} = |\cos c| \leq 1$$

따라서 $|\sin b - \sin a| \leq |b - a|$가 성립한다. 이는 사인 함수가 립시츠 연속(Lipschitz continuous)임을 보여준다.

## 연결

- **[함수](functions.html)** : 극한과 도함수는 함수의 개념 위에 세워진다. 정의역·공역·치역, 합성함수·역함수를 이해하는 것이 선행되어야 한다.
- **[미분 법칙·연쇄법칙](differentiation-rules.html)** : 도함수의 계산 법칙(선형성, 곱 법칙, 연쇄법칙)을 본격적으로 다루며, 극한 정의 없이 효율적으로 미분하는 방법을 배운다.
- **[편도함수·기울기 벡터](partial-derivatives.html)** : 극한과 도함수 개념을 다변수 함수로 확장하여 각 변수 방향의 변화율을 다룬다.
