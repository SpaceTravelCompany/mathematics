---
title: 시그모이드·소프트맥스 미분
slug: sigmoid-softmax
---

## 직관적 설명

**시그모이드 함수(sigmoid function)** $\sigma(x) = \frac{1}{1+e^{-x}}$는 입력을 $(0, 1)$ 구간으로 압축하는 S자 곡선이다. 큰 양수 입력은 1에, 큰 음수 입력은 0에 가까워진다. 매끄러운 계단 함수(smooth step function)라고 생각할 수 있다.

시그모이드의 미분은 $\sigma'(x) = \sigma(x)(1 - \sigma(x))$로, 매우 간단한 형태다. 이는 $\sigma$의 값만 알면 미분을 바로 계산할 수 있어 효율적이다. $\sigma'(x)$는 $x = 0$에서 최대값 $1/4$를 가지며, 양 끝($x \to \pm\infty$)에서는 0에 수렴한다. 이 현상을 **기울기 소실(vanishing gradient)** 이라 부르며, 깊은 구조에서 학습을 어렵게 만드는 원인 중 하나다.

**소프트맥스 함수(softmax function)** 는 시그모이드를 다중 클래스로 확장한다. $K$개의 실수 입력을 받아 $K$개의 양수 출력으로 변환하며, 출력의 합은 항상 1이다(확률분포). $i$번째 출력은:

$$\text{softmax}(x_i) = \frac{e^{x_i}}{\sum_{j=1}^K e^{x_j}}$$

소프트맥스의 미분(야코비안, Jacobian)은 $\frac{\partial s_i}{\partial x_j} = s_i(\delta_{ij} - s_j)$로, 시그모이드 미분의 행렬 일반화로 볼 수 있다.

## 정의

**시그모이드 함수 (sigmoid / logistic function):**

$$\sigma(x) = \frac{1}{1 + e^{-x}} = \frac{e^x}{1 + e^x}$$

**성질:**
- $\sigma: \mathbb{R} \to (0, 1)$
- 단조 증가(strictly monotonic increasing)
- 대칭: $\sigma(-x) = 1 - \sigma(x)$
- $\sigma(0) = 1/2$
- $\lim_{x \to \infty} \sigma(x) = 1$, $\lim_{x \to -\infty} \sigma(x) = 0$

**시그모이드 미분 (derivative of sigmoid):**

$$\sigma'(x) = \sigma(x)(1 - \sigma(x))$$

**소프트맥스 함수 (softmax function):** $x = (x_1, \ldots, x_K) \in \mathbb{R}^K$에 대해:

$$s_i = \text{softmax}(x_i) = \frac{e^{x_i}}{\sum_{j=1}^K e^{x_j}}, \quad i = 1, \ldots, K$$

**성질:**
- $s_i > 0$, $\sum_{i=1}^K s_i = 1$ → 확률분포
- 병진 불변(translation invariance): $s_i(x + c) = s_i(x)$, 여기서 $x + c = (x_1 + c, \ldots, x_K + c)$
- 순서 보존: $x_i > x_j$이면 $s_i > s_j$

**소프트맥스 야코비안 (softmax Jacobian):**

$$\frac{\partial s_i}{\partial x_j} = s_i (\delta_{ij} - s_j)$$

여기서 $\delta_{ij}$는 크로네커 델타(Kronecker delta): $i = j$일 때 1, $i \neq j$일 때 0.

**야코비안 행렬 ($K \times K$):**

$$J_s(x) = \begin{pmatrix}
s_1(1-s_1) & -s_1 s_2 & \cdots & -s_1 s_K \\
-s_2 s_1 & s_2(1-s_2) & \cdots & -s_2 s_K \\
\vdots & \vdots & \ddots & \vdots \\
-s_K s_1 & -s_K s_2 & \cdots & s_K(1-s_K)
\end{pmatrix}$$

**온도 파라미터가 있는 소프트맥스 (softmax with temperature):**

$$s_i = \frac{e^{x_i / T}}{\sum_j e^{x_j / T}}$$

$T > 0$는 온도(temperature) 파라미터다. $T \to 0$이면 argmax(one-hot)에 수렴하고, $T \to \infty$이면 균등분포에 수렴한다.

## 주요 정리와 증명

### 정리 1: 시그모이드 미분 공식 $\sigma'(x) = \sigma(x)(1-\sigma(x))$

**증명:** $\sigma(x) = (1 + e^{-x})^{-1}$로 쓰고 직접 미분한다.

$$\sigma'(x) = -1 \cdot (1 + e^{-x})^{-2} \cdot (-e^{-x}) = \frac{e^{-x}}{(1 + e^{-x})^2}$$

다른 형태로 변형:

$$\sigma'(x) = \frac{1}{1 + e^{-x}} \cdot \frac{e^{-x}}{1 + e^{-x}} = \sigma(x) \cdot \frac{e^{-x}}{1 + e^{-x}}$$

$\frac{e^{-x}}{1 + e^{-x}} = \frac{1}{1 + e^x} = 1 - \frac{1}{1 + e^{-x}} = 1 - \sigma(x)$이므로:

$$\sigma'(x) = \sigma(x)(1 - \sigma(x))$$

$\square$

**대체 증명 (항등식 활용):** $\sigma(x) = \frac{e^x}{1 + e^x}$로 쓰고 미분:

$$\sigma'(x) = \frac{e^x(1+e^x) - e^x \cdot e^x}{(1+e^x)^2} = \frac{e^x}{(1+e^x)^2} = \frac{e^x}{1+e^x} \cdot \frac{1}{1+e^x} = \sigma(x)(1-\sigma(x))$$

**따름정리:** $\sigma'(0) = \sigma(0)(1-\sigma(0)) = \frac{1}{2} \cdot \frac{1}{2} = \frac{1}{4}$.

### 정리 2: 소프트맥스 야코비안 유도 (Softmax Jacobian Derivation)

$s_i = \frac{e^{x_i}}{\sum_j e^{x_j}}$의 편미분 $\frac{\partial s_i}{\partial x_j}$를 구한다.

**증명 (몫 법칙, quotient rule):** 분모 $D = \sum_{k=1}^K e^{x_k}$라 하자. $s_i = e^{x_i} / D$.

**Case 1: $i = j$**

$$\frac{\partial s_i}{\partial x_i} = \frac{e^{x_i} D - e^{x_i} \cdot e^{x_i}}{D^2} = \frac{e^{x_i}(D - e^{x_i})}{D^2} = \frac{e^{x_i}}{D} \cdot \frac{D - e^{x_i}}{D} = s_i(1 - s_i)$$

**Case 2: $i \neq j$**

$$\frac{\partial s_i}{\partial x_j} = \frac{0 \cdot D - e^{x_i} \cdot e^{x_j}}{D^2} = -\frac{e^{x_i} e^{x_j}}{D^2} = -\frac{e^{x_i}}{D} \cdot \frac{e^{x_j}}{D} = -s_i s_j$$

두 경우를 통합하면 $\frac{\partial s_i}{\partial x_j} = s_i(\delta_{ij} - s_j)$.

$\square$

### 정리 3: 소프트맥스의 야코비안은 대칭이고 양반정치 (Softmax Jacobian is Symmetric PSD)

$J_s(x)$는 대칭행렬이고 양반정치(positive semidefinite)이며, rank는 $K-1$이다.

**증명:** $\frac{\partial s_i}{\partial x_j} = s_i \delta_{ij} - s_i s_j$이므로 $J_s = \text{diag}(s) - s s^T$로 쓸 수 있다(여기서 $s = (s_1, \ldots, s_K)^T$). $J_s$의 대칭성은 자명하다.

임의의 벡터 $v \in \mathbb{R}^K$에 대해:

$$v^T J_s v = \sum_{i,j} v_i (s_i \delta_{ij} - s_i s_j) v_j = \sum_i s_i v_i^2 - \left(\sum_i s_i v_i\right)^2$$

$s_i > 0$이고 $\sum s_i = 1$이므로, 이는 확률분포 $s$에 대한 $v$의 분산(variance)이다:

$$v^T J_s v = \text{Var}_s[v] = \mathbb{E}_s[v^2] - (\mathbb{E}_s[v])^2 \geq 0$$

따라서 $J_s$는 양반정치이다. $v^T J_s v = 0$인 필요충분조건은 $v$가 상수벡터($v_1 = \cdots = v_K$)인 것뿐이므로, nullspace의 차원은 1, rank는 $K-1$이다.

$\square$

### 정리 4: 시그모이드의 극한과 기울기 소실 (Vanishing Gradient)

$$\lim_{x \to \infty} \sigma'(x) = 0, \quad \lim_{x \to -\infty} \sigma'(x) = 0$$

**증명:** $\sigma'(x) = \sigma(x)(1 - \sigma(x))$에서 $\lim_{x \to \infty} \sigma(x) = 1$, $\lim_{x \to -\infty} \sigma(x) = 0$이므로:

$$\lim_{x \to \infty} \sigma'(x) = 1 \cdot 0 = 0, \quad \lim_{x \to -\infty} \sigma'(x) = 0 \cdot 1 = 0$$

$\square$

