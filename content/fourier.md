---
title: 푸리에 급수·푸리에 변환
slug: fourier
---

## 직관적 설명

**푸리에 급수(Fourier series)** 는 모든 주기 함수(periodic function)를 사인과 코사인의 무한합으로 분해한다. 마치 프리즘(prism)이 백색광을 스펙트럼 색상으로 분해하듯, 푸리에 급수는 시간 영역의 신호를 주파수 성분으로 분해한다. 복잡한 파형(music, 음성, 전파)이 단순한 정현파(sinusoid)들의 합성이라는 사실은 신호 처리, 양자역학, 편미분방정식 해법의 기초가 된다.

**푸리에 변환(Fourier transform)** 은 이 아이디어를 비주기 함수로 확장한다. 주기가 무한대인 함수를 생각하면 주파수 스펙트럼이 이산(discrete)에서 연속(continuous)으로 바뀐다. $\hat{f}(\omega)$는 주파수 $\omega$의 성분이 신호 $f$에 얼마나 포함되어 있는지 나타낸다. 역변환(inverse transform)은 스펙트럼으로부터 원래 신호를 재구성한다.

핵심 통찰은 삼각함수 집합 $\{1, \cos nx, \sin nx\}$이 내적공간 $L^2[-\pi, \pi]$의 **직교 기저(orthogonal basis)** 를 이룬다는 것이다. 푸리에 계수는 함수를 이 기저에 정사영(projection)한 좌표다.

---
## 정의

**주기 함수 (periodic function):** $f(x + T) = f(x)$를 모든 $x$에 대해 만족하는 $T > 0$가 존재할 때 $f$를 주기함수라 하고 $T$를 주기라 한다. 편의상 주기를 $2\pi$로 표준화한다.

**푸리에 급수 (실수 형태, Fourier series in real form):** 주기 $2\pi$인 함수 $f$의 푸리에 급수 표현:

$$f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty}(a_n \cos nx + b_n \sin nx)$$

푸리에 계수(Fourier coefficients):

$$a_n = \frac{1}{\pi}\int_{-\pi}^{\pi} f(x)\cos nx\,dx, \quad n = 0, 1, 2, \ldots$$

$$b_n = \frac{1}{\pi}\int_{-\pi}^{\pi} f(x)\sin nx\,dx, \quad n = 1, 2, 3, \ldots$$

$a_0/2$는 평균값(dc component)을 나타낸다.

**푸리에 급수 (복소 형태, Fourier series in complex form):** 오일러 공식 $e^{inx} = \cos nx + i\sin nx$를 이용하면

$$f(x) = \sum_{n=-\infty}^{\infty} c_n e^{inx}$$

$$c_n = \frac{1}{2\pi}\int_{-\pi}^{\pi} f(x)e^{-inx}\,dx, \quad n \in \mathbb{Z}$$

실수 계수와의 관계: $c_0 = a_0/2$, $c_n = \frac{a_n - i b_n}{2}$ ($n \geq 1$), $c_{-n} = \frac{a_n + i b_n}{2}$ ($n \geq 1$).

**푸리에 변환 (Fourier transform):** $f: \mathbb{R} \to \mathbb{R}$(또는 $\mathbb{C}$)에 대해

$$\hat{f}(\omega) = \int_{-\infty}^{\infty} f(x) e^{-i\omega x}\,dx$$

**역푸리에 변환 (inverse Fourier transform):**

$$f(x) = \frac{1}{2\pi} \int_{-\infty}^{\infty} \hat{f}(\omega) e^{i\omega x}\,d\omega$$

수렴 조건: $f \in L^1(\mathbb{R})$, 즉 $\int_{-\infty}^{\infty} |f(x)|\,dx < \infty$이면 푸리에 변환이 존재한다. $L^2(\mathbb{R})$으로 확장 가능하다.

**컨볼루션 (convolution):** 두 함수 $f, g$의 컨볼루션:

$$(f * g)(x) = \int_{-\infty}^{\infty} f(x - t) g(t)\,dt = \int_{-\infty}^{\infty} f(t) g(x - t)\,dt$$

---
## 주요 정리와 증명

