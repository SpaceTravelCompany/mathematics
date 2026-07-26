---
title: 회귀분석
slug: regression-analysis
---

## 직관적 설명

**회귀분석(regression analysis)**은 변수들 사이의 관계를 추정하고 예측하는 통계적 방법이다. "함께 움직인다"는 "원인이다"를 의미하지 않는다는 점이 가장 중요한 통찰이다.

단순 선형회귀(simple linear regression)는 하나의 설명변수(predictor) $X$와 반응변수(response) $Y$ 사이의 관계를 직선으로 모델링한다:
$$Y = \beta_0 + \beta_1 X + \epsilon$$

여기서 $\beta_0$는 절편(intercept), $\beta_1$은 기울기(slope), $\epsilon$은 오차항(error term)이다. 최소제곱법(ordinary least squares, OLS)은 잔차(residual) $e_i = y_i - \hat{y}_i$의 제곱합을 최소화하는 $\hat{\beta}_0, \hat{\beta}_1$을 찾는다.

회귀분석의 핵심 가정은 다음과 같다: (1) 선형성(linearity) — $X$와 $Y$의 관계가 선형, (2) 독립성(independence) — 오차가 서로 독립, (3) 등분산성(homoscedasticity) — 오차의 분산이 일정, (4) 정규성(normality) — 오차가 정규분포를 따름. 이 가정들이 깨지면 추정량의 성질이 달라진다.

**다중공선성(multicollinearity)**은 설명변수들 사이에 강한 상관관계가 있을 때 발생한다. 회귀계수의 표준오차가 커져 추정이 불안정해지고, 개별 변수의 효과를 분리하기 어려워진다. 분산팽창계수(VIF)로 진단한다.

**과적합(overfitting)**은 모델이 데이터의 우연한 패턴까지 학습하여 새로운 데이터에 대한 예측 성능이 떨어지는 현상이다. 변수가 많고 표본이 적을수록 과적합 위험이 커진다.

## 정의

**단순 선형회귀 모델 (simple linear regression model):**
$$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i, \quad i = 1, \ldots, n$$
$$\epsilon_i \stackrel{\text{iid}}{\sim} \mathcal{N}(0, \sigma^2)$$

**최소제곱 추정량 (OLS estimators):**
$$\hat{\beta}_1 = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^n (x_i - \bar{x})^2} = \frac{S_{xy}}{S_{xx}}$$
$$\hat{\beta}_0 = \bar{y} - \hat{\beta}_1 \bar{x}$$

**적합값 (fitted values)과 잔차 (residuals):**
$$\hat{y}_i = \hat{\beta}_0 + \hat{\beta}_1 x_i, \quad e_i = y_i - \hat{y}_i$$

**다중 선형회귀 (multiple linear regression):** $p$개의 설명변수가 있는 경우
$$Y_i = \beta_0 + \beta_1 X_{i1} + \cdots + \beta_p X_{ip} + \epsilon_i$$

행렬 표기법: $\mathbf{y} = X\boldsymbol{\beta} + \boldsymbol{\epsilon}$, 여기서 $X$는 $n \times (p+1)$ 설계행렬(design matrix), $\boldsymbol{\beta}$는 $(p+1) \times 1$ 계수벡터.

**OLS 추정량 (행렬 형태):** $\| \mathbf{y} - X\beta \|^2$ 최소화 → 정규방정식(normal equation):
$$X^T X \hat{\boldsymbol{\beta}} = X^T \mathbf{y}$$
$$\hat{\boldsymbol{\beta}} = (X^T X)^{-1} X^T \mathbf{y}$$

**결정계수 (coefficient of determination):**
$$R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}} = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}$$

$R^2$는 모델이 설명하는 분산의 비율로, $0 \leq R^2 \leq 1$이다. $R^2 = 1$은 완벽한 적합, $R^2 = 0$은 모델이 평균보다 나을 게 없음을 의미한다.

**조정된 결정계수 (adjusted $R^2$):**
$$\bar{R}^2 = 1 - \frac{SS_{\text{res}}/(n-p-1)}{SS_{\text{tot}}/(n-1)}$$

