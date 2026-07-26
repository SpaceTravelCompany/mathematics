---
title: 최소제곱법
slug: least-squares
---

## 직관적 설명

**최소제곱법(least squares method)**은 과대결정(overdetermined) 선형 시스템 $Ax \approx b$ — 방정식이 미지수보다 많은 경우 — 에서 "가장 그럴듯한" 해를 찾는 방법이다. 실험 데이터에 직선을 피팅하는 것이 가장 대표적인 예시다.

직관의 핵심은 간단하다: $Ax = b$의 정확한 해가 존재하지 않을 때, 잔차 $r = b - Ax$의 크기를 최소화하는 $x$를 구한다. 잔차의 크기를 측정하는 기준으로 **유클리드 노름의 제곱** $\|r\|^2 = \|b - Ax\|^2$을 사용하는 것이 최소제곱법이다.

이것은 단순한 계산 트릭이 아니라 기하학적으로 깊은 의미를 가진다. $Ax$는 $A$의 열공간 $\text{Col}(A)$의 원소다. 따라서 $\|b - Ax\|$를 최소화하는 것은 $b$를 $\text{Col}(A)$에 **직교투영(orthogonal projection)**하는 것과 같다. 잔차 $r = b - A\hat{x}$는 열공간에 수직이며, 이 직교 조건이 정규방정식(normal equation)을 유도한다.

최소제곱법은 측정 오차가 있는 현실 데이터를 다루는 거의 모든 분야의 기초다. 회귀분석(regression analysis), 신호처리, 제어 이론, 컴퓨터 그래픽스까지 응용 범위가 실로 광범위하다.

## 정의

**과대결정 시스템 (overdetermined system):** $m > n$인 $m \times n$ 행렬 $A$와 $b \in \mathbb{R}^m$에 대해
$$Ax = b$$
가 해를 가지지 않을 때(즉, $b \notin \text{Col}(A)$), 근사해를 구하는 문제를 고려한다.

**잔차 (residual):** $r(x) = b - Ax$는 주어진 $x$에 대한 오차 벡터다.

**목적함수 (objective function):**
$$\phi(x) = \|r(x)\|^2 = \|b - Ax\|^2 = (b - Ax)^T (b - Ax)$$

**최소제곱해 (least squares solution):** $\phi(x)$를 최소화하는 $\hat{x} \in \mathbb{R}^n$을 최소제곱해라 한다.

**정규방정식 (normal equation):** 최소제곱해 $\hat{x}$는 다음 방정식을 만족한다.
$$A^T A \hat{x} = A^T b$$

**가중 최소제곱 (weighted least squares):** 잔차의 각 성분에 가중치 $w_i > 0$를 부여할 때
$$\hat{x} = \arg\min \sum_{i=1}^m w_i (b_i - (Ax)_i)^2$$
행렬 형태: $W = \text{diag}(w_1, \ldots, w_m)$에 대해 $(A^T W A) \hat{x} = A^T W b$.

## 주요 정리와 증명

### 정리 1: 정규방정식의 유도 (기하학적 접근)

$\hat{x}$가 최소제곱해일 필요충분조건은 잔차 $r = b - A\hat{x}$가 $A$의 모든 열에 직교하는 것이다:
$$A^T (b - A\hat{x}) = 0$$

**증명:** $\hat{x}$가 최소제곱해라면 $A\hat{x}$는 $b$의 $\text{Col}(A)$ 위로의 직교투영이다. 직교투영의 정의에 의해 $b - A\hat{x}$는 $\text{Col}(A)$에 속하는 모든 벡터와 직교한다. 특히 $A$의 각 열 $a_j$ ($j = 1, \ldots, n$)에 대해
$$\langle a_j, b - A\hat{x} \rangle = a_j^T (b - A\hat{x}) = 0$$

이는 모든 $j$에 대해 성립하므로 행렬 형태로 $A^T(b - A\hat{x}) = 0$이 된다. 이를 정리하면 $A^T A \hat{x} = A^T b$를 얻는다.

(미분을 통한 유도: $\phi(x) = (b - Ax)^T(b - Ax) = b^T b - 2x^T A^T b + x^T A^T A x$를 $x$로 미분하여 $\nabla \phi(x) = -2A^T b + 2A^T A x = 0$으로부터 같은 결과를 얻을 수 있다.)