### 정리 1: 삼각함수 집합의 직교성 (Orthogonality)

구간 $[-\pi, \pi]$에서 다음 직교 관계가 성립한다:

$$\int_{-\pi}^{\pi} \cos mx \cos nx\,dx = \begin{cases}
0, & m \neq n \\
\pi, & m = n \neq 0 \\
2\pi, & m = n = 0
\end{cases}$$

$$\int_{-\pi}^{\pi} \sin mx \sin nx\,dx = \begin{cases}
0, & m \neq n \\
\pi, & m = n \neq 0
\end{cases}$$

$$\int_{-\pi}^{\pi} \cos mx \sin nx\,dx = 0, \quad \forall m, n$$

**증명:** 코사인 곱을 합으로 바꾸는 공식을 사용한다:

$$\cos mx \cos nx = \frac{1}{2}[\cos(m+n)x + \cos(m-n)x]$$

$m \neq n$일 때:

$$\int_{-\pi}^{\pi} \cos mx \cos nx\,dx = \frac{1}{2}\int_{-\pi}^{\pi} [\cos(m+n)x + \cos(m-n)x]\,dx$$

$\cos(m \pm n)x$의 $[-\pi, \pi]$에서의 적분은 0이므로(주기 $2\pi$의 정현파의 한 주기 적분은 0) 결과는 0이다.

$m = n \neq 0$일 때:

$$\int_{-\pi}^{\pi} \cos^2 nx\,dx = \frac{1}{2}\int_{-\pi}^{\pi} [1 + \cos 2nx]\,dx = \frac{1}{2}[x + \frac{\sin 2nx}{2n}]_{-\pi}^{\pi} = \frac{1}{2}(2\pi) = \pi$$

$m = n = 0$일 때: $\int_{-\pi}^{\pi} 1\,dx = 2\pi$.

사인 곱과 코사인-사인 혼합 곱도 유사하게 증명된다. $\square$

이 직교성은 집합 $\{\frac{1}{\sqrt{2\pi}}, \frac{\cos x}{\sqrt{\pi}}, \frac{\sin x}{\sqrt{\pi}}, \frac{\cos 2x}{\sqrt{\pi}}, \frac{\sin 2x}{\sqrt{\pi}}, \ldots\}$이 $L^2[-\pi,\pi]$의 정규직교기저(orthonormal basis)임을 의미한다.

### 정리 2: 푸리에 계수 공식의 유도 (직교투영)

푸리에 계수 $a_n$은 함수 $f$를 $\cos nx$에 정사영한 결과다.

**증명:** 내적공간 $L^2[-\pi,\pi]$에서 내적을 $\langle f, g \rangle = \int_{-\pi}^{\pi} f(x)g(x)\,dx$로 정의하자. $\cos nx$에 대한 $f$의 푸리에 계수는 내적을 노름 제곱으로 나눈 값이다:

$$a_n = \frac{\langle f, \cos nx \rangle}{\|\cos nx\|^2} = \frac{\int_{-\pi}^{\pi} f(x)\cos nx\,dx}{\int_{-\pi}^{\pi} \cos^2 nx\,dx} = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x)\cos nx\,dx$$

같은 방식으로 $b_n = \frac{\langle f, \sin nx \rangle}{\|\sin nx\|^2} = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x)\sin nx\,dx$.

$a_0$의 경우: $\|1\|^2 = \int_{-\pi}^{\pi} 1^2\,dx = 2\pi$이므로 $a_0 = \frac{\langle f, 1 \rangle}{\|1\|^2} = \frac{1}{\pi}\int_{-\pi}^{\pi} f(x)\,dx$이다. $\square$

이 관점은 푸리에 급수가 단순히 무한합이 아니라, 함수공간에서의 직교 분해(orthogonal decomposition)임을 명확히 보여준다.

### 정리 3: 파르스발 항등식 (Parseval's Identity)

$f$가 $[-\pi, \pi]$에서 리만 적분 가능하고 제곱 적분 가능(square integrable)하면

$$\frac{1}{\pi} \int_{-\pi}^{\pi} |f(x)|^2\,dx = \frac{a_0^2}{2} + \sum_{n=1}^{\infty} (a_n^2 + b_n^2)$$

