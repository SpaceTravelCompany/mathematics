---
title: 인과추론
slug: causal-inference
---

## 직관적 설명

**인과추론(causal inference)**은 "X가 Y의 원인인가?"라는 질문에 답하는 통계적 방법론이다. 상관관계(correlation)는 "X와 Y가 함께 움직인다"는 사실만 알려주지만, 인과관계(causation)는 "X를 바꾸면 Y가 변한다"는 것을 의미한다. 이 둘의 차이는 **개입(intervention)**의 개념에 있다.

관측 데이터에서 $X$와 $Y$의 상관관계 $P(Y|X)$는 교란변수(confounder) $Z$로 인해 실제 인과효과와 다를 수 있다. 예를 들어 아이스크림 판매량과 익사 사고 수는 여름(계절)이라는 교란변수 때문에 강한 상관을 보이지만, 아이스크림 판매를 금지해도 익사 사고는 줄지 않는다. 인과추론에서 중요한 것은 $P(Y|X)$가 아니라 $P(Y|\text{do}(X))$ — X에 인위적으로 개입했을 때 Y의 분포다.

**do-연산(do-operator)** $\text{do}(X=x)$은 "X를 외부에서 강제로 x로 설정하는 개입"을 의미한다. 이는 단순한 조건부 확률 $P(Y|X=x)$와 근본적으로 다르며, 구조방정식 모델(structural equation model, SEM)을 통해 정의된다.

인과추론의 주요 도구로는 **도구변수(instrumental variable, IV)**, **백도어 조정(backdoor adjustment)**, **반사실(counterfactual)** 분석, **무작위 대조시험(randomized controlled trial, RCT)** 등이 있다. RCT는 교란을 제거하는 가장 확실한 방법으로, 무작위 할당이 처리(treatment)와 교란변수를 독립적으로 만든다.

## 정의

**구조방정식 모델 (Structural Equation Model, SEM):** 각 변수를 그 원인들의 함수와 외생적(exogenous) 잡음으로 표현한다:
$$X_i = f_i(\text{PA}(X_i), U_i)$$

여기서 $\text{PA}(X_i)$는 $X_i$의 원인(부모, parents), $U_i$는 외생 잡음이다.

**인과 그래프 (causal graph):** 변수 간 인과 관계를 나타내는 방향성 비순환 그래프(directed acyclic graph, DAG). 노드는 변수, 화살표는 인과 방향을 나타낸다.

**개입 (intervention):** $\text{do}(X=x)$는 $X$의 값을 $x$로 강제 설정하는 조작으로, $X$에 영향을 미치는 모든 인과 경로를 차단한다. SEM에서 이는 $X = x$로 방정식을 대체하고 다른 변수의 구조는 유지하는 것과 같다.

**인과 효과 (causal effect):** $P(Y|\text{do}(X=x))$ — $X$를 $x$로 개입했을 때 $Y$의 분포.

**교란 (confounding):** $X$와 $Y$의 공통 원인 $Z$가 존재할 때 발생하는 편향(bias):
$$P(Y|X) \neq P(Y|\text{do}(X))$$
구조: $X \leftarrow Z \rightarrow Y$.

**백도어 기준 (backdoor criterion):** 변수 집합 $Z$가 다음을 만족하면 $Z$는 backdoor 경로를 차단한다:
(1) $Z$의 어떤 원소도 $X$의 자손(descendant)이 아니다.
(2) $Z$는 $X$와 $Y$ 사이의 모든 backdoor 경로($X$로 들어가는 화살표를 포함하는 경로)를 차단한다.
이때
$$P(Y|\text{do}(X)) = \sum_z P(Y|X, z) P(z)$$

**도구변수 (instrumental variable, IV):** 변수 $Z$가 도구변수가 되려면:
(1) $Z \rightarrow X$ ($Z$는 $X$에 영향을 미친다)
(2) $Z \not\rightarrow Y$ (직접 경로 없음)
(3) $Z \perp U_Y$ ($Z$는 $Y$의 교란변수와 독립)

