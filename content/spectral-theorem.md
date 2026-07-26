---
title: 대칭행렬·스펙트럼 정리·이차형식
slug: spectral-theorem
---

## 직관적 설명

**대칭행렬(symmetric matrix)**은 전치해도 자기 자신과 같은 행렬 $A = A^T$이다. 대칭행렬은 놀라운 성질을 가진다: 모든 고유값이 실수이고, 서로 다른 고유값에 대응하는 고유벡터들이 서로 직교하며, 항상 **직교 대각화(orthogonal diagonalization)**가 가능하다. 이 결과를 **스펙트럼 정리(spectral theorem)**라고 부른다.

**이차형식(quadratic form)** $Q(x) = x^T A x$는 대칭행렬 $A$가 정의하는 2차 함수다. $x^T A x$의 값의 부호와 분포는 $A$의 고유값에 의해 완전히 결정된다. 양정치(positive definite) 행렬의 이차형식은 타원체(ellipsoid)를, 부정부정(indefinite) 행렬은 쌍곡면(hyperboloid)을 정의한다.

스펙트럼 정리는 양자역학에서 관측 가능량(observable)이 에르미트 연산자(Hermitian operator)로 표현되는 이유의 수학적 기초다. 또한 주성분 분석(PCA), 이차 최적화(quadratic programming), 그래프 이론의 라플라시안 등 수많은 응용의 핵심에 자리잡고 있다.

## 정의

**대칭행렬 (symmetric matrix):** $A = A^T$를 만족하는 실정사각행렬. 즉, $a_{ij} = a_{ji}$.

**에르미트 행렬 (Hermitian matrix):** $A = A^*$를 만족하는 복소정사각행렬. 여기서 $A^* = \bar{A}^T$는 켤레전치(conjugate transpose)다. $A$가 실수이면 에르미트 = 대칭이다.

**이차형식 (quadratic form):** 대칭행렬 $A \in \mathbb{R}^{n \times n}$에 대해
$$Q(x) = x^T A x = \sum_{i=1}^n \sum_{j=1}^n a_{ij} x_i x_j$$

**직교 대각화 (orthogonal diagonalization):** 직교행렬 $Q$ ($Q^T Q = I$)와 대각행렬 $\Lambda$가 존재하여
$$A = Q \Lambda Q^T = \sum_{i=1}^n \lambda_i q_i q_i^T$$

여기서 $q_i$는 $Q$의 $i$번째 열(정규직교 고유벡터)이고 $\lambda_i$는 대응하는 고유값이다.

**레일리 몫 (Rayleigh quotient):** 영 아닌 벡터 $x$에 대해
$$R(x) = \frac{x^T A x}{x^T x}$$

대칭행렬의 경우, 레일리 몫의 최대값과 최소값은 각각 최대·최소 고유값이며, $x$가 대응하는 고유벡터일 때 달성된다.

**이차형식의 분류:**
- **양정치 (positive definite):** $x \neq 0 \Rightarrow x^T A x > 0$ (모든 고유값 > 0)
- **양반정치 (positive semidefinite):** $x \neq 0 \Rightarrow x^T A x \geq 0$ (모든 고유값 $\geq$ 0)
- **음정치 (negative definite):** $x \neq 0 \Rightarrow x^T A x < 0$ (모든 고유값 < 0)
- **부정부정 (indefinite):** 양수와 음수 값을 모두 가짐 (고유값에 양수와 음수 섞임)

## 주요 정리와 증명

### 정리 1: 대칭행렬의 고유값은 실수

실대칭행렬 $A$의 모든 고유값은 실수다.

**증명:** $\lambda$를 $A$의 고유값, $v$를 대응하는 고유벡터라 하자($Av = \lambda v$, $v \neq 0$). $\bar{v}^T A v$를 두 가지 방식으로 계산한다.

먼저 $Av = \lambda v$를 대입하면
$$\bar{v}^T A v = \bar{v}^T (\lambda v) = \lambda \|v\|^2$$

