---
title: 확률 행렬·마르코프 체인
slug: markov-chains
---

## 직관적 설명

**마르코프 체인(Markov chain)**은 시간에 따라 상태(state)가 확률적으로 변화하는 과정을 모델링한다. 핵심은 **마르코프 성질(Markov property)** — "미래는 오직 현재에만 의존한다" — 이다. 즉, $n+1$번째 상태는 $n$번째 상태만 알면 $n-1$번째 이전의 모든 과거와 독립적이다.

이 과정은 **전이확률행렬(transition probability matrix)** $P$로 완전히 기술된다. $P_{ij}$는 현재 상태가 $i$일 때 다음 상태가 $j$가 될 확률이다. 행 확률의 합은 항상 1이다($\sum_j P_{ij} = 1$). $n$단계 후의 전이확률은 $P^n$으로 주어지며, 이는 행렬곱이 "확률의 전파"라는 직관과 완벽하게 일치한다.

마르코프 체인의 가장 흥미로운 질문은 **정상분포(stationary distribution)** — 체인이 무한히 오래 작동한 후의 상태 분포 $\pi$ — 이다. $\pi$는 $\pi P = \pi$를 만족하며, $P$의 왼쪽 고유벡터(고유값 1)이다. 기약(irreducible)이고 비주기(aperiodic)인 체인은 초기 상태와 무관하게 유일한 정상분포로 수렴한다.

마르코프 체인은 구글 페이지랭크(웹페이지 중요도 측정), 텍스트 생성(Markov chain text generation), MCMC(마르코프 체인 몬테카를로) 샘플링, 날씨 모델링, 인구 동태, 금융 위험 평가 등 광범위하게 응용된다.

## 정의

**확률 과정 (stochastic process):** 이산 시간(discrete-time) 확률 과정 $\{X_n\}_{n=0}^\infty$은 각 시점 $n$에서 상태 $X_n$을 가지며, 상태 공간(state space) $S$에서 값을 취한다. 본 장에서는 $S$가 유한 집합 $\{1, 2, \ldots, N\}$인 경우를 다룬다.

**마르코프 성질 (Markov property):**
$$P(X_{n+1} = j \mid X_n = i, X_{n-1} = i_{n-1}, \ldots, X_0 = i_0) = P(X_{n+1} = j \mid X_n = i)$$

즉, 미래 상태($X_{n+1}$)는 현재 상태($X_n$)가 주어졌을 때 과거($X_{n-1}, \ldots, X_0$)와 조건부 독립이다.

**전이확률행렬 (transition probability matrix):** $P$는 $N \times N$ 행렬로 $P_{ij} = P(X_{n+1} = j \mid X_n = i)$이다. $P$는 **확률 행렬(stochastic matrix)** 로서 다음 성질을 만족한다:

1. **비음성 (non-negativity):** $P_{ij} \geq 0$ for all $i, j$.
2. **행 합 = 1 (row-stochastic):** $\sum_{j=1}^N P_{ij} = 1$ for all $i$.

$P$의 각 행은 현재 상태 $i$에서 가능한 모든 다음 상태로의 확률분포를 나타낸다.

**$n$단계 전이 확률:** $P^n_{ij} = P(X_n = j \mid X_0 = i)$. $P^n$의 $(i,j)$ 성분은 초기 상태 $i$에서 정확히 $n$단계 후에 상태 $j$에 도달할 확률이다. 이는 차프만-콜모고로프 방정식(Chapman-Kolmogorov equation) $P^{m+n} = P^m P^n$을 만족한다.

**초기 분포 (initial distribution):** $\pi^{(0)}_i = P(X_0 = i)$는 행벡터로 표현된다. $\pi^{(0)}$는 $\sum_i \pi^{(0)}_i = 1$, $\pi^{(0)}_i \geq 0$을 만족한다. $n$단계 후의 분포는 $\pi^{(n)} = \pi^{(0)} P^n$이다.