**반사실 (counterfactual):** "만약 $X$가 $x$였다면 $Y$는?"이라는 질문에 대한 답. $Y_{X=x}(u)$로 표기하며, 단위(unit) $u$에서 $X$를 $x$로 설정했을 때 $Y$의 값이다.

## 주요 정리와 증명

### 정리 1: 백도어 조정 공식 (Backdoor Adjustment)

**서술:** 변수 집합 $Z$가 backdoor 기준을 만족하면,
$$P(Y|\text{do}(X=x)) = \sum_z P(Y|X=x, Z=z) P(Z=z)$$

**증명:** do-연산의 규칙을 사용한다. 그래프 $G$에서 $\text{do}(X=x)$는 $X$로 들어오는 모든 화살표를 제거한 그래프 $G_{\underline{X}}$에서의 조건부 분포와 같다.

(1) $Z$가 backdoor 기준을 만족하므로 $G_{\underline{X}}$에서 $Y$와 $X$는 $Z$에 의해 d-분리(d-separate)된다. do-연산의 규칙 2(actions 관찰)에 의해:
$$P(Y|\text{do}(X=x), Z=z) = P(Y|X=x, Z=z)$$

(2) $Z$는 $X$의 자손이 아니므로 $\text{do}(X=x)$는 $Z$의 분포에 영향을 주지 않는다:
$$P(Z=z|\text{do}(X=x)) = P(Z=z)$$

(3) 전확률 공식(law of total probability)을 적용:
$$P(Y|\text{do}(X=x)) = \sum_z P(Y|\text{do}(X=x), Z=z) P(Z=z|\text{do}(X=x))$$
$$= \sum_z P(Y|X=x, Z=z) P(Z=z)$$

$\square$

**예시:** $X$: 약물 복용, $Y$: 회복, $Z$: 성별. 성별이 $X$와 $Y$의 공통 원인일 때, 백도어 조정은 각 성별 그룹 내에서 약물 효과를 계산하고 성별 분포로 가중평균한다.

**직접 조정(direct adjustment)과의 차이:** $P(Y|X) = \sum_z P(Y|X,z)P(z|X)$는 $P(z|X)$의 조건부 편향 때문에 $P(Y|\text{do}(X))$와 다르다.

### 정리 2: 교란 시 $P(Y|X) \neq P(Y|\text{do}(X))$ — 반례

**서술:** 교란변수 $Z$가 존재할 때 일반적으로 $P(Y|X) \neq P(Y|\text{do}(X))$이다.

**증명 (수치 반례):** 다음 구조방정식을 고려하자:
$$Z \sim \text{Bernoulli}(0.5)$$
$$X = Z + \epsilon_X, \quad \epsilon_X \sim \mathcal{N}(0, 0.1)$$
$$Y = X + Z + \epsilon_Y, \quad \epsilon_Y \sim \mathcal{N}(0, 0.1)$$

$Z$가 교란변수($X$와 $Y$ 모두의 원인)이므로:
$$\mathbb{E}[Y|X=1] - \mathbb{E}[Y|X=0] \neq \mathbb{E}[Y|\text{do}(X=1)] - \mathbb{E}[Y|\text{do}(X=0)]$$

구체적으로 계산하면(근사):
$P(Y|X=1)$: $X=1$이면 $Z$가 1일 확률이 높아(대략 0.91) $\mathbb{E}[Y|X=1] \approx 1 + 1 + 0.91 = 2.91$.
$P(Y|X=0)$: $X=0$이면 $Z$가 0일 확률이 높아(대략 0.91) $\mathbb{E}[Y|X=0] \approx 0 + 0 + 0.09 = 0.09$.

관측 차이 $\approx 2.82$.

