---
title: 급수와 수렴
slug: series-convergence
---

## 직관적 설명

**급수(series)** 는 "무한히 많은 항을 더하는 것"이다. 직관적으로는 무한대를 더하면 무한대로 발산할 것 같지만, 항이 충분히 빠르게 작아지면 합이 유한한 값에 **수렴(converge)** 할 수 있다. 예를 들어 $\sum_{n=1}^{\infty} 1/2^n = 1$은 반으로 자르는 종이를 계속 더해도 전체가 1을 넘지 않는다는 사실과 같다.

급수의 핵심 질문은 세 가지다: (1) 수렴하는가? (2) 수렴한다면 얼마인가? (3) 얼마나 빠르게 수렴하는가? 첫 번째 질문에 답하기 위해 다양한 판정법(comparison test, ratio test, integral test)이 개발되었다.

**멱급수(power series)** $\sum c_n (x-a)^n$는 함수를 "무한차 다항식"으로 표현하는 방법이다. **테일러 급수(Taylor series)** 는 함수의 국소적 정보(한 점에서의 모든 도함수 값)로부터 멱급수를 구성하여 함수 전체를 재구성한다. 이는 다항함수만 다룰 수 있었던 시대에서 삼각함수, 지수함수, 로그함수 등 모든 함수를 "계산 가능한 다항식의 극한"으로 다루는 패러다임 전환을 가져왔다.

**절대수렴(absolute convergence)** 은 급수의 각 항에 절댓값을 취한 급수가 수렴하는 경우이고, **조건수렴(conditional convergence)** 은 원래 급수는 수렴하지만 절댓값 급수는 발산하는 경우다. 조건수렴 급수는 항의 순서를 바꾸면 합이 달라질 수 있다는 놀라운 성질(리만 재배열 정리, Riemann rearrangement theorem)이 있다.

---
## 정의

**급수(series):** 수열 $\{a_n\}$에 대해 무한급수 $\sum_{n=0}^{\infty} a_n$은 부분합(partial sum) $S_N = \sum_{n=0}^N a_n$의 극한으로 정의된다.

$$\sum_{n=0}^{\infty} a_n = \lim_{N \to \infty} S_N$$

극한이 유한하게 존재하면 **수렴(convergent)** 한다고 하고, 그 극한값을 급수의 합이라 한다. 극한이 존재하지 않거나 무한대이면 **발산(divergent)** 한다.

**절대수렴(absolute convergence):** $\sum_{n=0}^{\infty} |a_n|$이 수렴하면 $\sum a_n$은 절대수렴한다고 한다. 절대수렴은 원래 급수의 수렴을 함의한다(절대수렴 $\Rightarrow$ 수렴).

**조건수렴(conditional convergence):** $\sum a_n$은 수렴하지만 $\sum |a_n|$은 발산하는 경우를 조건수렴이라 한다. 대표적인 예로 교대급수(alternating series) $\sum (-1)^n / n$이 있다.

**멱급수(power series):** $a$를 중심으로 하는 멱급수는 $\sum_{n=0}^{\infty} c_n (x - a)^n$ 형태의 급수이다. 여기서 $c_n$은 계수(coefficient)이다.

**수렴반경(radius of convergence) $R$:** 멱급수 $\sum c_n (x-a)^n$에 대해, $|x-a| < R$이면 급수가 절대수렴하고 $|x-a| > R$이면 발산하는 $R \geq 0$이 존재한다. $R = \infty$이면 모든 $x$에서 수렴한다. 경계 $|x-a| = R$에서의 수렴 여부는 별도로 판정해야 한다.

**하다마르 공식(Hadamard formula):** 수렴반경은 다음 공식으로 주어진다.

$$\frac{1}{R} = \limsup_{n \to \infty} |c_n|^{1/n}$$

(단, $0$과 $\infty$를 허용하는 관례에 따라 계산한다.)

**테일러 급수(Taylor series):** 함수 $f$가 $x = a$에서 무한히 미분가능할 때,

$$f(x) = \sum_{n=0}^{\infty} \frac{f^{(n)}(a)}{n!} (x - a)^n$$

이 급수를 $f$의 $a$에서의 테일러 급수라 한다. $a = 0$인 경우를 특별히 **매클로린 급수(Maclaurin series)** 라 부른다.

