---
title: 주요 분포
slug: distributions
---

## 직관적 설명

확률분포(probability distribution)는 "확률변수가 어떤 값들을 얼마나 자주 가지는지"를 완전히 기술한다. 현실에서 자주 마주치는 패턴들은 이름 붙은 분포로 정리되어 있다.

**베르누이 분포(Bernoulli distribution)**는 "예/아니오" 질문의 결과를 모델링한다. 동전 던지기, 성공/실패, 스팸/정상 메일 등이다.

**이항 분포(binomial distribution)**는 베르누이 시행을 $n$번 반복했을 때 성공 횟수를 센다. 10번의 동전 던지기에서 앞면이 3번 나올 확률 등에 사용된다.

**포아송 분포(Poisson distribution)**는 드문 사건이 단위 시간/공간에서 발생하는 횟수를 모델링한다. 시간당 평균 2건의 교통사고가 발생하는 교차로에서 1시간 동안 5건의 사고가 날 확률 같은 경우다.

**정규 분포(normal distribution, Gaussian)**는 자연과 사회에서 가장 널리 나타나는 분포다. 측정 오차, 키, 시험 점수 등 많은 현상이 종 모양(bell curve) 분포를 따른다. 중심극한정리에 의해, 독립 확률변수의 합은 어떤 분포를 따르든 정규분포로 수렴한다.

**지수 분포(exponential distribution)**는 "다음 사건이 발생할 때까지의 대기 시간"을 모델링한다. 전구의 수명, 지진 간격, 다음 손님의 도착 시간 등이 대표적이다. 이 분포의 핵심 성질은 **무기억성(memoryless property)**이다.

## 정의

**베르누이 분포 $\text{Ber}(p)$:** 성공($X=1$) 확률 $p$, 실패($X=0$) 확률 $1-p$.

$$P(X=x) = p^x(1-p)^{1-x},\quad x \in \{0,1\}$$

$\mathbb{E}[X] = p$, $\text{Var}(X) = p(1-p)$.

**이항 분포 $\text{Bin}(n,p)$:** $n$번의 독립 베르누이 시행에서 성공 횟수.

$$P(X=k) = \binom{n}{k} p^k (1-p)^{n-k},\quad k = 0, 1, \ldots, n$$

$\mathbb{E}[X] = np$, $\text{Var}(X) = np(1-p)$.

**포아송 분포 $\text{Pois}(\lambda)$:** 단위 시간당 평균 발생 횟수 $\lambda > 0$인 희귀 사건의 발생 횟수.

$$P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!},\quad k = 0, 1, 2, \ldots$$

$\mathbb{E}[X] = \lambda$, $\text{Var}(X) = \lambda$.

**균등 분포 $\text{U}(a,b)$:** 구간 $[a,b]$에서 모든 값이 같은 밀도로 나타남.

$$f(x) = \frac{1}{b-a},\quad a \leq x \leq b$$

$\mathbb{E}[X] = \frac{a+b}{2}$, $\text{Var}(X) = \frac{(b-a)^2}{12}$.

**정규 분포 $\mathcal{N}(\mu, \sigma^2)$:** 평균 $\mu$, 분산 $\sigma^2$의 종 모양 분포.

$$f(x) = \frac{1}{\sqrt{2\pi}\,\sigma} e^{-\frac{(x-\mu)^2}{2\sigma^2}},\quad x \in \mathbb{R}$$

$\mathbb{E}[X] = \mu$, $\text{Var}(X) = \sigma^2$.

**지수 분포 $\text{Exp}(\lambda)$:** 비율 $\lambda > 0$인 사건의 대기 시간.

**감마 분포 $\text{Gamma}(\alpha, \beta)$:** $\alpha$번의 지수분포 사건이 발생할 때까지의 대기 시간.

$$f(x) = \frac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x},\quad x \geq 0$$

$\mathbb{E}[X] = \alpha/\beta$, $\text{Var}(X) = \alpha/\beta^2$. $\alpha = 1$일 때 지수분포가 된다.

**베타 분포 $\text{Beta}(\alpha, \beta)$:** 구간 $[0,1]$에서 정의된 분포로, 확률 $p$의 사전분포로 자주 사용된다.

$$f(x) = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)},\quad 0 \leq x \leq 1$$

여기서 $B(\alpha,\beta) = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$는 베타 함수다. $\mathbb{E}[X] = \alpha/(\alpha+\beta)$.

$$f(x) = \lambda e^{-\lambda x},\quad x \geq 0$$

$F(x) = 1 - e^{-\lambda x}$ ($x \geq 0$). $\mathbb{E}[X] = 1/\lambda$, $\text{Var}(X) = 1/\lambda^2$.

