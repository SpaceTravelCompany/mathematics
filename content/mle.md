---
title: 최대가능도추정 MLE
slug: mle
---

## 직관적 설명

**최대가능도추정(maximum likelihood estimation, MLE)**은 "지금 관측된 데이터가 나올 확률을 가장 높게 만드는 모수(parameter)를 찾는 방법"이다. 동전을 10번 던져 7번 앞면이 나왔다면, "이런 결과가 가장 자연스러운" 앞면 확률 $p$는 얼마일까? 직관적으로 $p=0.7$이 가장 합리적으로 보인다. MLE는 이 직관을 엄밀한 수학으로 만든 것이다.

가능도(likelihood)는 확률과 같지만 **관점이 다르다**. 확률은 모수가 고정되고 데이터가 변하는 관점 $P(\text{data}|\theta)$라면, 가능도는 데이터가 고정되고 모수가 변하는 관점 $L(\theta|\text{data})$이다. 즉 "데이터는 이미 주어졌고, 어떤 $\theta$가 이 데이터를 가장 잘 설명하는가"를 묻는다.

**점추정(point estimation)**은 모수를 하나의 값으로 추정하는 것이고, **구간추정(interval estimation)**은 신뢰구간(confidence interval)으로 추정의 불확실성을 함께 제시한다. MLE는 점추정의 대표적인 방법이다.

---
## 정의

**가능도함수(likelihood function):** $n$개의 i.i.d.(independent and identically distributed) 확률변수 $X_1, \ldots, X_n$이 PDF/PMF $f(x|\theta)$를 따를 때

$$L(\theta) = L(\theta; x_1, \ldots, x_n) = \prod_{i=1}^n f(x_i|\theta)$$

$\theta$는 추정할 모수(parameter)다.

**로그 가능도(log-likelihood):** 곱(product)을 합(sum)으로 바꾸어 계산을 편리하게 한다.

$$\ell(\theta) = \ln L(\theta) = \sum_{i=1}^n \ln f(x_i|\theta)$$

**최대가능도추정량(MLE):**

$$\hat{\theta}_{\text{MLE}} = \arg\max_{\theta \in \Theta} \ell(\theta)$$

즉, 로그가능도를 최대화하는 $\theta$ 값이다.

---
## 주요 정리와 증명

### 정리 1: 로그 변환의 불변성 — $\log$를 취해도 $\arg\max$는 같다

함수 $f(\theta) > 0$에 대해

$$\arg\max_\theta f(\theta) = \arg\max_\theta \ln f(\theta)$$

**증명:** $\ln$ 함수는 $\mathbb{R}^+$에서 단조 증가(monotonic increasing)한다. 즉 $a > b > 0$이면 $\ln a > \ln b$이다. 따라서 $\theta^*$가 $f$의 최대점일 때 모든 $\theta$에 대해

$$f(\theta^*) \geq f(\theta) \quad \Longrightarrow \quad \ln f(\theta^*) \geq \ln f(\theta)$$

역으로 $\ln f(\theta^*) \geq \ln f(\theta)$이면 $f(\theta^*) \geq f(\theta)$이다. 따라서 두 최적화 문제의 해는 일치한다. $\square$

이 정리 덕분에 곱의 형태인 가능도 대신 합의 형태인 로그가능도를 최대화할 수 있다. 미분과 최적화가 훨씬 간편해진다.

### 정리 2: 정규분포의 MLE

$X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \mathcal{N}(\mu, \sigma^2)$일 때

$$\hat{\mu}_{\text{MLE}} = \frac{1}{n}\sum_{i=1}^n x_i = \bar{x}, \qquad \hat{\sigma}^2_{\text{MLE}} = \frac{1}{n}\sum_{i=1}^n (x_i - \bar{x})^2$$

**증명:** 정규분포의 PDF $f(x|\mu,\sigma^2) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$를 이용해 로그가능도를 구성한다.

$$\ell(\mu,\sigma^2) = \sum_{i=1}^n \left[-\frac{1}{2}\ln(2\pi) - \frac{1}{2}\ln\sigma^2 - \frac{(x_i-\mu)^2}{2\sigma^2}\right]$$

$$= -\frac{n}{2}\ln(2\pi) - \frac{n}{2}\ln\sigma^2 - \frac{1}{2\sigma^2} \sum_{i=1}^n (x_i - \mu)^2$$

**$\mu$에 대한 최적화:** $\ell$을 $\mu$로 편미분하여 0으로 둔다.

$$\frac{\partial \ell}{\partial \mu} = \frac{1}{\sigma^2} \sum_{i=1}^n (x_i - \mu) = 0$$

$$\sum_{i=1}^n x_i - n\mu = 0 \quad \Longrightarrow \quad \hat{\mu} = \frac{1}{n}\sum_{i=1}^n x_i = \bar{x}$$

**$\sigma^2$에 대한 최적화:** $\ell$을 $\sigma^2$로 편미분한다. $\sigma^2$ 자체를 변수로 취급하는 것이 편리하다.

