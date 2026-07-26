---
title: SVD
slug: svd
---

## 직관적 설명

**특이값 분해(Singular Value Decomposition, SVD)**는 모든 행렬(직사각형 행렬 포함)을 세 개의 간단한 행렬의 곱으로 분해한다:
$$A = U \Sigma V^T$$

여기서 $U$와 $V$는 직교행렬(orthogonal matrix)이고 $\Sigma$는 대각행렬이다. 기하학적으로 이것은 임의의 선형변환이 **"회전 → 각 축 방향으로 스케일링 → 다시 회전"** 의 세 단계로 분해됨을 의미한다.

SVD는 선형대수에서 가장 강력하고 범용적인 도구다. 고유값 분해는 정사각행렬에만 적용되지만, SVD는 모든 행렬에 존재한다. 행렬의 rank 결정, 최적 저랭크 근사, 의사역행렬(pseudoinverse), 주성분 분석(PCA), 추천 시스템의 잠재 요인 모델, 이미지 압축, 자연어 처리의 잠재 의미 분석(LSA)까지 응용이 무궁무진하다.

SVD는 "선형대수의 최종 보스"라 불릴 만하다 — 지금까지 배운 모든 개념(내적, 직교성, 고유값, 대칭행렬)이 이 하나의 분해에 집결된다.

## 정의

**특이값 분해 (SVD):** $m \times n$ 행렬 $A$ ($m \geq n$, 일반성을 잃지 않음)는 다음과 같이 분해된다:
$$A = U \Sigma V^T$$

여기서
- $U$: $m \times m$ 직교행렬 ($U^T U = I_m$). 열을 **좌특이벡터(left singular vector)** $u_i$라 한다.
- $V$: $n \times n$ 직교행렬 ($V^T V = I_n$). 열을 **우특이벡터(right singular vector)** $v_i$라 한다.
- $\Sigma$: $m \times n$ 직사각 대각행렬. 대각 성분 $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_r \geq 0$ ($r = \text{rank}(A)$)을 **특이값(singular value)**이라 한다.

**특이값과 고유값의 관계:**
$$\sigma_i = \sqrt{\lambda_i(A^T A)} = \sqrt{\lambda_i(A A^T)}$$

즉, 특이값은 $A^T A$ (또는 $A A^T$)의 고유값의 제곱근이다.

**축소 SVD (reduced / thin SVD):** $r = \text{rank}(A)$일 때
$$A = U_r \Sigma_r V_r^T$$

여기서 $U_r$은 $m \times r$, $\Sigma_r$은 $r \times r$, $V_r$은 $n \times r$이며, 0이 아닌 특이값만 포함한다.

**의사역행렬 (pseudoinverse):** $A^+ = V \Sigma^+ U^T$, 여기서 $\Sigma^+$는 $\Sigma$에서 0이 아닌 특이값들을 역수로 바꾼 행렬. 최소제곱 문제 $Ax \approx b$의 최소 노름 해는 $x = A^+ b$로 주어진다.

## 주요 정리와 증명

### 정리 1: SVD 존재 정리

모든 $m \times n$ 실수 행렬 $A$는 SVD $A = U \Sigma V^T$로 분해된다.

**증명 (구성적 증명):**

1단계: $A^T A$는 $n \times n$ 대칭행렬이므로 스펙트럼 정리에 의해 직교 대각화 가능하다. $A^T A$의 고유값을 $\lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_n \geq 0$이라 하고(양반정치이므로), 대응하는 정규직교 고유벡터를 $v_1, \ldots, v_n$이라 하자.

2단계: $i = 1, \ldots, n$에 대해 $\sigma_i = \sqrt{\lambda_i}$를 **특이값**이라 정의한다. $r = \text{rank}(A)$일 때 $\sigma_1 \geq \cdots \geq \sigma_r > 0$이고 $\sigma_{r+1} = \cdots = \sigma_n = 0$이다.

3단계: $i = 1, \ldots, r$에 대해 **좌특이벡터**를 다음과 같이 정의한다:
$$u_i = \frac{1}{\sigma_i} A v_i$$

이들이 정규직교함을 보인다:
$$u_i^T u_j = \frac{1}{\sigma_i \sigma_j} v_i^T A^T A v_j = \frac{1}{\sigma_i \sigma_j} v_i^T (\lambda_j v_j) = \frac{\lambda_j}{\sigma_i \sigma_j} \delta_{ij} = \delta_{ij}$$

