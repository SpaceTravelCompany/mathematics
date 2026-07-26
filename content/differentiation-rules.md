---
title: 미분 법칙·연쇄법칙
slug: differentiation-rules
---

## 직관적 설명

미분 법칙(differentiation rules)은 도함수의 극한 정의를 매번 계산하지 않고도 효율적으로 미분할 수 있는 도구들이다. **선형성(linearity)** 은 "각각 미분해서 더한다"는 뜻이다. **곱 법칙(product rule)** 은 "첫 번째 미분 × 두 번째 + 첫 번째 × 두 번째 미분"으로 기억된다. **연쇄법칙(chain rule)** 은 합성함수의 미분으로, "바깥 함수 미분 × 안 함수 미분"이다.

연쇄법칙의 직관: $y = g(u)$, $u = f(x)$일 때, $\frac{dy}{dx} = \frac{dy}{du} \cdot \frac{du}{dx}$이다. 이는 "변화가 전달되는 비율의 곱"으로 해석할 수 있다. $x$가 변할 때 $u$가 변하고, 그 변화가 $y$에 전달되며, 전달 비율이 곱해진다. 이 개념은 다변수 함수의 연쇄법칙, 역전파(backpropagation), 미분방정식의 변수분리 등으로 확장된다.

**역함수 미분법(inverse function rule)** 은 연쇄법칙의 직접적인 결과로, 역함수의 도함수를 원래 함수의 도함수로 표현한다.

## 정의

**선형성(linearity of differentiation):** $\alpha, \beta \in \mathbb{R}$이고 $f, g$가 미분가능할 때,

$$(\alpha f + \beta g)' = \alpha f' + \beta g'$$

**곱 법칙(product rule):**

$$(fg)' = f'g + fg'$$

**몫 법칙(quotient rule):** $g(x) \neq 0$에서

$$\left(\frac{f}{g}\right)' = \frac{f'g - fg'}{g^2}$$

**연쇄법칙(chain rule):** $f$가 $x$에서 미분가능하고 $g$가 $f(x)$에서 미분가능할 때,

$$(g \circ f)'(x) = g'(f(x)) \cdot f'(x)$$

라이프니츠 표기법으로는 $z = g(y)$, $y = f(x)$일 때 $\frac{dz}{dx} = \frac{dz}{dy} \cdot \frac{dy}{dx}$이다.

**역함수 미분법(inverse function rule):** $f$가 $x$에서 미분가능하고 $f'(x) \neq 0$이며 $f$가 $x$ 근방에서 전단사이면,

$$(f^{-1})'(y) = \frac{1}{f'(f^{-1}(y))}$$

여기서 $y = f(x)$이다. 동등하게 $(f^{-1})'(f(x)) = \frac{1}{f'(x)}$로도 쓸 수 있다.

**일반 거듭제곱 법칙(General Power Rule):** $f(x) = x^r$ ($r \in \mathbb{R}$)에 대해

$$\frac{d}{dx} x^r = r x^{r-1}$$

이는 자연수 지수에서 시작하여 정수, 유리수, 실수 지수로 점진적으로 확장된다.

**음함수 미분법(Implicit Differentiation):** $y$가 $x$의 함수로 $F(x, y) = 0$ 꼴로 주어졌을 때, 양변을 $x$에 대해 미분하고 $y'$에 대해 푼다. 연쇄법칙이 핵심 도구다: $\frac{d}{dx} f(y) = f'(y) \cdot \frac{dy}{dx}$.

## 주요 정리와 증명

### 정리 1: 곱 법칙 (Product Rule)

$f$와 $g$가 $x$에서 미분가능하면 $fg$도 $x$에서 미분가능하고 $(fg)'(x) = f'(x)g(x) + f(x)g'(x)$이다.

**증명:** 도함수의 정의를 $fg$에 직접 적용한다.

$$(fg)'(x) = \lim_{h \to 0} \frac{f(x+h)g(x+h) - f(x)g(x)}{h}$$

분자에 $f(x+h)g(x) - f(x+h)g(x) = 0$을 더하고 뺀다(일종의 "telescoping" 트릭).

$$= \lim_{h \to 0} \frac{f(x+h)g(x+h) - f(x+h)g(x) + f(x+h)g(x) - f(x)g(x)}{h}$$

$$= \lim_{h \to 0} \left[ f(x+h) \cdot \frac{g(x+h) - g(x)}{h} + \frac{f(x+h) - f(x)}{h} \cdot g(x) \right]$$

$f$가 $x$에서 미분가능하므로 연속이고 따라서 $\lim_{h \to 0} f(x+h) = f(x)$이다. 극한의 성질을 적용하면

$$(fg)'(x) = f(x) \cdot g'(x) + f'(x) \cdot g(x)$$

