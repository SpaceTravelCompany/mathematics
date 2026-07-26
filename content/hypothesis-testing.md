---
title: 가설검정·p-value·신뢰구간
slug: hypothesis-testing
---

## 직관적 설명

**가설검정(hypothesis testing)**은 "관측된 결과가 우연인가, 진짜인가?"를 판단하는 통계적 절차다. 핵심 아이디어는 간단하다: 귀무가설(null hypothesis) $H_0$가 참이라고 가정할 때, 현재 관측된 결과(또는 그보다 극단적인 결과)가 나올 확률을 계산한다. 이 확률이 충분히 작으면(unlikely enough), 귀무가설을 기각한다. 이 확률이 바로 **p-value(유의확률)**다.

p-value는 가장 널리 사용되면서도 가장 자주 오해받는 통계량이기도 하다. "p-value가 0.05 미만이므로 효과가 있다"는 흔한 해석은 **틀렸다**. p-value는 귀무가설이 참일 때의 조건부 확률 $P(\text{데이터}|H_0)$이지, $P(H_0|\text{데이터})$가 아니며, "효과의 크기"나 "가설이 참일 확률"을 직접 측정하지 않는다.

신뢰구간(confidence interval)은 이와 다른 관점을 제공한다. 95% 신뢰구간은 "모수가 이 구간 안에 있을 확률이 95%"라는 뜻이 아니라, "같은 방식으로 반복 추정했을 때 95%의 구간이 모수를 포함한다"는 빈도주의(frequentist) 해석을 가진다. 신뢰구간과 가설검정은 쌍대성(duality)을 가진다: 모평균 $\mu_0$가 95% 신뢰구간 안에 있다면, $\mu = \mu_0$에 대한 양측검정을 유의수준 $\alpha = 0.05$에서 기각할 수 없다.

**다중검정 문제(multiple testing problem)**는 여러 가설을 동시에 검정할 때 발생한다. 100개의 가설을 각각 $\alpha = 0.05$로 검정하면, 모든 귀무가설이 참일 때도 평균 5개의 "유의한" 결과가 우연히 나온다. 본페로니 보정(Bonferroni correction) $\alpha' = \alpha/m$는 가장 단순한 해결책이다.

## 정의

**귀무가설(null hypothesis) $H_0$:** 기각하려는 대상, 보통 "효과가 없다" 또는 "차이가 없다"는 진술. 유지되는 기본 가정(default assumption)이다.

**대립가설(alternative hypothesis) $H_1$:** 지지하려는 주장, 보통 "효과가 있다" 또는 "차이가 있다"는 진술.

**검정통계량(test statistic) $T$:** 관측 데이터로부터 계산되는 값으로, 귀무가설 하에서의 분포가 알려져 있다.

**기각역(rejection region) $R$:** 검정통계량이 이 영역에 속하면 $H_0$를 기각한다.

**유의수준(significance level) $\alpha$:** 1종 오류(type I error)의 최대 허용 확률:
$$\alpha = P(\text{기각} \mid H_0)$$

**p-value (유의확률):** 귀무가설 $H_0$가 참일 때, 관측된 검정통계량 $t_{\text{obs}}$보다 더 극단적인 값이 관측될 확률. 단측 검정(one-tailed)의 경우:
$$p = P_{H_0}(T \geq t_{\text{obs}})$$

**1종 오류 (type I error):** $H_0$가 참인데 기각하는 오류. 확률 = $\alpha$.

**2종 오류 (type II error):** $H_1$이 참인데 $H_0$를 기각하지 않는 오류. 확률 = $\beta$.

**검정력 (statistical power):** $1 - \beta = P(\text{기각} \mid H_1)$, 즉 대립가설이 참일 때 올바르게 기각할 확률.

**신뢰구간 (confidence interval):** 모수 $\theta$에 대한 $100(1-\alpha)\%$ 신뢰구간은
$$\hat{\theta} \pm z_{\alpha/2} \cdot \text{SE}(\hat{\theta})$$

**정규 모평균 검정 (z-test):** $n$개의 i.i.d. 표본 $X_1, \ldots, X_n \sim \mathcal{N}(\mu, \sigma^2)$에서 $\sigma$를 알 때,
$$Z = \frac{\bar{X} - \mu_0}{\sigma/\sqrt{n}} \sim \mathcal{N}(0, 1) \quad \text{under } H_0: \mu = \mu_0$$

**본페로니 보정 (Bonferroni correction):** $m$개의 가설을 동시에 검정할 때, 개별 유의수준을 $\alpha' = \alpha/m$으로 설정하여 전체 family-wise error rate(FWER)를 $\alpha$ 이하로 유지한다.