**정상분포 (stationary distribution):** 행벡터 $\pi$가 다음을 만족하면 $\pi$를 정상분포라 한다:
$$\pi P = \pi, \quad \sum_i \pi_i = 1, \quad \pi_i \geq 0$$

정상분포는 체인의 동적 평형 상태, 즉 한 번 도달하면 변하지 않는 분포를 나타낸다.

**기약성 (irreducibility):** 마르코프 체인이 **기약(irreducible)** 이라 함은 모든 상태 $i, j \in S$에 대해 어떤 $n \geq 0$이 존재하여 $P^n_{ij} > 0$인 경우다. 즉, 모든 상태가 서로 도달 가능하다.

**비주기성 (aperiodicity):** 상태 $i$의 **주기(period)** 는 $\gcd\{n \geq 1 \mid P^n_{ii} > 0\}$이다. 모든 상태의 주기가 1이면 **비주기(aperiodic)** 라 한다.

## 주요 정리와 증명

### 정리 1: 유한 기약 마르코프 체인의 정상분포 존재

유한 상태 공간을 가진 기약 마르코프 체인은 유일한 정상분포 $\pi$를 가진다.

**증명 (페론-프로베니우스 정리 활용):** $P$가 기약 확률 행렬(irreducible stochastic matrix)일 때, 페론-프로베니우스 정리(Perron-Frobenius Theorem)의 따름정리로 정상분포의 존재와 유일성이 보장된다.

**Perron-Frobenius 정리 (인용):** 모든 성분이 양수인 정사각행렬 $A > 0$는 다음 성질을 가진다:
1. 스펙트럼 반경 $\rho(A) > 0$에 해당하는 주 고유값(Perron root)이 존재한다.
2. $\rho(A)$는 대수적 중복도 1의 단순 고유값이다.
3. $\rho(A)$에 대응하는 고유벡터는 모든 성분이 양수이다 (고유벡터의 유일성, 스케일링까지).

**확률 행렬에의 적용:** $P$가 기약이고 비음수 행렬이므로, 충분히 큰 $m$에 대해 $(I + P)^m$은 모든 성분이 양수이다. $P$의 스펙트럼 반경은 1이다($P$의 모든 행 합이 1이므로 $P \mathbf{1} = \mathbf{1}$, 즉 $\mathbf{1} = (1,1,\ldots,1)^T$는 고유값 1의 우고유벡터).

페론-프로베니우스 정리에 의해 고유값 1은 대수적 중복도 1의 단순 고유값이며, 이에 대응하는 좌고유벡터 $\pi$ (즉, $\pi P = \pi$)는 유일하며 모든 성분이 양수이다. 이 $\pi$를 정규화($\sum \pi_i = 1$)하면 유일한 정상분포를 얻는다.

**참고:** 기약성은 전이행렬이 분해 불가능함을 보장하며, 이는 페론-프로베니우스 정리의 적용 조건을 만족시킨다.

### 정리 2: 수렴 정리 (Convergence Theorem)

기약이고 비주기인 유한 마르코프 체인은 초기 분포 $\pi^{(0)}$와 무관하게 유일한 정상분포 $\pi$로 수렴한다:
$$\lim_{n \to \infty} P^n = \mathbf{1} \pi^T$$

즉, $\lim_{n \to \infty} P^n_{ij} = \pi_j$ (모든 $i$에 대해 동일한 극한), 그리고 $\lim_{n \to \infty} \pi^{(n)} = \pi$.

**증명 스케치 (고유값 분해):** $P$가 대각화 가능하다고 가정하자 ($P$가 비주기적 기약 확률 행렬이면 고유값 분해가 잘 작동한다). $P = V D V^{-1}$로 대각화하자. $P$의 고유값을 $\lambda_1 = 1, \lambda_2, \ldots, \lambda_N$이라 하면, 비주기성과 기약성에 의해 $|\lambda_k| < 1$ for all $k \geq 2$이다.

