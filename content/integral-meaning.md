---
title: 적분의 의미
slug: integral-meaning
---

## 직관적 설명

**적분(integral)** 은 "잘게 쪼개서 더하기"다. 면적, 부피, 질량, 일(work), 확률 등 연속적인 양의 누적을 계산하는 방법이다. 함수 $f(x)$의 그래프 아래 면적을 구하기 위해, 영역을 아주 좁은 직사각형들로 쪼개고 각각의 넓이를 더한 후 직사각형의 폭을 0으로 보내는 극한이 적분이다.

**미적분학의 기본정리(Fundamental Theorem of Calculus, FTC)** 는 미분과 적분이 역연산 관계임을 말해준다. 즉, "속도를 적분하면 거리, 밀도를 적분하면 질량"이 되고, 반대로 "거리를 미분하면 속도"가 된다. 이 정리는 미분(differentiation)과 적분(integration)이라는 별개의 개념을 연결하여 미적분학의 통일된 이론을 완성한다.

**부정적분(indefinite integral, antiderivative)** $F(x)$는 $F'(x) = f(x)$를 만족하는 함수이고, **정적분(definite integral)** $\int_a^b f(x)\,dx$는 구간 $[a, b]$에서의 $f$의 누적량을 나타낸다. FTC는 이 둘이 본질적으로 같은 것임을 보여준다: $\int_a^b f = F(b) - F(a)$.

## 정의

**분할(partition):** 구간 $[a, b]$의 분할 $P = \{x_0, x_1, \ldots, x_n\}$은 $a = x_0 < x_1 < \cdots < x_n = b$를 만족하는 점들의 집합이다. $i$번째 하위구간의 길이는 $\Delta x_i = x_i - x_{i-1}$이다. 분할의 **세분(norm)** 은 $\|\Delta\| = \max_i \Delta x_i$이다.

**리만 합(Riemann sum):** 분할 $P$와 각 하위구간에서 선택점(sample point) $c_i \in [x_{i-1}, x_i]$에 대해

$$R(f, P, c) = \sum_{i=1}^n f(c_i) \Delta x_i$$

**리만 적분(Riemann integral):** $f$가 $[a, b]$에서 유계(bounded)라고 하자. 다음 극한이 존재할 때 $f$는 $[a, b]$에서 **리만 적분 가능(Riemann integrable)** 하다고 하고, 그 값을 정적분이라 한다.

$$\int_a^b f(x)\,dx = \lim_{\|\Delta\| \to 0} \sum_{i=1}^n f(c_i) \Delta x_i$$

엄밀히: 임의의 $\epsilon > 0$에 대해 $\delta > 0$이 존재하여 $\|\Delta\| < \delta$인 모든 분할과 임의의 선택점에 대해 $\left| \sum f(c_i) \Delta x_i - I \right| < \epsilon$이면 $I$가 적분값이다.

**상적분과 하적분( upper and lower integrals):** 다르부 적분(Darboux integral) 접근법에서는 각 하위구간에서 $f$의 최댓값 $M_i = \sup_{[x_{i-1}, x_i]} f(x)$와 최솟값 $m_i = \inf_{[x_{i-1}, x_i]} f(x)$를 이용해 상합(upper sum) $U(f, P) = \sum M_i \Delta x_i$와 하합(lower sum) $L(f, P) = \sum m_i \Delta x_i$을 정의한다. 상적분 $U = \inf_P U(f, P)$와 하적분 $L = \sup_P L(f, P)$이 같으면 $f$는 적분 가능하다.

**부정적분(indefinite integral, antiderivative):** $F'(x) = f(x)$를 만족하는 함수 $F$를 $f$의 부정적분이라 한다. 일반적으로 $\int f(x)\,dx = F(x) + C$로 표기하며, $C$는 적분 상수(constant of integration)이다.

**미적분학의 기본정리(Fundamental Theorem of Calculus):**