## 주요 정리와 증명

### 정리 1: p-value의 정확한 의미와 오해

**p-value의 정의:** p-value는 *귀무가설 하에서* 관측된 검정통계량보다 더 극단적인 결과가 나올 확률이다.
$$p = P_{H_0}(T \geq t_{\text{obs}})$$

**흔한 오해 3가지:**

**오해 1:** "p-value가 0.05 미만이면 $H_0$가 참일 확률이 5% 미만이다."
- **반박:** p-value는 $P(\text{데이터}|H_0)$이지 $P(H_0|\text{데이터})$가 아니다. 베이즈 정리에 의해 후자는 사전확률 $P(H_0)$에 의존한다. p-value가 작다고 해서 $H_0$가 참일 확률이 작은 것은 아니다.

**오해 2:** "p-value가 0.05 미만이면 효과가 '실질적으로 유의미'하다."
- **반박:** p-value는 표본 크기에 크게 민감하다. 표본이 충분히 크면 아주 작은 효과도 통계적으로 유의해진다. 반대로 표본이 작으면 큰 효과도 유의하지 않을 수 있다. 효과 크기(effect size)를 별도로 고려해야 한다.

**오해 3:** "1 - p-value는 $H_1$이 참일 확률이다."
- **반박:** p-value는 $H_0$ 하에서 계산된 값으로, $H_1$의 확률에 대한 정보를 직접 주지 않는다. $P(H_1|\text{데이터})$를 구하려면 베이즈 접근법이 필요하다.

### 정리 2: 정규 모평균 검정 — Z-검정

**서술:** $X_1, \ldots, X_n \stackrel{\text{iid}}{\sim} \mathcal{N}(\mu, \sigma^2)$이고 $\sigma$가 알려져 있을 때, $H_0: \mu = \mu_0$에 대한 검정통계량은
$$Z = \frac{\bar{X} - \mu_0}{\sigma/\sqrt{n}}$$
이며, $H_0$ 하에서 $Z \sim \mathcal{N}(0, 1)$을 따른다.

**증명:** 중심극한정리(CLT)에 의해 표본평균은 $\bar{X} \sim \mathcal{N}(\mu, \sigma^2/n)$이다(정규모집단이므로 정확히 정규분포). $H_0$ 하에서 $\mu = \mu_0$이므로
$$\bar{X} \sim \mathcal{N}\left(\mu_0, \frac{\sigma^2}{n}\right)$$

따라서
$$Z = \frac{\bar{X} - \mu_0}{\sigma/\sqrt{n}} \sim \mathcal{N}(0, 1)$$

양측검정(two-tailed test)의 기각역(유의수준 $\alpha$)은 $|Z| > z_{\alpha/2}$이다.

p-value 계산:
$$p = 2 \cdot P(Z \geq |z_{\text{obs}}|) = 2(1 - \Phi(|z_{\text{obs}}|))$$

여기서 $\Phi$는 표준정규분포의 CDF다. $\square$

### 정리 3: 신뢰구간과 가설검정의 쌍대성

**서술:** 모평균 $\mu$에 대한 $100(1-\alpha)\%$ 신뢰구간 $(\bar{x} - z_{\alpha/2}\sigma/\sqrt{n}, \bar{x} + z_{\alpha/2}\sigma/\sqrt{n})$에 대해,
$\mu_0$가 이 구간 안에 속할 필요충분조건은 $H_0: \mu = \mu_0$에 대한 양측검정을 유의수준 $\alpha$에서 기각하지 못하는 것이다.

**증명:** 양측검정에서 $H_0: \mu = \mu_0$를 기각하지 않는 조건은
$$|z_{\text{obs}}| = \left|\frac{\bar{x} - \mu_0}{\sigma/\sqrt{n}}\right| \leq z_{\alpha/2}$$

이를 $\mu_0$에 대해 풀면:
$$\bar{x} - z_{\alpha/2}\frac{\sigma}{\sqrt{n}} \leq \mu_0 \leq \bar{x} + z_{\alpha/2}\frac{\sigma}{\sqrt{n}}$$

이는 $\mu_0$가 $100(1-\alpha)\%$ 신뢰구간 안에 있음을 의미한다. 역방향도 같은 논리로 성립한다. $\square$

**의미:** 이 쌍대성은 신뢰구간과 가설검정이 본질적으로 동일한 정보를 제공함을 보여준다. 신뢰구간은 "기각되지 않는 모수값들의 집합"이다.