## 주요 정리와 증명

### 정리 1: 이항분포의 포아송 근사 (Poisson Limit Theorem)

$n \to \infty$, $p \to 0$이고 $np \to \lambda > 0$일 때, $\text{Bin}(n,p)$는 $\text{Pois}(\lambda)$로 수렴한다.

**증명:** $p = \lambda/n$으로 두고 $n \to \infty$일 때의 극한을 계산하자.

$$
\begin{aligned}
P(X = k) &= \binom{n}{k} \left(\frac{\lambda}{n}\right)^k \left(1 - \frac{\lambda}{n}\right)^{n-k} \\
&= \frac{n!}{k!(n-k)!} \frac{\lambda^k}{n^k} \left(1 - \frac{\lambda}{n}\right)^n \left(1 - \frac{\lambda}{n}\right)^{-k}
\end{aligned}
$$

각 항을 분해하자.

$$\frac{n!}{(n-k)!\,n^k} = \frac{n(n-1)\cdots(n-k+1)}{n^k} = 1 \cdot \left(1 - \frac{1}{n}\right) \cdots \left(1 - \frac{k-1}{n}\right) \xrightarrow{n\to\infty} 1$$

$$\left(1 - \frac{\lambda}{n}\right)^n \xrightarrow{n\to\infty} e^{-\lambda}$$

$$\left(1 - \frac{\lambda}{n}\right)^{-k} \xrightarrow{n\to\infty} 1$$

따라서

$$\lim_{n\to\infty} P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}$$

이는 $\text{Pois}(\lambda)$의 PMF와 같다. $\square$

이 근사는 $n \geq 100$이고 $p \leq 0.05$일 때 실용적으로 정확하다.

### 정리 2: 정규분포 PDF의 적분값 = 1

정규분포 PDF는 적분 시 1이 된다.

$$\int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi}\,\sigma} e^{-\frac{(x-\mu)^2}{2\sigma^2}}\,dx = 1$$

**증명:** 표준정규분포 $\mathcal{N}(0,1)$의 경우만 보이면 충분하다 ($z = (x-\mu)/\sigma$ 치환). $I = \int_{-\infty}^{\infty} e^{-x^2/2}\,dx$라 하자.

$$I^2 = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} e^{-(x^2+y^2)/2}\,dx\,dy$$

극좌표 변환 $x = r\cos\theta$, $y = r\sin\theta$를 적용하면 야코비안 $r$이 곱해져

$$I^2 = \int_0^{2\pi} \int_0^{\infty} e^{-r^2/2} r\,dr\,d\theta = 2\pi \int_0^{\infty} r e^{-r^2/2}\,dr$$

$u = r^2/2$, $du = r\,dr$로 치환하면

$$I^2 = 2\pi \int_0^{\infty} e^{-u}\,du = 2\pi [-e^{-u}]_0^{\infty} = 2\pi$$

따라서 $I = \sqrt{2\pi}$이고, $\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty} e^{-x^2/2}\,dx = 1$이다. $\square$

### 정리 3: 지수분포의 무기억성 (Memoryless Property)

$X \sim \text{Exp}(\lambda)$에 대해 모든 $s, t \geq 0$에서

$$P(X > s + t \mid X > s) = P(X > t)$$

**증명:** 지수분포의 생존함수(survival function)는 $P(X > x) = e^{-\lambda x}$ ($x \geq 0$)이다. 조건부확률의 정의에 의해

$$
\begin{aligned}
P(X > s + t \mid X > s) &= \frac{P(X > s + t \cap X > s)}{P(X > s)} \\
&= \frac{P(X > s + t)}{P(X > s)} \quad (\text{since } s + t > s) \\
&= \frac{e^{-\lambda(s+t)}}{e^{-\lambda s}} = e^{-\lambda t} = P(X > t)
\end{aligned}
$$

$\square$

이는 지수분포의 고유한 성질이다. 기계의 수명이 지수분포를 따르면, $s$시간 동안 고장 나지 않았다는 사실이 앞으로 $t$시간 더 생존할 확률에 아무 영향도 주지 않는다.

### 정리 4: 표준화 (Standardization)

$X \sim \mathcal{N}(\mu, \sigma^2)$이면 $Z = \frac{X - \mu}{\sigma} \sim \mathcal{N}(0, 1)$이다.

**증명:** $Z$의 CDF를 구하자.

$$F_Z(z) = P\left(\frac{X - \mu}{\sigma} \leq z\right) = P(X \leq \mu + \sigma z) = F_X(\mu + \sigma z)$$

양변을 $z$로 미분하면 $Z$의 PDF를 얻는다.