변수가 추가될수록 $R^2$는 항상 증가하지만, $\bar{R}^2$는 불필요한 변수에 페널티를 준다.

## 주요 정리와 증명

### 정리 1: OLS 추정량의 유도 (정규방정식)

**서술:** $\boldsymbol{\beta}$의 OLS 추정량 $\hat{\boldsymbol{\beta}}$는 잔차 제곱합 $S(\boldsymbol{\beta}) = \|\mathbf{y} - X\boldsymbol{\beta}\|^2$를 최소화하며, 다음 정규방정식을 만족한다:
$$X^T X \hat{\boldsymbol{\beta}} = X^T \mathbf{y}$$

**증명:** 목적함수를 전개한다.
$$S(\boldsymbol{\beta}) = (\mathbf{y} - X\boldsymbol{\beta})^T (\mathbf{y} - X\boldsymbol{\beta}) = \mathbf{y}^T\mathbf{y} - 2\boldsymbol{\beta}^T X^T \mathbf{y} + \boldsymbol{\beta}^T X^T X \boldsymbol{\beta}$$

$\boldsymbol{\beta}$에 대해 미분하여 0으로 둔다.
$$\frac{\partial S}{\partial \boldsymbol{\beta}} = -2 X^T \mathbf{y} + 2 X^T X \boldsymbol{\beta} = 0$$

따라서 $X^T X \boldsymbol{\beta} = X^T \mathbf{y}$를 얻는다. $X^T X$가 가역($X$의 열이 일차독립)이면 유일해 $\hat{\boldsymbol{\beta}} = (X^T X)^{-1} X^T \mathbf{y}$를 가진다.

이 해가 실제로 최소값임을 확인하려면 헤세 행렬(2계 미분) $\partial^2 S / \partial \boldsymbol{\beta} \partial \boldsymbol{\beta}^T = 2 X^T X$이 양반정치(positive semidefinite)임을 확인하면 된다. $\square$

### 정리 2: 가우스-마르코프 정리 (Gauss-Markov Theorem)

**서술:** 오차항이 $\mathbb{E}[\epsilon_i] = 0$, $\text{Var}(\epsilon_i) = \sigma^2$, $\text{Cov}(\epsilon_i, \epsilon_j) = 0$ ($i \neq j$)을 만족할 때(정규성은 불필요), OLS 추정량 $\hat{\boldsymbol{\beta}}$는 최소분산 선형 비편향 추정량(Best Linear Unbiased Estimator, BLUE)이다. 즉, $\hat{\boldsymbol{\beta}}$의 각 성분은 모든 선형 비편향 추정량 중에서 가장 작은 분산을 가진다.

**증명 (단순회귀의 경우):** $\hat{\beta}_1 = \sum c_i y_i$ for $c_i = (x_i - \bar{x})/S_{xx}$임을 확인한다. $\hat{\beta}_1$은 선형 추정량이며, $\mathbb{E}[\hat{\beta}_1] = \beta_1$이므로 비편향이다.

다른 임의의 선형 비편향 추정량 $\tilde{\beta}_1 = \sum d_i y_i$를 고려하자. 비편향성 $\mathbb{E}[\tilde{\beta}_1] = \beta_1$은 $\sum d_i = 0$과 $\sum d_i x_i = 1$을 요구한다.

분산을 비교한다:
$$\text{Var}(\hat{\beta}_1) = \sigma^2 \sum c_i^2 = \frac{\sigma^2}{S_{xx}}$$
$$\text{Var}(\tilde{\beta}_1) = \sigma^2 \sum d_i^2$$

$d_i = c_i + (d_i - c_i) = c_i + e_i$라 쓰자. $\sum e_i = 0$, $\sum e_i x_i = 0$이다.
$$\sum d_i^2 = \sum c_i^2 + \sum e_i^2 + 2\sum c_i e_i$$

$\sum c_i e_i = \frac{1}{S_{xx}} \sum (x_i - \bar{x})e_i = 0$이므로,
$$\sum d_i^2 = \sum c_i^2 + \sum e_i^2 \geq \sum c_i^2$$