**테일러 정리(Taylor's theorem)와 나머지 항:** $f$가 $a$를 포함하는 구간에서 $n+1$번 미분가능하면,

$$f(x) = \sum_{k=0}^{n} \frac{f^{(k)}(a)}{k!} (x - a)^k + R_n(x)$$

여기서 $R_n(x)$는 나머지 항(remainder)이다. 라그랑주 형태(Lagrange form)의 나머지:

$$R_n(x) = \frac{f^{(n+1)}(c)}{(n+1)!} (x - a)^{n+1}$$

단, $c$는 $x$와 $a$ 사이에 존재하는 어떤 값이다.

---
## 주요 정리와 증명

### 정리 1: 수렴의 필요조건 (Necessary Condition for Convergence)

급수 $\sum_{n=1}^{\infty} a_n$이 수렴하면 $\lim_{n \to \infty} a_n = 0$이다.

**증명:** 부분합 $S_N = \sum_{k=1}^N a_k$라 하자. 급수가 $S$로 수렴한다는 것은 $\lim_{N \to \infty} S_N = S$임을 의미한다. $a_n = S_n - S_{n-1}$이므로

$$\lim_{n \to \infty} a_n = \lim_{n \to \infty} (S_n - S_{n-1}) = \lim_{n \to \infty} S_n - \lim_{n \to \infty} S_{n-1} = S - S = 0$$

$\square$

**중요:** 이 조건은 필요조건일 뿐 충분조건이 아니다. $\lim a_n = 0$이어도 급수가 발산할 수 있다. 대표적인 반례가 조화급수(harmonic series) $\sum 1/n$으로, $a_n \to 0$이지만 급수는 발산한다.

**대우(contrapositive) 활용:** $\lim_{n \to \infty} a_n \neq 0$이면 $\sum a_n$은 발산한다. 이는 발산 판정의 가장 간단한 도구다.

### 정리 2: 비교판정법 (Comparison Test)

$0 \leq a_n \leq b_n$ for all $n$이라 하자.

1. $\sum b_n$이 수렴하면 $\sum a_n$도 수렴한다.
2. $\sum a_n$이 발산하면 $\sum b_n$도 발산한다.

**증명:** $A_N = \sum_{k=1}^N a_k$, $B_N = \sum_{k=1}^N b_k$라 하자. $0 \leq a_n \leq b_n$이므로 $A_N \leq B_N$이다. 두 부분합 수열은 단조증가하므로(항이 음수가 아니므로) 수렴 여부는 유계성(boundedness)에 달려있다.

1. $\sum b_n$이 수렴하면 $\{B_N\}$은 위로 유계이다. $\{A_N\}$도 위로 유계이므로( $A_N \leq B_N$) 수렴한다.
2. $\sum a_n$이 발산하면 $\{A_N\}$은 위로 유계가 아니다. $\{B_N\} \geq \{A_N\}$이므로 $\{B_N\}$도 위로 유계가 아니며, 따라서 $\sum b_n$도 발산한다.

$\square$

**극한 비교판정법(Limit Comparison Test):** $a_n, b_n > 0$이고 $\lim_{n \to \infty} a_n/b_n = L$ ($0 < L < \infty$)이면 $\sum a_n$과 $\sum b_n$은 수렴성을 공유한다.

### 정리 3: 비판정법 (Ratio Test)

$\lim_{n \to \infty} \left| \frac{a_{n+1}}{a_n} \right| = L$이라 하자.

- $L < 1$이면 $\sum a_n$은 절대수렴한다.
- $L > 1$이면 $\sum a_n$은 발산한다.
- $L = 1$이면 판정이 불가능하다.

**증명 ( $L < 1$인 경우):** $L < r < 1$인 $r$을 선택하자. 충분히 큰 $N$에 대해 $n \geq N$이면 $\left| \frac{a_{n+1}}{a_n} \right| \leq r$이다. 따라서

$$|a_{N+1}| \leq r|a_N|,\; |a_{N+2}| \leq r|a_{N+1}| \leq r^2|a_N|,\; \ldots$$

일반적으로 $|a_{N+k}| \leq r^k |a_N|$이다. 따라서

$$\sum_{n=N}^{\infty} |a_n| \leq |a_N| \sum_{k=0}^{\infty} r^k = \frac{|a_N|}{1 - r} < \infty$$

등비급수 $\sum r^k$가 $r < 1$에서 수렴하므로, 비교판정법에 의해 $\sum |a_n|$도 수렴한다. 즉 $\sum a_n$은 절대수렴한다.

**증명 ( $L > 1$인 경우):** $L > r > 1$인 $r$을 선택하자. 충분히 큰 $n$에 대해 $\left| \frac{a_{n+1}}{a_n} \right| \geq r > 1$이므로 $|a_n|$은 증가하고 0으로 수렴하지 않는다. 수렴의 필요조건에 의해 $\sum a_n$은 발산한다.

**참고:** $L = 1$일 때 판정이 불가능한 이유는 $\sum 1/n$(발산)과 $\sum 1/n^2$(수렴) 모두 $L = 1$을 만족하기 때문이다.

### 정리 4: 근 판정법 (Root Test)

$\limsup_{n \to \infty} |a_n|^{1/n} = L$이라 하자.

- $L < 1$이면 $\sum a_n$은 절대수렴한다.
- $L > 1$이면 $\sum a_n$은 발산한다.
- $L = 1$이면 판정이 불가능하다.

**증명 ( $L < 1$인 경우):** $L < r < 1$인 $r$을 선택하자. $\limsup$의 정의에 의해 충분히 큰 $N$에 대해 $n \geq N$이면 $|a_n|^{1/n} \leq r$, 즉 $|a_n| \leq r^n$이다. $\sum r^n$은 $r < 1$에서 수렴하는 등비급수이므로, 비교판정법에 의해 $\sum |a_n|$은 수렴한다. 따라서 $\sum a_n$은 절대수렴한다.

**증명 ( $L > 1$인 경우):** 충분히 큰 $n$에 대해 $|a_n|^{1/n} \geq 1$, 즉 $|a_n| \geq 1$이므로 $a_n$은 0으로 수렴하지 않는다. 수렴의 필요조건에 의해 급수는 발산한다.

근 판정법은 비판정법보다 더 강력한 경우가 있는데, 특히 계수가 $n^n$ 형태로 나타날 때 유용하다. 예를 들어 $\sum \frac{x^n}{n^n}$의 수렴반경은 근 판정법으로 $\lim (|x|^n / n^n)^{1/n} = \lim |x|/n = 0$이므로 $R = \infty$이다.

### 정리 5: 적분 판정법 (Integral Test)

$f$가 $[1, \infty)$에서 연속이고 양수이며 단조감소하는 함수라고 하자. $a_n = f(n)$일 때

$$\sum_{n=1}^{\infty} a_n \text{ 수렴 } \iff \int_1^{\infty} f(x)\,dx \text{ 수렴 }$$

**증명:** $f$가 단조감소하므로 $k \leq x \leq k+1$에서 $f(k+1) \leq f(x) \leq f(k)$이다. 각 구간에서 적분하면

$$f(k+1) \leq \int_k^{k+1} f(x)\,dx \leq f(k)$$

$k = 1$부터 $N$까지 합하면

$$\sum_{k=2}^{N+1} f(k) \leq \int_1^{N+1} f(x)\,dx \leq \sum_{k=1}^{N} f(k)$$

즉 $S_{N+1} - a_1 \leq I_{N+1} \leq S_N$이다. 급수의 부분합 $S_N$이 유계인 것과 적분 $I_{N+1}$이 유계인 것이 동치이므로, 둘 다 같은 수렴성을 가진다. $\square$

적분 판정법은 $p$-급수 $\sum 1/n^p$의 수렴을 판정하는 가장 간단한 방법을 제공한다.

### 정리 6: 교대급수 판정법 (Alternating Series Test)

$a_n \geq 0$이 단조감소하고 $\lim_{n \to \infty} a_n = 0$이면 $\sum_{n=1}^{\infty} (-1)^{n-1} a_n$은 수렴한다.

**증명:** 부분합 $S_{2n}$과 $S_{2n+1}$을 고려한다. $S_{2n} = S_{2n-2} + a_{2n-1} - a_{2n} \geq S_{2n-2}$이므로 짝수 부분합은 단조증가한다. 또한 $S_{2n+1} = S_{2n-1} - a_{2n} + a_{2n+1} \leq S_{2n-1}$이므로 홀수 부분합은 단조감소한다. $S_2 \leq S_4 \leq \cdots \leq S_5 \leq S_3 \leq S_1$이므로 두 부분합 수열은 같은 극한으로 수렴하며, 따라서 전체 급수는 수렴한다.

### 정리 7: 테일러 정리 (Taylor's Theorem with Lagrange Remainder)

$f$가 $a$를 포함하는 열린구간에서 $n+1$번 미분가능하면, $x$와 $a$ 사이에 존재하는 어떤 $c$에 대해

$$f(x) = \sum_{k=0}^{n} \frac{f^{(k)}(a)}{k!} (x - a)^k + \frac{f^{(n+1)}(c)}{(n+1)!} (x - a)^{n+1}$$

**증명 (코시 평균값 정리 반복 적용):** $R_n(x) = f(x) - \sum_{k=0}^n \frac{f^{(k)}(a)}{k!} (x-a)^k$라 정의하자. 함수 $g(t) = (x - t)^{n+1}$에 대해 $R_n(x)$와 $g(x)$에 코시 평균값 정리(Cauchy Mean Value Theorem)를 반복 적용한다.

더 간단한 접근: 구간 $[a, x]$에서 함수

$$F(t) = f(x) - \sum_{k=0}^n \frac{f^{(k)}(t)}{k!} (x - t)^k, \quad G(t) = (x - t)^{n+1}$$

을 정의한다. $F(a) = R_n(x)$, $F(x) = 0$, $G(a) = (x - a)^{n+1}$, $G(x) = 0$이다. 코시 평균값 정리에 의해 $\frac{F(a) - F(x)}{G(a) - G(x)} = \frac{F'(c)}{G'(c)}$인 $c \in (a, x)$가 존재한다. $F'(t) = -\frac{f^{(n+1)}(t)}{n!} (x - t)^n$이고 $G'(t) = -(n+1)(x - t)^n$임을 계산하면

$$\frac{R_n(x)}{(x - a)^{n+1}} = \frac{f^{(n+1)}(c)}{(n+1)!}$$

을 얻는다. 따라서 $R_n(x) = \frac{f^{(n+1)}(c)}{(n+1)!} (x - a)^{n+1}$이다. $\square$

### 주요 테일러 급수 전개

다음은 중요한 함수들의 $a = 0$에서의 테일러(매클로린) 급수 전개이다.

$$e^x = \sum_{n=0}^{\infty} \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots, \quad R = \infty$$

$$\sin x = \sum_{n=0}^{\infty} \frac{(-1)^n x^{2n+1}}{(2n+1)!} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots, \quad R = \infty$$

$$\cos x = \sum_{n=0}^{\infty} \frac{(-1)^n x^{2n}}{(2n)!} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots, \quad R = \infty$$

$$\frac{1}{1 - x} = \sum_{n=0}^{\infty} x^n = 1 + x + x^2 + x^3 + \cdots, \quad R = 1 \quad (|x| < 1)$$

$$\ln(1 + x) = \sum_{n=1}^{\infty} \frac{(-1)^{n-1} x^n}{n} = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots, \quad R = 1$$

---
## 예제

**예제 1 (비교판정법):** 급수 $\sum_{n=1}^{\infty} \frac{1}{n^2}$의 수렴을 비교판정법으로 증명하라.

**풀이:** $n \geq 2$에 대해 $\frac{1}{n^2} \leq \frac{1}{n(n-1)}$이다. 부분분수 분해(partial fraction decomposition)를 이용한다.

$$\sum_{n=2}^{\infty} \frac{1}{n(n-1)} = \sum_{n=2}^{\infty} \left( \frac{1}{n-1} - \frac{1}{n} \right)$$

이는 망원급수(telescoping series)로, 부분합이 $S_N = 1 - \frac{1}{N} \to 1$로 수렴한다.

$$\sum_{n=2}^{\infty} \frac{1}{n(n-1)} = 1 < \infty$$

비교판정법에 의해 $0 \leq \frac{1}{n^2} \leq \frac{1}{n(n-1)}$이므로 $\sum 1/n^2$도 수렴한다. (실제 값은 $\sum_{n=1}^{\infty} 1/n^2 = \pi^2/6$으로 알려져 있다 — 바젤 문제, Basel problem.)

**예제 2 (조건수렴):** 교대급수 $\sum_{n=1}^{\infty} \frac{(-1)^n}{n}$의 수렴 여부와 절대수렴 여부를 판정하라.

**풀이:** $a_n = (-1)^n / n$에 대해 $\sum |a_n| = \sum 1/n$은 조화급수로 발산한다. 따라서 절대수렴하지 않는다.

그러나 원래 급수는 교대급수 판정법(Alternating Series Test)에 의해 수렴한다. $b_n = 1/n$이 단조감소하고 0으로 수렴하므로, 라이프니츠 판정법(Leibniz test)에 의해 $\sum (-1)^n / n$은 수렴한다. (그 합은 $-\ln 2$이다.)

따라서 $\sum (-1)^n / n$은 조건수렴(conditionally convergent)한다. 이 급수는 항의 순서를 재배열하면 임의의 실수로 수렴하게 할 수 있으며(리만 재배열 정리), 이는 조건수렴 급수의 놀라운 성질이다.

**예제 3 (테일러 급수로 $e$ 근사):** $e^x$의 테일러 급수를 이용하여 $e$의 값을 오차 $10^{-4}$ 이내로 근사하라.

**풀이:** $e^x = \sum_{k=0}^{\infty} \frac{x^k}{k!}$에서 $x = 1$을 대입하면 $e = \sum_{k=0}^{\infty} \frac{1}{k!}$이다.

$n$차 근사 $S_n = \sum_{k=0}^n \frac{1}{k!}$의 오차는 라그랑주 나머지로 추정한다. $f^{(n+1)}(c) = e^c$이고 $c \in (0, 1)$이므로 $e^c < 3$이다.

$$|R_n(1)| = \frac{e^c}{(n+1)!} < \frac{3}{(n+1)!}$$

$\frac{3}{(n+1)!} < 10^{-4}$가 되려면 $(n+1)! > 30000$이어야 한다. $8! = 40320$이므로 $n = 7$이면 충분하다.

$$e \approx \sum_{k=0}^{7} \frac{1}{k!} = 1 + 1 + \frac{1}{2} + \frac{1}{6} + \frac{1}{24} + \frac{1}{120} + \frac{1}{720} + \frac{1}{5040}$$

$$= 2 + 0.5 + 0.1666667 + 0.0416667 + 0.0083333 + 0.0013889 + 0.0001984 = 2.718254$$

실제 $e \approx 2.7182818$과 비교하면 오차가 약 $2.78 \times 10^{-5}$로 $10^{-4}$ 이내다.

**예제 4 (수렴반경 계산):** 멱급수 $\sum_{n=1}^{\infty} \frac{x^n}{n^2}$의 수렴반경을 구하라.

**풀이:** 비판정법을 사용한다.

$$\lim_{n \to \infty} \left| \frac{a_{n+1}}{a_n} \right| = \lim_{n \to \infty} \left| \frac{x^{n+1}}{(n+1)^2} \cdot \frac{n^2}{x^n} \right| = \lim_{n \to \infty} |x| \cdot \frac{n^2}{(n+1)^2} = |x|$$

비판정법에 의해 $|x| < 1$에서 절대수렴, $|x| > 1$에서 발산한다. $|x| = 1$일 때는 $\sum 1/n^2$이 되어 수렴한다. 따라서 수렴반경 $R = 1$, 수렴구간은 $[-1, 1]$이다.

하다마르 공식으로도 확인: $c_n = 1/n^2$이므로 $|c_n|^{1/n} = (1/n^{2/n}) \to 1^0 = 1$이다. 따라서 $1/R = 1$, $R = 1$.

**예제 5 (적분 판정법):** 급수 $\sum_{n=2}^{\infty} \frac{1}{n \ln n}$의 수렴 여부를 판정하라.

**풀이:** $f(x) = \frac{1}{x \ln x}$는 $[2, \infty)$에서 양수이고 연속이며 단조감소한다. 이상적분을 평가한다.

$$\int_2^{\infty} \frac{1}{x \ln x}\,dx = \lim_{b \to \infty} \int_2^b \frac{1}{x \ln x}\,dx$$

$u = \ln x$로 치환하면 $du = \frac{1}{x}\,dx$이므로

$$\int \frac{1}{x \ln x}\,dx = \int \frac{1}{u}\,du = \ln|u| + C = \ln(\ln x) + C$$

따라서

$$\int_2^{\infty} \frac{1}{x \ln x}\,dx = \lim_{b \to \infty} [\ln(\ln b) - \ln(\ln 2)] = \infty$$

적분이 발산하므로 적분 판정법에 의해 $\sum_{n=2}^{\infty} \frac{1}{n \ln n}$도 발산한다.

**예제 6 (근 판정법):** $\sum_{n=1}^{\infty} \left( \frac{n}{n+1} \right)^{n^2}$의 수렴 여부를 판정하라.

**풀이:** 근 판정법을 적용한다.

$$|a_n|^{1/n} = \left( \frac{n}{n+1} \right)^{n} = \left(1 + \frac{1}{n}\right)^{-n} = \frac{1}{(1 + 1/n)^n} \to \frac{1}{e} < 1$$

극한이 $1/e < 1$이므로 급수는 절대수렴한다.

**예제 7 (멱급수의 수렴반경과 수렴구간):** $\sum_{n=1}^{\infty} \frac{(-1)^n x^n}{\sqrt{n}}$의 수렴반경과 수렴구간을 구하라.

**풀이:** 비판정법으로 수렴반경을 먼저 찾는다.

$$\lim_{n \to \infty} \left| \frac{a_{n+1}}{a_n} \right| = \lim_{n \to \infty} \left| \frac{x^{n+1}}{\sqrt{n+1}} \cdot \frac{\sqrt{n}}{x^n} \right| = \lim_{n \to \infty} |x| \sqrt{\frac{n}{n+1}} = |x|$$

비판정법에 의해 $|x| < 1$에서 절대수렴, $|x| > 1$에서 발산하므로 $R = 1$이다.

경계 $x = 1$에서 급수는 $\sum (-1)^n / \sqrt{n}$이 된다. 이는 교대급수이며 $1/\sqrt{n} \to 0$ 단조감소하므로 교대급수 판정법에 의해 수렴한다. 그러나 $\sum |(-1)^n / \sqrt{n}| = \sum 1/n^{1/2}$는 $p = 1/2 < 1$인 $p$-급수이므로 발산한다. 따라서 $x = 1$에서 조건수렴한다.

경계 $x = -1$에서 급수는 $\sum (-1)^n (-1)^n / \sqrt{n} = \sum 1/\sqrt{n}$이므로 발산한다. 따라서 수렴구간은 $(-1, 1]$이다.

**예제 8 (멱급수의 미분과 적분):** $\frac{1}{1-x} = \sum_{n=0}^{\infty} x^n$을 항별로 적분하여 $\ln(1-x)$의 멱급수 전개를 유도하라.

**풀이:** $|x| < 1$에서 $\frac{1}{1-x} = \sum_{n=0}^{\infty} x^n$이다. 양변을 0부터 $x$까지 적분한다.

$$\int_0^x \frac{1}{1-t}\,dt = \int_0^x \sum_{n=0}^{\infty} t^n\,dt = \sum_{n=0}^{\infty} \int_0^x t^n\,dt = \sum_{n=0}^{\infty} \frac{x^{n+1}}{n+1} = \sum_{n=1}^{\infty} \frac{x^n}{n}$$

좌변은 $-\ln(1-x)$이므로

$$-\ln(1-x) = \sum_{n=1}^{\infty} \frac{x^n}{n} \quad\Rightarrow\quad \ln(1-x) = -\sum_{n=1}^{\infty} \frac{x^n}{n}$$

$x$ 대신 $-x$를 대입하면 $\ln(1+x) = \sum_{n=1}^{\infty} \frac{(-1)^{n-1} x^n}{n}$을 얻는다. 이는 앞서 제시한 $\ln(1+x)$의 전개와 일치한다.

---
## 연결

- **[수열과 급수 기초](sequences-series.html)** : 급수의 기본 개념(부분합, 등비급수, 조화급수, 수렴 필요조건)이 선행되어야 한다.
- **[테일러 전개](taylor-expansion.html)** : 테일러 급수는 함수의 근사와 멱급수 전개의 핵심 도구이며, 다변수 함수의 2차 근사까지 확장된다.
- **[푸리에 급수·푸리에 변환](fourier.html)** : 함수를 삼각함수의 급수로 전개하는 푸리에 급수는 테일러 급수와 다른 각도에서 함수를 분해하며, 멱급수와 함께 해석학의 양대 급수 전개 이론을 이룬다.