이로써 곱 법칙이 증명되었다. $\Delta$ 표기법으로 표현하면 $\Delta(fg) = f\Delta g + g\Delta f + \Delta f \Delta g$이며, $h \to 0$에서 $\Delta f \Delta g$ 항은 $h$보다 고차의 무한소가 되어 사라진다.

### 정리 2: 연쇄법칙 (Chain Rule)

$f$가 $x = a$에서 미분가능하고 $g$가 $b = f(a)$에서 미분가능하면 $g \circ f$는 $a$에서 미분가능하고 $(g \circ f)'(a) = g'(f(a)) f'(a)$이다.

**증명:** $h \neq 0$에 대해 차분몫(difference quotient)을 고려하자.

$$\frac{g(f(a+h)) - g(f(a))}{h}$$

목표는 이 식이 $h \to 0$일 때 $g'(f(a)) f'(a)$로 수렴함을 보이는 것이다.

$f(a+h) = f(a) + \Delta$라 두면 $\Delta = f(a+h) - f(a)$이고, $f$의 연속성에 의해 $h \to 0$일 때 $\Delta \to 0$이다. 그러면

$$\frac{g(f(a+h)) - g(f(a))}{h} = \frac{g(f(a) + \Delta) - g(f(a))}{h}$$

$\Delta$가 0이 아닌 경우와 0인 경우를 나누어야 한다.

**Case 1:** $\Delta \neq 0$인 $h$가 충분히 작은 범위에 존재하는 경우.

$$\frac{g(f(a+h)) - g(f(a))}{h} = \frac{g(f(a) + \Delta) - g(f(a))}{\Delta} \cdot \frac{\Delta}{h} = \frac{g(f(a) + \Delta) - g(f(a))}{\Delta} \cdot \frac{f(a+h) - f(a)}{h}$$

$h \to 0$일 때 $\frac{f(a+h) - f(a)}{h} \to f'(a)$이고, $\Delta \to 0$이므로 $\frac{g(f(a) + \Delta) - g(f(a))}{\Delta} \to g'(f(a))$이다. 따라서 곱의 극한은 $g'(f(a)) f'(a)$로 수렴한다.

**Case 2:** 임의의 작은 $h \neq 0$에 대해 $\Delta = 0$인 경우가 무한히 존재하는 경우. 이 경우 차분몫은 $\frac{g(f(a)) - g(f(a))}{h} = 0$이고 $f'(a) = 0$임을 보일 수 있다. 따라서 $g'(f(a)) f'(a) = 0$이므로 양변이 일치한다.

두 경우 모두 극한값이 $g'(f(a)) f'(a)$임이 확인된다. $\square$

**참고:** 위 증명에서 $\Delta = 0$인 경우를 따로 처리하지 않고 세심하게 구성한 증명이 표준적이다. 더 엄밀한 증명은 함수

$$\phi(t) = \begin{cases} \frac{g(t) - g(f(a))}{t - f(a)}, & t \neq f(a) \\ g'(f(a)), & t = f(a) \end{cases}$$

을 도입하여 $\frac{g(f(a+h)) - g(f(a))}{h} = \phi(f(a+h)) \cdot \frac{f(a+h) - f(a)}{h}$를 이용한다.

### 정리 3: 역함수 미분법 (Inverse Function Rule)

$f$가 $x$ 근방에서 미분가능하고 $f'(x) \neq 0$이며 연속인 역함수 $f^{-1}$을 가지면, $y = f(x)$에서 $f^{-1}$은 미분가능하고

$$(f^{-1})'(y) = \frac{1}{f'(f^{-1}(y))}$$

이다.

**증명:** $f(f^{-1}(y)) = y$의 양변을 $y$에 대해 미분한다. 좌변은 연쇄법칙에 의해 $f'(f^{-1}(y)) \cdot (f^{-1})'(y)$이고, 우변은 1이다. 따라서

$$f'(f^{-1}(y)) \cdot (f^{-1})'(y) = 1$$

$f'(f^{-1}(y)) \neq 0$이므로 양변을 나눠 원하는 결과를 얻는다. 이 증명은 $f^{-1}$의 미분가능성이 전제되어야 하지만, 실제로는 $f' \neq 0$과 $f$의 연속성이 $f^{-1}$의 미분가능성을 보장한다(역함수 정리, Inverse Function Theorem).

**기하학적 의미:** $y = f(x)$의 그래프와 $x = f^{-1}(y)$의 그래프는 직선 $y = x$에 대해 대칭이다. 접선의 기울기는 역수 관계에 있다.

$$(f^{-1})'(y_0) = \frac{1}{f'(x_0)}$$

여기서 $y_0 = f(x_0)$이다.