복소 형태에서는

$$\frac{1}{2\pi} \int_{-\pi}^{\pi} |f(x)|^2\,dx = \sum_{n=-\infty}^{\infty} |c_n|^2$$

**증명:** 푸리에 급수 $f(x) = a_0/2 + \sum_{n=1}^{\infty}(a_n\cos nx + b_n\sin nx)$를 고려하자. $f$의 $L^2$ 노름을 계산한다:

$$\|f\|^2 = \int_{-\pi}^{\pi} f(x)^2\,dx$$

푸리에 급수를 대입하고 직교성을 이용하면 모든 교차항이 사라진다:

$$
\begin{aligned}
\int_{-\pi}^{\pi} f(x)^2\,dx &= \int_{-\pi}^{\pi} \left(\frac{a_0}{2}\right)^2 dx + \sum_{n=1}^{\infty} \int_{-\pi}^{\pi} (a_n^2\cos^2 nx + b_n^2\sin^2 nx)\,dx \\
&= \frac{a_0^2}{4} \cdot 2\pi + \sum_{n=1}^{\infty} (a_n^2 \cdot \pi + b_n^2 \cdot \pi)
\end{aligned}
$$

양변을 $\pi$로 나누면 $\frac{1}{\pi}\int_{-\pi}^{\pi} f^2 = \frac{a_0^2}{2} + \sum (a_n^2 + b_n^2)$. $\square$

파르스발 항등식은 신호 처리에서 에너지 보존으로 해석된다: 시간 도메인의 총 에너지 = 주파수 도메인의 총 에너지.

### 정리 4: 컨볼루션 정리 (Convolution Theorem)

$$\widehat{f * g}(\omega) = \hat{f}(\omega) \cdot \hat{g}(\omega)$$

즉, 시간 도메인의 컨볼루션은 주파수 도메인의 곱셈에 대응한다.

**증명:** 정의에서 출발한다:

$$
\begin{aligned}
\widehat{f * g}(\omega) &= \int_{-\infty}^{\infty} (f * g)(x) e^{-i\omega x}\,dx \\
&= \int_{-\infty}^{\infty} \left( \int_{-\infty}^{\infty} f(x - t) g(t)\,dt \right) e^{-i\omega x}\,dx
\end{aligned}
$$

적분 순서를 교환한다(푸비니 정리, $f, g \in L^1$ 가정):

$$= \int_{-\infty}^{\infty} g(t) \left( \int_{-\infty}^{\infty} f(x - t) e^{-i\omega x}\,dx \right) dt$$

내부 적분에서 $u = x - t$로 치환하면 $x = u + t$, $dx = du$:

$$\int_{-\infty}^{\infty} f(x - t) e^{-i\omega x}\,dx = \int_{-\infty}^{\infty} f(u) e^{-i\omega(u + t)}\,du = e^{-i\omega t} \int_{-\infty}^{\infty} f(u) e^{-i\omega u}\,du = e^{-i\omega t} \hat{f}(\omega)$$

원래 식에 대입:

$$\widehat{f * g}(\omega) = \int_{-\infty}^{\infty} g(t) e^{-i\omega t} \hat{f}(\omega)\,dt = \hat{f}(\omega) \int_{-\infty}^{\infty} g(t) e^{-i\omega t}\,dt = \hat{f}(\omega) \hat{g}(\omega)$$

$\square$

대칭적으로, $\widehat{f \cdot g}(\omega) = \frac{1}{2\pi} (\hat{f} * \hat{g})(\omega)$도 성립한다. 이 쌍대성(duality)은 푸리에 변환의 강력한 특징이다.

**따름정리:** $f$가 $n$번 미분 가능하고 각 도함수가 $L^1$이면

$$\widehat{f^{(n)}}(\omega) = (i\omega)^n \hat{f}(\omega)$$

미분이 주파수 도메인에서 다항식 곱셈으로 바뀌므로, 미분방정식이 대수방정식이 된다.

### 정리 5: 푸리에 변환의 선형성과 평행이동