$$P^n = V D^n V^{-1}$$

$D^n$의 대각 성분은 $\lambda_k^n$이다. $n \to \infty$에서 $|\lambda_k| < 1$이므로 $\lambda_k^n \to 0$ for $k \geq 2$이다. 따라서:

$$\lim_{n \to \infty} P^n = V \begin{pmatrix}
1 & 0 & \cdots & 0 \\
0 & 0 & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & 0
\end{pmatrix} V^{-1} = \mathbf{1} \pi^T$$

여기서 $\pi$는 $P$의 정상분포(좌고유벡터)이고 $\mathbf{1}$은 모든 원소가 1인 열벡터(우고유벡터)이다. 마지막 등식은 고유값 1에 대응하는 좌·우 고유벡터가 각각 $\pi^T$와 $\mathbf{1}$이라는 사실에서 유도된다.

**수렴 속도:** 수렴 속도는 두 번째로 큰 고유값(spectral gap) $\lambda_2$에 의해 결정된다:
$$\|P^n - \mathbf{1}\pi^T\| = O(|\lambda_2|^n)$$

$|\lambda_2|$가 1에 가까울수록 수렴이 느리다(mixing time이 길다).

### 정리 3: $\pi$는 $P^T$의 고유값 1에 대한 고유벡터

정상분포 $\pi$가 $\pi P = \pi$를 만족함은 $P^T \pi^T = \pi^T$와 동치이다. 즉, $\pi^T$는 $P^T$의 고유값 1에 대응하는 우고유벡터이다.

**증명:**
$$\pi P = \pi \quad \Longleftrightarrow \quad (\pi P)^T = \pi^T \quad \Longleftrightarrow \quad P^T \pi^T = \pi^T$$

이는 행렬 전치의 기본 성질이다. 따라서 정상분포를 구하는 문제는 $P^T$의 고유값 1에 대응하는 고유벡터를 찾는 문제와 동치이다. 이 관점은 페이지랭크 알고리즘에서 직접 활용된다.

**실용적 의미:** $\pi$를 구하는 한 가지 방법은 $P^T$의 고유벡터를 수치적으로 계산하는 것이다 (power iteration). $P$가 $10^9$ 차원이어도 power iteration은 가능하다.

### 정리 4: 상세 균형 (Detailed Balance)과 가역성

마르코프 체인이 **상세 균형 조건(detailed balance)** 을 만족하면 **가역(reversible)** 이라 한다:
$$\pi_i P_{ij} = \pi_j P_{ji} \quad \text{for all } i, j$$

상세 균형은 각 상태 쌍 사이의 확률 흐름이 정상분포에서 균형을 이룸을 의미한다: $i$에서 $j$로 가는 기대 유량(expected flux)이 $j$에서 $i$로 가는 유량과 같다.

**증명 (상세 균형 $\Rightarrow$ 정상분포):** 상세 균형이 성립하면 $\pi$는 정상분포이다:
$$\sum_i \pi_i P_{ij} = \sum_i \pi_j P_{ji} = \pi_j \sum_i P_{ji} = \pi_j$$

따라서 $\pi P = \pi$가 성립한다. 그러나 역(정상분포 $\Rightarrow$ 상세 균형)은 일반적으로 성립하지 않는다.

## 예제

**예제 1 (2상태 날씨 모델):** 날씨가 맑음(1) 또는 비(2) 두 상태만 가진다고 하자. 전이확률행렬:
$$P = \begin{pmatrix}
0.9 & 0.1 \\
0.5 & 0.5
\end{pmatrix}$$

오늘 맑을 때 내일 맑을 확률 = 0.9, 오늘 비가 올 때 내일 맑을 확률 = 0.5. 정상분포 $\pi = (\pi_1, \pi_2)$를 구하자.