### 정리 2: $A^T A$의 가역성

$m \times n$ 행렬 $A$ ($m \geq n$)의 열들이 일차독립이면 $A^T A$는 가역(invertible)이다.

**증명:** $A^T A x = 0$이라 가정하자. 양변에 $x^T$를 곱하면
$$x^T A^T A x = (Ax)^T (Ax) = \|Ax\|^2 = 0$$

따라서 $Ax = 0$이다. $A$의 열들이 일차독립이므로 $Ax = 0$의 해는 $x = 0$뿐이다. 따라서 $\ker(A^T A) = \{0\}$이고 $A^T A$는 가역이다.

**역방향:** $A^T A$가 가역이면 $A$의 열은 일차독립이다. $Ax = 0$이면 $A^T A x = 0$이고, $A^T A$의 가역성에 의해 $x = 0$이므로 열이 일차독립이다.

### 정리 3: 최소제곱해의 유일성

$A$의 열이 일차독립이면 최소제곱해는 유일하며 다음으로 주어진다:
$$\hat{x} = (A^T A)^{-1} A^T b$$

**증명:** 정규방정식 $A^T A \hat{x} = A^T b$에서 $A^T A$가 가역이므로 $\hat{x} = (A^T A)^{-1} A^T b$이다. $A$의 열이 일차독립이면 $A^T A$가 가역이므로 해가 유일하다. 열이 일차종속이면 $A^T A$가 특이(singular) 행렬이 되어 해가 무수히 많다.

### 정리 4: 투영 행렬 (Projection Matrix)

행렬 $P = A(A^T A)^{-1}A^T$는 $\mathbb{R}^m$에서 $\text{Col}(A)$ 위로의 직교투영 행렬이다. 즉,
$$A\hat{x} = A(A^T A)^{-1} A^T b = P b$$

**증명:** $P$의 성질을 확인한다.
- **대칭성:** $P^T = (A(A^T A)^{-1} A^T)^T = A(A^T A)^{-T} A^T = A(A^T A)^{-1} A^T = P$
- **멱등성:** $P^2 = A(A^T A)^{-1} A^T A (A^T A)^{-1} A^T = A(A^T A)^{-1} A^T = P$
- $\text{Col}(A)$의 원소 $y = Ax$에 대해 $Py = A(A^T A)^{-1} A^T Ax = Ax = y$

따라서 $P$는 $\text{Col}(A)$ 위로의 직교투영 행렬이다.

### 정리 5: 최소제곱 오차

최소제곱 오차(잔차 노름의 최소값)는 다음으로 주어진다:
$$\|b - A\hat{x}\|^2 = \|b\|^2 - \|A\hat{x}\|^2 = b^T b - b^T A(A^T A)^{-1} A^T b$$

**증명:** $b = A\hat{x} + r$에서 $A\hat{x} \perp r$이므로 피타고라스 정리에 의해
$$\|b\|^2 = \|A\hat{x}\|^2 + \|r\|^2$$
$$\|r\|^2 = \|b\|^2 - \|A\hat{x}\|^2 = b^T b - \hat{x}^T A^T A \hat{x} = b^T b - b^T A(A^T A)^{-1} A^T b$$

### 정리 6: 결정계수 (Coefficient of Determination, $R^2$)

데이터 피팅의 적합도를 측정하는 $R^2$ 통계량은
$$R^2 = 1 - \frac{\|b - A\hat{x}\|^2}{\|b - \bar{b}\mathbf{1}\|^2}$$
여기서 $\bar{b}$는 $b$의 평균, $\mathbf{1}$은 모든 성분이 1인 벡터다. $R^2 = 1$에 가까울수록 모형이 데이터를 잘 설명한다.

**증명:** $\text{SS}_{\text{res}} = \|b - A\hat{x}\|^2$ (잔차 제곱합), $\text{SS}_{\text{tot}} = \|b - \bar{b}\mathbf{1}\|^2$ (총 제곱합)이라 할 때, $R^2 = 1 - \text{SS}_{\text{res}} / \text{SS}_{\text{tot}}$이다.