$$\frac{\partial \ell}{\partial \sigma^2} = -\frac{n}{2}\cdot\frac{1}{\sigma^2} + \frac{1}{2\sigma^4} \sum_{i=1}^n (x_i - \mu)^2 = 0$$

양변에 $2\sigma^4$를 곱하면

$$-n\sigma^2 + \sum_{i=1}^n (x_i - \mu)^2 = 0 \quad \Longrightarrow \quad \hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (x_i - \mu)^2$$

여기에 $\mu$ 대신 $\hat{\mu} = \bar{x}$를 대입하면

$$\hat{\sigma}^2_{\text{MLE}} = \frac{1}{n}\sum_{i=1}^n (x_i - \bar{x})^2$$

$\square$

참고: $\hat{\sigma}^2_{\text{MLE}}$는 편향(biased) 추정량이다. 불편추정량(unbiased estimator)은 $s^2 = \frac{1}{n-1}\sum (x_i - \bar{x})^2$로, $n$ 대신 $n-1$로 나눈다.

### 정리 3: 베르누이 분포의 MLE

$X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \text{Ber}(p)$일 때

$$\hat{p}_{\text{MLE}} = \bar{x} = \frac{1}{n}\sum_{i=1}^n x_i$$

**증명:** 베르누이 분포의 PMF는 $P(X=x) = p^x (1-p)^{1-x}$, $x \in \{0,1\}$이다.

$$\ell(p) = \sum_{i=1}^n \left[x_i \ln p + (1-x_i) \ln(1-p)\right]$$

$$= \left(\sum_{i=1}^n x_i\right) \ln p + \left(n - \sum_{i=1}^n x_i\right) \ln(1-p)$$

$p$로 미분하여 0으로 둔다.

$$\frac{d\ell}{dp} = \frac{\sum x_i}{p} - \frac{n - \sum x_i}{1-p} = 0$$

$$\frac{\sum x_i}{p} = \frac{n - \sum x_i}{1-p}$$

$$(\sum x_i)(1-p) = p(n - \sum x_i)$$

$$\sum x_i - p\sum x_i = np - p\sum x_i$$

$$\sum x_i = np \quad \Longrightarrow \quad \hat{p} = \frac{1}{n}\sum_{i=1}^n x_i = \bar{x}$$

$\square$

### 정리 4: MLE의 불변성 (Invariance Property)

$g$가 일대일 함수(one-to-one function)이면

$$\widehat{g(\theta)}_{\text{MLE}} = g(\hat{\theta}_{\text{MLE}})$$

**증명 (서술):** $\hat{\theta}$는 가능도 $L(\theta)$를 최대화한다. $\eta = g(\theta)$라고 할 때, $g$가 일대일이므로 역함수 $\theta = g^{-1}(\eta)$가 존재한다. 가능도를 $\eta$의 함수로 표현하면 $L^*( \eta) = L(g^{-1}(\eta))$이다. $\hat{\theta}$에서 $L(\theta)$가 최대이므로 $\hat{\eta} = g(\hat{\theta})$에서 $L^*(\eta)$가 최대가 된다. 따라서 $\widehat{g(\theta)} = g(\hat{\theta})$이다. $\square$

이 성질은 매우 실용적이다. 예를 들어 정규분포의 $\sigma$에 대한 MLE는 $\hat{\sigma}_{\text{MLE}} = \sqrt{\hat{\sigma}^2_{\text{MLE}}}$로 간단히 구해진다.

### 정리 5: MLE의 점근적 정규성 (Asymptotic Normality)

적절한 정규성 조건(regularity conditions) 하에서

$$\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} \mathcal{N}\left(0, \frac{1}{I(\theta_0)}\right)$$

여기서 $\theta_0$는 참값(true parameter)이고, $I(\theta_0)$는 **피셔 정보량(Fisher information)**이다.

$$I(\theta) = \mathbb{E}\left[\left(\frac{\partial}{\partial\theta} \ln f(X|\theta)\right)^2\right] = -\mathbb{E}\left[\frac{\partial^2}{\partial\theta^2} \ln f(X|\theta)\right]$$

**증명 (서술):** 로그가능도의 테일러 전개와 중심극한정리(CLT)를 활용한다. $\ell'(\hat{\theta}) = 0$에서 출발하여 $\hat{\theta}$ 근방에서 1차 테일러 전개를 하면

$$0 = \ell'(\hat{\theta}) \approx \ell'(\theta_0) + \ell''(\theta_0)(\hat{\theta} - \theta_0)$$

$$\sqrt{n}(\hat{\theta} - \theta_0) \approx -\frac{\ell'(\theta_0)/\sqrt{n}}{\ell''(\theta_0)/n}$$

분자 $\ell'(\theta_0)/\sqrt{n}$는 CLT에 의해 $\mathcal{N}(0, I(\theta_0))$로 수렴하고, 분모 $\ell''(\theta_0)/n$은 대수의 법칙에 의해 $-I(\theta_0)$로 수렴한다. 슬러츠키 정리(Slutsky's theorem)를 적용하면 원하는 결과를 얻는다. $\square$