인과 효과: $Y|\text{do}(X=1)$은 $Z$가 변하지 않으므로($Z$는 $X$의 개입과 무관) $\mathbb{E}[Y|\text{do}(X=1)] = 1 + \mathbb{E}[Z] + 0 = 1.5$.
$\mathbb{E}[Y|\text{do}(X=0)] = 0 + \mathbb{E}[Z] + 0 = 0.5$.
인과 효과 $= 1.0$.

$2.82 \neq 1.0$ — 관측 차이가 인과 효과를 크게 과대추정한다. $\square$

### 정리 3: 도구변수 추정

**서술:** $Y = \beta X + U$, $\text{Cov}(X, U) \neq 0$(교란 존재)일 때, 도구변수 $Z$가 다음 조건을 만족하면:
(1) $\text{Cov}(Z, X) \neq 0$ (관련성, relevance)
(2) $\text{Cov}(Z, U) = 0$ (외생성, exogeneity)
(3) $Z \not\to Y$ 직접 (배제 제약, exclusion restriction)

$\beta$의 IV 추정량은
$$\hat{\beta}_{\text{IV}} = \frac{\text{Cov}(Z, Y)}{\text{Cov}(Z, X)}$$

이며, 이는 $\beta$의 일치 추정량(consistent estimator)이다.

**증명:** 구조방정식 $Y = \beta X + U$의 양변에 $Z$의 공분산을 취한다:
$$\text{Cov}(Z, Y) = \beta \text{Cov}(Z, X) + \text{Cov}(Z, U)$$

외생성 조건 $\text{Cov}(Z, U) = 0$에 의해
$$\text{Cov}(Z, Y) = \beta \text{Cov}(Z, X)$$

관련성 조건 $\text{Cov}(Z, X) \neq 0$에 의해
$$\beta = \frac{\text{Cov}(Z, Y)}{\text{Cov}(Z, X)}$$

표본 유사도(sample analogue)로 대체하면 IV 추정량을 얻는다. 대수의 법칙에 의해 표본 공분산은 모공분산으로 수렴하므로, $\hat{\beta}_{\text{IV}} \xrightarrow{p} \beta$이다(일치성). $\square$

**2SLS (two-stage least squares):** $\hat{\beta}_{\text{IV}}$는 다음 두 단계로도 계산된다:
1단계: $X$를 $Z$에 회귀 → $\hat{X} = \hat{\gamma} Z$
2단계: $Y$를 $\hat{X}$에 회귀 → $\hat{\beta}_{\text{2SLS}}$
이는 다중 도구변수로 확장될 때 더 효율적이다.

### 정리 4: RCT가 교란을 제거하는 이유

**서술:** 무작위 대조시험(RCT)에서 처리 $T$가 무작위로 할당되면, $T$는 모든 교란변수 $Z$와 독립이다:
$$T \perp Z \quad \forall Z$$

이 조건 하에서 $P(Y|\text{do}(T)) = P(Y|T)$가 성립하며, 즉 관측된 차이가 인과 효과와 일치한다.

**증명:** RCT의 무작위 할당 메커니즘은 $\text{do}(T=t)$와 동등하다. 처리 $T$의 할당이 모든 잠재적 교란변수와 독립이므로,
$$P(Y|\text{do}(T=t)) = P(Y|T=t)$$

이는 다음과 같이 증명된다. 백도어 조정 공식에서, $T$와 $Z$의 독립성($P(z|T=t) = P(z)$)을 적용하면:
$$P(Y|\text{do}(T=t)) = \sum_z P(Y|T=t, z) P(z)$$
$$= \sum_z P(Y|T=t, z) P(z|T=t) = P(Y|T=t)$$

(두 번째 등호는 $T \perp Z$로 인해 $P(z) = P(z|T=t)$, 세 번째 등호는 전확률 공식.)

