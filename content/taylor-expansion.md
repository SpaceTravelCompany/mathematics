---
title: 테일러 전개
slug: taylor-expansion
---

## 직관적 설명

**테일러 전개(Taylor expansion)** 는 복잡한 함수를 특정 점 근처에서 간단한 다항식으로 근사하는 방법이다. "모르는 함수라도 한 점에서의 값과 미분계수들을 알면 그 근처에서 예측할 수 있다"는 아이디어다.

1차 근사(선형 근사)는 "현재 위치 + 기울기"로 미래를 예측한다: $f(x) \approx f(a) + f'(a)(x-a)$. 2차 근사는 여기에 곡률 정보를 추가한다: $f(x) \approx f(a) + f'(a)(x-a) + \frac{1}{2}f''(a)(x-a)^2$.

차수를 높일수록 근사가 더 정확해지고, 모든 차수를 더하면(급수, series) 원래 함수와 완전히 일치하게 된다(해석함수, analytic function의 경우).

소진동 근사(small-angle approximation) $\sin\theta \approx \theta$나 $e^x \approx 1 + x$는 테일러 전개의 1차 항만 취한 것이다. 물리학과 공학에서 비선형 시스템을 선형화할 때 테일러 전개가 필수적이다.

## 정의

**1변수 테일러 전개 (Taylor expansion, 1D):** $f: \mathbb{R} \to \mathbb{R}$이 $C^{n+1}$ 함수일 때, $x = a$ 근방에서:

$$f(x) = \sum_{k=0}^n \frac{f^{(k)}(a)}{k!}(x-a)^k + R_n(x)$$

여기서 $f^{(k)}(a)$는 $k$계 도함수, $k!$은 팩토리얼, $R_n(x)$는 나머지항(remainder)이다.

**라그랑주 나머지 (Lagrange remainder):**

$$R_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}(x-a)^{n+1}$$

단, $\xi$는 $a$와 $x$ 사이에 존재하는 어떤 값이다.

**다변수 테일러 전개 (Taylor expansion, multivariate):** $f: \mathbb{R}^n \to \mathbb{R}$이 $C^3$일 때, $a$ 근방에서:

$$f(a+h) = f(a) + \nabla f(a)^T h + \frac{1}{2} h^T H(a) h + O(\|h\|^3)$$

여기서 $\nabla f(a)$는 그래디언트(gradient), $H(a)$는 헤시안(Hessian)이다.

**일반 항:** $|\alpha| = k$차 항은 $\frac{1}{\alpha!} \partial^\alpha f(a) h^\alpha$ 꼴이다. 여기서 $\alpha = (\alpha_1, \ldots, \alpha_n)$은 다중지수(multi-index), $\alpha! = \alpha_1! \cdots \alpha_n!$, $\partial^\alpha f = \partial^{\alpha_1}_{x_1} \cdots \partial^{\alpha_n}_{x_n} f$, $h^\alpha = h_1^{\alpha_1} \cdots h_n^{\alpha_n}$.

**매클로린 급수 (Maclaurin series):** $a = 0$인 특수한 테일러 전개:

$$f(x) = \sum_{k=0}^\infty \frac{f^{(k)}(0)}{k!} x^k$$

**선형 근사 (linear approximation):** $f(x) \approx f(a) + f'(a)(x-a)$ (1차 근사)

**2차 근사 (quadratic approximation):** $f(x) \approx f(a) + f'(a)(x-a) + \frac{1}{2}f''(a)(x-a)^2$

## 주요 정리와 증명

### 정리 1: 테일러 정리 — 라그랑주 나머지 (Taylor's Theorem with Lagrange Remainder)

$f: \mathbb{R} \to \mathbb{R}$이 $[a, x]$에서 $C^{n+1}$이면, 어떤 $\xi \in (a, x)$가 존재하여:

$$f(x) = \sum_{k=0}^n \frac{f^{(k)}(a)}{k!}(x-a)^k + \frac{f^{(n+1)}(\xi)}{(n+1)!}(x-a)^{n+1}$$

**증명:** $R_n(x) = f(x) - \sum_{k=0}^n \frac{f^{(k)}(a)}{k!}(x-a)^k$로 정의하자. 함수 $g(t)$를 다음과 같이 정의한다:

$$g(t) = f(x) - \sum_{k=0}^n \frac{f^{(k)}(t)}{k!}(x-t)^k - R_n(x) \frac{(x-t)^{n+1}}{(x-a)^{n+1}}$$

$g(a) = 0$이고 $g(x) = 0$이다(직접 대입 확인). $g$에 롤 정리(Rolle's theorem)를 적용하면 $g'(\xi) = 0$인 $\xi \in (a, x)$가 존재한다. $g'(t)$를 계산하면 많은 항이 소멸(cancel)되고:

$$g'(t) = \frac{f^{(n+1)}(t)}{n!}(x-t)^n + (n+1)R_n(x)\frac{(x-t)^n}{(x-a)^{n+1}}$$

$g'(\xi) = 0$에서 $R_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}(x-a)^{n+1}$를 얻는다.

$\square$

**의미:** 나머지항은 $f$의 $(n+1)$계 도함수의 부호와 크기에 의해 결정된다. $|f^{(n+1)}(\xi)| \leq M$이면 $|R_n(x)| \leq \frac{M}{(n+1)!}|x-a|^{n+1}$이다.

### 정리 2: 다변수 테일러 전개 (Multivariate Taylor Expansion)

$f: \mathbb{R}^n \to \mathbb{R}$이 $C^2$이면, $a$에서:

$$f(a+h) = f(a) + \nabla f(a)^T h + \frac{1}{2} h^T H(a) h + o(\|h\|^2)$$

**증명:** $g(t) = f(a + th)$로 정의한다($t \in \mathbb{R}$). $g$는 1변수 함수다. $g$를 $t = 0$에서 테일러 전개한다:

$$g(t) = g(0) + g'(0)t + \frac{1}{2}g''(0)t^2 + o(t^2)$$

연쇄법칙(chain rule)으로 $g'(0)$과 $g''(0)$을 계산한다:

$$g'(t) = \nabla f(a + th) \cdot h, \quad g'(0) = \nabla f(a)^T h$$

$$g''(t) = h^T H(a + th) h, \quad g''(0) = h^T H(a) h$$

$t = 1$을 대입하면:

$$f(a+h) = f(a) + \nabla f(a)^T h + \frac{1}{2} h^T H(a) h + o(\|h\|^2)$$

$\square$

**일반 $n$차 항:** $g^{(k)}(0)$을 $f$의 $k$계 도함수로 표현하면:

$$f(a+h) = \sum_{|\alpha| \leq n} \frac{\partial^\alpha f(a)}{\alpha!} h^\alpha + o(\|h\|^n)$$

### 정리 3: 뉴턴법 (Newton's Method)

방정식 $f(x) = 0$의 해를 찾는 뉴턴법(Newton's method)은 1차 테일러 전개에서 유도된다.

**유도:** $f(x) \approx f(x_0) + f'(x_0)(x - x_0) = 0$으로 두고 $x$에 대해 풀면:

$$x_1 = x_0 - \frac{f(x_0)}{f'(x_0)}$$

이 과정을 반복($x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$)하면 $f(x) = 0$의 해에 수렴한다(초기값이 충분히 가까울 때).

**수렴 속도 (quadratic convergence):** $f$가 $C^2$이고 $f'(x^*) \neq 0$이면, $|x_{n+1} - x^*| \leq C|x_n - x^*|^2$로 이차 수렴한다.

**증명:** $x^*$가 $f(x^*) = 0$인 근이라고 하자. $x_n$에서 2차 테일러 전개:

$$0 = f(x^*) = f(x_n) + f'(x_n)(x^* - x_n) + \frac{1}{2}f''(\xi)(x^* - x_n)^2$$

뉴턴법 갱신식 $x_{n+1} = x_n - f(x_n)/f'(x_n)$을 대입하여 정리하면:

$$x_{n+1} - x^* = \frac{f''(\xi)}{2f'(x_n)}(x_n - x^*)^2$$

따라서 $|x_{n+1} - x^*| \leq \frac{\max |f''|}{2\min |f'|}|x_n - x^*|^2$이다.

$\square$

### 정리 4: 주요 함수의 테일러 급수 (Important Taylor Series)

다음은 $a = 0$에서의 테일러 급수(매클로린 급수)다:

$$e^x = \sum_{k=0}^\infty \frac{x^k}{k!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots \quad (\forall x \in \mathbb{R})$$

$$\sin x = \sum_{k=0}^\infty \frac{(-1)^k x^{2k+1}}{(2k+1)!} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots \quad (\forall x \in \mathbb{R})$$

$$\cos x = \sum_{k=0}^\infty \frac{(-1)^k x^{2k}}{(2k)!} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots \quad (\forall x \in \mathbb{R})$$

$$\frac{1}{1-x} = \sum_{k=0}^\infty x^k = 1 + x + x^2 + x^3 + \cdots \quad (|x| < 1)$$

$$\ln(1+x) = \sum_{k=1}^\infty \frac{(-1)^{k+1} x^k}{k} = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots \quad (-1 < x \leq 1)$$

$$(1+x)^\alpha = \sum_{k=0}^\infty \binom{\alpha}{k} x^k = 1 + \alpha x + \frac{\alpha(\alpha-1)}{2!}x^2 + \cdots \quad (|x| < 1, \text{ 이항급수})$$

## 예제

**예제 1:** $e^x$의 $a = 0$에서 3차 테일러 전개와 나머지항을 구하고, $e^{0.1}$의 근삿값과 오차를 평가하라.

**풀이:** $e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + R_3(x)$.

$R_3(x) = \frac{e^\xi}{4!}x^4$, $\xi \in (0, x)$.

$x = 0.1$에서 3차 근사: $e^{0.1} \approx 1 + 0.1 + \frac{0.01}{2} + \frac{0.001}{6} = 1.1051666\ldots$

오차 상한: $|R_3(0.1)| \leq \frac{e^{0.1}}{24}(0.1)^4 \approx \frac{1.1052}{24} \times 10^{-4} \approx 4.6 \times 10^{-6}$.

실제값 $e^{0.1} \approx 1.1051709$와 비교하면 오차가 $4.3 \times 10^{-6}$으로 상한 내에 있다.

**예제 2:** $f(x, y) = e^{x+y}$의 $(0, 0)$에서 2차 테일러 근사를 구하라.

**풀이:** $f(0, 0) = 1$, $\nabla f = (e^{x+y}, e^{x+y})$, $\nabla f(0, 0) = (1, 1)$.

헤시안: $H = \begin{pmatrix} e^{x+y} & e^{x+y} \\ e^{x+y} & e^{x+y} \end{pmatrix}$, $H(0, 0) = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}$.

2차 근사:

$$f(x, y) \approx 1 + (1, 1)\begin{pmatrix} x \\ y \end{pmatrix} + \frac{1}{2}(x, y)\begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}\begin{pmatrix} x \\ y \end{pmatrix}$$

$$= 1 + x + y + \frac{1}{2}(x^2 + 2xy + y^2) = 1 + x + y + \frac{1}{2}(x + y)^2$$

$e^{x+y}$의 1변수 테일러 전개 $e^t = 1 + t + t^2/2 + \cdots$에 $t = x+y$를 대입한 결과와 일치한다.

**예제 3 (뉴턴법으로 $\sqrt{2}$ 계산):** 뉴턴법을 사용하여 $\sqrt{2}$를 소수점 6자리까지 계산하라.

**풀이:** $f(x) = x^2 - 2 = 0$의 해를 구한다. $f'(x) = 2x$.

뉴턴 갱신: $x_{n+1} = x_n - \frac{x_n^2 - 2}{2x_n} = \frac{x_n + 2/x_n}{2}$.

초기값 $x_0 = 1$:

$x_1 = (1 + 2/1)/2 = 1.5$

$x_2 = (1.5 + 2/1.5)/2 = (1.5 + 1.3333)/2 = 1.416667$

$x_3 = (1.416667 + 2/1.416667)/2 = (1.416667 + 1.411765)/2 = 1.414216$

$x_4 = (1.414216 + 2/1.414216)/2 = 1.414214$

3회 반복으로 $1.414214$를 얻었으며, $\sqrt{2} \approx 1.41421356$과 6자리까지 일치한다. 수렴 속도가 매우 빠름(2차 수렴)을 확인할 수 있다.

**예제 4 (소진동 근사):** 진자(pendulum) 운동방정식 $\frac{d^2\theta}{dt^2} = -\frac{g}{L}\sin\theta$에서 $\sin\theta \approx \theta$로 근사하면 단순 조화 진동자(simple harmonic oscillator)가 된다. $\theta = 0.1$ rad에서 근사의 상대 오차를 구하라.

**풀이:** $\sin\theta = \theta - \frac{\theta^3}{6} + O(\theta^5)$.

$\theta = 0.1$에서 $\sin(0.1) = 0.0998334\ldots$, 선형 근사 $\theta = 0.1$.

상대 오차 $= \frac{|0.0998334 - 0.1|}{0.0998334} \approx 0.00167 = 0.167\%$.

3차 항을 포함하면: $\theta - \theta^3/6 = 0.1 - 0.001/6 = 0.0998333\ldots$, 오차가 $10^{-6}$ 수준으로 줄어든다.

**예제 5:** $f(x) = \ln(1+x)$의 $a = 0$에서 4차 테일러 전개를 구하고, $\ln(1.2)$의 근삿값을 계산하라.

**풀이:** $f^{(k)}(x) = (-1)^{k-1}(k-1)!(1+x)^{-k}$이므로 $f^{(k)}(0) = (-1)^{k-1}(k-1)!$.

$$\ln(1+x) = x - \frac{x^2}{2} + \frac{x^3}{3} - \frac{x^4}{4} + R_4(x)$$

$x = 0.2$: $\ln(1.2) \approx 0.2 - 0.02 + 0.002667 - 0.0004 = 0.182267$.

실제값 $\ln(1.2) \approx 0.182322$와 비교하면 오차 약 $5.5 \times 10^{-5}$.

**예제 6 (다변수 선형 근사):** $f(x, y) = \sqrt{x^2 + y^2}$의 $(3, 4)$에서 1차 근사를 구하고, $f(3.1, 3.9)$의 근삿값을 계산하라.

**풀이:** $f(3, 4) = \sqrt{9 + 16} = 5$.

$\nabla f = \left(\frac{x}{\sqrt{x^2 + y^2}}, \frac{y}{\sqrt{x^2 + y^2}}\right)$, $\nabla f(3, 4) = (3/5, 4/5)$.

1차 근사: $f(3.1, 3.9) \approx 5 + (0.6)(0.1) + (0.8)(-0.1) = 5 + 0.06 - 0.08 = 4.98$.

실제값: $\sqrt{3.1^2 + 3.9^2} = \sqrt{9.61 + 15.21} = \sqrt{24.82} \approx 4.9820$.

**예제 7 (2차 근사로 극값 판정):** $f(x, y) = \cos x + \cos y$의 $(0, 0)$에서 2차 테일러 근사를 구하고 극값을 판정하라.

**풀이:** $\nabla f = (-\sin x, -\sin y)$, $\nabla f(0, 0) = (0, 0)$ → 임계점.

$H = \begin{pmatrix} -\cos x & 0 \\ 0 & -\cos y \end{pmatrix}$, $H(0, 0) = \begin{pmatrix} -1 & 0 \\ 0 & -1 \end{pmatrix}$ (음정치).

2차 근사: $\cos x + \cos y \approx 2 - \frac{1}{2}x^2 - \frac{1}{2}y^2$.

$f(0, 0) = 2$에서 $x^2 + y^2$ 항이 음수이므로 극대. $\cos$ 함수의 그래프를 생각하면 타당하다.

## 연결

- **[급수와 수렴](series-convergence.html)** : 테일러 급수의 수렴 반경과 급수 판정법을 다룬다.
- **[야코비안·헤시안](jacobian-hessian.html)** : 다변수 테일러 전개의 1차·2차 항을 구성한다.
- **[라그랑주 승수법](lagrange-multipliers.html)** : 제약 최적화에서 2차 충분 조건에 테일러 전개가 사용된다.
- **[2계 도함수·헤시안·곡률](second-derivatives.html)** : 2차 테일러 항의 계수인 헤시안을 심화 학습한다.