따라서 $\text{Var}(\tilde{\beta}_1) \geq \text{Var}(\hat{\beta}_1)$이며, 등호는 $e_i = 0$ 즉 모든 $i$에 대해 $d_i = c_i$일 때 성립한다. $\square$

**의미:** OLS 추정량은 선형 추정량 중 가장 효율적이다. 단, 이는 오차항의 등분산성과 무상관성이라는 조건 하에서만 성립한다. 이분산성(heteroscedasticity)이나 자기상관(autocorrelation)이 있으면 가중 최소제곱(WLS)이나 일반화 최소제곱(GLS)이 더 효율적일 수 있다.

### 정리 3: $\hat{\beta}_1$의 분산

**서술:** 단순 선형회귀에서 $\hat{\beta}_1$의 분산은 다음과 같다:
$$\text{Var}(\hat{\beta}_1) = \frac{\sigma^2}{\sum_{i=1}^n (x_i - \bar{x})^2} = \frac{\sigma^2}{S_{xx}}$$

**증명:** $\hat{\beta}_1 = \sum c_i y_i$ for $c_i = (x_i - \bar{x})/S_{xx}$이다. $y_i$들이 서로 독립이고 $\text{Var}(y_i) = \sigma^2$이므로
$$\text{Var}(\hat{\beta}_1) = \sum c_i^2 \text{Var}(y_i) = \sigma^2 \sum c_i^2$$

$\sum c_i^2$를 계산한다:
$$\sum c_i^2 = \sum \frac{(x_i - \bar{x})^2}{S_{xx}^2} = \frac{1}{S_{xx}^2} \cdot S_{xx} = \frac{1}{S_{xx}}$$

따라서 $\text{Var}(\hat{\beta}_1) = \sigma^2/S_{xx}$이다.

**관찰:** $\text{Var}(\hat{\beta}_1)$은 $S_{xx}$(설명변수의 변동)에 반비례한다. $x$값이 넓게 퍼져 있을수록 기울기 추정이 더 정밀해진다. $\sigma^2$의 불편 추정량은
$$\hat{\sigma}^2 = \frac{1}{n-2} \sum_{i=1}^n (y_i - \hat{y}_i)^2 = \frac{SS_{\text{res}}}{n-2}$$

이다. 자유도가 $n-2$인 이유는 두 개의 모수($\beta_0, \beta_1$)를 추정했기 때문이다. $\square$

### 정리 4: 상관과 인과의 차이 — 교란변수

**서술:** 관측된 상관관계 $P(Y|X)$는 인과관계 $P(Y|\text{do}(X))$와 일반적으로 같지 않다. 교란변수(confounder) $Z$가 $X$와 $Y$ 모두에 영향을 미칠 때, $X$와 $Y$ 사이에 가짜 상관(spurious correlation)이 발생할 수 있다.

**증명 (반례):** $Z \sim \text{Bernoulli}(0.5)$, $X = Z + \epsilon_X$, $Y = Z + \epsilon_Y$ ($\epsilon_X, \epsilon_Y$는 독립 표준정규)인 구조를 생각하자. $X$와 $Y$ 사이에는 상관관계가 있지만($\text{Cov}(X,Y) = \text{Var}(Z) > 0$), $X$를 조작해도 $Y$는 변하지 않는다 — $Y$는 오직 $Z$와 $\epsilon_Y$에만 의존하기 때문이다.

회귀분석에서 교란변수를 통제하지 않으면 편향(bias)이 발생한다:
$$\mathbb{E}[\hat{\beta}_1] = \beta_1 + \frac{\text{Cov}(X, Z)}{\text{Var}(X)} \cdot \gamma$$

여기서 $\gamma$는 $Z$의 $Y$에 대한 효과다. $\text{Cov}(X, Z) \neq 0$이면 추정량이 편향된다.