### 정리 4: 다중검정 문제와 본페로니 보정

**서술:** $m$개의 독립적인 가설검정을 각각 유의수준 $\alpha$로 수행할 때, 적어도 하나의 1종 오류가 발생할 확률(FWER)은
$$\text{FWER} = 1 - (1-\alpha)^m \leq m\alpha$$

본페로니 보정: 각 개별 검정의 유의수준을 $\alpha' = \alpha/m$으로 설정하면 FWER $\leq \alpha$가 보장된다.

**증명:** 각 검정의 1종 오류 확률을 $\alpha'$이라 하자. 번사이 부등식(Boole's inequality, union bound)에 의해
$$\text{FWER} = P\left(\bigcup_{i=1}^m \{\text{검정 } i \text{ 기각}\}\right) \leq \sum_{i=1}^m P(\text{검정 } i \text{ 기각}) = m \cdot \alpha'$$

$\alpha' = \alpha/m$을 대입하면 FWER $\leq \alpha$를 얻는다. $\square$

**참고:** 본페로니 보정은 매우 보수적이다(conservative). 검정 간 상관관계가 있으면 실제 FWER는 $m\alpha'$보다 훨씬 작으며, 따라서 본페로니 보정은 검정력을 크게 감소시킨다. 이 경우 FDR(false discovery rate) 제어(Benjamini-Hochberg) 같은 덜 보수적인 방법을 사용할 수 있다.

### 정리 5: 검정력 함수 (서술)

**서술:** $H_0: \mu = \mu_0$ vs $H_1: \mu = \mu_1$ ($\mu_1 > \mu_0$)에 대한 단측 z-검정의 검정력은
$$1 - \beta = P\left(Z > z_\alpha - \frac{\mu_1 - \mu_0}{\sigma/\sqrt{n}}\right) = \Phi\left(\frac{\mu_1 - \mu_0}{\sigma/\sqrt{n}} - z_\alpha\right)$$

**증명 (스케치):** $H_1$ 하에서 $\bar{X} \sim \mathcal{N}(\mu_1, \sigma^2/n)$이다. $H_0$ 기각 조건 $\bar{X} > \mu_0 + z_\alpha\sigma/\sqrt{n}$을 $H_1$ 하에서 평가하면
$$1 - \beta = P\left(\bar{X} > \mu_0 + z_\alpha\frac{\sigma}{\sqrt{n}} \,\middle|\, \mu = \mu_1\right)$$
$$= P\left(\frac{\bar{X} - \mu_1}{\sigma/\sqrt{n}} > \frac{\mu_0 - \mu_1}{\sigma/\sqrt{n}} + z_\alpha\right)$$
$$= P\left(Z > z_\alpha - \frac{\mu_1 - \mu_0}{\sigma/\sqrt{n}}\right) = \Phi\left(\frac{\mu_1 - \mu_0}{\sigma/\sqrt{n}} - z_\alpha\right)$$

검정력은 효과 크기 $(\mu_1 - \mu_0)/\sigma$와 $\sqrt{n}$에 비례하여 증가한다. $\square$

## 예제

**예제 1 (동전의 공정성 검정):** 동전을 100번 던져 60번 앞면이 나왔다. 이 동전이 공정한지($H_0: p = 0.5$) 유의수준 $\alpha = 0.05$에서 검정하라.

**풀이:** 이항분포 $X \sim \text{Bin}(100, 0.5)$ 하에서 p-value를 계산한다. CLT에 의해 근사적으로 $X \sim \mathcal{N}(50, 25)$이므로
$$z_{\text{obs}} = \frac{60 - 50}{\sqrt{25}} = \frac{10}{5} = 2.0$$

양측 p-value:
$$p = 2 \cdot P(Z \geq 2.0) = 2(1 - \Phi(2.0)) \approx 2 \times 0.0228 = 0.0456$$

$p = 0.0456 < 0.05$이므로 귀무가설을 기각한다. 즉, 이 동전은 공정하지 않다고 판단한다.

**해석 주의:** p-value가 0.05 미만이지만, 그 차이가 "실질적으로" 의미 있는지는 별개의 문제다. $n$을 1000으로 늘리면 60%에서 55%만 되어도 유의해질 수 있다.

**예제 2 (정규 검정 — 모평균 비교):** 어떤 공정에서 생산된 제품의 무게가 정규분포를 따른다고 알려져 있고, $\sigma = 5$g이다. 25개 표본의 평균이 102g일 때, $H_0: \mu = 100$g vs $H_1: \mu \neq 100$g을 $\alpha = 0.05$에서 검정하라.