다음으로 $A = A^T$임을 이용한다. $\bar{v}^T A v$는 스칼라이므로 자신의 전치와 같다:
$$\bar{v}^T A v = (\bar{v}^T A v)^T = v^T A^T \bar{v} = v^T A \bar{v}$$

$A$가 실수행렬이므로 $A\bar{v} = \overline{Av} = \bar{\lambda} \bar{v}$이다. 따라서
$$\bar{v}^T A v = v^T (\bar{\lambda} \bar{v}) = \bar{\lambda} \|v\|^2$$

위에서 구한 두 표현을 같게 놓으면
$$\lambda \|v\|^2 = \bar{\lambda} \|v\|^2$$

$\|v\| \neq 0$이므로 $\lambda = \bar{\lambda}$, 즉 $\lambda$는 실수다.

### 정리 2: 대칭행렬의 서로 다른 고유값의 고유벡터는 직교

실대칭행렬 $A$의 두 고유값 $\lambda \neq \mu$와 대응하는 고유벡터 $v$, $w$에 대해 $\langle v, w \rangle = 0$이다.

**증명:** $Av = \lambda v$, $Aw = \mu w$이고 $A = A^T$이다.
$$\langle Av, w \rangle = (\lambda v)^T w = \lambda v^T w$$

한편 $A$의 대칭성을 이용하면
$$\langle Av, w \rangle = (Av)^T w = v^T A^T w = v^T A w = v^T (\mu w) = \mu v^T w$$

따라서 $\lambda v^T w = \mu v^T w$, 즉 $(\lambda - \mu) v^T w = 0$이다. $\lambda \neq \mu$이므로 $v^T w = 0$이고, 따라서 $v \perp w$이다.

### 정리 3: 스펙트럼 정리 (Spectral Theorem for Real Symmetric Matrices)

실대칭행렬 $A \in \mathbb{R}^{n \times n}$은 직교 대각화 가능하다. 즉, 직교행렬 $Q$와 대각행렬 $\Lambda = \text{diag}(\lambda_1, \ldots, \lambda_n)$가 존재하여
$$A = Q \Lambda Q^T$$

**증명 (귀납법):** $n = 1$인 경우 자명하다. $n \geq 2$라 가정하자.

1단계: 정리 1에 의해 $A$는 실고유값 $\lambda_1$과 대응하는 단위 고유벡터 $q_1$($\|q_1\| = 1$)을 가진다.

2단계: $q_1$을 첫 번째 열로 포함하는 정규직교기저 $\{q_1, u_2, \ldots, u_n\}$를 구성한다(예: 그람-슈미트). $Q_1 = [q_1 \; u_2 \; \cdots \; u_n]$을 직교행렬이라 하자.

3단계: $Q_1^T A Q_1$을 계산한다. 첫 번째 열은 $Q_1^T A q_1 = Q_1^T (\lambda_1 q_1) = \lambda_1 Q_1^T q_1 = \lambda_1 e_1$ ($e_1$은 첫 번째 표준단위벡터). 첫 번째 행도 대칭성에 의해 $\lambda_1 e_1^T$가 된다. 따라서
$$Q_1^T A Q_1 = \begin{pmatrix} \lambda_1 & 0 \\ 0 & B \end{pmatrix}$$
여기서 $B$는 $(n-1) \times (n-1)$ 대칭행렬이다($Q_1^T A Q_1$이 대칭이므로 $B$도 대칭).

4단계: 귀납가설에 의해 $(n-1) \times (n-1)$ 대칭행렬 $B$는 직교 대각화 가능하다. 즉, 직교행렬 $Q_2'$가 존재하여 $B = Q_2' \Lambda_2 Q_2'^T$이다.

5단계: $Q_2 = \begin{pmatrix} 1 & 0 \\ 0 & Q_2' \end{pmatrix}$라 정의하면 $Q_2$는 직교행렬이다. $Q = Q_1 Q_2$로 두면
$$Q^T A Q = Q_2^T (Q_1^T A Q_1) Q_2 = \begin{pmatrix} 1 & 0 \\ 0 & Q_2'^T \end{pmatrix} \begin{pmatrix} \lambda_1 & 0 \\ 0 & B \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & Q_2' \end{pmatrix} = \begin{pmatrix} \lambda_1 & 0 \\ 0 & \Lambda_2 \end{pmatrix} = \Lambda$$

