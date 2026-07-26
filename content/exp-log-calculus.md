---
title: 지수·로그 함수의 미분
slug: exp-log-calculus
---

## 직관적 설명

지수함수 $e^x$는 미적분학에서 가장 특별한 함수 중 하나다. **미분해도 자기 자신**이기 때문이다. 즉, $e^x$의 변화율이 현재의 값과 항상 같다. 이것이 의미하는 바: "성장률이 현재 값에 비례한다"는 것이다. 인구 성장, 복리 이자, 방사능 붕괴, 냉각 과정 등 자연과 사회의 수많은 현상이 이 성질을 따른다.

자연로그(natural logarithm) $\ln x$는 $e^x$의 역함수이며, 그 미분은 $\frac{1}{x}$이다. $\ln x$는 적분 $\int_1^x \frac{1}{t}\,dt$로 정의할 수도 있는데, 이는 $1/x$의 적분을 자연스럽게 로그로 연결해준다.

지수함수와 로그함수는 미분방정식 $\frac{dy}{dt} = ky$의 해로서, 지수성장(exponential growth)과 지수붕괴(exponential decay)의 모델을 제공한다. $k > 0$이면 성장, $k < 0$이면 붕괴다.

## 정의

**자연상수 $e$:**

$$e = \lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n \approx 2.71828\ldots$$

동등하게 $e = \sum_{n=0}^{\infty} \frac{1}{n!}$(테일러 급수)로도 정의된다.

**지수함수 $\exp(x) = e^x$:** 다음 미분방정식의 초기값 문제(initial value problem)의 유일한 해로 정의할 수 있다.

$$f'(x) = f(x), \quad f(0) = 1$$

이 정의는 $e^x$의 핵심 성질을 가장 직접적으로 드러낸다.

**자연로그(natural logarithm):** $x > 0$에 대해 $\ln x$는 $e^{\ln x} = x$를 만족하는 수, 즉 $e^x$의 역함수로 정의된다. 또는 적분으로도 정의할 수 있다.

$$\ln x = \int_1^x \frac{1}{t}\,dt,\quad x > 0$$

두 정의는 동등함이 증명된다.

**일반 지수함수(general exponential):** $a > 0$, $a \neq 1$에 대해

$$a^x = e^{x \ln a}$$

로 정의된다. 이 정의는 지수법칙을 보존하면서 실수 전체로 $a^x$를 확장한다.

**일반 로그함수(general logarithm):**

$$\log_a x = \frac{\ln x}{\ln a},\quad x > 0$$

**지수성장 모델(exponential growth model):**

$$\frac{dy}{dt} = ky \quad\Rightarrow\quad y(t) = Ce^{kt}$$

여기서 $C = y(0)$은 초기값, $k$는 성장률(growth rate)이다.

**쌍곡선 함수(hyperbolic functions):** 지수함수의 특별한 조합으로 정의되는 함수들로, 삼각함수와 유사한 성질을 가진다.

$$\sinh x = \frac{e^x - e^{-x}}{2}, \qquad \cosh x = \frac{e^x + e^{-x}}{2}$$

$$\tanh x = \frac{\sinh x}{\cosh x} = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

쌍곡선 함수의 미분:
- $\frac{d}{dx} \sinh x = \cosh x$
- $\frac{d}{dx} \cosh x = \sinh x$
- $\frac{d}{dx} \tanh x = \text{sech}^2 x$

쌍곡선 함수는 현수선(catenary), 상대론적 속도 덧셈, 변분법의 브라키스토크론(brachistochrone) 문제 등 다양한 물리적 상황에 자연스럽게 등장한다.

## 주요 정리와 증명

### 정리 1: $\frac{d}{dx} e^x = e^x$

**증명 (극한 정의 사용):** 도함수의 정의에 의해

$$\frac{d}{dx} e^x = \lim_{h \to 0} \frac{e^{x+h} - e^x}{h} = \lim_{h \to 0} \frac{e^x e^h - e^x}{h} = e^x \lim_{h \to 0} \frac{e^h - 1}{h}$$

따라서 $\lim_{h \to 0} \frac{e^h - 1}{h} = 1$임을 보이면 된다.