- **FTC 1 (미분 버전):** $f$가 $[a, b]$에서 연속이고 $F(x) = \int_a^x f(t)\,dt$라 하면 $F$는 $[a, b]$에서 연속이고 $(a, b)$에서 미분가능하며 $F'(x) = f(x)$이다.

- **FTC 2 (적분 버전):** $f$가 $[a, b]$에서 연속이고 $F$가 $f$의 임의의 부정적분이면 $\int_a^b f(x)\,dx = F(b) - F(a)$이다.

**이상적분(improper integral):** 적분 구간이 무한하거나 피적분함수가 구간 내에서 유계가 아닌 경우를 다루는 적분.

1. **무한 구간:** $\int_a^\infty f(x)\,dx = \lim_{b \to \infty} \int_a^b f(x)\,dx$ (극한이 존재하면 수렴)
2. **비유계 피적분함수:** $f$가 $x = a$에서 무한대로 발산할 때 $\int_a^b f(x)\,dx = \lim_{t \to a^+} \int_t^b f(x)\,dx$

**부분적분(integration by parts):** 곱 법칙의 적분 버전.

$$\int u\,dv = uv - \int v\,du$$

또는 정적분 형태: $\int_a^b u(x) v'(x)\,dx = [u(x)v(x)]_a^b - \int_a^b u'(x) v(x)\,dx$

**치환적분(substitution rule):** 연쇄법칙의 적분 버전. $u = g(x)$일 때

$$\int f(g(x)) g'(x)\,dx = \int f(u)\,du$$

정적분에서는 $\int_a^b f(g(x)) g'(x)\,dx = \int_{g(a)}^{g(b)} f(u)\,du$

## 주요 정리와 증명

### 정리 1: 미적분학의 기본정리 1 (FTC1)

$f$가 $[a, b]$에서 연속이라 하자. $F(x) = \int_a^x f(t)\,dt$ ($a \leq x \leq b$)로 정의하면 $F$는 $(a, b)$에서 미분가능하고 $F'(x) = f(x)$이다.

**증명:** 미분계수의 정의를 $F$에 적용한다. $x \in (a, b)$와 $h \neq 0$(단 $x+h \in (a, b)$)에 대해

$$\frac{F(x+h) - F(x)}{h} = \frac{1}{h} \left[ \int_a^{x+h} f(t)\,dt - \int_a^x f(t)\,dt \right] = \frac{1}{h} \int_x^{x+h} f(t)\,dt$$

이제 적분 평균값 정리(Mean Value Theorem for Integrals, 아래 정리 4)를 적용한다. $f$가 연속이므로 $\int_x^{x+h} f(t)\,dt = f(c) \cdot h$인 $c$가 $x$와 $x+h$ 사이에 존재한다. 따라서

$$\frac{F(x+h) - F(x)}{h} = \frac{1}{h} \cdot f(c) \cdot h = f(c)$$

$h \to 0$이면 $c \to x$이고, $f$의 연속성에 의해 $f(c) \to f(x)$이다. 따라서

$$F'(x) = \lim_{h \to 0} \frac{F(x+h) - F(x)}{h} = f(x)$$

$\square$

이 증명은 FTC1이 왜 $f$의 연속성을 필요로 하는지 보여준다: $c \to x$일 때 $f(c) \to f(x)$가 보장되어야 하기 때문이다. $f$가 불연속인 점에서는 $F$가 미분가능하지 않을 수 있다.

### 정리 2: 미적분학의 기본정리 2 (FTC2)

$f$가 $[a, b]$에서 연속이고 $F$가 $f$의 임의의 부정적분이면 $\int_a^b f(x)\,dx = F(b) - F(a)$이다.

**증명:** $G(x) = \int_a^x f(t)\,dt$라 하자. FTC1에 의해 $G'(x) = f(x)$이다. $F$도 $F'(x) = f(x)$를 만족하므로 $F$와 $G$는 같은 도함수를 가진다. 따라서 $F(x) - G(x)$의 도함수는 0이고, $F(x) = G(x) + C$($C$는 상수)이다.