$Q$는 직교행렬들의 곱이므로 직교행렬이다. 따라서 $A = Q \Lambda Q^T$.

**따름정리 (스펙트럼 분해):**
$$A = \sum_{i=1}^n \lambda_i q_i q_i^T$$
여기서 $q_i$는 정규직교 고유벡터들이다. 이 표현을 $A$의 **스펙트럼 분해(spectral decomposition)**라 한다.

### 정리 4: 이차형식의 주축 정리 (Principal Axis Theorem)

대칭행렬 $A$에 대해 이차형식 $x^T A x$는 직교변수변환 $x = Qy$ ($Q$ 직교)를 통해 표준형으로 변환된다:
$$x^T A x = y^T \Lambda y = \sum_{i=1}^n \lambda_i y_i^2$$

**증명:** 스펙트럼 정리에 의해 $A = Q \Lambda Q^T$ ($Q$ 직교)이므로
$$x^T A x = x^T Q \Lambda Q^T x = (Q^T x)^T \Lambda (Q^T x) = y^T \Lambda y = \sum_{i=1}^n \lambda_i y_i^2$$

여기서 $y = Q^T x$이다. $Q$가 직교이므로 $\|y\| = \|x\|$이다.

**기하학적 해석:** $x^T A x = 1$은 $\sum \lambda_i y_i^2 = 1$로 변환된다. $\lambda_i$의 부호에 따라 이는 타원체(모두 > 0), 쌍곡면(섞인 부호), 또는 실린더(일부 = 0)를 정의한다.

### 정리 5: 레일리-리츠 정리 (Rayleigh-Ritz Theorem)

대칭행렬 $A$의 고유값을 $\lambda_{\min} = \lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n = \lambda_{\max}$라 할 때
$$\lambda_{\min} = \min_{\|x\| = 1} x^T A x, \quad \lambda_{\max} = \max_{\|x\| = 1} x^T A x$$

더 일반적으로 (Courant-Fischer min-max 정리):
$$\lambda_k = \min_{\dim S = k} \max_{0 \neq x \in S} \frac{x^T A x}{x^T x} = \max_{\dim S = n-k+1} \min_{0 \neq x \in S} \frac{x^T A x}{x^T x}$$

**증명 ($\lambda_{\max}$):** $A = Q \Lambda Q^T$라 하자. $y = Q^T x$로 변수변환하면 $\|y\| = \|x\| = 1$이고
$$x^T A x = y^T \Lambda y = \sum \lambda_i y_i^2 \leq \lambda_{\max} \sum y_i^2 = \lambda_{\max}$$

등호는 $y = e_n$ (즉 $x = q_n$, $\lambda_{\max}$에 대응하는 고유벡터)일 때 성립한다. $\lambda_{\min}$도 유사하다.

### 정리 6: 동시 대각화 (Simultaneous Diagonalization)

두 대칭행렬 $A, B$가 $AB = BA$ (가환)이면 같은 직교행렬로 동시에 대각화 가능하다. 즉, 직교행렬 $Q$가 존재하여 $Q^T A Q$와 $Q^T B Q$가 모두 대각행렬이다.

**증명 (개요):** $A$의 고유공간 $E_\lambda$에서 $B$는 $A$와 가환이므로 $E_\lambda$를 보존한다($B(E_\lambda) \subseteq E_\lambda$). 각 고유공간에서 $B$를 대각화하면 전체 공간에서 동시 대각화를 얻는다.

## 예제

**예제 1:** $A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$를 직교 대각화하라.