**선형성:** $\widehat{\alpha f + \beta g} = \alpha \hat{f} + \beta \hat{g}$

**시간 평행이동:** $\widehat{f(x - a)}(\omega) = e^{-i\omega a} \hat{f}(\omega)$

**주파수 평행이동:** $\widehat{e^{i\omega_0 x} f(x)}(\omega) = \hat{f}(\omega - \omega_0)$

**증명 (시간 평행이동):**

$$\widehat{f(x - a)}(\omega) = \int_{-\infty}^{\infty} f(x - a) e^{-i\omega x}\,dx$$

$u = x - a$로 치환하면 $x = u + a$, $dx = du$:

$$= \int_{-\infty}^{\infty} f(u) e^{-i\omega(u + a)}\,du = e^{-i\omega a} \int_{-\infty}^{\infty} f(u) e^{-i\omega u}\,du = e^{-i\omega a} \hat{f}(\omega)$$

$\square$

---
## 예제

**예제 1 (구형파의 푸리에 급수):** 구형파(square wave) $f(x) = \begin{cases} -1, & -\pi < x < 0 \\ 1, & 0 < x < \pi \end{cases}$ (주기 $2\pi$)의 푸리에 급수를 구하라.

**풀이:** $f$는 기함수(odd function)이므로 $a_n = 0$ (모든 $n$). $b_n$만 계산한다:

$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin nx\,dx = \frac{1}{\pi} \left[ \int_{-\pi}^0 (-\sin nx)\,dx + \int_0^{\pi} \sin nx\,dx \right]$$

각 적분:

$$\int_{-\pi}^0 \sin nx\,dx = \left[-\frac{\cos nx}{n}\right]_{-\pi}^0 = -\frac{1}{n}(1 - \cos(-n\pi)) = -\frac{1}{n}(1 - (-1)^n)$$

$$\int_0^{\pi} \sin nx\,dx = \left[-\frac{\cos nx}{n}\right]_0^{\pi} = -\frac{1}{n}(\cos n\pi - 1) = -\frac{1}{n}((-1)^n - 1)$$

합하면:

$$b_n = \frac{1}{\pi} \left[ -(-\frac{1}{n})(1 - (-1)^n) + \frac{1}{n}(1 - (-1)^n) \right] = \frac{2}{n\pi}(1 - (-1)^n)$$

$n$이 짝수면 $b_n = 0$, $n$이 홀수면 $b_n = \frac{4}{n\pi}$.

푸리에 급수:

$$f(x) = \frac{4}{\pi} \sum_{k=0}^{\infty} \frac{\sin((2k+1)x)}{2k+1} = \frac{4}{\pi}\left(\sin x + \frac{1}{3}\sin 3x + \frac{1}{5}\sin 5x + \cdots\right)$$

$\square$

이 급수는 $x = \pi/2$에서 $\frac{\pi}{4} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots$라는 유명한 라이프니츠 급수(Leibniz series)를 유도한다.

**예제 2 ($e^{-|x|}$의 푸리에 변환):** $f(x) = e^{-|x|}$ ($x \in \mathbb{R}$)의 푸리에 변환을 구하라.

**풀이:** $f$는 우함수(even function)이므로 사인 항은 0이다.

$$\hat{f}(\omega) = \int_{-\infty}^{\infty} e^{-|x|} e^{-i\omega x}\,dx = \int_{-\infty}^0 e^{x} e^{-i\omega x}\,dx + \int_0^{\infty} e^{-x} e^{-i\omega x}\,dx$$

$$= \int_{-\infty}^0 e^{(1-i\omega)x}\,dx + \int_0^{\infty} e^{-(1+i\omega)x}\,dx = \left[ \frac{e^{(1-i\omega)x}}{1-i\omega} \right]_{-\infty}^0 + \left[ \frac{e^{-(1+i\omega)x}}{-(1+i\omega)} \right]_0^{\infty}$$

첫째 항: $x \to -\infty$에서 $e^{(1-i\omega)x} \to 0$이므로 $\frac{1}{1-i\omega}$.

둘째 항: $x \to \infty$에서 $e^{-(1+i\omega)x} \to 0$이므로 $\frac{1}{1+i\omega}$.