$e$의 정의 $e = \lim_{n \to \infty} (1 + 1/n)^n$에서 $h = 1/n$으로 치환하면, $h \to 0$일 때 $n \to \infty$이므로

$$e = \lim_{h \to 0} (1 + h)^{1/h}$$

양변에 자연로그를 취하면 $\lim_{h \to 0} \frac{\ln(1+h)}{h} = 1$이다. 역함수 관계를 이용하여 $t = \ln(1+h)$, 즉 $h = e^t - 1$로 치환하면 $h \to 0$일 때 $t \to 0$이므로

$$\lim_{t \to 0} \frac{t}{e^t - 1} = 1 \quad\Longrightarrow\quad \lim_{t \to 0} \frac{e^t - 1}{t} = 1$$

따라서 $\frac{d}{dx} e^x = e^x \cdot 1 = e^x$이다. $\square$

**증명 (미분방정식 정의 사용):** $f(x) = e^x$가 $f' = f$, $f(0) = 1$의 해로 정의되었다면, 도함수는 정의에 의해 자명하게 $f$ 자신이다. 이 정의는 $e^x$의 본질을 가장 깔끔하게 포착한다.

### 정리 2: $\frac{d}{dx} \ln x = \frac{1}{x}$

**증명:** $\ln x$는 $e^x$의 역함수이므로 역함수 미분법(inverse function rule)을 적용한다. $f(x) = e^x$라 하면 $f^{-1}(y) = \ln y$이고 $f'(x) = e^x$이다. 따라서

$$(f^{-1})'(y) = \frac{1}{f'(f^{-1}(y))} = \frac{1}{e^{\ln y}} = \frac{1}{y}$$

변수명을 바꿔 $\frac{d}{dx} \ln x = \frac{1}{x}$ ($x > 0$)이다. $\square$

**증명 (적분 정의 사용):** $\ln x = \int_1^x \frac{1}{t}\,dt$로 정의했다면, 미적분학의 기본정리(Fundamental Theorem of Calculus)에 의해 곧바로 $\frac{d}{dx} \ln x = \frac{1}{x}$이다.

### 정리 3: 미분방정식 $f' = f$, $f(0) = 1$의 해 유일성

$f'(x) = f(x)$, $f(0) = 1$을 만족하는 함수는 유일하다.

**증명:** 두 함수 $f_1$, $f_2$가 모두 주어진 미분방정식과 초기조건을 만족한다고 가정하자. $g(x) = f_1(x) e^{-x}$를 정의하고 미분한다.

$$g'(x) = f_1'(x) e^{-x} + f_1(x) \cdot (-e^{-x}) = f_1(x) e^{-x} - f_1(x) e^{-x} = 0$$

따라서 $g$는 상수함수이다. $g(0) = f_1(0) e^0 = 1$이므로 $g(x) = 1$ for all $x$이다. 즉,

$$f_1(x) e^{-x} = 1 \quad\Longrightarrow\quad f_1(x) = e^x$$

같은 방법으로 $f_2(x) = e^x$임을 보일 수 있으므로 $f_1 = f_2$이다. $\square$

이 증명의 핵심 아이디어는 $g(x) = f(x)e^{-x}$라는 **적분 인자(integrating factor)** 를 도입하는 것이다. 이 기법은 1계 선형 미분방정식을 푸는 표준 방법이다.

### 정리 4: $\frac{d}{dx} a^x = a^x \ln a$

**증명:** $a^x = e^{x \ln a}$이므로 연쇄법칙을 적용한다.

$$\frac{d}{dx} a^x = \frac{d}{dx} e^{x \ln a} = e^{x \ln a} \cdot \ln a = a^x \ln a$$

특별히 $a = e$이면 $\ln e = 1$이므로 $\frac{d}{dx} e^x = e^x$가 되어 일관된다.

**따름정리:** $\frac{d}{dx} \log_a x = \frac{1}{x \ln a}$.

**증명:** $\log_a x = \frac{\ln x}{\ln a}$이므로

$$\frac{d}{dx} \log_a x = \frac{1}{\ln a} \cdot \frac{d}{dx} \ln x = \frac{1}{\ln a} \cdot \frac{1}{x} = \frac{1}{x \ln a}$$

