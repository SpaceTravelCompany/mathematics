---
title: 수열과 급수 기초
slug: sequences-series
---

## 직관적 설명

**수열(sequence)** 은 숫자를 순서대로 늘어놓은 것이다. 영화의 프레임처럼, 각 항목에는 위치(첫 번째, 두 번째, ...)가 있다. **급수(series)** 는 수열의 항들을 계속 더해나가는 것이다. 급수의 핵심 질문은 "무한히 더했을 때 유한한 값이 나오는가"이다. 이 질문은 고대 그리스의 제논의 역설(Zeno's paradox)에서 시작하여, 미적분학의 기초와 현대 해석학(analysis)의 출발점이 되었다. 무한급수는 함수를 다항식으로 근사하는 테일러 급수(Taylor series)의 기반이며, 확률론에서 중심극한정리(Central Limit Theorem)의 증명에도 등장한다.

## 정의

**수열(sequence):** 자연수 집합 $\mathbb{N}$에서 실수 집합 $\mathbb{R}$로 가는 함수 $a: \mathbb{N} \to \mathbb{R}$이다. $a(n)$ 대신 $a_n$으로 표기하고, 수열 전체를 $\{a_n\}_{n=1}^\infty$ 또는 간단히 $\{a_n\}$으로 나타낸다.

**등차수열(arithmetic sequence):** 연속한 두 항의 차이가 일정한 수열.

$$a_n = a_1 + (n-1)d$$

여기서 $d$를 **공차(common difference)** 라 한다.

**등비수열(geometric sequence):** 연속한 두 항의 비(ratio)가 일정한 수열.

$$a_n = a_1 r^{\,n-1}$$

여기서 $r$을 **공비(common ratio)** 라 한다.

**시그마 표기법(summation notation):**

$$\sum_{k=1}^{n} a_k = a_1 + a_2 + \cdots + a_n$$

**급수(series):** 수열 $\{a_n\}$의 항들을 순서대로 더한 것. **부분합(partial sum)** $S_N$과 **무한급수(infinite series)** 는 다음과 같이 정의된다.

$$S_N = \sum_{n=1}^{N} a_n, \qquad \sum_{n=1}^{\infty} a_n = \lim_{N\to\infty} S_N$$

**수렴(convergence):** 급수 $\sum a_n$이 수렴한다는 것은 극한 $\lim_{N\to\infty} S_N$이 유한한 값으로 존재한다는 뜻이다. 엄밀히: 임의의 $\epsilon > 0$에 대해 어떤 $N \in \mathbb{N}$이 존재하여 $m > n \geq N$이면 $|S_m - S_n| < \epsilon$이다 (코시 수렴 판정, Cauchy convergence criterion).

## 주요 정리와 증명

### 정리 1: 등차수열의 합

첫 항이 $a_1$, 공차가 $d$인 등차수열의 처음 $n$항까지의 합 $S_n$은

$$S_n = \frac{n(a_1 + a_n)}{2} = \frac{n[2a_1 + (n-1)d]}{2}$$

**증명:** 합을 순서대로 그리고 역순으로 써서 더한다.

$$S_n = a_1 + (a_1 + d) + (a_1 + 2d) + \cdots + (a_1 + (n-1)d)$$
$$S_n = a_n + (a_n - d) + (a_n - 2d) + \cdots + (a_n - (n-1)d)$$

두 식을 더하면 각 열의 합이 $a_1 + a_n$으로 일정하다.

$$2S_n = n(a_1 + a_n)$$

따라서 $S_n = \frac{n(a_1 + a_n)}{2} = \frac{n[2a_1 + (n-1)d]}{2}$.

### 정리 2: 등비수열의 합과 등비급수

첫 항이 $a_1$, 공비가 $r \neq 1$인 등비수열의 처음 $n$항까지의 합은

$$S_n = a_1 \frac{1 - r^n}{1 - r}$$

**증명:** $S_n = a_1 + a_1 r + a_1 r^2 + \cdots + a_1 r^{\,n-1}$에 $r$을 곱한다.

$$r S_n = a_1 r + a_1 r^2 + a_1 r^3 + \cdots + a_1 r^{\,n}$$

뺄셈 $S_n - r S_n = a_1 - a_1 r^{\,n}$이므로

$$S_n(1 - r) = a_1(1 - r^n) \;\Longrightarrow\; S_n = a_1 \frac{1 - r^n}{1 - r}$$

**등비급수:** $|r| < 1$일 때 $\lim_{n\to\infty} r^n = 0$이므로

$$\sum_{n=0}^{\infty} a_1 r^{\,n} = \lim_{n\to\infty} a_1 \frac{1 - r^{\,n}}{1 - r} = \frac{a_1}{1 - r}$$

|$r| \geq 1$이면 급수는 발산한다 (수렴하지 않는다).

### 정리 3: 수렴의 필요조건

급수 $\sum_{n=1}^{\infty} a_n$이 수렴하면 $\lim_{n\to\infty} a_n = 0$이다.

**증명:** 부분합 $S_N = \sum_{k=1}^{N} a_k$라 하자. 급수가 $S$로 수렴하면 $\lim_{N\to\infty} S_N = S$이다. $a_n = S_n - S_{n-1}$이므로

$$\lim_{n\to\infty} a_n = \lim_{n\to\infty} (S_n - S_{n-1}) = \lim_{n\to\infty} S_n - \lim_{n\to\infty} S_{n-1} = S - S = 0$$

**대우(contrapositive) 활용:** $\lim_{n\to\infty} a_n \neq 0$이면 급수 $\sum a_n$은 발산한다. 단, 이 조건은 필요조건일 뿐 충분조건은 아니다. 즉 $\lim a_n = 0$이어도 급수가 수렴하지 않을 수 있다 (예: 조화급수).

**조화급수(harmonic series)의 발산:**

$$\sum_{n=1}^{\infty} \frac{1}{n} = 1 + \frac{1}{2} + \frac{1}{3} + \frac{1}{4} + \cdots = \infty$$

**증명:** 항을 다음과 같이 묶는다.

$$1 + \frac{1}{2} + \left(\frac{1}{3} + \frac{1}{4}\right) + \left(\frac{1}{5} + \cdots + \frac{1}{8}\right) + \cdots$$

각 괄호 안의 합은 최소한 $\frac{1}{2}$이다. 예를 들어 $\frac{1}{3} + \frac{1}{4} > \frac{1}{4} + \frac{1}{4} = \frac{1}{2}$, $\frac{1}{5} + \cdots + \frac{1}{8} > \frac{1}{8} \times 4 = \frac{1}{2}$ 등. 따라서 $N$번째 부분합은 $1 + N \cdot \frac{1}{2}$보다 크므로 $N \to \infty$에서 발산한다. 이는 $a_n \to 0$이어도 급수가 수렴하지 않을 수 있음을 보여주는 대표적 반례이다.

## 예제

**예제 1:** 첫 항이 3, 공차가 4인 등차수열의 10번째 항과 처음 10항의 합을 구하라.

**풀이:** $a_1 = 3$, $d = 4$이므로 $a_{10} = 3 + 9 \cdot 4 = 39$.
$$S_{10} = \frac{10(3 + 39)}{2} = 5 \cdot 42 = 210$$

**예제 2:** 등비급수 $\sum_{n=0}^{\infty} \left(\frac{2}{3}\right)^n$의 합을 구하라.

**풀이:** 첫 항 $a_1 = 1$, 공비 $r = 2/3$이다. $|r| = 2/3 < 1$이므로

$$\sum_{n=0}^{\infty} \left(\frac{2}{3}\right)^n = \frac{1}{1 - 2/3} = \frac{1}{1/3} = 3$$

**예제 3:** 급수 $\sum_{n=1}^{\infty} \frac{2n}{n+1}$의 수렴 여부를 판정하라.

**풀이:** 일반항의 극한을 확인한다.

$$\lim_{n\to\infty} a_n = \lim_{n\to\infty} \frac{2n}{n+1} = \lim_{n\to\infty} \frac{2}{1 + 1/n} = 2 \neq 0$$

수렴의 필요조건에 의해 $\lim a_n \neq 0$이므로 이 급수는 발산한다.

## 연결

- **[급수와 수렴](series-convergence.html)** : 다양한 수렴 판정법(비교판정법, 비율판정법, 적분판정법)과 테일러 급수를 본격적으로 다룬다.
- **[중심극한정리](clt.html)** : 확률변수의 합이 정규분포로 수렴하는 과정은 급수와 수열 극한의 개념 위에 세워진다.
- **[지수와 로그](exponentials-logarithms.html)** : $e = \sum_{n=0}^\infty 1/n!$로 자연상수 $e$는 급수로 정의될 수 있다.