$$f_Z(z) = F'_Z(z) = F'_X(\mu + \sigma z) \cdot \sigma = f_X(\mu + \sigma z) \cdot \sigma$$

$f_X(x) = \frac{1}{\sqrt{2\pi}\sigma} e^{-(x-\mu)^2/2\sigma^2}$을 대입하면

$$f_Z(z) = \frac{1}{\sqrt{2\pi}\sigma} e^{-((\mu+\sigma z)-\mu)^2/2\sigma^2} \cdot \sigma = \frac{1}{\sqrt{2\pi}} e^{-z^2/2}$$

이는 $\mathcal{N}(0,1)$의 PDF다. $\square$

## 예제

**예제 1 (이항→포아송 근사):** 어떤 웹사이트에 평균적으로 100명 중 3명이 방문하여 구매한다. 100명의 방문자 중 정확히 5명이 구매할 확률을 이항분포와 포아송 근사로 각각 구하고 비교하라.

**풀이:** $X \sim \text{Bin}(100, 0.03)$.

이항분포: $P(X=5) = \binom{100}{5}(0.03)^5(0.97)^{95} \approx 0.1013$

포아송 근사: $\lambda = np = 3$이므로 $P(X=5) \approx \frac{3^5 e^{-3}}{5!} = \frac{243 \times 0.0498}{120} \approx 0.1008$

두 값이 매우 가깝다 ($p = 0.03$이고 $n=100$이면 근사 조건 충족).

**예제 2 (정규분포 68-95-99.7 법칙):** $X \sim \mathcal{N}(\mu, \sigma^2)$일 때

$$P(\mu - \sigma \leq X \leq \mu + \sigma) \approx 0.6827$$
$$P(\mu - 2\sigma \leq X \leq \mu + 2\sigma) \approx 0.9545$$
$$P(\mu - 3\sigma \leq X \leq \mu + 3\sigma) \approx 0.9973$$

이는 표준정규분포의 CDF $\Phi(z)$를 이용해 계산한다. 예를 들어 첫 번째는 $\Phi(1) - \Phi(-1) = 2\Phi(1) - 1 \approx 0.6827$이다.

**예제 3 (지수분포 대기시간):** 한 은행 창구의 평균 서비스 시간이 3분이다(즉 $\lambda = 1/3$). 다음 고객이 5분 이상 기다릴 확률은?

**풀이:** 서비스 시간 $X \sim \text{Exp}(1/3)$.

$$P(X > 5) = e^{-(1/3) \cdot 5} = e^{-5/3} \approx 0.1889$$

약 18.9%다. 또한 이전 고객이 이미 2분 동안 서비스를 받고 있어도, 다음 5분을 더 기다려야 할 확률은 역시 $P(X > 5) = e^{-5/3}$으로 동일하다(무기억성).

**예제 4 (정규분포의 선형 결합):** $X \sim \mathcal{N}(2, 9)$이고 $Y \sim \mathcal{N}(1, 4)$가 독립일 때, $Z = 2X - 3Y$의 분포는?

**풀이:** 정규분포의 선형 결합은 정규분포다.
- $\mathbb{E}[Z] = 2\mathbb{E}[X] - 3\mathbb{E}[Y] = 2 \times 2 - 3 \times 1 = 1$
- $\text{Var}(Z) = 2^2\text{Var}(X) + (-3)^2\text{Var}(Y) = 4 \times 9 + 9 \times 4 = 72$

따라서 $Z \sim \mathcal{N}(1, 72)$이다.

**예제 5 (포아송 분포 — 희귀 질환):** 어떤 희귀 질환이 연간 인구 100,000명당 평균 2건 발생한다. 특정 해에 100,000명의 도시에서 이 질환이 0건 발생할 확률은?

**풀이:** $X \sim \text{Pois}(2)$.

$$P(X=0) = \frac{2^0 e^{-2}}{0!} = e^{-2} \approx 0.1353$$

약 13.5%다.

## 연결

- **[경우의 수](topics/counting.html)** : 이항분포의 계수 $\binom{n}{k}$는 조합론에서 나온다. $n$번 중 $k$번 성공하는 순서 조합의 수가 확률 계산의 핵심이다.
- **[중심극한정리](topics/clt.html)** : 정규분포가 특별한 이유는 CLT 때문이다. 이항분포도 $n$이 크면 정규분포로 근사된다(드무아브르-라플라스 정리).
- **[최대가능도추정](topics/mle.html)** : 각 분포의 모수(parameter)는 MLE로 추정된다. $p, \lambda, \mu, \sigma^2$ 등의 추정량은 데이터로부터 계산된다.