4단계: $\{u_1, \ldots, u_r\}$을 $\mathbb{R}^m$의 정규직교기저로 확장하여 $u_{r+1}, \ldots, u_m$을 추가한다.

5단계: $U = [u_1 \; \cdots \; u_m]$, $V = [v_1 \; \cdots \; v_n]$이라 하고 $\Sigma$를 $\Sigma_{ii} = \sigma_i$ ($i \leq r$), 나머지 0인 $m \times n$ 행렬이라 하자. 이제 $AV = U\Sigma$임을 확인한다:
$$AV = [Av_1 \; \cdots \; Av_n] = [\sigma_1 u_1 \; \cdots \; \sigma_r u_r \; 0 \; \cdots \; 0] = U\Sigma$$

따라서 $A = U\Sigma V^T$이다.

### 정리 2: SVD와 행렬의 기본공간

SVD는 행렬의 네 기본공간(fundamental subspaces)을 명시적으로 드러낸다:
- $\text{Col}(A) = \text{span}\{u_1, \ldots, u_r\}$
- $\text{Null}(A^T) = \text{span}\{u_{r+1}, \ldots, u_m\}$
- $\text{Row}(A) = \text{span}\{v_1, \ldots, v_r\}$ ($V$의 열)
- $\text{Null}(A) = \text{span}\{v_{r+1}, \ldots, v_n\}$

**증명:** $Av_i = \sigma_i u_i$에서 $i \leq r$일 때 $Av_i = \sigma_i u_i \neq 0$이므로 $v_i$ ($i \leq r$)는 $\text{Row}(A)$의 기저이고, $u_i$ ($i \leq r$)는 $\text{Col}(A)$의 기저이다. $i > r$일 때 $Av_i = 0$이므로 $v_i$는 $\text{Null}(A)$의 기저이고, $A^T u_i = 0$이므로 $u_i$ ($i > r$)는 $\text{Null}(A^T)$의 기저이다.

### 정리 3: rank와 특이값

$\text{rank}(A)$는 0이 아닌 특이값의 개수 $r$과 같다.

**증명:** $A$의 rank는 $\text{Col}(A)$의 차원이다. 위 정리에서 $\text{Col}(A) = \text{span}\{u_1, \ldots, u_r\}$이고 $\{u_i\}$는 일차독립이므로 $\dim(\text{Col}(A)) = r$이다.

### 정리 4: 최적 저랭크 근사 (Eckart-Young 정리)

$A_k = \sum_{i=1}^k \sigma_i u_i v_i^T$를 $A$의 rank-$k$ 근사라 할 때 ($k < r$), Frobenius 노름에서 다음이 성립한다:
$$\min_{\text{rank}(B) \leq k} \|A - B\|_F = \|A - A_k\|_F = \sqrt{\sum_{i=k+1}^r \sigma_i^2}$$

즉, 가장 큰 $k$개의 특이값만 유지한 근사가 최적의 rank-$k$ 근사다.

**증명 개요:** $\|A - B\|_F^2 = \sum_{i,j} (a_{ij} - b_{ij})^2 = \text{tr}((A-B)^T(A-B))$이다. SVD와 직교 불변성을 이용하면 $\|A - B\|_F^2 \geq \sum_{i=k+1}^r \sigma_i^2$임을 보일 수 있다. $B = A_k$일 때 등호가 성립한다.

**참고:** 동일한 결과가 스펙트럴 노름(2-노름)에서도 성립한다: $\|A - A_k\|_2 = \sigma_{k+1}$.

### 정리 5: SVD의 유일성

SVD는 일반적으로 유일하지 않다. 그러나 특이값 $\sigma_i$는 중복도를 포함해 유일하게 결정된다. 중복된 특이값에 대응하는 특이벡터들은 해당 고유공간 내에서 임의의 직교기저를 선택할 수 있다.

**증명:** $A^T A$의 고유값이 $\sigma_i^2$으로 유일하게 결정되므로 특이값은 유일하다. 중복 특이값의 고유공간 내에서는 어떤 정규직교기저를 선택해도 SVD가 성립한다.