**풀이:**
$$z_{\text{obs}} = \frac{102 - 100}{5/\sqrt{25}} = \frac{2}{1} = 2.0$$

양측 p-value: $p = 2(1 - \Phi(2.0)) \approx 0.0456 < 0.05$. 따라서 $H_0$를 기각한다.

95% 신뢰구간:
$$\bar{x} \pm z_{0.025} \cdot \frac{\sigma}{\sqrt{n}} = 102 \pm 1.96 \times 1 = (100.04, 103.96)$$

$\mu_0 = 100$이 이 구간 밖에 있으므로(100.04보다 작음), $H_0$가 기각됨을 확인한다(쌍대성).

**예제 3 (신뢰구간 해석의 오해):** 95% 신뢰구간 $(100.04, 103.96)$에 대해 "$\mu$가 이 구간 안에 있을 확률이 95%다"라는 해석은 **빈도주의** 관점에서 틀렸다. $\mu$는 고정된 상수이므로 확률적 진술의 대상이 아니다. 올바른 해석: "같은 방식으로 100번 반복 추정하면, 약 95개의 구간이 $\mu$를 포함할 것이다."

**예제 4 (검정력 계산):** 예제 2에서 실제 평균이 $\mu = 102$일 때 검정력을 구하라.

**풀이:**
$$1 - \beta = \Phi\left(\frac{102 - 100}{5/\sqrt{25}} - 1.96\right) = \Phi\left(\frac{2}{1} - 1.96\right) = \Phi(0.04) \approx 0.516$$

검정력이 약 51.6%로 낮다. 즉, 실제 효과가 2g임에도 25개 표본으로는 절반 정도밖에 검출하지 못한다. 검정력을 높이려면 $n$을 늘려야 한다.

**예제 5 (본페로니 보정):** 20개의 유전자가 특정 질병과 관련 있는지 각각 $\alpha = 0.05$로 검정한다. 모든 귀무가설이 참일 때, 적어도 하나의 유의한 결과가 나올 확률은?

**풀이 (보정 전):** $\text{FWER} = 1 - (1-0.05)^{20} \approx 0.642$. 즉, 64.2%의 확률로 거짓 양성이 발생한다.

**본페로니 보정 후:** $\alpha' = 0.05/20 = 0.0025$. 각 검정을 $\alpha' = 0.0025$로 수행하면 FWER $\leq 0.05$가 보장된다.

단점: $p = 0.001$인 결과는 유의하지만, $p = 0.004$인 결과는 유의하지 않게 된다. 이렇게 보수적인 기준은 실제 효과를 놓칠 수 있다(2종 오류 증가).

**예제 6 (표본 크기 결정):** 검정력 $1-\beta = 0.8$을 달성하려면 필요한 표본 크기는? $\alpha = 0.05$, $\mu_1 - \mu_0 = 2$, $\sigma = 5$라고 할 때.

**풀이:** 검정력 공식에서
$$0.8 = \Phi\left(\frac{2}{5/\sqrt{n}} - 1.96\right) \quad \Rightarrow \quad \frac{2\sqrt{n}}{5} - 1.96 = \Phi^{-1}(0.8) \approx 0.84$$
$$\frac{2\sqrt{n}}{5} = 2.80 \quad \Rightarrow \quad \sqrt{n} = 7.0 \quad \Rightarrow \quad n = 49$$

따라서 최소 49개의 표본이 필요하다.

## 연결

- **[중심극한정리](topics/clt.html)** : z-검정과 정규근사의 이론적 근거는 CLT다. 표본평균의 분포가 정규분포에 수렴하기 때문에 p-value를 표준정규분포로 계산할 수 있다.
- **[회귀분석](topics/regression-analysis.html)** : 회귀계수의 유의성 검정(t-검정, F-검정)은 가설검정의 틀을 따른다. $p < 0.05$로 변수를 선택하는 단계적 회귀(stepwise regression)는 다중검정 문제의 대표적 사례다.
- **[몬테카를로](topics/monte-carlo.html)** : p-value의 분포를 시뮬레이션으로 추정할 수 있다. 순열 검정(permutation test)은 비모수적 p-value 계산의 예시다.
- **[조건부 확률·베이즈](topics/conditional-bayes.html)** : p-value의 오해는 조건부 확률 $P(A|B)$와 $P(B|A)$의 혼동에서 비롯된다. 베이즈 요인(Bayes factor)은 p-value의 대안으로 더 직관적인 해석을 제공한다.