### 정리 4: 일반화된 곱 법칙 (Generalized Product Rule)

$n$개의 함수 $f_1, f_2, \ldots, f_n$이 모두 미분가능할 때

$$(f_1 f_2 \cdots f_n)' = f_1' f_2 \cdots f_n + f_1 f_2' \cdots f_n + \cdots + f_1 f_2 \cdots f_n'$$

**증명:** 수학적 귀납법(mathematical induction)으로 증명한다. $n = 2$일 때는 곱 법칙 자체다. $n = k$일 때 성립한다고 가정하고 $n = k+1$일 때를 보인다.

$$(f_1 \cdots f_k f_{k+1})' = ((f_1 \cdots f_k) \cdot f_{k+1})' = (f_1 \cdots f_k)' f_{k+1} + (f_1 \cdots f_k) f_{k+1}'$$

귀납 가정을 $(f_1 \cdots f_k)'$에 적용하면

$$= (f_1' f_2 \cdots f_k + \cdots + f_1 \cdots f_{k-1} f_k') f_{k+1} + f_1 \cdots f_k f_{k+1}'$$

$$= f_1' f_2 \cdots f_k f_{k+1} + \cdots + f_1 \cdots f_{k-1} f_k' f_{k+1} + f_1 \cdots f_k f_{k+1}'$$

따라서 $n = k+1$에서도 성립한다. $\square$

### 정리 5: 몫 법칙의 곱 법칙으로부터의 유도

몫 법칙 $\left(\frac{f}{g}\right)' = \frac{f'g - fg'}{g^2}$은 곱 법칙과 연쇄법칙으로부터 유도될 수 있다.

**증명:** $\frac{f}{g} = f \cdot g^{-1}$로 쓰고 곱 법칙을 적용한다.

$$\left(\frac{f}{g}\right)' = f' \cdot g^{-1} + f \cdot (g^{-1})'$$

$g^{-1}$의 미분은 연쇄법칙으로 계산한다. $h(x) = 1/x$라 하면 $h(g(x)) = g(x)^{-1}$이고 $h'(x) = -1/x^2$이므로

$$(g^{-1})' = h'(g(x)) \cdot g'(x) = -\frac{1}{g(x)^2} \cdot g'(x)$$

따라서

$$\left(\frac{f}{g}\right)' = \frac{f'}{g} - \frac{fg'}{g^2} = \frac{f'g - fg'}{g^2}$$

가 성립한다. 이 유도는 몫 법칙을 별도로 외울 필요 없이 곱 법칙과 연쇄법칙만으로 처리할 수 있음을 보여준다.

## 예제

**예제 1 (연쇄법칙):** $\frac{d}{dx} \sin(x^2)$를 구하라.

**풀이:** $f(x) = x^2$, $g(u) = \sin u$라 하면 $g \circ f (x) = \sin(x^2)$이다. 연쇄법칙에 의해

$$\frac{d}{dx} \sin(x^2) = \cos(x^2) \cdot \frac{d}{dx}(x^2) = \cos(x^2) \cdot 2x = 2x \cos(x^2)$$

일반화: $\frac{d}{dx} \sin(g(x)) = g'(x) \cos(g(x))$이다.

**예제 2 (연쇄법칙 반복 적용):** $\frac{d}{dx} e^{\sin x}$를 구하라.

**풀이:** 세 함수의 합성으로 본다: $x \mapsto \sin x \mapsto e^{\sin x}$.

$$\frac{d}{dx} e^{\sin x} = e^{\sin x} \cdot \frac{d}{dx}(\sin x) = e^{\sin x} \cdot \cos x = \cos x \cdot e^{\sin x}$$

곱 법칙과 연쇄법칙이 결합된 문제: $\frac{d}{dx} (\sin x \cdot e^{x^2})$는

$$\cos x \cdot e^{x^2} + \sin x \cdot e^{x^2} \cdot 2x = e^{x^2}(\cos x + 2x \sin x)$$

**예제 3 (역함수 미분법으로 $\ln x$ 미분 유도):** $\frac{d}{dx} \ln x = \frac{1}{x}$임을 역함수 미분법으로 유도하라.

**풀이:** $\ln x$는 $e^x$의 역함수이다. 즉 $f(x) = e^x$라 하면 $f^{-1}(y) = \ln y$이다. $f'(x) = e^x$이므로, 역함수 미분법에 의해

$$(f^{-1})'(y) = \frac{1}{f'(f^{-1}(y))} = \frac{1}{e^{\ln y}} = \frac{1}{y}$$

변수명을 $x$로 바꾸면 $\frac{d}{dx} \ln x = \frac{1}{x}$이다. 단, $x > 0$에서 성립한다.