$$\hat{f}(\omega) = \frac{1}{1-i\omega} + \frac{1}{1+i\omega} = \frac{2}{1 + \omega^2}$$

$\square$

이 변환은 코시 분포(Cauchy distribution)의 특성함수와 연결된다. $e^{-|x|}$는 빠르게 감소하지만 $C^0$만($x=0$에서 미분 불가능)이며, 그 변환 $\frac{2}{1+\omega^2}$는 대수적으로 감소한다($|\omega| \to \infty$에서 $O(1/\omega^2)$).

**예제 3 (컨볼루션 정리 적용):** $f(x) = e^{-x^2/2}$와 $g(x) = e^{-x^2/2}$의 컨볼루션을 구하라. (가우시안 함수의 컨볼루션)

**풀이:** 가우시안의 푸리에 변환도 가우시안임이 알려져 있다:

$$\hat{f}(\omega) = \hat{g}(\omega) = \sqrt{2\pi} e^{-\omega^2/2}$$

컨볼루션 정리에 의해 $\widehat{f * g}(\omega) = \hat{f}(\omega)\hat{g}(\omega) = 2\pi e^{-\omega^2}$.

역변환: $2\pi e^{-\omega^2}$의 역푸리에 변환은 $\frac{1}{2\pi} \int 2\pi e^{-\omega^2} e^{i\omega x}\,d\omega = \int e^{-\omega^2} e^{i\omega x}\,d\omega$.

$\int e^{-\omega^2} e^{i\omega x}\,d\omega = \sqrt{\pi} e^{-x^2/4}$ (가우시안 적분 공식 활용).

따라서 $(f * g)(x) = \sqrt{\pi} e^{-x^2/4}$.

검증: $e^{-x^2/2} * e^{-x^2/2} = \sqrt{\pi} e^{-x^2/4}$으로, 두 가우시안의 컨볼루션은 분산이 합쳐진 가우시안이다. $\square$

**예제 4 (미분의 푸리에 변환):** 열방정식(heat equation) $u_t = u_{xx}$를 푸리에 변환으로 풀기 위한 기초를 마련하라.

**풀이:** 초기조건 $u(x,0) = f(x)$인 열방정식을 $x$에 대해 푸리에 변환한다. $t$는 매개변수로 취급:

$$\hat{u}_t(\omega, t) = \widehat{u_{xx}}(\omega, t) = (i\omega)^2 \hat{u}(\omega, t) = -\omega^2 \hat{u}(\omega, t)$$

이제 $t$에 대한 상미분방정식이 되었다:

$$\frac{\partial}{\partial t} \hat{u}(\omega, t) = -\omega^2 \hat{u}(\omega, t) \;\Longrightarrow\; \hat{u}(\omega, t) = \hat{f}(\omega) e^{-\omega^2 t}$$

역변환하면 $u(x,t) = \frac{1}{2\pi} \int \hat{f}(\omega) e^{-\omega^2 t} e^{i\omega x}\,d\omega = f * G_t$ ($G_t$는 가우시안 커널). $\square$

---
## 연결

- **[삼각함수](trigonometric-functions.html)** : 푸리에 급수의 기저 함수인 $\sin nx$와 $\cos nx$는 삼각함수에서 정의된다. 덧셈정리, 배각 공식이 직교성 증명에 사용된다.
- **[급수와 수렴](series-convergence.html)** : 푸리에 급수의 수렴($L^2$ 수렴, 점별 수렴, 깁스 현상)은 급수 이론의 핵심 응용이다. 함수의 푸리에 급수가 원래 함수로 수렴하는 조건은 해석학의 중요한 주제다.
- **[내적·노름·코사인 유사도](inner-product-norm.html)** : 푸리에 계수는 함수를 삼각 기저에 정사영한 결과이며, 이는 유한차원 내적공간의 투영(projection) 개념을 무한차원 함수공간으로 확장한 것이다.
- **[다중적분](multiple-integrals.html)** : 푸리에 변환의 컨볼루션 정리 증명에서 이중적분과 적분 순서 교환(푸비니 정리)이 사용된다.