$x = a$에서 $G(a) = \int_a^a f(t)\,dt = 0$이므로 $C = F(a) - G(a) = F(a)$이다. 따라서 $G(x) = F(x) - F(a)$이고,

$$\int_a^b f(x)\,dx = G(b) = F(b) - F(a)$$

$\square$

FTC2는 정적분 계산을 부정적분의 값 차이로 대체함으로써, 리만 합의 극한을 직접 계산하지 않아도 되게 해준다. 이 정리 이전에는 각 적분을 개별적인 극한 문제로 풀어야 했지만, FTC 이후에는 도함수의 역연산(부정적분)으로 일관되게 처리할 수 있게 되었다.

### 정리 3: 적분의 선형성과 구간 가법성

**선형성(linearity):** $f, g$가 $[a, b]$에서 적분 가능하고 $\alpha, \beta \in \mathbb{R}$이면

$$\int_a^b [\alpha f(x) + \beta g(x)]\,dx = \alpha \int_a^b f(x)\,dx + \beta \int_a^b g(x)\,dx$$

**증명:** 리만 합의 선형성에서 직접 유도된다.

$$\sum [\alpha f(c_i) + \beta g(c_i)] \Delta x_i = \alpha \sum f(c_i) \Delta x_i + \beta \sum g(c_i) \Delta x_i$$

극한을 취하면 원하는 결과를 얻는다.

**구간 가법성(additivity of interval):** $a < c < b$이고 $f$가 $[a, b]$에서 적분 가능하면

$$\int_a^b f(x)\,dx = \int_a^c f(x)\,dx + \int_c^b f(x)\,dx$$

**증명:** $a < c < b$인 분할을 고려하면 리만 합이 두 구간의 리만 합의 합으로 분해된다.

### 정리 4: 적분 평균값 정리 (Mean Value Theorem for Integrals)

$f$가 $[a, b]$에서 연속이면 $\int_a^b f(x)\,dx = f(c)(b-a)$를 만족하는 $c \in [a, b]$가 존재한다.

**증명:** $f$가 $[a, b]$에서 연속이므로 최대최소 정리에 의해 최댓값 $M$과 최솟값 $m$을 갖는다. $m \leq f(x) \leq M$이므로

$$m(b-a) \leq \int_a^b f(x)\,dx \leq M(b-a)$$

양변을 $b-a$로 나누면 $\frac{1}{b-a} \int_a^b f(x)\,dx$는 $m$과 $M$ 사이의 값이다. $f$가 연속이므로 중간값 정리(Intermediate Value Theorem)에 의해 이 값과 같은 $f(c)$를 만족하는 $c \in [a, b]$가 존재한다. 따라서

$$f(c) = \frac{1}{b-a} \int_a^b f(x)\,dx \quad\Longleftrightarrow\quad \int_a^b f(x)\,dx = f(c)(b-a)$$

$\square$

기하학적 의미: 곡선 아래 면적과 같은 넓이를 가진 직사각형의 높이가 $f(c)$이다.

### 정리 5: 이상적분의 수렴 판정 — $p$-적분

$\int_1^\infty \frac{1}{x^p}\,dx$는 $p > 1$일 때 수렴하고 $p \leq 1$일 때 발산한다.

**증명:** $p \neq 1$일 때

$$\int_1^b \frac{1}{x^p}\,dx = \left[ \frac{x^{1-p}}{1-p} \right]_1^b = \frac{b^{1-p} - 1}{1-p}$$

$b \to \infty$일 때, $p > 1$이면 $b^{1-p} \to 0$이므로 극한값 $\frac{1}{p-1}$로 수렴한다. $p < 1$이면 $b^{1-p} \to \infty$이므로 발산한다.

$p = 1$일 때는 $\int_1^b \frac{1}{x}\,dx = \ln b \to \infty$이므로 발산한다. $\square$