### 정리 7: 직교분해와 최소제곱

QR 분해 $A = QR$ ($Q$ 직교열, $R$ 상삼각)을 이용하면 최소제곱해가 효율적으로 계산된다:
$$\hat{x} = R^{-1} Q^T b, \quad \|b - A\hat{x}\|^2 = \|b\|^2 - \|Q^T b\|^2$$

**증명:** $A\hat{x} = QR\hat{x}$를 정규방정식에 대입하면
$$(QR)^T QR \hat{x} = R^T Q^T Q R \hat{x} = R^T R \hat{x} = (QR)^T b = R^T Q^T b$$
$R$이 가역이므로 $R\hat{x} = Q^T b$, 즉 $\hat{x} = R^{-1} Q^T b$를 얻는다. 이는 정규방정식을 푸는 것보다 수치적으로 안정적이다.

## 예제

**예제 1:** 세 점 $(1, 2)$, $(2, 3)$, $(3, 5)$를 가장 잘 근사하는 직선 $y = \beta_0 + \beta_1 x$를 최소제곱법으로 구하라.

**풀이:** 각 점에 대해 $y_i = \beta_0 + \beta_1 x_i$를 세우면
$$\begin{cases} 2 = \beta_0 + \beta_1 \cdot 1 \\ 3 = \beta_0 + \beta_1 \cdot 2 \\ 5 = \beta_0 + \beta_1 \cdot 3 \end{cases}$$

행렬 형태:
$$A = \begin{pmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \end{pmatrix}, \quad x = \begin{pmatrix} \beta_0 \\ \beta_1 \end{pmatrix}, \quad b = \begin{pmatrix} 2 \\ 3 \\ 5 \end{pmatrix}$$

$$A^T A = \begin{pmatrix} 1 & 1 & 1 \\ 1 & 2 & 3 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 2 \\ 1 & 3 \end{pmatrix} = \begin{pmatrix} 3 & 6 \\ 6 & 14 \end{pmatrix}$$

$$A^T b = \begin{pmatrix} 1 & 1 & 1 \\ 1 & 2 & 3 \end{pmatrix} \begin{pmatrix} 2 \\ 3 \\ 5 \end{pmatrix} = \begin{pmatrix} 10 \\ 23 \end{pmatrix}$$

정규방정식:
$$\begin{pmatrix} 3 & 6 \\ 6 & 14 \end{pmatrix} \begin{pmatrix} \beta_0 \\ \beta_1 \end{pmatrix} = \begin{pmatrix} 10 \\ 23 \end{pmatrix}$$

$$\det(A^T A) = 3\cdot14 - 6\cdot6 = 42 - 36 = 6$$
$$(A^T A)^{-1} = \frac{1}{6} \begin{pmatrix} 14 & -6 \\ -6 & 3 \end{pmatrix}$$

$$\hat{x} = \frac{1}{6} \begin{pmatrix} 14 & -6 \\ -6 & 3 \end{pmatrix} \begin{pmatrix} 10 \\ 23 \end{pmatrix} = \frac{1}{6} \begin{pmatrix} 140 - 138 \\ -60 + 69 \end{pmatrix} = \frac{1}{6} \begin{pmatrix} 2 \\ 9 \end{pmatrix} = \begin{pmatrix} 1/3 \\ 3/2 \end{pmatrix}$$

따라서 최적 직선은 $y = \frac13 + \frac32 x$이다.

잔차 확인:
$r_1 = 2 - (1/3 + 3/2 \cdot 1) = 2 - 11/6 = 1/6$
$r_2 = 3 - (1/3 + 3/2 \cdot 2) = 3 - 10/3 = -1/3$
$r_3 = 5 - (1/3 + 3/2 \cdot 3) = 5 - 29/6 = 1/6$
잔차의 합 = $1/6 - 1/3 + 1/6 = 0$ (직교 조건 확인).

**예제 2:** $A = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ 0 & 2 \end{pmatrix}$, $b = \begin{pmatrix} 1 \\ 1 \\ 2 \end{pmatrix}$의 최소제곱해를 구하라.

**풀이:**
$$A^T A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 2 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 5 & 2 \\ 2 & 5 \end{pmatrix}$$
$$A^T b = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 3 \\ 5 \end{pmatrix}$$

정규방정식: $\begin{pmatrix} 5 & 2 \\ 2 & 5 \end{pmatrix} \hat{x} = \begin{pmatrix} 3 \\ 5 \end{pmatrix}$.

$$(A^T A)^{-1} = \frac{1}{5\cdot5 - 2\cdot2} \begin{pmatrix} 5 & -2 \\ -2 & 5 \end{pmatrix} = \frac{1}{21} \begin{pmatrix} 5 & -2 \\ -2 & 5 \end{pmatrix}$$
$$\hat{x} = \frac{1}{21} \begin{pmatrix} 5 & -2 \\ -2 & 5 \end{pmatrix} \begin{pmatrix} 3 \\ 5 \end{pmatrix} = \frac{1}{21} \begin{pmatrix} 15 - 10 \\ -6 + 25 \end{pmatrix} = \frac{1}{21} \begin{pmatrix} 5 \\ 19 \end{pmatrix}$$

투영된 벡터: $A\hat{x} = \frac{1}{21} \left( \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} 5 \\ 19 \end{pmatrix} \right) = \frac{1}{21} \begin{pmatrix} 5 \\ 29 \\ 38 \end{pmatrix}$.