**예제 4 (몫 법칙):** $f(x) = \frac{x^2}{x^3 + 1}$의 도함수를 구하라.

**풀이:** 몫 법칙을 적용한다.

$$f'(x) = \frac{(2x)(x^3 + 1) - (x^2)(3x^2)}{(x^3 + 1)^2} = \frac{2x^4 + 2x - 3x^4}{(x^3 + 1)^2} = \frac{-x^4 + 2x}{(x^3 + 1)^2} = \frac{x(2 - x^3)}{(x^3 + 1)^2}$$

**예제 5 (곱 법칙과 연쇄법칙의 결합):** $f(x) = (x^2 + 1)^3 (2x - 1)^4$의 도함수를 구하라.

**풀이:** $f(x) = u(x)v(x)$로 보고 곱 법칙과 연쇄법칙을 적용한다.

$$f'(x) = 3(x^2 + 1)^2 \cdot 2x \cdot (2x - 1)^4 + (x^2 + 1)^3 \cdot 4(2x - 1)^3 \cdot 2$$

$$= 6x(x^2 + 1)^2 (2x - 1)^4 + 8(x^2 + 1)^3 (2x - 1)^3$$

$$= 2(x^2 + 1)^2 (2x - 1)^3 [3x(2x - 1) + 4(x^2 + 1)]$$

$$= 2(x^2 + 1)^2 (2x - 1)^3 (6x^2 - 3x + 4x^2 + 4)$$

$$= 2(x^2 + 1)^2 (2x - 1)^3 (10x^2 - 3x + 4)$$

**예제 6 (음함수 미분, implicit differentiation):** $x^2 + y^2 = 25$가 정의하는 곡선 위의 점 $(3, 4)$에서의 접선의 기울기를 구하라.

**풀이:** $y$를 $x$의 함수로 보고 양변을 $x$에 대해 미분한다.

$$\frac{d}{dx}(x^2) + \frac{d}{dx}(y^2) = \frac{d}{dx}(25) \;\Rightarrow\; 2x + 2y \frac{dy}{dx} = 0$$

$y'$에 대해 정리하면 $\frac{dy}{dx} = -\frac{x}{y}$이다. 점 $(3, 4)$에서의 기울기는 $-\frac{3}{4}$이다.

**예제 7 (음함수 미분과 연쇄법칙의 심화):** $\sin(xy) = x$의 $\frac{dy}{dx}$를 구하라.

**풀이:** 양변을 $x$에 대해 미분한다. 좌변은 연쇄법칙을 적용한다.

$$\cos(xy) \cdot \frac{d}{dx}(xy) = 1 \;\Rightarrow\; \cos(xy) \cdot \left( y + x \frac{dy}{dx} \right) = 1$$

$y + x y' = \frac{1}{\cos(xy)} = \sec(xy)$이므로

$$y' = \frac{\sec(xy) - y}{x}$$

**예제 8 (연쇄법칙의 다중 적용):** $f(x) = \sin^3(2x)$의 도함수를 구하라.

**풀이:** $f(x) = [\sin(2x)]^3$으로 보고 연쇄법칙을 세 번 적용한다(바깥: $u^3$, 중간: $\sin u$, 안: $2x$).

$$f'(x) = 3[\sin(2x)]^2 \cdot \cos(2x) \cdot 2 = 6 \sin^2(2x) \cos(2x)$$

**예제 9 (일반 거듭제곱 법칙의 활용):** $\frac{d}{dx} \sqrt{x^2 + 1}$을 구하라.

**풀이:** $\sqrt{x^2 + 1} = (x^2 + 1)^{1/2}$이므로 일반 거듭제곱 법칙과 연쇄법칙을 적용한다.

$$\frac{d}{dx} (x^2 + 1)^{1/2} = \frac{1}{2}(x^2 + 1)^{-1/2} \cdot 2x = \frac{x}{\sqrt{x^2 + 1}}$$

## 연결

- **[극한·연속·도함수](topics/limits-derivatives.html)** : 모든 미분 법칙은 극한 정의에서 출발한다. 도함수의 정의와 기본 성질(미분가능성, 연속성)이 선행되어야 한다.
- **[지수·로그 함수의 미분](topics/exp-log-calculus.html)** : $e^x$의 미분이 자기 자신임은 연쇄법칙과 함께 지수함수 미분의 핵심이 된다. 역함수 미분법으로 $\ln x$의 미분을 유도한다.
- **[다변수 연쇄법칙](topics/multivar-chain-rule.html)** : 연쇄법칙을 다변수 함수로 확장하면 편미분의 행렬곱(야코비안 곱)으로 표현되며, 이는 인공 신경망의 역전파 알고리즘의 수학적 기초다.