이 결과는 급수의 수렴 판정(적분 판정법)의 기초가 된다. 예를 들어 $\sum 1/n^p$는 $p > 1$일 때 수렴하고 $p \leq 1$일 때 발산하는데, 이를 $p$-급수(p-series)라 한다.

### 정리 6: 부분적분 공식의 증명

$\int u\,dv = uv - \int v\,du$

**증명:** 곱 법칙 $(uv)' = u'v + uv'$의 양변을 적분한다.

$$\int (uv)'\,dx = \int u'v\,dx + \int uv'\,dx$$

좌변은 FTC에 의해 $uv$가 된다. 따라서

$$uv = \int v\,du + \int u\,dv$$

(여기서 $du = u'\,dx$, $dv = v'\,dx$). 적분항을 정리하면 $\int u\,dv = uv - \int v\,du$를 얻는다. $\square$

## 예제

**예제 1 (리만 합으로 정적분 직접 계산):** $\int_0^1 x^2\,dx = \frac{1}{3}$임을 리만 합의 극한으로 직접 증명하라.

**풀이:** $[0, 1]$을 $n$개의 동일한 하위구간으로 분할한다. $\Delta x = \frac{1}{n}$, $x_i = \frac{i}{n}$ ($i = 0, 1, \ldots, n$). 오른쪽 끝점(right endpoint)을 선택점으로 사용하면 $c_i = x_i = \frac{i}{n}$이다.

리만 합은

$$R_n = \sum_{i=1}^n f\left(\frac{i}{n}\right) \cdot \frac{1}{n} = \sum_{i=1}^n \left(\frac{i}{n}\right)^2 \cdot \frac{1}{n} = \frac{1}{n^3} \sum_{i=1}^n i^2 = \frac{1}{n^3} \cdot \frac{n(n+1)(2n+1)}{6}$$

$$= \frac{(n+1)(2n+1)}{6n^2} = \frac{2n^2 + 3n + 1}{6n^2} = \frac{1}{3} + \frac{1}{2n} + \frac{1}{6n^2}$$

$n \to \infty$에서 $R_n \to \frac{1}{3}$이므로 $\int_0^1 x^2\,dx = \frac{1}{3}$이다.

**예제 2 (FTC로 면적 계산):** $\int_0^{\pi} \sin x\,dx$를 FTC로 계산하라.

**풀이:** $\frac{d}{dx}(-\cos x) = \sin x$이므로 부정적분은 $F(x) = -\cos x$이다. FTC2에 의해

$$\int_0^{\pi} \sin x\,dx = F(\pi) - F(0) = (-\cos\pi) - (-\cos 0) = (-(-1)) - (-1) = 1 + 1 = 2$$

이 값은 $y = \sin x$의 $0$부터 $\pi$까지의 그래프 아래 면적이 2임을 의미한다.

**예제 3 (치환적분, substitution):** $\int_0^1 \sqrt{1 - x^2}\,dx$를 계산하라. (단, 도형의 넓이로 해석할 것.)

**풀이:** $y = \sqrt{1 - x^2}$는 반지름 1인 원의 상반부 방정식 $x^2 + y^2 = 1$ ($y \geq 0$)이다. $x \in [0, 1]$ 구간은 1사분면의 원호에 해당한다.

따라서 $\int_0^1 \sqrt{1 - x^2}\,dx$는 반지름 1인 원의 1/4 넓이, 즉 $\frac{\pi \cdot 1^2}{4} = \frac{\pi}{4}$이다.

치환 $x = \sin \theta$($dx = \cos \theta\,d\theta$)로도 같은 결과를 얻을 수 있다:

$$\int_0^1 \sqrt{1 - x^2}\,dx = \int_0^{\pi/2} \sqrt{1 - \sin^2 \theta} \cdot \cos \theta \,d\theta = \int_0^{\pi/2} \cos^2 \theta \,d\theta$$