**의미:** $\sigma'(x)$는 $x = 0$에서 $1/4$로 최대이며, $|x|$가 커질수록 0에 수렴한다. 따라서 시그모이드 뉴런이 포화(saturation) 상태(출력이 0 또는 1에 가까움)이면 그래디언트가 거의 0이 되어 학습이 느려지거나 멈춘다. 이것이 기울기 소실(vanishing gradient) 문제다.

### 정리 5: 소프트맥스의 병진 불변성 (Translation Invariance)

모든 $c \in \mathbb{R}$에 대해 $\text{softmax}(x_i + c) = \text{softmax}(x_i)$.

**증명:**

$$\text{softmax}(x_i + c) = \frac{e^{x_i + c}}{\sum_j e^{x_j + c}} = \frac{e^c e^{x_i}}{e^c \sum_j e^{x_j}} = \frac{e^{x_i}}{\sum_j e^{x_j}} = \text{softmax}(x_i)$$

$\square$

**의미:** 소프트맥스는 입력의 절대적 크기가 아닌 상대적 차이에만 의존한다. 따라서 수치적으로 안정적인(numerically stable) 계산을 위해 $\tilde{x}_i = x_i - \max_j x_j$로 시프트해도 결과가 같다.

## 예제

**예제 1:** $\sigma'(0) = 1/4$를 검증하고, $\sigma'(2)$와 $\sigma'(-2)$를 계산하라.

**풀이:** $\sigma(0) = \frac{1}{1+e^0} = \frac{1}{2}$, $\sigma'(0) = \frac{1}{2} \cdot \frac{1}{2} = \frac{1}{4}$.

$\sigma(2) = \frac{1}{1+e^{-2}} \approx \frac{1}{1+0.1353} \approx 0.8808$, $\sigma'(2) \approx 0.8808 \times 0.1192 \approx 0.1050$.

$\sigma(-2) = \frac{1}{1+e^{2}} \approx \frac{1}{1+7.389} \approx 0.1192$, $\sigma'(-2) \approx 0.1192 \times 0.8808 \approx 0.1050$.

$\sigma'(2) = \sigma'(-2)$로 대칭성을 확인할 수 있다. 두 값 모두 $1/4$보다 작다.

**예제 2:** 3클래스 소프트맥스 $x = (1, 2, 3)$에 대해 출력 $s$와 야코비안 $J_s$를 계산하라.

**풀이:** $D = e^1 + e^2 + e^3 \approx 2.718 + 7.389 + 20.086 = 30.193$.

$s_1 = 2.718/30.193 \approx 0.090$, $s_2 = 7.389/30.193 \approx 0.245$, $s_3 = 20.086/30.193 \approx 0.665$.

야코비안:

$$J_s = \begin{pmatrix}
s_1(1-s_1) & -s_1 s_2 & -s_1 s_3 \\
-s_2 s_1 & s_2(1-s_2) & -s_2 s_3 \\
-s_3 s_1 & -s_3 s_2 & s_3(1-s_3)
\end{pmatrix}
\approx \begin{pmatrix}
0.0819 & -0.0221 & -0.0599 \\
-0.0221 & 0.1850 & -0.1629 \\
-0.0599 & -0.1629 & 0.2228
\end{pmatrix}$$

각 행의 합: $0.0819 - 0.0221 - 0.0599 = 0$, $i \neq j$의 합과 $i = j$ 항이 상쇄됨을 확인할 수 있다.

고유값: $0$, $\approx 0.047$, $\approx 0.443$ — 하나는 0(병진 불변성), 나머지는 양수.

**예제 3:** $\sigma(x) = \frac{1}{1+e^{-x}}$의 $x = 1$에서 접선의 방정식을 구하고, $\sigma(1.1)$의 선형 근사값과 실제값을 비교하라.

**풀이:** $\sigma(1) = \frac{1}{1+e^{-1}} \approx \frac{1}{1+0.3679} \approx 0.7311$.

$\sigma'(1) = \sigma(1)(1-\sigma(1)) \approx 0.7311 \times 0.2689 \approx 0.1966$.

접선: $y = \sigma(1) + \sigma'(1)(x-1) = 0.7311 + 0.1966(x-1)$.

$x = 1.1$: 근사값 $= 0.7311 + 0.1966 \times 0.1 \approx 0.7508$.

실제값: $\sigma(1.1) = \frac{1}{1+e^{-1.1}} \approx \frac{1}{1+0.3329} \approx 0.7503$.

오차 $\approx 0.0005$로 1차 근사가 꽤 정확하다.

**예제 4 (온도 파라미터):** $x = (1, 2, 3)$에서 온도 $T = 0.5$, $T = 1$, $T = 2$의 소프트맥스 출력을 비교하라.

**풀이:**

$T = 0.5$: $\tilde{x} = (2, 4, 6)$, $D = e^2 + e^4 + e^6 \approx 7.389 + 54.598 + 403.429 = 465.416$.