### 정리 6: SVD와 행렬의 노름

Frobenius 노름과 스펙트럴 노름은 특이값으로 표현된다:
$$\|A\|_F = \sqrt{\sum_{i=1}^r \sigma_i^2}, \quad \|A\|_2 = \sigma_1$$

**증명:** Frobenius 노름: $\|A\|_F^2 = \text{tr}(A^T A) = \sum \lambda_i(A^T A) = \sum \sigma_i^2$. 스펙트럴 노름(2-노름): $\|A\|_2 = \max_{\|x\|=1} \|Ax\| = \max_i \sigma_i = \sigma_1$.

## 예제

**예제 1:** $A = \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \end{pmatrix}$의 SVD를 계산하라.

**풀이:** $A$는 $2 \times 3$ 행렬.
$$A^T A = \begin{pmatrix} 1 & 0 \\ 0 & 1 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \\ 1 & 1 & 2 \end{pmatrix}$$

$A^T A$의 고유값:
$$\det\begin{pmatrix} 1-\lambda & 0 & 1 \\ 0 & 1-\lambda & 1 \\ 1 & 1 & 2-\lambda \end{pmatrix} = (1-\lambda)((1-\lambda)(2-\lambda)-1) - 1(0-(1-\lambda))$$
$$= (1-\lambda)((1-\lambda)(2-\lambda)-1) + (1-\lambda) = (1-\lambda)((1-\lambda)(2-\lambda))$$
$$= (1-\lambda)^2 (2-\lambda) - (1-\lambda) + (1-\lambda) = (1-\lambda)((1-\lambda)(2-\lambda)) \quad \text{— 재계산 필요}$$

행렬을 다시 계산하자.
$A A^T = \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & 1 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$.

$A A^T$의 고유값: $\det\begin{pmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{pmatrix} = (2-\lambda)^2 - 1 = \lambda^2 - 4\lambda + 3 = (\lambda-1)(\lambda-3)$.
따라서 $\lambda_1 = 3$, $\lambda_2 = 1$.
특이값: $\sigma_1 = \sqrt{3}$, $\sigma_2 = 1$.

$A A^T$의 고유벡터($U$의 열):
$\lambda_1 = 3$: $\begin{pmatrix} -1 & 1 \\ 1 & -1 \end{pmatrix}v = 0$ → $u_1 = \frac{1}{\sqrt{2}}(1, 1)$.
$\lambda_2 = 1$: $\begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}v = 0$ → $u_2 = \frac{1}{\sqrt{2}}(1, -1)$.

$U = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$.

$V$는 $A^T A$의 고유벡터 또는 $v_i = A^T u_i / \sigma_i$로 계산:
$v_1 = \frac{A^T u_1}{\sigma_1} = \frac{1}{\sqrt{3}} \cdot \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 0 \\ 0 & 1 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{\sqrt{6}} \begin{pmatrix} 1 \\ 1 \\ 2 \end{pmatrix}$.
$v_2 = \frac{A^T u_2}{\sigma_2} = \frac{1}{1} \cdot \frac{1}{\sqrt{2}} \begin{pmatrix} 1 & 0 \\ 0 & 1 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 1 \\ -1 \end{pmatrix} = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -1 \\ 0 \end{pmatrix}$.

$v_3$은 $\text{Null}(A)$의 기저에서 구한다(또는 $v_1, v_2$에 직교하는 단위벡터). $v_3$는 $Av_3 = 0$이므로 $v_3 = \frac{1}{\sqrt{3}}(1, 1, -1)$ (직교 확인).

따라서
$$U = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}, \quad \Sigma = \begin{pmatrix} \sqrt{3} & 0 & 0 \\ 0 & 1 & 0 \end{pmatrix}, \quad V = \begin{pmatrix} 1/\sqrt{6} & 1/\sqrt{2} & 1/\sqrt{3} \\ 1/\sqrt{6} & -1/\sqrt{2} & 1/\sqrt{3} \\ 2/\sqrt{6} & 0 & -1/\sqrt{3} \end{pmatrix}$$

**예제 2:** $A = \begin{pmatrix} 3 & 1 \\ 1 & 3 \\ 0 & 0 \end{pmatrix}$의 SVD와 rank-1 근사를 구하라.