잔차: $r = b - A\hat{x} = \frac{1}{21} \begin{pmatrix} 21 - 5 \\ 21 - 29 \\ 42 - 38 \end{pmatrix} = \frac{1}{21} \begin{pmatrix} 16 \\ -8 \\ 4 \end{pmatrix}$.

직교 확인: $A^T r = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 2 \end{pmatrix} \cdot \frac{1}{21} \begin{pmatrix} 16 \\ -8 \\ 4 \end{pmatrix} = \frac{1}{21} \begin{pmatrix} 16 - 16 \\ -8 + 8 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$.

**예제 3:** 비선형 모델인 $y = ae^{bx}$에 데이터 $(0, 1), (1, 2), (2, 4)$를 피팅하라 (선형화 기법).

**풀이:** 양변에 로그를 취하면 $\ln y = \ln a + bx$. $Y = \ln y$, $X = x$, $\beta_0 = \ln a$, $\beta_1 = b$라 하자.
데이터: $(0, 0), (1, \ln 2), (2, \ln 4) = (0, 0), (1, 0.693), (2, 1.386)$.

$$A = \begin{pmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{pmatrix}, \quad Y = \begin{pmatrix} 0 \\ 0.693 \\ 1.386 \end{pmatrix}$$
$$A^T A = \begin{pmatrix} 3 & 3 \\ 3 & 5 \end{pmatrix}, \quad A^T Y = \begin{pmatrix} 2.079 \\ 3.465 \end{pmatrix}$$

정규방정식 풀이:
$$\begin{pmatrix} 3 & 3 \\ 3 & 5 \end{pmatrix} \begin{pmatrix} \beta_0 \\ \beta_1 \end{pmatrix} = \begin{pmatrix} 2.079 \\ 3.465 \end{pmatrix}$$
첫 식: $3\beta_0 + 3\beta_1 = 2.079$, 둘째 식: $3\beta_0 + 5\beta_1 = 3.465$.
두 식을 빼면 $2\beta_1 = 1.386$, $\beta_1 = 0.693$.
$3\beta_0 = 2.079 - 3\cdot0.693 = 2.079 - 2.079 = 0$, $\beta_0 = 0$.

따라서 $\ln a = 0$ → $a = 1$, $b = 0.693$이므로 $y = e^{0.693x} = 2^x$ (정확히 데이터를 통과한다!).

**예제 4 (다항식 피팅):** 세 점 $(-1, 1), (0, 0), (1, 1), (2, 4)$를 가장 잘 근사하는 2차 다항식 $y = \beta_0 + \beta_1 x + \beta_2 x^2$을 최소제곱법으로 구하라.

**풀이:** 각 점에서
$\begin{cases} 1 = \beta_0 - \beta_1 + \beta_2 \\ 0 = \beta_0 \\ 1 = \beta_0 + \beta_1 + \beta_2 \\ 4 = \beta_0 + 2\beta_1 + 4\beta_2 \end{cases}$

$$A = \begin{pmatrix} 1 & -1 & 1 \\ 1 & 0 & 0 \\ 1 & 1 & 1 \\ 1 & 2 & 4 \end{pmatrix}, \quad b = \begin{pmatrix} 1 \\ 0 \\ 1 \\ 4 \end{pmatrix}$$
$$A^T A = \begin{pmatrix} 4 & 2 & 6 \\ 2 & 6 & 8 \\ 6 & 8 & 18 \end{pmatrix}, \quad A^T b = \begin{pmatrix} 6 \\ 7 \\ 14 \end{pmatrix}$$

정규방정식 $A^T A \hat{x} = A^T b$를 풀면 (가우스 소거 사용 가능)
$$\hat{\beta}_0 = 0, \quad \hat{\beta}_1 = \frac12, \quad \hat{\beta}_2 = 1$$

따라서 $y = \frac12 x + x^2$이 최적 2차 다항식이다.

**예제 5:** 최소제곱법으로 원점을 지나는 직선 $y = mx$를 세 점 $(-1, 0), (0, 2), (1, 4)$에 피팅하라.

**풀이:** $A = \begin{pmatrix} -1 \\ 0 \\ 1 \end{pmatrix}$, $b = \begin{pmatrix} 0 \\ 2 \\ 4 \end{pmatrix}$.
$A^T A = (-1)^2 + 0^2 + 1^2 = 2$.
$A^T b = (-1)\cdot0 + 0\cdot2 + 1\cdot4 = 4$.
$\hat{m} = (A^T A)^{-1} A^T b = 4/2 = 2$.
따라서 $y = 2x$가 최적 직선이다. 잔차: $r = (0, 2, 4) - (-2, 0, 2) = (2, 2, 2)$, $\|r\|^2 = 12$.

**예제 6 (다중선형회귀):** 세 변수 $x_1, x_2$에 대한 4개 관측값이 다음과 같을 때 $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2$를 피팅하라.

데이터: $(x_1, x_2, y) = (1, 0, 2), (0, 1, 1), (2, 1, 4), (1, 2, 5)$.

**풀이:** 
$$A = \begin{pmatrix} 1 & 1 & 0 \\ 1 & 0 & 1 \\ 1 & 2 & 1 \\ 1 & 1 & 2 \end{pmatrix}, \quad b = \begin{pmatrix} 2 \\ 1 \\ 4 \\ 5 \end{pmatrix}$$
$$A^T A = \begin{pmatrix} 4 & 4 & 4 \\ 4 & 6 & 3 \\ 4 & 3 & 6 \end{pmatrix}, \quad A^T b = \begin{pmatrix} 12 \\ 15 \\ 15 \end{pmatrix}$$

정규방정식 풀이(가우스 소거):
$$\begin{pmatrix} 4 & 4 & 4 & | & 12 \\ 4 & 6 & 3 & | & 15 \\ 4 & 3 & 6 & | & 15 \end{pmatrix} \to \begin{pmatrix} 4 & 4 & 4 & | & 12 \\ 0 & 2 & -1 & | & 3 \\ 0 & -1 & 2 & | & 3 \end{pmatrix}$$
$$\to \begin{pmatrix} 4 & 4 & 4 & | & 12 \\ 0 & 2 & -1 & | & 3 \\ 0 & 0 & 3/2 & | & 9/2 \end{pmatrix}$$

$\beta_2 = 3$, $\beta_1 = 3$, $\beta_0 = 12/4 - 3 - 3 = -3$.
따라서 $y = -3 + 3x_1 + 3x_2$가 최적 피팅이다.

잔차 검증: $r = (2 - (-3+3), \; 1 - (-3+3), \; 4 - (-3+6+3), \; 5 - (-3+3+6)) = (2, 1, -2, -1)$.
$\|r\|^2 = 4 + 1 + 4 + 1 = 10$.

## 연결

- **[직교성·직교투영·그람-슈미트](orthogonality.html)** : 최소제곱해는 직교투영의 직접적인 응용이다.
- **[회귀분석](regression-analysis.html)** : 통계학에서 최소제곱법은 선형 회귀의 핵심 추정 도구이며, $R^2$, $t$-검정 등으로 확장된다.