---
## 예제

**예제 1 (정규분포 MLE):** 한 공정에서 생산된 5개 제품의 길이(cm)가 다음과 같다.

$$10.1,\; 9.9,\; 10.3,\; 10.0,\; 9.7$$

정규분포를 가정할 때 $\mu$와 $\sigma^2$의 MLE를 구하라.

**풀이:**

$$\hat{\mu} = \frac{10.1 + 9.9 + 10.3 + 10.0 + 9.7}{5} = \frac{50.0}{5} = 10.0$$

$$\hat{\sigma}^2 = \frac{1}{5} \left[(0.1)^2 + (-0.1)^2 + (0.3)^2 + 0^2 + (-0.3)^2\right] = \frac{0.01+0.01+0.09+0+0.09}{5} = \frac{0.20}{5} = 0.04$$

따라서 $\hat{\mu}=10.0$, $\hat{\sigma}^2 = 0.04$ ($\hat{\sigma}=0.2$)이다.

**예제 2 (지수분포 MLE):** $X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \text{Exp}(\lambda)$일 때 $\lambda$의 MLE를 구하라. 지수분포의 PDF는 $f(x|\lambda) = \lambda e^{-\lambda x}$ ($x \geq 0$)이다.

**풀이:**

$$\ell(\lambda) = \sum_{i=1}^n (\ln\lambda - \lambda x_i) = n\ln\lambda - \lambda\sum_{i=1}^n x_i$$

$$\frac{d\ell}{d\lambda} = \frac{n}{\lambda} - \sum_{i=1}^n x_i = 0 \quad \Longrightarrow \quad \frac{n}{\hat{\lambda}} = \sum_{i=1}^n x_i$$

$$\hat{\lambda}_{\text{MLE}} = \frac{n}{\sum_{i=1}^n x_i} = \frac{1}{\bar{x}}$$

표본평균이 클수록 추정된 비율(rate) $\lambda$는 작아진다. 평균 대기시간이 길면 단위시간당 발생률이 낮기 때문이다.

**예제 3 (포아송 MLE):** $X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \text{Pois}(\lambda)$일 때 $\lambda$의 MLE를 구하라. 포아송 분포의 PMF는 $P(X=k) = \lambda^k e^{-\lambda}/k!$이다.

**풀이:**

$$\ell(\lambda) = \sum_{i=1}^n \left[ x_i \ln\lambda - \lambda - \ln(x_i!) \right]$$

$$= \left(\sum_{i=1}^n x_i\right) \ln\lambda - n\lambda - \sum_{i=1}^n \ln(x_i!)$$

$$\frac{d\ell}{d\lambda} = \frac{\sum x_i}{\lambda} - n = 0 \quad \Longrightarrow \quad \hat{\lambda} = \frac{\sum x_i}{n} = \bar{x}$$

포아송 분포의 MLE도 표본평균이다. 이는 $\mathbb{E}[X] = \lambda$이므로 적률법(method of moments) 추정량과도 일치한다.

**예제 4 (베르누이 MLE — 동전 던지기):** 동전을 100번 던져 63번 앞면이 나왔다. 앞면이 나올 확률 $p$의 MLE를 구하라.

**풀이:** $\hat{p} = 63/100 = 0.63$이다. 95% 근사 신뢰구간(asymptotic confidence interval)은 MLE의 점근적 정규성을 이용해

$$\hat{p} \pm 1.96 \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}} = 0.63 \pm 1.96 \cdot \sqrt{\frac{0.63 \times 0.37}{100}} = 0.63 \pm 0.095$$

즉 $[0.535, 0.725]$이다.

**예제 5 (MLE 불변성 활용):** 정규분포에서 $\mu$의 MLE가 $\hat{\mu} = \bar{x}$일 때, $g(\mu) = \mu^2$의 MLE를 구하라.

**풀이:** MLE의 불변성에 의해 $\widehat{\mu^2} = (\hat{\mu})^2 = \bar{x}^2$이다. 예를 들어 데이터가 [2, 4, 6]이면 $\hat{\mu}=4$이고 $\widehat{\mu^2}=16$이다.

---
## 연결

- **[주요 분포](distributions.html)** : MLE의 입력은 데이터, 출력은 분포의 모수다. 각 분포(정규, 베르누이, 포아송, 지수)의 PDF/PMF를 알아야 로그가능도를 구성할 수 있다.
- **[베이지안 추론](bayesian-inference.html)** : MLE는 사전정보 없이 데이터만으로 추정하는 빈도주의(frequentist) 접근이다. 베이지안 추론은 사전분포를 추가하여 MAP 추정으로 확장한다. $n$이 커질수록 MLE와 MAP는 수렴한다.
- **[가설검정](hypothesis-testing.html)** : MLE는 우도비 검정(likelihood ratio test)의 핵심 재료다. $LR = -2\ln(L(\theta_0)/L(\hat{\theta}))$는 귀무가설 검정에 사용된다.