여기서 $a > 0$, $a \neq 1$이고 $x > 0$이다. $\square$

## 예제

**예제 1 (지수성장 모델):** 어떤 세포 배양의 개체 수가 초기 $1000$개에서 3시간 후 $8000$개로 증가했다. 성장이 지수적이라고 가정할 때, (a) 성장률 $k$를 구하고, (b) 6시간 후의 개체 수를 예측하라.

**풀이:** (a) 지수성장 모델 $P(t) = P_0 e^{kt}$에서 $P_0 = 1000$, $P(3) = 8000$이므로

$$8000 = 1000 e^{3k} \;\Rightarrow\; 8 = e^{3k} \;\Rightarrow\; 3k = \ln 8 \;\Rightarrow\; k = \frac{\ln 8}{3} = \frac{3 \ln 2}{3} = \ln 2 \approx 0.6931$$

성장률은 약 $0.6931$ (시간당 $69.31\%$)이다.

(b) $P(6) = 1000 e^{6 \ln 2} = 1000 e^{\ln 64} = 1000 \cdot 64 = 64000$개. 즉 6시간 후에는 $64000$개가 된다.

**예제 2 (지수붕괴 모델):** 방사성 동위원소의 반감기(half-life)가 10년이다. 초기량의 $10\%$만 남는 데 걸리는 시간을 구하라.

**풀이:** $N(t) = N_0 e^{-kt}$ ($k > 0$). 반감기 조건에서 $N(10) = N_0/2$이므로

$$\frac{N_0}{2} = N_0 e^{-10k} \;\Rightarrow\; \frac{1}{2} = e^{-10k} \;\Rightarrow\; -10k = \ln(1/2) = -\ln 2 \;\Rightarrow\; k = \frac{\ln 2}{10}$$

초기량의 $10\%$가 남는 시간 $t$를 구한다.

$$0.1 N_0 = N_0 e^{-kt} \;\Rightarrow\; 0.1 = e^{-kt} \;\Rightarrow\; -kt = \ln 0.1 \;\Rightarrow\; t = -\frac{\ln 0.1}{k} = -\frac{-\ln 10}{\ln 2 / 10} = \frac{10 \ln 10}{\ln 2} \approx 33.22$$

약 33.22년 후에 초기량의 $10\%$만 남는다.

**예제 3 (로그 미분법, logarithmic differentiation):** $f(x) = x^x$ ($x > 0$)의 도함수를 구하라.

**풀이:** $x^x$는 거듭제곱 법칙($x^n$)도 지수 법칙($a^x$)도 직접 적용할 수 없는 형태다. 양변에 자연로그를 취한 후 미분한다.

$$y = x^x \;\Rightarrow\; \ln y = \ln(x^x) = x \ln x$$

양변을 $x$에 대해 미분한다. 좌변은 연쇄법칙에 의해 $\frac{1}{y} \cdot y'$, 우변은 곱 법칙에 의해 $\ln x + x \cdot \frac{1}{x} = \ln x + 1$이다.