따라서 RCT에서는 단순한 조건부 비교가 인과 효과를 식별한다:
$$\mathbb{E}[Y|T=1] - \mathbb{E}[Y|T=0] = \mathbb{E}[Y(1)] - \mathbb{E}[Y(0)]$$

여기서 $Y(t)$는 $T=t$일 때의 잠재적 결과(potential outcome)다. $\square$

**RCT의 한계:** 비용, 윤리적 문제(예: 흡연 강제 할당 불가), 외부 타당도(external validity) 문제 등으로 RCT가 항상 가능한 것은 아니다. 이때 관측 연구(observational study)에서의 인과추론 방법이 필요하다.

## 예제

**예제 1 (아이스크림-익사 교란):** 여름철 데이터에서 아이스크림 판매량($X$)과 익사 사고 수($Y$) 사이에 강한 양의 상관관계가 관측된다. $r = 0.8$로 매우 높다.

**인과 구조:** 계절 $Z$가 $X$와 $Y$의 공통 원인이다:
$$Z \to X \quad (\text{여름에 아이스크림 판매 증가})$$
$$Z \to Y \quad (\text{여름에 수영 증가 → 익사 증가})$$
$$X \not\to Y \quad (\text{아이스크림이 익사를 유발하지 않음})$$

$P(Y|X)$는 강한 상관을 보이지만, $P(Y|\text{do}(X)) = P(Y)$ ($X$의 개입이 $Y$에 영향 없음). 즉, 아이스크림 판매를 금지해도 익사는 줄지 않는다. 백도어 조정으로 $Z$를 통제하면:
$$P(Y|\text{do}(X)) = \sum_{z \in \{\text{여름}, \text{겨울}\}} P(Y|X, z) P(z) = P(Y)$$

실제로는 $P(Y|X, z)$가 $X$와 무관하다(계절 $z$가 고정되면 $X$와 $Y$는 독립).

**예제 2 (흡연-폐암 — 관찰 vs 개입):** 관측 연구에서 흡연자($X=1$)의 폐암 발생률($Y=1$)이 비흡연자보다 높다:
$$P(Y=1|X=1) = 0.15, \quad P(Y=1|X=0) = 0.01$$

이 차이가 인과 효과일까? 교란변수 $Z$ = 유전적 요인(흡연 욕구와 폐암 감수성에 동시 영향)이 있을 수 있다.

**RCT를 통한 확인:** 흡연을 무작위 할당할 수 없으므로(윤리적 문제), 관측 연구에서의 인과추론이 필요하다. 도구변수로 담배 세금($Z$)을 사용할 수 있다:
$$Z \to X \quad (\text{세금 ↑ → 흡연 ↓})$$
$$Z \not\to Y \quad (\text{세금은 폐암에 직접 영향 없음})$$
$$Z \perp U_Y \quad (\text{세금은 유전적 요인과 무관})$$

IV 추정량: $\hat{\beta}_{\text{IV}} = \text{Cov}(Z, Y) / \text{Cov}(Z, X)$.

**예제 3 (도구변수 추정 구조 — 구체적):** 다음과 같은 구조를 가정하자:
$$X = 0.5Z + U_X, \quad U_X \sim \mathcal{N}(0, 1)$$
$$Y = 2X + U_Y, \quad U_Y \sim \mathcal{N}(0, 1), \quad \text{Cor}(U_X, U_Y) = 0.7$$
$$Z \sim \mathcal{N}(0, 1), \quad Z \perp (U_X, U_Y)$$

$Z$와 $U_Y$의 독립($\text{Cov}(Z, U_Y) = 0$)과 $Z$의 $X$에 대한 영향($\text{Cov}(Z, X) = 0.5$)을 확인한다.

OLS 추정량 $\hat{\beta}_{\text{OLS}}$는 $\text{Cov}(X, U_Y) \neq 0$으로 인해 편향된다.
$$\text{Cov}(X, U_Y) = \text{Cov}(0.5Z + U_X, U_Y) = 0 + \text{Cov}(U_X, U_Y) = 0.7 \neq 0$$

