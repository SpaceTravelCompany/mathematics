---
title: 지수와 로그
slug: exponentials-logarithms
---

## 직관적 설명

**지수(exponential)** 는 "반복된 곱셈의 압축 표현"이다. $2^5$는 $2$를 다섯 번 곱하라는 명령을 한 줄로 줄인 것에 불과하지만, 이 아이디어를 정수에서 실수로, 나아가 복소수로 확장하면 전혀 새로운 세계가 열린다. **로그(logarithm)** 는 그 역연산으로, "몇 번 곱해야 목표에 도달하는가"를 묻는다. 로그는 곱셈을 덧셈으로 바꾸는 마법 같은 성질을 가지고 있어, 과거에는 계산자(slide rule)의 원리였고 오늘날에는 정보이론(information theory)에서 놀라움의 양(entropy)을 측정하는 도구가 된다. 자연상수 $e$는 미적분학에서 가장 아름다운 발견 중 하나로, $e^x$는 미분해도 자기 자신인 유일한 함수(상수배 무시)이다.

## 정의

**자연수 지수:** $a^n = a \times a \times \cdots \times a$ ($n$번 곱함).

**정수 지수로 확장:** $a^0 = 1$ ($a \neq 0$), $a^{-n} = \frac{1}{a^n}$.

**유리수 지수로 확장:** $a^{1/n} = \sqrt[n]{a}$, $a^{m/n} = (\sqrt[n]{a})^m$.

**실수 지수로 확장:** 무리수 $\alpha$에 대해서는 $a^\alpha$를 유리수 지수의 극한(limit)으로 정의한다. 즉, $\alpha$로 수렴하는 유리수열 $\{r_n\}$에 대해 $a^\alpha = \lim_{n\to\infty} a^{r_n}$.

**자연상수 $e$:**

$$e = \lim_{n\to\infty} \left(1 + \frac{1}{n}\right)^n \approx 2.71828\ldots$$

또는 동등하게 $e = \sum_{n=0}^{\infty} \frac{1}{n!}$ (테일러 급수).

**로그(logarithm):** $a > 0$, $a \neq 1$이고 $x > 0$일 때,

$$\log_a x = y \iff a^y = x$$

즉, $\log_a x$는 "$a$를 몇 번 곱해야 $x$가 되는가"를 답한다.

**자연로그(natural logarithm):** $\ln x = \log_e x$.

**상용로그(common logarithm):** $\log_{10} x$.

## 주요 정리와 증명

### 정리 1: 지수법칙 (Laws of Exponents)

$a > 0$, $b > 0$이고 $m, n$이 실수일 때 다음이 성립한다.

1. $a^m \cdot a^n = a^{m+n}$
2. $(a^m)^n = a^{mn}$
3. $(ab)^n = a^n b^n$
4. $\frac{a^m}{a^n} = a^{m-n}$ ($a \neq 0$)

**증명 (자연수 지수의 경우):** 자연수 $m, n$에 대해, $a^m \cdot a^n$은 $a$를 $m$번 곱한 것과 $n$번 곱한 것을 함께 곱한 것이므로 총 $m+n$번 곱한 것과 같다. 따라서 $a^m \cdot a^n = a^{m+n}$이다. 나머지 법칙들도 유사하게 곱셈의 정의에서 직접 유도된다. 실수 지수로의 확장은 극한을 통해 일관성을 유지한다.

### 정리 2: 로그법칙 (Laws of Logarithms)

$a > 0$, $a \neq 1$이고 $x, y > 0$일 때 다음이 성립한다.

1. $\log_a(xy) = \log_a x + \log_a y$
2. $\log_a\left(\frac{x}{y}\right) = \log_a x - \log_a y$
3. $\log_a(x^r) = r \log_a x$

**증명 (첫 번째 법칙):** $u = \log_a x$, $v = \log_a y$라 하자. 로그의 정의에 의해 $a^u = x$, $a^v = y$이다. 따라서

$$xy = a^u \cdot a^v = a^{u+v}$$