**풀이:** $A^T A = \begin{pmatrix} 3 & 1 & 0 \\ 1 & 3 & 0 \end{pmatrix} \begin{pmatrix} 3 & 1 \\ 1 & 3 \\ 0 & 0 \end{pmatrix} = \begin{pmatrix} 10 & 6 \\ 6 & 10 \end{pmatrix}$.
$\det\begin{pmatrix} 10-\lambda & 6 \\ 6 & 10-\lambda \end{pmatrix} = (10-\lambda)^2 - 36 = \lambda^2 - 20\lambda + 64 = (\lambda-4)(\lambda-16)$.
$\lambda_1 = 16$, $\lambda_2 = 4$.
$\sigma_1 = 4$, $\sigma_2 = 2$.

고유벡터:
$\lambda_1 = 16$: $\begin{pmatrix} -6 & 6 \\ 6 & -6 \end{pmatrix}v = 0$ → $v_1 = \frac{1}{\sqrt{2}}(1, 1)$.
$\lambda_2 = 4$: $\begin{pmatrix} 6 & 6 \\ 6 & 6 \end{pmatrix}v = 0$ → $v_2 = \frac{1}{\sqrt{2}}(1, -1)$.

$U$ 계산:
$u_1 = \frac{A v_1}{\sigma_1} = \frac{1}{4} \begin{pmatrix} 3 & 1 \\ 1 & 3 \\ 0 & 0 \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{4\sqrt{2}} \begin{pmatrix} 4 \\ 4 \\ 0 \end{pmatrix} = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}$.
$u_2 = \frac{A v_2}{\sigma_2} = \frac{1}{2} \begin{pmatrix} 3 & 1 \\ 1 & 3 \\ 0 & 0 \end{pmatrix} \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix} = \frac{1}{2\sqrt{2}} \begin{pmatrix} 2 \\ -2 \\ 0 \end{pmatrix} = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \\ 0 \end{pmatrix}$.
$u_3$은 $u_1, u_2$에 직교하는 단위벡터: $u_3 = (0, 0, 1)$.

$$A = U \Sigma V^T = \begin{pmatrix} 1/\sqrt{2} & 1/\sqrt{2} & 0 \\ 1/\sqrt{2} & -1/\sqrt{2} & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 4 & 0 \\ 0 & 2 \\ 0 & 0 \end{pmatrix} \begin{pmatrix} 1/\sqrt{2} & 1/\sqrt{2} \\ 1/\sqrt{2} & -1/\sqrt{2} \end{pmatrix}$$

Rank-1 근사: $A_1 = \sigma_1 u_1 v_1^T = 4 \cdot \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix} \cdot \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \end{pmatrix} = \begin{pmatrix} 2 & 2 \\ 2 & 2 \\ 0 & 0 \end{pmatrix}$.

원래 $A = \begin{pmatrix} 3 & 1 \\ 1 & 3 \\ 0 & 0 \end{pmatrix}$와 비교하면 rank-1 근사가 상당히 가까움을 알 수 있다.

**예제 3 (이미지 압축 관점):** $4 \times 4$ 행렬 $A = \begin{pmatrix} 1 & 1 & 0 & 0 \\ 1 & 1 & 0 & 0 \\ 0 & 0 & 1 & 1 \\ 0 & 0 & 1 & 1 \end{pmatrix}$의 SVD를 관찰로 구하라.

**풀이:** $A$의 rank는 2이다 (두 블록이 독립). $A^T A$를 계산하면 두 개의 0이 아닌 고유값이 2씩임을 알 수 있다(각 블록이 $2 \times 2$ all-ones 행렬). $\sigma_1 = \sigma_2 = 2$.

좌특이벡터: $u_1 = \frac{1}{\sqrt{2}}(1, 1, 0, 0)^T$, $u_2 = \frac{1}{\sqrt{2}}(0, 0, 1, 1)^T$.
우특이벡터: $v_1 = \frac{1}{\sqrt{2}}(1, 1, 0, 0)^T$, $v_2 = \frac{1}{\sqrt{2}}(0, 0, 1, 1)^T$.

$$A = 2 \cdot u_1 v_1^T + 2 \cdot u_2 v_2^T$$

rank-1 근사 $A_1 = 2 u_1 v_1^T$는 첫 번째 $2 \times 2$ 블록만 남기고 나머지는 0이 된다.