IV 추정량:
$$\hat{\beta}_{\text{IV}} = \frac{\text{Cov}(Z, Y)}{\text{Cov}(Z, X)} = \frac{\text{Cov}(Z, 2X + U_Y)}{\text{Cov}(Z, X)} = \frac{2\text{Cov}(Z, X) + \text{Cov}(Z, U_Y)}{\text{Cov}(Z, X)} = 2$$

IV 추정량은 $\beta = 2$를 일치 추정한다.

**예제 4 (심슨의 역설과 교란):** UC 버클리 대학원 입학 데이터(1973) — 성별에 따른 입학률 차이.

|       | 지원자 수 | 입학률 |
|-------|----------|--------|
| 남성  | 8442     | 44%    |
| 여성  | 4321     | 35%    |

성별($X$)과 입학($Y$) 사이에 상관이 있어 보이지만, 학과($Z$)로 층화(stratify)하면 상황이 역전된다: 대부분의 학과에서 여성의 입학률이 더 높다.

**원인:** 학과별 지원률의 차이(여성은 입학률이 낮은 인기 학과에 집중 지원)가 교란을 유발했다. $Z$(학과)가 $X$(성별)와 $Y$(입학)의 공통 원인은 아니지만, $X$와 $Y$의 관계를 교란하는 역할을 한다.

백도어 조정: $P(Y|\text{do}(X)) = \sum_z P(Y|X, z) P(z)$를 적용하면, 성별의 인과 효과는 각 학과 내 입학률의 가중평균이 된다. 대부분의 학과에서 여성 입학률이 더 높거나 비슷하므로, 실제로는 성별 차별이 없었거나 오히려 여성에게 유리했다는 결론이 나온다.

**예제 5 (반사실 — 개인 수준의 인과):** 특정 환자가 약물 $X=1$을 복용했고 회복 $Y=1$했다. "약물을 복용하지 않았다면($X=0$) 회복했을까?"라는 반사실 질문이 있다.

잠재적 결과(potential outcome) 프레임워크에서:
$Y(1)$: 약물 복용 시 결과(관측됨, $Y=1$)
$Y(0)$: 약물 미복용 시 결과(반사실, 미관측)

개인 수준 인과 효과: $\tau = Y(1) - Y(0)$

$\tau$는 직접 관측할 수 없는 **근본적 인과 추론 문제(fundamental problem of causal inference)**다. 한 개인에 대해 두 결과를 동시에 관측할 수 없기 때문이다. RCT는 집단 수준에서 $\mathbb{E}[Y(1)] - \mathbb{E}[Y(0)]$을 식별한다.

## 연결

- **[회귀분석](topics/regression-analysis.html)** : 회귀분석에서 통제 변수를 추가하는 것은 교란 통제의 한 형태다. 그러나 "통제하면 된다"는 단순한 생각은 위험하다 — 통제해서는 안 되는 변수(매개변수, mediator; 충돌변수, collider)가 있다.
- **[조건부 확률의 함정](topics/conditional-traps.html)** : 심슨의 역설은 조건부 확률의 오해에서 비롯된다. 층화(stratification)가 역설을 만들 수도 있고 해결할 수도 있으며, 이는 인과 구조에 의존한다.
- **[상관관계와 인과](topics/joint-marginal-conditional.html)** : 결합분포 $P(X,Y)$와 조건부분포 $P(Y|X)$는 인과 관계 없이도 강한 상관을 보일 수 있다. 인과추론은 $P(Y|X)$에서 $P(Y|\text{do}(X))$를 분리하는 방법이다.
- **[가설검정](topics/hypothesis-testing.html)** : RCT에서 처리 효과의 통계적 유의성은 가설검정을 통해 평가한다. p-value는 인과 효과의 존재 여부를 판단하는 한 도구이지, 인과 효과 그 자체는 아니다.
