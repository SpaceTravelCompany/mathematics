---
title: 임베딩 공간의 기하학
slug: embedding-geometry
---

## 직관적 설명

**임베딩 공간(embedding space)**은 데이터를 고차원 벡터로 표현한 공간이다. 예를 들어 단어를 300차원 벡터로, 이미지를 4096차원 벡터로 표현하면 각 데이터는 $\mathbb{R}^n$의 한 점이 된다. 이 공간에서의 기하학적 관계(거리, 각도, 밀도)가 데이터의 의미적 관계를 반영한다.

고차원 공간은 우리의 3차원 직관이 완전히 무너지는 곳이다. 가장 충격적인 현상은 **차원의 저주(curse of dimensionality)** — 차원이 증가할수록 공간의 기하학이 우리의 예상과 극적으로 달라진다는 사실이다.

고차원 단위구(unit ball)의 부피는 차원이 증가함에 따라 0으로 수렴한다. 동시에 부피의 대부분은 표면 근처의 얇은 껍질(shell)에 집중된다. 고차원 공간에서 두 점을 무작위로 선택하면 거리는 거의 일정해지며(거리 집중), 두 랜덤 벡터는 거의 직교한다. 이러한 현상들은 고차원 데이터를 다룰 때 알고리즘 설계의 근본적인 제약과 기회를 제공한다.

임베딩 공간의 기하학은 정보 검색(코사인 유사도 기반 유사도 검색), 차원 축소(PCA, t-SNE, UMAP), 밀도 추정, 이상 탐지, 매니폴드 학습(manifold learning) 등 다양한 분야의 수학적 기초다.

## 정의

**유클리드 거리 (Euclidean distance):** $x, y \in \mathbb{R}^n$ 사이의 유클리드 거리:
$$d(x, y) = \|x - y\|_2 = \sqrt{\sum_{i=1}^n (x_i - y_i)^2}$$

**코사인 유사도 (cosine similarity):** 두 벡터 사이의 각도의 코사인:
$$\cos(\theta) = \frac{x \cdot y}{\|x\| \|y\|} = \frac{\sum_{i=1}^n x_i y_i}{\sqrt{\sum_{i=1}^n x_i^2} \sqrt{\sum_{i=1}^n y_i^2}}$$

코사인 유사도는 $[-1, 1]$ 범위이며, 벡터의 크기와 무관하게 방향만 측정한다.

**고차원 구 (ball)와 구면 (sphere):**

$n$차원 반지름 $r$인 **구(ball)** $B^n(r) = \{x \in \mathbb{R}^n \mid \|x\| \leq r\}$의 **부피(volume)**:
$$V_n(r) = \frac{\pi^{n/2}}{\Gamma(n/2 + 1)} r^n$$

여기서 $\Gamma$는 감마 함수(Gamma function)로, 정수 $n$에 대해 $\Gamma(n) = (n-1)!$이고 반정수에 대해서는 $\Gamma(k+1/2) = \frac{(2k)!}{4^k k!} \sqrt{\pi}$이다.

**단위구 부피의 특수값:**
$$V_1(r) = 2r$$
$$V_2(r) = \pi r^2$$
$$V_3(r) = \frac{4}{3} \pi r^3$$

**단위구면 (unit sphere)** $S^{n-1} = \{x \in \mathbb{R}^n \mid \|x\| = 1\}$의 **표면적(surface area)**:
$$A_{n-1} = n V_n(1) = \frac{2\pi^{n/2}}{\Gamma(n/2)}$$

**매니폴드 (manifold) 직관:** 매니폴드는 국소적으로 $\mathbb{R}^k$와 닮은 위상공간으로, 고차원 공간에 내장된 저차원 구조다. 예를 들어 3차원 공간 속의 2차원 구면 $S^2$은 2차원 매니폴드다. 임베딩 공간의 데이터는 종종 고차원 공간 속의 저차원 매니폴드 근처에 분포한다(매니폴드 가설).

## 주요 정리와 증명

### 정리 1: 고차원 단위구의 부피가 0으로 수렴

$n \to \infty$일 때 $n$차원 단위구 $B^n(1)$의 부피 $V_n = V_n(1)$은 0으로 수렴한다:
$$\lim_{n \to \infty} V_n = 0$$