**예제 4 (이미지 압축 — SVD 관점):** $5 \times 5$ 행렬 $A$가 특이값 $\sigma = (10, 5, 2, 0.5, 0.1)$을 가질 때, rank-3 근사의 상대 오차를 구하라.

**풀이:** Frobenius 노름 기준:
$$\|A\|_F^2 = \sum \sigma_i^2 = 100 + 25 + 4 + 0.25 + 0.01 = 129.26$$
$$\|A - A_3\|_F^2 = \sigma_4^2 + \sigma_5^2 = 0.25 + 0.01 = 0.26$$
상대 오차: $\sqrt{0.26/129.26} \approx \sqrt{0.002} \approx 0.045$ (4.5%).
10개의 특이값 중 3개만으로 원본의 95.5%를 복원한다.

**예제 5 (SVD의 기하학):** $A = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix}$의 SVD를 구하고 단위원이 어떻게 변환되는지 설명하라.

**풀이:** $A^T A = \begin{pmatrix} 4 & 2 \\ 2 & 5 \end{pmatrix}$.
$\det\begin{pmatrix} 4-\lambda & 2 \\ 2 & 5-\lambda \end{pmatrix} = \lambda^2 - 9\lambda + 16 = 0$.
$\lambda = \frac{9 \pm \sqrt{81-64}}{2} = \frac{9 \pm \sqrt{17}}{2}$.
$\sigma_1 = \sqrt{(9+\sqrt{17})/2} \approx \sqrt{6.56} \approx 2.56$, $\sigma_2 = \sqrt{(9-\sqrt{17})/2} \approx \sqrt{2.44} \approx 1.56$.

$A^T A$의 고유벡터($V$의 열):
$\lambda_1 = (9+\sqrt{17})/2$: $v_1 \approx (0.615, 0.788)$.
$\lambda_2 = (9-\sqrt{17})/2$: $v_2 \approx (-0.788, 0.615)$.

$u_1 = Av_1/\sigma_1$, $u_2 = Av_2/\sigma_2$.

**기하학적 해석:** $A$는 단위원을 장축 길이 $\sigma_1 \approx 2.56$, 단축 길이 $\sigma_2 \approx 1.56$인 타원으로 변환한다. 장축 방향은 $u_1$, 단축 방향은 $u_2$이며, $v_1$은 타원의 장축이 되는 원 위의 방향, $v_2$는 단축이 되는 방향이다.

**예제 6 (SVD와 최소제곱):** $A = \begin{pmatrix} 1 & 1 \\ 1 & 1 \\ 1 & 0 \end{pmatrix}$, $b = \begin{pmatrix} 2 \\ 3 \\ 1 \end{pmatrix}$의 최소제곱해를 SVD 의사역행렬로 구하라.

**풀이:** $A$의 SVD를 먼저 구한다.
$$A^T A = \begin{pmatrix} 1 & 1 & 1 \\ 1 & 1 & 0 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 3 & 2 \\ 2 & 2 \end{pmatrix}$$
고유값: $\det\begin{pmatrix} 3-\lambda & 2 \\ 2 & 2-\lambda \end{pmatrix} = (3-\lambda)(2-\lambda) - 4 = \lambda^2 - 5\lambda + 2$.
$\lambda = \frac{5 \pm \sqrt{17}}{2}$, $\sigma_1^2 = \frac{5+\sqrt{17}}{2}$, $\sigma_2^2 = \frac{5-\sqrt{17}}{2}$.

의사역행렬 $A^+ = V \Sigma^+ U^T$로 최소제곱해를 구할 수 있다. (계산은 복잡하므로 생략한다.)

## 연결

- **[rank·열공간·널공간](topics/rank-nullspace.html)** : SVD는 행렬의 네 기본공간을 한 번에 드러낸다 — rank는 0이 아닌 특이값의 개수와 같다.
- **[고유값·고유벡터](topics/eigenvalues.html)** : SVD는 $A^T A$의 고유값 분해에서 출발하며, 고유값 개념을 직사각행렬로 확장한다.
- **[대칭행렬·스펙트럼 정리](topics/spectral-theorem.html)** : SVD 존재 증명은 $A^T A$의 스펙트럼 정리에 의존한다.