$$\frac{y'}{y} = \ln x + 1 \;\Rightarrow\; y' = y (\ln x + 1) = x^x (\ln x + 1)$$

로그 미분법은 지수와 곱이 복잡하게 얽힌 함수(예: $f(x) = \frac{(x+1)^3 \sqrt{x}}{(2x-1)^4}$)의 미분에 유용하다.

**예제 4 (연속 복리, continuous compounding):** 원금 $P$를 연이율 $r$로 $t$년 동안 연속 복리(continuous compounding)로 투자했을 때의 최종 금액을 구하라.

**풀이:** $n$회 복리 공식 $A_n = P(1 + r/n)^{nt}$에서 $n \to \infty$의 극한을 취한다.

$$A = \lim_{n \to \infty} P\left(1 + \frac{r}{n}\right)^{nt} = P \lim_{n \to \infty} \left[\left(1 + \frac{r}{n}\right)^{n/r}\right]^{rt} = P \left[\lim_{m \to \infty} \left(1 + \frac{1}{m}\right)^m\right]^{rt} = P e^{rt}$$

여기서 $m = n/r$로 치환했다. 즉 연속 복리에서는 $A = Pe^{rt}$가 성립한다. 예를 들어 $P = 1000$만 원, $r = 5\% = 0.05$, $t = 10$년이면 $A = 1000 e^{0.5} \approx 1648.72$만 원이다.

**예제 5 (로그 미분법 심화):** $f(x) = \frac{(x+1)^3 \sqrt{x}}{(2x-1)^4}$ ($x > 0$, $x \neq 1/2$)의 도함수를 구하라.

**풀이:** 양변에 자연로그를 취한다.

$$\ln f(x) = 3 \ln(x+1) + \frac{1}{2} \ln x - 4 \ln(2x-1)$$

양변을 미분하면

$$\frac{f'(x)}{f(x)} = \frac{3}{x+1} + \frac{1}{2x} - \frac{4 \cdot 2}{2x-1} = \frac{3}{x+1} + \frac{1}{2x} - \frac{8}{2x-1}$$

따라서

$$f'(x) = \frac{(x+1)^3 \sqrt{x}}{(2x-1)^4} \left( \frac{3}{x+1} + \frac{1}{2x} - \frac{8}{2x-1} \right)$$

**예제 6 (쌍곡선 함수의 미분 확인):** $\frac{d}{dx} \sinh x = \cosh x$임을 지수함수 표현과 미분법으로 증명하라.

**풀이:** $\sinh x = \frac{e^x - e^{-x}}{2}$이므로

$$\frac{d}{dx} \sinh x = \frac{d}{dx} \frac{e^x - e^{-x}}{2} = \frac{e^x - (-e^{-x})}{2} = \frac{e^x + e^{-x}}{2} = \cosh x$$

같은 방법으로 $\frac{d}{dx} \cosh x = \frac{e^x - e^{-x}}{2} = \sinh x$이다.

**예제 7 (연쇄법칙과 지수함수의 결합):** $f(x) = e^{-x^2}$의 도함수를 구하고, $f'(x) = 0$이 되는 $x$를 찾아라.

**풀이:** 연쇄법칙에 의해

$$f'(x) = e^{-x^2} \cdot (-2x) = -2x e^{-x^2}$$

$e^{-x^2} > 0$이므로 $f'(x) = 0$ $\iff$ $x = 0$이다. $x < 0$에서 $f'(x) > 0$(함수 증가), $x > 0$에서 $f'(x) < 0$(함수 감소)이므로 $x = 0$에서 최댓값 $f(0) = 1$을 가진다. 함수 $e^{-x^2}$는 가우시안 함수(Gaussian function)로 정규분포의 확률밀도함수의 핵심이다.

**예제 8 (로지스틱 함수의 미분):** 로지스틱 함수 $f(x) = \frac{1}{1 + e^{-x}}$의 도함수를 구하라.

**풀이:** 몫 법칙과 연쇄법칙을 적용하거나, $f(x) = (1 + e^{-x})^{-1}$로 보고 연쇄법칙을 적용한다.

$$f'(x) = -(1 + e^{-x})^{-2} \cdot (-e^{-x}) = \frac{e^{-x}}{(1 + e^{-x})^2}$$

이 표현은 $f(x)$를 이용해 더 간단히 쓸 수 있다. $1 - f(x) = \frac{e^{-x}}{1 + e^{-x}}$이므로

$$f'(x) = f(x) (1 - f(x))$$

즉, 로지스틱 함수의 미분은 자기 자신과 여함수(complement)의 곱이다. 이 성질은 로지스틱 회귀(logistic regression)의 우도 최적화에 중요하게 사용된다.

## 연결

- **[지수와 로그](topics/exponentials-logarithms.html)** : 지수법칙과 로그법칙, $e$의 정의 등 미분의 전제가 되는 기초 개념을 다룬다.
- **[극한·연속·도함수](topics/limits-derivatives.html)** : $e^x$의 미분은 극한 $\lim_{h\to 0} (e^h-1)/h = 1$에서 출발하며, 이 극한값은 $e$의 정의와 연결된다.
- **[상미분방정식 기초](topics/ode-basics.html)** : $f' = f$의 유일성 증명과 지수성장 모델은 상미분방정식의 가장 기본적인 예시다. 분리 가능 미분방정식(separable ODE)의 표준 사례이기도 하다.