(지수법칙 사용). 다시 로그의 정의를 적용하면

$$\log_a(xy) = u + v = \log_a x + \log_a y$$

**밑변환 공식(change of base):**

$$\log_a x = \frac{\log_b x}{\log_b a}$$

**증명:** $\log_a x = y$라 하면 $a^y = x$이다. 양변에 $\log_b$를 취하면 $y \log_b a = \log_b x$. 따라서 $y = \frac{\log_b x}{\log_b a}$.

### 정리 3: $e^x$의 미분은 자기 자신

함수 $f(x) = e^x$는 $f'(x) = e^x$를 만족한다.

**증명 (극한 정의 사용):** 도함수의 정의에 의해

$$f'(x) = \lim_{h \to 0} \frac{e^{x+h} - e^x}{h} = \lim_{h \to 0} \frac{e^x e^h - e^x}{h} = e^x \lim_{h \to 0} \frac{e^h - 1}{h}$$

따라서 $\lim_{h \to 0} \frac{e^h - 1}{h} = 1$임을 보이면 된다.

$e$의 정의 $e = \lim_{n\to\infty} (1 + 1/n)^n$에서 $h = 1/n$으로 치환하면, $h \to 0$일 때 $n \to \infty$이다.

$$e = \lim_{h \to 0} (1 + h)^{1/h}$$

양변에 자연로그를 취하면 $\lim_{h \to 0} \frac{\ln(1+h)}{h} = 1$이다. 역함수 관계를 이용하여 $t = \ln(1+h)$, 즉 $h = e^t - 1$로 치환하면 $h \to 0$일 때 $t \to 0$이므로

$$\lim_{t \to 0} \frac{t}{e^t - 1} = 1 \;\Longrightarrow\; \lim_{t \to 0} \frac{e^t - 1}{t} = 1$$

따라서 $f'(x) = e^x \cdot 1 = e^x$이다.

## 예제

**예제 1:** 지수방정식 $2^{x+1} = 8$을 풀어라.

**풀이 1 (밑을 맞춤):** $8 = 2^3$이므로 $2^{x+1} = 2^3$이다. 밑이 같으므로 $x+1 = 3$, 따라서 $x = 2$.

**풀이 2 (로그 사용):** 양변에 $\log_2$를 취하면 $x+1 = \log_2 8 = 3$, 따라서 $x = 2$.

**예제 2:** 다음을 계산하라: $\log_2 32 + \log_3 81 - \log_5 1$.

**풀이:**
$\log_2 32 = \log_2 2^5 = 5$,
$\log_3 81 = \log_3 3^4 = 4$,
$\log_5 1 = 0$ (어떤 밑에서든 $\log_a 1 = 0$).
따라서 $5 + 4 - 0 = 9$.

**예제 3:** 연이율 5%의 복리 예금에 100만 원을 저금했을 때, 원리금이 200만 원이 되는 데 걸리는 시간을 구하라.

**풀이:** 복리 공식 $A = P(1 + r)^t$에서 $P = 100$, $A = 200$, $r = 0.05$이다.

$$200 = 100(1.05)^t \;\Rightarrow\; 2 = (1.05)^t$$

양변에 자연로그를 취한다.

$$\ln 2 = t \ln(1.05) \;\Rightarrow\; t = \frac{\ln 2}{\ln 1.05} \approx \frac{0.6931}{0.04879} \approx 14.21$$

약 14.2년 후에 원리금이 200만 원이 된다.

## 연결

- **[지수·로그 함수의 미분](topics/exp-log-calculus.html)** : 미적분학에서 $e^x$와 $\ln x$의 미분과 적분을 본격적으로 다룬다.
- **[엔트로피와 KL 발산](topics/entropy-kl.html)** : 정보량 $I(x) = -\log P(x)$는 로그로 정의되며, 엔트로피는 그 기댓값이다.
- **[수열과 급수 기초](topics/sequences-series.html)** : $e$의 정의는 수열의 극한이며, 지수함수는 등비수열의 연속 일반화이다.