**심슨의 역설 (Simpson's paradox):** 집단 변수(group variable)를 통제하지 않으면 전체 상관관계와 그룹 내 상관관계의 방향이 반대가 될 수 있다. 이는 교란변수로 인한 가짜 상관의 극단적인 예다. $\square$

## 예제

**예제 1 (단순회귀 $\hat{\beta}$ 계산):** 다음 데이터에 대해 단순 선형회귀 $Y = \beta_0 + \beta_1 X$를 적합하라.

$X = (1, 2, 3, 4, 5)$, $Y = (2, 3, 5, 4, 6)$.

**풀이:**
$\bar{x} = 3$, $\bar{y} = 4$,
$$S_{xx} = \sum (x_i - 3)^2 = 4 + 1 + 0 + 1 + 4 = 10$$
$$S_{xy} = \sum (x_i - 3)(y_i - 4) = (-1)(-2) + (-1)(-1) + 0 + 1(0) + 2(2) = 2 + 1 + 0 + 0 + 4 = 7$$

$$\hat{\beta}_1 = \frac{7}{10} = 0.7, \quad \hat{\beta}_0 = 4 - 0.7 \times 3 = 4 - 2.1 = 1.9$$

회귀선: $\hat{Y} = 1.9 + 0.7X$.

**$R^2$ 계산:**
적합값: $\hat{y} = (2.6, 3.3, 4.0, 4.7, 5.4)$
잔차: $e = (-0.6, -0.3, 1.0, -0.7, 0.6)$
$$SS_{\text{res}} = 0.36 + 0.09 + 1.0 + 0.49 + 0.36 = 2.30$$
$$SS_{\text{tot}} = \sum (y_i - 4)^2 = 4 + 1 + 1 + 0 + 4 = 10$$
$$R^2 = 1 - \frac{2.30}{10} = 0.770$$

모델이 $Y$ 분산의 77%를 설명한다.

**예제 2 (다중회귀 행렬 계산):** $n = 4$, $p = 2$인 데이터:
$$X = \begin{pmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \\ 1 & 4 \end{pmatrix}, \quad \mathbf{y} = \begin{pmatrix} 2 \\ 3 \\ 5 \\ 4 \end{pmatrix}$$

(예제 1과 동일, $x_1$ 열은 절편)

$$X^T X = \begin{pmatrix} 1 & 1 & 1 & 1 \\ 1 & 2 & 3 & 4 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \\ 1 & 4 \end{pmatrix} = \begin{pmatrix} 4 & 10 \\ 10 & 30 \end{pmatrix}$$
$$(X^T X)^{-1} = \frac{1}{4 \cdot 30 - 10^2} \begin{pmatrix} 30 & -10 \\ -10 & 4 \end{pmatrix} = \frac{1}{20} \begin{pmatrix} 30 & -10 \\ -10 & 4 \end{pmatrix}$$
$$X^T \mathbf{y} = \begin{pmatrix} 1 & 1 & 1 & 1 \\ 1 & 2 & 3 & 4 \end{pmatrix} \begin{pmatrix} 2 \\ 3 \\ 5 \\ 4 \end{pmatrix} = \begin{pmatrix} 14 \\ 41 \end{pmatrix}$$

$$\hat{\boldsymbol{\beta}} = \frac{1}{20} \begin{pmatrix} 30 & -10 \\ -10 & 4 \end{pmatrix} \begin{pmatrix} 14 \\ 41 \end{pmatrix} = \frac{1}{20} \begin{pmatrix} 420 - 410 \\ -140 + 164 \end{pmatrix} = \frac{1}{20} \begin{pmatrix} 10 \\ 24 \end{pmatrix} = \begin{pmatrix} 0.5 \\ 1.2 \end{pmatrix}$$

회귀선: $\hat{Y} = 0.5 + 1.2X$. (예제 1과 다른 이유는 절편을 포함한 계산 방식의 차이 때문)

**예제 3 (다중공선성 예시):** 두 설명변수 $X_1$과 $X_2$가 거의 같은 정보를 가질 때($\text{Cor}(X_1, X_2) \approx 1$), 분산팽창계수(VIF)는
$$\text{VIF}_j = \frac{1}{1 - R_j^2}$$

여기서 $R_j^2$는 $X_j$를 나머지 설명변수들로 회귀한 결정계수다. $X_1$과 $X_2$의 상관계수가 0.95이면 $R_j^2 \approx 0.9025$, VIF $\approx 10.3$이다. VIF $> 10$은 심각한 다중공선성의 신호로, 개별 회귀계수의 표준오차가 $\sqrt{\text{VIF}}$ 배만큼 증가한다.

**해결책:** 상관이 높은 변수 중 하나를 제거하거나, 주성분 회귀(PCR), 능형 회귀(ridge regression) 등 정규화 방법을 사용한다.

**예제 4 (잔차 분석):** 예제 1의 잔차 $e = (-0.6, -0.3, 1.0, -0.7, 0.6)$를 분석한다.

(1) **등분산성 검토:** 잔차 vs 적합값 산점도(scatter plot)에서 잔차가 적합값에 따라 체계적인 패턴 없이 무작위로 퍼져 있어야 한다. 깔때기 모양(funnel shape)이 보이면 이분산성을 의심한다.

(2) **정규성 검토:** Q-Q plot(quantile-quantile plot)으로 잔차의 정규성을 확인한다. 잔차가 대각선을 따라 있으면 정규성 가정을 만족한다.

(3) **독립성 검토:** 더빈-왓슨(Durbin-Watson) 통계량으로 자기상관을 진단한다.

(4) **영향점 진단:** 쿡의 거리(Cook's distance)로 특정 관측값이 회귀계수 추정에 미치는 영향을 측정한다.
$$D_i = \frac{e_i^2}{(p+1)\hat{\sigma}^2} \cdot \frac{h_{ii}}{(1-h_{ii})^2}$$

여기서 $h_{ii}$는 지렛대값(leverage)이다.

**예제 5 (회귀분석에서의 가설검정):** $H_0: \beta_1 = 0$ vs $H_1: \beta_1 \neq 0$에 대한 t-검정:
$$t_{\text{obs}} = \frac{\hat{\beta}_1}{\text{SE}(\hat{\beta}_1)}$$

예제 1에서 $\hat{\sigma}^2 = 2.30/3 \approx 0.767$, $\text{SE}(\hat{\beta}_1) = \sqrt{0.767/10} \approx 0.277$,
$$t_{\text{obs}} = 0.7/0.277 \approx 2.527$$

자유도 3에서 $t_{0.025, 3} = 3.182$이므로 $H_0$를 기각할 수 없다 — 표본이 너무 작아 기울기가 유의하지 않다.

**예제 6 (과적합 예시):** 10개의 데이터 포인트에 9차 다항식을 적합하면 $R^2 = 1$이 된다 — 완벽한 적합. 하지만 이 모델은 데이터의 노이즈까지 학습했으므로 새로운 데이터에 대한 예측 성능이 매우 나쁘다. 교차 검증(cross-validation)으로 이를 진단한다: 훈련 $R^2$는 높지만 검증 $R^2$는 낮으면 과적합의 신호다.

## 연결

- **[최소제곱법](topics/least-squares.html)** : OLS 추정량은 최소제곱법의 통계적 응용이다. 정규방정식 $X^T X \hat{\beta} = X^T y$와 기하학적 해석(직교투영)이 동일하다.
- **[인과추론](topics/causal-inference.html)** : "상관≠인과"는 회귀분석 해석의 가장 큰 함정이다. 교란변수 통제를 위해 회귀에 추가 변수를 포함하는 것이 인과추론의 첫걸음이다.
- **[조건부 확률의 함정](topics/conditional-traps.html)** : 심슨의 역설과 교란변수는 조건부 확률의 오해에서 비롯된다. 회귀분석에서 조건부 편향(selection bias)의 이해에 연결된다.
- **[가설검정](topics/hypothesis-testing.html)** : 회귀계수의 t-검정과 F-검정은 가설검정의 틀을 따른다. 다중검정 문제는 단계적 변수 선택에서 중요해진다.
- **[고유값·고유벡터](topics/eigenvalues.html)** : 다중공선성은 $X^T X$의 조건수(condition number)가 클 때 발생하며, 이는 작은 고유값에 대응한다. 주성분 회귀(PCA regression)는 고유값 분해로 다중공선성을 해결한다.