**증명 (스털링 근사):** $V_n = \frac{\pi^{n/2}}{\Gamma(n/2 + 1)}$에 스털링 근사(Stirling's approximation) $\Gamma(z+1) \sim \sqrt{2\pi z} (z/e)^z$를 적용한다.

$z = n/2$라 하면:
$$\Gamma(n/2 + 1) \sim \sqrt{2\pi \cdot n/2} \left(\frac{n/2}{e}\right)^{n/2} = \sqrt{\pi n} \left(\frac{n}{2e}\right)^{n/2}$$

따라서:
$$V_n \sim \frac{\pi^{n/2}}{\sqrt{\pi n} (n/(2e))^{n/2}} = \frac{1}{\sqrt{\pi n}} \left(\frac{2\pi e}{n}\right)^{n/2}$$

$n \to \infty$에서 $(2\pi e / n)^{n/2} \to 0$ (밑이 1보다 작아지므로), 따라서 $V_n \to 0$이다.

**더 직접적인 증명:** $V_n$의 점화 관계 $V_n = V_{n-1} \cdot \int_{-1}^1 (1 - t^2)^{(n-1)/2} dt$에서, 적분값이 $n$이 증가함에 따라 0으로 수렴함을 보일 수도 있다.

**수치 결과:** $V_1 = 2$, $V_2 = \pi \approx 3.14$, $V_3 = 4\pi/3 \approx 4.19$, $V_5 \approx 5.26$, $V_{10} \approx 2.55$, $V_{20} \approx 0.026$, $V_{50} \approx 1.05 \times 10^{-14}$.

### 정리 2: 부피의 껍질 집중 (Concentration of Volume in the Shell)

고차원 구의 부피는 중심 근처가 아니라 표면 근처의 얇은 껍질에 집중된다. 구 $B^n(r)$에서 반지름 $r-\epsilon$에서 $r$ 사이의 껍질(shell)의 부피 비율은:
$$\frac{V_n(r) - V_n(r-\epsilon)}{V_n(r)} = 1 - \left(1 - \frac{\epsilon}{r}\right)^n$$

$n \to \infty$에서 이 비율은 1로 수렴한다 (단, $\epsilon > 0$).

**증명:**
$$\frac{V_n(r) - V_n(r-\epsilon)}{V_n(r)} = \frac{r^n - (r-\epsilon)^n}{r^n} = 1 - \left(1 - \frac{\epsilon}{r}\right)^n$$

$n \to \infty$에서 $|1 - \epsilon/r| < 1$이므로 $(1 - \epsilon/r)^n \to 0$. 따라서 껍질 부피 비율 $\to 1$.

**의미:** $n = 1000$, $r = 1$, $\epsilon = 0.01$이면 부피의 $1 - (0.99)^{1000} \approx 1 - 4.3 \times 10^{-5} \approx 0.999957$, 즉 99.9957%가 표면에서 1% 두께의 껍질에 집중된다. 고차원 데이터를 다룰 때 "중심" 근처에는 데이터가 거의 존재하지 않는다는 의미다.

### 정리 3: 고차원 랜덤 벡터의 직교성

$X, Y \in \mathbb{R}^n$이 각각 구면에서 균일하게 분포(uniform on sphere)하는 독립 확률벡터일 때, $n \to \infty$에서 두 벡터의 내적은 0에 집중된다:
$$\frac{X \cdot Y}{\|X\| \|Y\|} \to 0 \quad \text{in probability}$$

더 정확히는, $\mathbb{E}[X \cdot Y] = 0$이고 $\text{Var}(X \cdot Y) \to 0$ (수렴 속도는 $1/n$).

**증명 스케치 (집중 부등식 활용):** $n$차원 단위구면 $S^{n-1}$ 위의 균일 분포에서 $X$의 각 성분 $X_i$는 $\mathbb{E}[X_i] = 0$, $\text{Var}(X_i) = 1/n$, $\sum_i X_i^2 = 1$을 만족한다. 독립인 $X, Y$에 대해:
$$\mathbb{E}[X \cdot Y] = \sum_i \mathbb{E}[X_i Y_i] = \sum_i \mathbb{E}[X_i]\mathbb{E}[Y_i] = 0$$

분산:
$$\begin{aligned}
\text{Var}(X \cdot Y) &= \mathbb{E}[(X \cdot Y)^2] - (\mathbb{E}[X \cdot Y])^2 \\
&= \mathbb{E}\left[\sum_i \sum_j X_i Y_i X_j Y_j\right] \\
&= \sum_i \mathbb{E}[X_i^2]\mathbb{E}[Y_i^2] + \sum_{i \neq j} \mathbb{E}[X_i X_j]\mathbb{E}[Y_i Y_j] \\
&= \sum_i \frac{1}{n} \cdot \frac{1}{n} + 0 = n \cdot \frac{1}{n^2} = \frac{1}{n}
\end{aligned}$$

체비쇼프 부등식(Chebyshev's inequality)에 의해, 임의의 $\epsilon > 0$에 대해:
$$P(|X \cdot Y| > \epsilon) \leq \frac{1}{n \epsilon^2} \to 0 \quad \text{as } n \to \infty$$

따라서 고차원에서는 거의 모든 벡터 쌍이 서로 직교(orthogonal)에 가깝다. 이는 고차원 공간의 "놀라운 직교성(blessing of dimensionality)"으로, 유사도 검색과 차원 축소의 이론적 기초다.

**참고:** 이 결과는 $X, Y$가 독립일 때 성립한다. 두 벡터가 특정 구조(예: 같은 데이터의 변형)를 공유하면 내적이 0이 아닐 수 있다.

## 예제

**예제 1 (차원별 단위구 부피 계산):** $n = 1, 2, 3, 5, 10, 20, 50$에서 $V_n(1)$을 계산하라.

**풀이:**
- $n = 1$: $V_1 = 2$ (길이 2의 선분)
- $n = 2$: $V_2 = \pi \approx 3.1416$
- $n = 3$: $V_3 = 4\pi/3 \approx 4.1888$
- $n = 5$: $V_5 = \frac{\pi^{5/2}}{\Gamma(5/2+1)} = \frac{\pi^{5/2}}{\Gamma(7/2)} = \frac{\pi^{5/2}}{(5/2)(3/2)(1/2)\sqrt{\pi}} = \frac{\pi^2}{(5/2)(3/2)(1/2)} = \frac{8\pi^2}{15} \approx 5.2638$
- $n = 10$: $V_{10} = \frac{\pi^5}{5!} = \frac{\pi^5}{120} \approx 2.5502$
- $n = 20$: $V_{20} = \frac{\pi^{10}}{10!} \approx \frac{93648}{3628800} \approx 0.0258$
- $n = 50$: $V_{50} \approx 1.05 \times 10^{-14}$

부피가 $n=5$까지 증가하다가 급격히 감소함을 관찰할 수 있다.

**예제 2 (껍질 비율 계산):** $n = 2, 10, 100, 1000$에 대해, 단위구에서 반지름 0.9에서 1.0 사이 껍질의 부피 비율을 계산하라.

**풀이:** 껍질 비율 $= 1 - (0.9)^n$ (정리 2, $r=1$, $\epsilon=0.1$):
- $n = 2$: $1 - 0.81 = 0.19$ (19%)
- $n = 10$: $1 - 0.9^{10} = 1 - 0.3487 = 0.6513$ (65.1%)
- $n = 100$: $1 - 0.9^{100} = 1 - 2.66 \times 10^{-5} \approx 0.99997$ (99.997%)
- $n = 1000$: $1 - 0.9^{1000} \approx 1 - 1.75 \times 10^{-46} \approx 1.0$ (≈ 100%)

고차원에서는 부피의 거의 전부가 표면 근처에 있다. 이는 고차원 데이터의 밀도 추정에서 중요한 함의를 가진다: 커널 밀도 추정(KDE)은 고차원에서 심각한 희소성 문제를 겪는다.

**예제 3 (고차원 거리 집중 현상):** $n$차원 단위구 $B^n(1)$에 균일 분포된 두 점 $x, y$ 사이의 거리 제곱의 기댓값과 분산을 계산하라.

**풀이:** 각 점 $x$의 성분 $x_i$는 $\mathbb{E}[x_i] = 0$, $\mathbb{E}[x_i^2] = 1/(n+2)$ (구 내부 균일 분포의 성질). $x$와 $y$가 독립이면:
$$\mathbb{E}[\|x - y\|^2] = \mathbb{E}[\|x\|^2 + \|y\|^2 - 2x \cdot y] = 2 \mathbb{E}[\|x\|^2] - 2\mathbb{E}[x \cdot y]$$

$\mathbb{E}[\|x\|^2] = \sum_i \mathbb{E}[x_i^2] = \frac{n}{n+2} \to 1$, $\mathbb{E}[x \cdot y] = \sum_i \mathbb{E}[x_i]\mathbb{E}[y_i] = 0$.

따라서 $\mathbb{E}[\|x - y\|^2] = \frac{2n}{n+2} \to 2$ (즉, 거리 $\to \sqrt{2}$).

분산 $\text{Var}(\|x - y\|^2) \to 0$ as $n \to \infty$. 즉, 고차원에서는 **모든 점 쌍의 거리가 거의 동일**해진다. 이는 거리 기반 방법(k-NN, clustering)이 고차원에서 실패하는 근본 원인이다: "가장 가까운 이웃"과 "가장 먼 이웃"의 차이가 사라진다.

**예제 4:** $n = 3$과 $n = 100$에서 두 랜덤 단위 벡터의 코사인 유사도의 분산을 비교하라.

**풀이:** $n$차원 단위구면 위의 균일 분포에서 $\text{Var}(\cos\theta) = 1/n$ (정리 3 증명 참조):
- $n = 3$: $\text{Var}(\cos\theta) = 1/3 \approx 0.333$, 표준편차 $\approx 0.577$
- $n = 100$: $\text{Var}(\cos\theta) = 1/100 = 0.01$, 표준편차 $= 0.1$

$n=3$에서는 $\cos\theta$의 표준편차가 0.577로 분포가 넓지만, $n=100$에서는 0.1로 매우 좁다. 고차원에서는 두 랜덤 벡터가 거의 항상 직교($\cos\theta \approx 0$)한다.

**예제 5 (단위구면의 표면적):** $n = 2, 3, 4, 10$에서 $S^{n-1}$의 표면적을 계산하라.

**풀이:** $A_{n-1} = \frac{2\pi^{n/2}}{\Gamma(n/2)}$:
- $n = 2$ ($S^1$, 원주): $A_1 = 2\pi$
- $n = 3$ ($S^2$, 구면): $A_2 = \frac{2\pi^{3/2}}{\Gamma(3/2)} = \frac{2\pi^{3/2}}{\sqrt{\pi}/2} = 4\pi$
- $n = 4$ ($S^3$): $A_3 = \frac{2\pi^2}{\Gamma(2)} = 2\pi^2 \approx 19.74$
- $n = 10$ ($S^9$): $A_9 = \frac{2\pi^5}{\Gamma(5)} = \frac{2\pi^5}{24} = \frac{\pi^5}{12} \approx 25.57$

표면적도 $n$이 증가함에 따라 일정 값까지 증가했다가 감소한다.

**예제 6 (고차원 가우시안 분포):** $n$차원 표준정규분포 $\mathcal{N}(0, I_n)$에서 샘플링한 점의 대부분은 평균에서 거리 $\sqrt{n}$ 근처에 위치함을 보여라.

**풀이:** $\|X\|^2 = \sum_{i=1}^n X_i^2$는 자유도 $n$의 카이제곱 분포(chi-square distribution) $\chi^2_n$을 따른다. 카이제곱 분포의 성질:
$$\mathbb{E}[\|X\|^2] = n, \quad \text{Var}(\|X\|^2) = 2n$$

표준편차는 $\sqrt{2n}$이므로, $\|X\|$는 $\sqrt{n}$ 주변에 폭이 $O(1)$인 영역에 집중된다(평균 $\sqrt{n}$, 분산은 $O(1)$). 즉, 고차원 가우시안 분포에서 샘플은 평균으로부터 거의 모두 $\sqrt{n}$ 거리의 얇은 껍질에 존재한다.

이는 고차원 가우시안의 밀도가 원점에서 가장 높지만(최빈값), 대부분의 확률 질량은 $\sqrt{n}$ 근처의 껍질에 집중된다는 역설적인 현상을 설명한다.

## 연결

- **[내적·노름·코사인 유사도](inner-product-norm.html)** : 임베딩 공간의 거리와 각도를 측정하는 기본 도구로, 고차원 기하학의 모든 계산은 내적과 노름에서 출발한다.
- **[정보기하·자연 그래디언트](information-geometry.html)** : 확률분포 공간은 정보기하학적 관점에서 리만 매니폴드로 이해되며, 고차원 임베딩 공간의 기하학과 밀접하게 연결된다.
- **[가우시안 과정](gaussian-process.html)** : 고차원 함수 공간 위의 확률분포로, 커널 함수에 의해 결정되는 기하학적 구조를 가진다.
- **[주성분 분석(PCA)](svd.html)** : 고차원 데이터의 분산이 가장 큰 방향을 찾는 선형 차원 축소 방법으로, 임베딩 공간의 기하학적 구조를 단순화한다.