**풀이:** 고유값: $\det\begin{pmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{pmatrix} = (2-\lambda)^2 - 1 = \lambda^2 - 4\lambda + 3 = (\lambda - 1)(\lambda - 3)$.
$\lambda_1 = 1$, $\lambda_2 = 3$.

$\lambda_1 = 1$: $(A - I)v = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}v = 0$ → $v_1 = \begin{pmatrix} 1 \\ -1 \end{pmatrix}$, $q_1 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix}$.
$\lambda_2 = 3$: $(A - 3I)v = \begin{pmatrix} -1 & 1 \\ 1 & -1 \end{pmatrix}v = 0$ → $v_2 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$, $q_2 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$.

직교 확인: $\langle q_1, q_2 \rangle = \frac12(1\cdot1 + (-1)\cdot1) = 0$.

$$Q = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}, \quad \Lambda = \begin{pmatrix} 1 & 0 \\ 0 & 3 \end{pmatrix}$$
$$A = Q \Lambda Q^T = \frac12 \begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & 3 \end{pmatrix} \begin{pmatrix} 1 & -1 \\ 1 & 1 \end{pmatrix}$$

**예제 2:** $A = \begin{pmatrix} 5 & 4 & 0 \\ 4 & 5 & 0 \\ 0 & 0 & 1 \end{pmatrix}$를 직교 대각화하라.

**풀이:** 특성방정식: $\det\begin{pmatrix} 5-\lambda & 4 & 0 \\ 4 & 5-\lambda & 0 \\ 0 & 0 & 1-\lambda \end{pmatrix} = (1-\lambda)((5-\lambda)^2 - 16) = 0$.

$(1-\lambda)(\lambda^2 - 10\lambda + 9) = (1-\lambda)(\lambda - 1)(\lambda - 9) = 0$.
$\lambda_{1,2} = 1$ (중복), $\lambda_3 = 9$.

$\lambda = 9$: $(A - 9I)v = \begin{pmatrix} -4 & 4 & 0 \\ 4 & -4 & 0 \\ 0 & 0 & -8 \end{pmatrix}v = 0$.
$-4x + 4y = 0$, $-8z = 0$ → $x = y$, $z = 0$. $v_3 = \frac{1}{\sqrt{2}}(1, 1, 0)$.

$\lambda = 1$: $(A - I)v = \begin{pmatrix} 4 & 4 & 0 \\ 4 & 4 & 0 \\ 0 & 0 & 0 \end{pmatrix}v = 0$.
$x + y = 0$, $z$ 자유. $E_1 = \text{span}\{(1, -1, 0), (0, 0, 1)\}$.

그람-슈미트로 정규직교화: $q_1 = \frac{1}{\sqrt{2}}(1, -1, 0)$, $q_2 = (0, 0, 1)$.
$q_3$과의 직교 확인: $\langle q_1, q_3 \rangle = \frac12(1\cdot1 + (-1)\cdot1) = 0$, $\langle q_2, q_3 \rangle = 0$.

$$Q = \begin{pmatrix} 1/\sqrt{2} & 0 & 1/\sqrt{2} \\ -1/\sqrt{2} & 0 & 1/\sqrt{2} \\ 0 & 1 & 0 \end{pmatrix}, \quad \Lambda = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 9 \end{pmatrix}$$

**예제 3:** 이차형식 $Q(x, y) = x^2 + 4xy + y^2$를 표준형으로 변환하라.

**풀이:** 행렬 표현: $Q(x) = \begin{pmatrix} x & y \end{pmatrix} \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}$.

$A = \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix}$의 고유값: $\det\begin{pmatrix} 1-\lambda & 2 \\ 2 & 1-\lambda \end{pmatrix} = (1-\lambda)^2 - 4 = \lambda^2 - 2\lambda - 3 = (\lambda - 3)(\lambda + 1)$.
$\lambda_1 = 3$, $\lambda_2 = -1$.

고유벡터: $\lambda_1 = 3$: $(A-3I)v = \begin{pmatrix} -2 & 2 \\ 2 & -2 \end{pmatrix}v = 0$ → $v_1 = (1, 1)$, $q_1 = \frac{1}{\sqrt{2}}(1, 1)$.
$\lambda_2 = -1$: $(A+I)v = \begin{pmatrix} 2 & 2 \\ 2 & 2 \end{pmatrix}v = 0$ → $v_2 = (1, -1)$, $q_2 = \frac{1}{\sqrt{2}}(1, -1)$.