**풀이:** $\pi P = \pi$에서:
$$\begin{aligned}
0.9\pi_1 + 0.5\pi_2 &= \pi_1 \\
0.1\pi_1 + 0.5\pi_2 &= \pi_2
\end{aligned}$$

첫 방정식에서 $-0.1\pi_1 + 0.5\pi_2 = 0$, 따라서 $\pi_1 = 5\pi_2$. 정규화 조건 $\pi_1 + \pi_2 = 1$에서 $\pi_2 = 1/6$, $\pi_1 = 5/6$. 정상분포: $\pi = (5/6, 1/6)$.

장기적으로 맑은 날 83.3%, 비 오는 날 16.7%.

**예제 2 ($P^n$ 수렴 확인):** 예제 1의 $P$에 대해 $P^2, P^4, P^8$를 계산하고 수렴을 확인하라.

**풀이:**
$$P^2 = \begin{pmatrix}
0.9 & 0.1 \\
0.5 & 0.5
\end{pmatrix}^2 = \begin{pmatrix}
0.86 & 0.14 \\
0.70 & 0.30
\end{pmatrix}$$

$$P^4 = (P^2)^2 = \begin{pmatrix}
0.86 & 0.14 \\
0.70 & 0.30
\end{pmatrix}^2 = \begin{pmatrix}
0.8376 & 0.1624 \\
0.8120 & 0.1880
\end{pmatrix}$$

$$P^8 = (P^4)^2 \approx \begin{pmatrix}
0.8334 & 0.1666 \\
0.8330 & 0.1670
\end{pmatrix}$$

$P^8$의 각 행이 거의 $\pi = (5/6, 1/6) \approx (0.8333, 0.1667)$에 수렴했음을 확인할 수 있다.

$P$의 고유값: $\lambda_1 = 1$, $\lambda_2 = 0.4$. $|\lambda_2| = 0.4$이므로 수렴 속도는 $O(0.4^n)$으로 빠르다.

**예제 3 (페이지랭크의 수학적 구조):** 구글 페이지랭크(PageRank)는 웹을 거대한 마르코프 체인으로 모델링한다. $N$개의 웹페이지가 있고, 페이지 $i$에서 $d_i$개의 외부 링크가 있다면:
$$P_{ij} = \begin{cases}
\frac{1}{d_i} & \text{if page $i$ links to page $j$} \\
0 & \text{otherwise}
\end{cases}$$

그러나 이 행렬은 기약이 아닐 수 있다(링크가 없는 페이지, 링크 함정). 해결을 위해 **감쇠 인자(damping factor)** $\alpha = 0.85$를 도입하여 수정된 전이행렬을 사용한다:
$$G = \alpha P + (1-\alpha) \frac{1}{N} \mathbf{1} \mathbf{1}^T$$

이 $G$는 모든 성분이 양수이므로 기약이고 비주기적이다. 정상분포 $\pi$ (페이지랭크 점수)는 $\pi G = \pi$를 만족하며, power iteration으로 효율적으로 계산된다.

**참고:** 페이지랭크의 원래 논문(Brin & Page, 1998)은 웹 서핑을 "링크를 따라가거나" "임의의 페이지로 점프하는" 확률 과정으로 모델링했다. $\alpha$는 링크를 따라갈 확률이고, $1-\alpha$는 임의 점프 확률이다.

**예제 4 (3상태 마르코프 체인):** 전이행렬 $P = \begin{pmatrix}
0.7 & 0.2 & 0.1 \\
0.3 & 0.4 & 0.3 \\
0.2 & 0.3 & 0.5
\end{pmatrix}$의 정상분포를 구하라.

**풀이:** $\pi P = \pi$에서 선형방정식 $\pi(P - I) = 0$과 $\sum \pi_i = 1$을 풀면 된다.

행렬 $P - I$:
$$P - I = \begin{pmatrix}
-0.3 & 0.2 & 0.1 \\
0.3 & -0.6 & 0.3 \\
0.2 & 0.3 & -0.5
\end{pmatrix}$$