$$= \int_0^{\pi/2} \frac{1 + \cos 2\theta}{2} \,d\theta = \frac{1}{2} \left[ \theta + \frac{\sin 2\theta}{2} \right]_0^{\pi/2} = \frac{1}{2} \cdot \frac{\pi}{2} = \frac{\pi}{4}$$

**예제 4 (부정적분과 FTC의 활용):** $f(x) = \frac{d}{dx} \int_0^x e^{-t^2}\,dt$를 구하라.

**풀이:** FTC1에 의해 $\frac{d}{dx} \int_0^x e^{-t^2}\,dt = e^{-x^2}$이다. $\int_0^x e^{-t^2}\,dt$는 초등함수로 표현할 수 없는 적분(오차 함수, error function $\text{erf}(x)$로 알려져 있음)이지만, FTC1 덕분에 그 도함수는 쉽게 계산된다.

**예제 5 (부분적분, integration by parts):** $\int_0^1 x e^x\,dx$를 계산하라.

**풀이:** $u = x$, $dv = e^x\,dx$로 두면 $du = dx$, $v = e^x$이다. 부분적분 공식에 의해

$$\int_0^1 x e^x\,dx = [x e^x]_0^1 - \int_0^1 e^x\,dx = (1 \cdot e^1 - 0 \cdot e^0) - [e^x]_0^1 = e - (e - 1) = 1$$

**예제 6 (이상적분, improper integral):** $\int_1^\infty \frac{1}{x^2}\,dx$의 수렴 여부와 수렴값을 판정하라.

**풀이:** 이상적분의 정의에 의해

$$\int_1^\infty \frac{1}{x^2}\,dx = \lim_{b \to \infty} \int_1^b \frac{1}{x^2}\,dx = \lim_{b \to \infty} \left[ -\frac{1}{x} \right]_1^b = \lim_{b \to \infty} \left( -\frac{1}{b} + 1 \right) = 1$$

따라서 이 적분은 1로 수렴한다. 이는 유한한 면적(1)이 무한히 긴 영역에 펼쳐져 있는 경우다.

**예제 7 (이상적분 — 비유계 피적분함수):** $\int_0^1 \frac{1}{\sqrt{x}}\,dx$를 계산하라.

**풀이:** $x \to 0^+$에서 $1/\sqrt{x} \to \infty$이므로 이상적분이다.

$$\int_0^1 \frac{1}{\sqrt{x}}\,dx = \lim_{t \to 0^+} \int_t^1 x^{-1/2}\,dx = \lim_{t \to 0^+} [2\sqrt{x}]_t^1 = \lim_{t \to 0^+} (2 - 2\sqrt{t}) = 2$$

$1/\sqrt{x}$는 $x = 0$에서 무한대로 발산하지만, 그 적분은 유한한 값 2로 수렴한다.

**예제 8 (치환적분 심화):** $\int_0^{\pi/2} \sin x \cos x\,dx$를 치환 $u = \sin x$로 계산하라.

**풀이:** $u = \sin x$라 하면 $du = \cos x\,dx$이고, $x = 0$에서 $u = 0$, $x = \pi/2$에서 $u = 1$이다.

$$\int_0^{\pi/2} \sin x \cos x\,dx = \int_0^1 u\,du = \left[ \frac{u^2}{2} \right]_0^1 = \frac{1}{2}$$

## 연결

- **[다중적분](multiple-integrals.html)** : 리만 적분을 2차원, 3차원으로 확장하여 부피와 질량을 계산한다. 반복적분(iterated integral)과 푸비니 정리(Fubini's theorem)가 핵심이다.
- **[급수와 수렴](series-convergence.html)** : 적분과 급수는 깊이 연결되어 있다. 적분 판정법(integral test)은 급수의 수렴을 적분으로 판정하고, 함수를 다항식으로 전개하는 테일러 급수는 적분으로 표현되는 나머지 항을 가진다.