변수변환: $\begin{pmatrix} x \\ y \end{pmatrix} = Q \begin{pmatrix} u \\ v \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix} \begin{pmatrix} u \\ v \end{pmatrix}$.

표준형: $Q = 3u^2 - v^2$.

**해석:** $\lambda_1 > 0$, $\lambda_2 < 0$이므로 이 이차형식은 부정부정(indefinite)이다. $Q = 1$은 쌍곡선을, $Q = 0$은 두 직선 $3u^2 = v^2$ 즉 $v = \pm \sqrt{3}u$를 나타낸다.

**예제 4:** $\mathbb{R}^3$에서 $x^T A x = 9$가 정의하는 곡면을 분류하라. 여기서 $A = \text{diag}(4, 1, -9)$.

**풀이:** $4x^2 + y^2 - 9z^2 = 9$ → $\frac{x^2}{(3/2)^2} + \frac{y^2}{3^2} - \frac{z^2}{1^2} = 1$.
이는 한 장 쌍곡면(hyperboloid of one sheet)이다. $xy$-평면에서 타원, $z$ 방향으로 쌍곡선 단면.

**예제 5 (에르미트 행렬):** 복소 행렬 $A = \begin{pmatrix} 2 & 1+i \\ 1-i & 3 \end{pmatrix}$가 에르미트 행렬임을 확인하고 고유값이 실수임을 보이라.

**풀이:** $A^* = \bar{A}^T = \begin{pmatrix} 2 & \overline{1-i} \\ \overline{1+i} & 3 \end{pmatrix} = \begin{pmatrix} 2 & 1+i \\ 1-i & 3 \end{pmatrix} = A$이므로 에르미트 행렬이다.

특성방정식: $\det\begin{pmatrix} 2-\lambda & 1+i \\ 1-i & 3-\lambda \end{pmatrix} = (2-\lambda)(3-\lambda) - (1+i)(1-i)$
$= \lambda^2 - 5\lambda + 6 - (1+1) = \lambda^2 - 5\lambda + 4 = (\lambda-1)(\lambda-4)$.
$\lambda_1 = 1$, $\lambda_2 = 4$로 모두 실수다.

**예제 6 (이차형식 최적화):** 제약 $\|x\| = 1$ 아래에서 $Q(x) = 2x_1^2 + 2x_1x_2 + 2x_2^2$의 최대값과 최소값을 구하라.

**풀이:** $A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$의 고유값은 $\lambda_1 = 1$, $\lambda_2 = 3$.
따라서 $\min Q(x) = \lambda_1 = 1$ ($x = \frac{1}{\sqrt{2}}(1, -1)$에서), $\max Q(x) = \lambda_2 = 3$ ($x = \frac{1}{\sqrt{2}}(1, 1)$에서).

**예제 7 (레일리 몫):** $A = \begin{pmatrix} 3 & 2 \\ 2 & 3 \end{pmatrix}$의 레일리 몫의 최대값과 최소값을 구하라.

**풀이:** 고유값은 $\lambda_1 = 1$, $\lambda_2 = 5$이므로
$$\min_{\|x\| = 1} x^T A x = 1, \quad \max_{\|x\| = 1} x^T A x = 5$$

$x = q_1 = \frac{1}{\sqrt{2}}(1, -1)$일 때 $x^T A x = 1$, $x = q_2 = \frac{1}{\sqrt{2}}(1, 1)$일 때 $x^T A x = 5$이다.

## 연결

- **[고유값·고유벡터](topics/eigenvalues.html)** : 스펙트럼 정리는 대칭행렬의 고유값이 가지는 특별한 성질을 종합한다.
- **[양정치 행렬](topics/positive-definite.html)** : 이차형식의 부호 판정은 양정치 행렬의 정의와 직접 연결된다.
- **[기저 변환](topics/change-of-basis.html)** : 직교 대각화는 기저변환의 특수한 경우로, 정규직교기저 간의 변환이다.