$s \approx (0.016, 0.117, 0.867)$ — 가장 큰 값에 집중(날카로운 분포, peaked).

$T = 1$: $s \approx (0.090, 0.245, 0.665)$ (위 예제 2).

$T = 2$: $\tilde{x} = (0.5, 1, 1.5)$, $D = e^{0.5} + e^1 + e^{1.5} \approx 1.649 + 2.718 + 4.482 = 8.849$.

$s \approx (0.186, 0.307, 0.507)$ — 더 평평한 분포(flat, uniform에 가까움).

온도가 낮을수록 최대값이 두드러지고, 온도가 높을수록 분포가 균등해진다.

**예제 5 (시그모이드와 소프트맥스의 관계):** 2클래스 소프트맥스가 시그모이드와 동등함을 보여라.

**풀이:** 클래스 2개 $x_1, x_2$에 대해 소프트맥스:

$$s_1 = \frac{e^{x_1}}{e^{x_1} + e^{x_2}} = \frac{1}{1 + e^{-(x_1 - x_2)}} = \sigma(x_1 - x_2)$$

$s_2 = 1 - s_1 = \sigma(x_2 - x_1)$. 따라서 2클래스 소프트맥스는 두 출력의 차이에 대한 시그모이드와 같다.

**예제 6 (로그-소프트맥스, Log-Softmax):** $\log s_i = x_i - \log\sum_j e^{x_j}$의 미분을 구하라.

**풀이:** $\frac{\partial}{\partial x_j} \log s_i = \frac{1}{s_i} \cdot \frac{\partial s_i}{\partial x_j} = \frac{1}{s_i} \cdot s_i(\delta_{ij} - s_j) = \delta_{ij} - s_j$.

로그-소프트맥스의 미분은 $\delta_{ij} - s_j$로 매우 간단하다. 따라서 소프트맥스에 로그를 취한 형태(cross-entropy loss에 자주 등장)의 그래디언트 계산이 효율적이다.

**예제 7 (시그모이드의 2계 도함수):** $\sigma''(x)$를 구하고 $\sigma''(0)$을 계산하라.

**풀이:** $\sigma'(x) = \sigma(x)(1 - \sigma(x))$에서:

$$\sigma''(x) = \sigma'(x)(1 - \sigma(x)) + \sigma(x)(-\sigma'(x)) = \sigma'(x)(1 - 2\sigma(x))$$

$\sigma'(x) = \sigma(x)(1-\sigma(x))$를 대입:

$$\sigma''(x) = \sigma(x)(1-\sigma(x))(1 - 2\sigma(x))$$

$\sigma''(0) = \frac{1}{2} \cdot \frac{1}{2} \cdot (1 - 1) = 0$. $x = 0$에서 $\sigma$는 선형에 가깝고(변곡점, inflection point), $\sigma''(x) = 0$이다.

**예제 8:** $L(s, y) = -\sum_{i=1}^K y_i \log s_i$ (cross-entropy)에서 $s = \text{softmax}(x)$일 때 $\frac{\partial L}{\partial x_j}$를 구하라($y$는 one-hot 벡터: $y_k = 1$, 나머지 0).

**풀이:** $L = -\sum_i y_i \log s_i$이고 $y_k = 1$, $y_{i \neq k} = 0$이므로 $L = -\log s_k$.

$$\frac{\partial L}{\partial x_j} = -\frac{1}{s_k} \cdot \frac{\partial s_k}{\partial x_j} = -\frac{1}{s_k} \cdot s_k(\delta_{kj} - s_j) = -( \delta_{kj} - s_j) = s_j - \delta_{kj}$$

따라서 $\frac{\partial L}{\partial x_j} = \begin{cases} s_k - 1 & (j = k) \\ s_j & (j \neq k) \end{cases}$.

묶어 쓰면 $\frac{\partial L}{\partial x} = s - y$, 즉 그래디언트가 예측 $s$와 정답 $y$의 차이로 아주 단순해진다.

## 연결

- **[지수·로그 함수의 미분](topics/exp-log-calculus.html)** : 시그모이드와 소프트맥스의 정의에 $e^x$가 핵심이다.
- **[엔트로피·KL발산](topics/entropy-kl.html)** : 소프트맥스 출력과 cross-entropy의 연결을 통해 확률분포 간의 거리를 측정한다.
- **[연쇄법칙](topics/differentiation-rules.html)** : 로그-소프트맥스 미분에서 연쇄법칙이 사용된다.
- **[야코비안·헤시안](topics/jacobian-hessian.html)** : 소프트맥스 야코비안은 다변수 벡터 함수 미분의 대표적 예시다.