$\pi(P - I) = 0$의 첫 두 방정식과 정규화 조건을 연립한다:
$$\begin{cases}
-0.3\pi_1 + 0.3\pi_2 + 0.2\pi_3 = 0 \\
0.2\pi_1 - 0.6\pi_2 + 0.3\pi_3 = 0 \\
\pi_1 + \pi_2 + \pi_3 = 1
\end{cases}$$

첫 방정식에서 $3\pi_2 = 3\pi_1 - 2\pi_3$, 두 번째에서 $2\pi_1 - 6\pi_2 + 3\pi_3 = 0$. 대입하여 풀면:
$$\pi_1 = \frac{32}{77} \approx 0.416, \quad \pi_2 = \frac{19}{77} \approx 0.247, \quad \pi_3 = \frac{26}{77} \approx 0.338$$

**예제 5 (2단계 전이 확률):** 예제 4의 $P$에 대해, 상태 1에서 시작하여 2단계 후 각 상태에 있을 확률을 계산하라.

**풀이:** $P^2$의 첫 번째 행이 초기 상태 1에 대한 2단계 분포다:
$$P^2 = \begin{pmatrix}
0.7 & 0.2 & 0.1 \\
0.3 & 0.4 & 0.3 \\
0.2 & 0.3 & 0.5
\end{pmatrix}^2 = \begin{pmatrix}
0.7\cdot0.7 + 0.2\cdot0.3 + 0.1\cdot0.2 & 0.7\cdot0.2 + 0.2\cdot0.4 + 0.1\cdot0.3 & 0.7\cdot0.1 + 0.2\cdot0.3 + 0.1\cdot0.5 \\
\vdots & \vdots & \vdots
\end{pmatrix}$$

첫 행만 계산:
$$P^2_{11} = 0.49 + 0.06 + 0.02 = 0.57$$
$$P^2_{12} = 0.14 + 0.08 + 0.03 = 0.25$$
$$P^2_{13} = 0.07 + 0.06 + 0.05 = 0.18$$

검증: $0.57 + 0.25 + 0.18 = 1.0$.

**예제 6 (기대 방문 횟수):** 상태 $j$의 기대 방문 횟수(return probability)와 재귀성(recurrence)의 관계를 설명하라.

**풀이:** $f_{ii}$를 상태 $i$에서 출발하여 다시 $i$로 돌아올 확률이라 하자. $f_{ii} = 1$이면 **재귀적(recurrent)**, $f_{ii} < 1$이면 **일시적(transient)** 이라 한다. 유한 마르코프 체인에서 모든 상태는 재귀적이다.

기대 재방문 시간(expected return time) $\mu_i = \sum_{n=1}^\infty n f_{ii}^{(n)}$ (여기서 $f_{ii}^{(n)}$은 정확히 $n$단계 후 처음으로 $i$에 도달할 확률)은 정상분포와 관계된다:
$$\pi_i = \frac{1}{\mu_i}$$

즉, 정상분포에서 상태 $i$의 확률은 평균 재방문 시간의 역수이다.

## 연결

- **[고유값·고유벡터](eigenvalues.html)** : 정상분포 $\pi$는 $P^T$의 고유값 1에 대응하는 고유벡터이며, 수렴 속도는 두 번째 고유값에 의해 결정된다.
- **[마르코프 결정과정](mdp.html)** : 마르코프 체인에 행동(action)과 보상(reward)을 추가하면 MDP가 된다. MDP는 강화학습의 수학적 기초다.
- **[몬테카를로](monte-carlo.html)** : MCMC는 마르코프 체인을 사용하여 복잡한 분포에서 샘플링하는 방법이다.
- **[행렬곱과 선형변환](matrix-multiplication.html)** : $P^n$의 계산은 반복된 행렬곱이며, 상태 분포의 진화는 선형변환으로 이해된다.
