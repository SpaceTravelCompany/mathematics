---
title: 마르코프 결정과정
slug: mdp
---

## 직관적 설명

**마르코프 결정과정(Markov Decision Process, MDP)**은 순차적 의사결정(sequential decision making) 문제를 수학적으로 형식화한 틀이다. 에이전트(agent)는 환경(environment)의 상태(state)를 관찰하고, 행동(action)을 선택하며, 그 결과로 보상(reward)을 받고 새로운 상태로 전이된다. 목표는 **누적 기대 보상의 합을 최대화하는 정책(policy)** 을 찾는 것이다.

MDP의 핵심은 마르코프 성질(Markov property) — "미래는 오직 현재에만 의존한다" — 이다. 현재 상태 $s$와 행동 $a$가 주어지면, 다음 상태 $s'$로의 전이확률 $\Pr(s'|s,a)$은 과거의 모든 이력을 무시한다. 이 가정이 문제를 다루기 쉽게 만든다.

가치함수(value function) $V^\pi(s)$는 정책 $\pi$를 따를 때 상태 $s$에서 시작하여 얻을 수 있는 기대 할인 누적 보상(discounted cumulative reward)이다. 벨만 방정식(Bellman equation)은 이 가치함수를 재귀적(recursive)으로 표현한다:
$$V^\pi(s) = \sum_a \pi(a|s) \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^\pi(s')]$$

최적 정책(optimal policy) $\pi^*$은 모든 상태에서 가치함수를 최대화한다. 벨만 최적 방정식(Bellman optimality equation)은 최적 가치함수 $V^*$에 대해:
$$V^*(s) = \max_a \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^*(s')]$$

가치 반복(value iteration)과 정책 반복(policy iteration)은 이 방정식을 풀어 최적 정책을 찾는 대표적 알고리즘이다.

## 정의

**마르코프 결정과정 (Markov Decision Process):** MDP는 다음 5개의 요소로 구성된 튜플 $(\mathcal{S}, \mathcal{A}, P, R, \gamma)$이다.

- $\mathcal{S}$: **상태 공간 (state space)** — 유한 집합이라고 가정한다.
- $\mathcal{A}$: **행동 공간 (action space)** — 각 상태 $s$에서 선택 가능한 행동의 집합.
- $P$: **전이확률 (transition probability)** — $P(s'|s,a) = \Pr(S_{t+1} = s' \mid S_t = s, A_t = a)$.
- $R$: **보상 함수 (reward function)** — $R(s,a,s')$ 또는 $R(s,a)$로 표현되는 즉각적 보상.
- $\gamma \in [0,1)$: **할인율 (discount factor)** — 미래 보상을 현재 가치로 할인한다. $\gamma = 0$이면 즉각 보상만 고려하고, $\gamma \to 1$이면 먼 미래까지 동등하게 고려한다.

**정책 (policy):** $\pi(a|s) = \Pr(A_t = a \mid S_t = s)$. 결정론적 정책(deterministic policy)은 $\pi(s) = a$로 함수 형태로 표현된다.

**반환값 (return):** $G_t = \sum_{k=0}^\infty \gamma^k R_{t+k+1}$ — 시간 $t$ 이후의 할인 누적 보상.

**상태 가치함수 (state-value function):**
$$V^\pi(s) = \mathbb{E}_\pi[G_t \mid S_t = s] = \mathbb{E}_\pi\left[\sum_{k=0}^\infty \gamma^k R_{t+k+1} \,\middle|\, S_t = s\right]$$

**행동 가치함수 (action-value function):**
$$Q^\pi(s,a) = \mathbb{E}_\pi[G_t \mid S_t = s, A_t = a]$$

**벨만 방정식 (Bellman equation) for $V^\pi$:**
$$V^\pi(s) = \sum_a \pi(a|s) \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^\pi(s')]$$

**최적 가치함수 (optimal value function):**
$$V^*(s) = \max_\pi V^\pi(s), \quad Q^*(s,a) = \max_\pi Q^\pi(s,a)$$

**벨만 최적 방정식 (Bellman optimality equation):**
$$V^*(s) = \max_a \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^*(s')]$$
$$Q^*(s,a) = \sum_{s'} P(s'|s,a)\left[R(s,a,s') + \gamma \max_{a'} Q^*(s',a')\right]$$

## 주요 정리와 증명

### 정리 1: 벨만 방정식의 유도

**서술:** $V^\pi(s)$는 다음 재귀 방정식을 만족한다:
$$V^\pi(s) = \sum_a \pi(a|s) \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^\pi(s')]$$

**증명:** 반환값의 정의에서 시작한다.
$$V^\pi(s) = \mathbb{E}_\pi\left[\sum_{k=0}^\infty \gamma^k R_{t+k+1} \,\middle|\, S_t = s\right]$$
$$= \mathbb{E}_\pi\left[R_{t+1} + \gamma \sum_{k=0}^\infty \gamma^k R_{t+k+2} \,\middle|\, S_t = s\right]$$

기댓값의 선형성과 조건부 기댓값의 법칙(law of total expectation)을 적용한다:
$$= \mathbb{E}_\pi[R_{t+1} \mid S_t = s] + \gamma \mathbb{E}_\pi\left[ \sum_{k=0}^\infty \gamma^k R_{t+k+2} \,\middle|\, S_t = s\right]$$

첫 항: $\mathbb{E}_\pi[R_{t+1} \mid S_t = s] = \sum_a \pi(a|s) \sum_{s'} P(s'|s,a) R(s,a,s')$.

두 번째 항: 마르코프 성질에 의해 $S_{t+1}$이 주어지면 $S_t$는 $G_{t+1}$과 조건부 독립이다. 따라서
$$\mathbb{E}_\pi[G_{t+1} \mid S_t = s] = \mathbb{E}_\pi[\mathbb{E}_\pi[G_{t+1} \mid S_{t+1}] \mid S_t = s] = \sum_a \pi(a|s) \sum_{s'} P(s'|s,a) V^\pi(s')$$

종합하면:
$$V^\pi(s) = \sum_a \pi(a|s) \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^\pi(s')]$$

$\square$

### 정리 2: 최적 정책의 존재

**서술:** 유한 MDP(유한 $\mathcal{S}$, 유한 $\mathcal{A}$)에서 다음을 만족하는 최적 정책 $\pi^*$가 항상 존재한다:
$$V^{\pi^*}(s) = V^*(s) \geq V^\pi(s) \quad \forall s \in \mathcal{S}, \forall \pi$$

**서술 증명:** 벨만 최적 방정식 $V^*(s) = \max_a \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^*(s')]$는 축소사상(contraction mapping)이므로 유일한 고정점(fixed point)을 가진다. 이 고정점이 $V^*$이며, $V^*$에 도달하는 정책이 최적 정책이다.

$V^*$가 주어졌을 때, 결정론적 최적 정책은
$$\pi^*(s) = \arg\max_a \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V^*(s')]$$

으로 구성된다. 이 정책이 $V^{\pi^*} = V^*$을 만족함은 벨만 최적 방정식에 의해 보장된다. 또한 임의의 $\pi$에 대해 $V^\pi \leq V^*$임을 귀납법으로 보일 수 있다. $\square$

### 정리 3: 가치 반복의 수렴

**서술:** 벨만 최적 연산자(Bellman optimality operator) $\mathcal{T}$를 다음과 같이 정의하자:
$$(\mathcal{T}V)(s) = \max_a \sum_{s'} P(s'|s,a)[R(s,a,s') + \gamma V(s')]$$

$\mathcal{T}$는 $L_\infty$ 노름에서 $\gamma$-축소사상($\gamma$-contraction)이다:
$$\|\mathcal{T}V_1 - \mathcal{T}V_2\|_\infty \leq \gamma \|V_1 - V_2\|_\infty$$

따라서 임의의 초기 $V_0$에서 시작하는 가치 반복 $V_{k+1} = \mathcal{T}V_k$는 $V^*$로 선형 수렴한다:
$$\|V_k - V^*\|_\infty \leq \gamma^k \|V_0 - V^*\|_\infty$$

**증명:** 먼저 $\mathcal{T}$가 단조(monotone) 연산자임을 확인한다: $V_1 \leq V_2$ (모든 $s$에서)이면 $\mathcal{T}V_1 \leq \mathcal{T}V_2$.

임의의 $s$에 대해
$$|(\mathcal{T}V_1)(s) - (\mathcal{T}V_2)(s)|$$
$$= \left|\max_a f(s,a,V_1) - \max_a f(s,a,V_2)\right|$$
여기서 $f(s,a,V) = \sum_{s'} P(s'|s,a)[R + \gamma V(s')]$이다.

$\max$ 연산자가 립시츠(Lipschitz) 상수 1을 가짐을 이용하면:
$$\leq \max_a |f(s,a,V_1) - f(s,a,V_2)|$$
$$= \max_a \gamma \left|\sum_{s'} P(s'|s,a)(V_1(s') - V_2(s'))\right|$$
$$\leq \max_a \gamma \sum_{s'} P(s'|s,a) |V_1(s') - V_2(s')|$$
$$\leq \gamma \|V_1 - V_2\|_\infty$$

모든 $s$에 대해 성립하므로 $\|\mathcal{T}V_1 - \mathcal{T}V_2\|_\infty \leq \gamma \|V_1 - V_2\|_\infty$이다.

축소사상 정리(contraction mapping theorem)에 의해 $\mathcal{T}$는 유일한 고정점 $V^*$를 가지며, 임의의 $V_0$에서 $V_{k+1} = \mathcal{T}V_k$로 생성된 수열은 $V^*$로 수렴한다. 오차 한계:
$$\|V_k - V^*\|_\infty \leq \gamma^k \|V_0 - V^*\|_\infty$$

$\square$

**수렴 속도:** 할인율 $\gamma$가 작을수록 수렴이 빠르다. $\gamma = 0.9$면 100회 반복 후 $0.9^{100} \approx 0.000026$로 정확도가 높아진다.

### 정리 4: 정책 개선 정리 (Policy Improvement Theorem)

**서술:** 현재 정책 $\pi$에 대해 $Q^\pi(s, \pi'(s)) \geq V^\pi(s)$ for all $s$를 만족하는 새로운 정책 $\pi'$이 있으면, $\pi'$은 $\pi$보다 나쁘지 않다:
$$V^{\pi'}(s) \geq V^\pi(s) \quad \forall s \in \mathcal{S}$$

특히, 결정론적 정책 $\pi(s) = a$에 대해 탐욕 정책(greedy policy)
$$\pi'(s) = \arg\max_a Q^\pi(s,a)$$
은 $\pi$를 개선한다($\pi'$이 $\pi$보다 엄격히 좋거나 같다).

**증명:** $Q^\pi(s, \pi'(s)) \geq V^\pi(s)$에서 시작하여 $V^{\pi'}$를 전개한다.
$$V^\pi(s) \leq Q^\pi(s, \pi'(s)) = \mathbb{E}[R_{t+1} + \gamma V^\pi(S_{t+1}) \mid S_t = s, A_t = \pi'(s)]$$

귀납적으로 $k$단계 확장하면:
$$V^\pi(s) \leq \mathbb{E}_{\pi'}[R_{t+1} + \gamma V^\pi(S_{t+1}) \mid S_t = s]$$
$$\leq \mathbb{E}_{\pi'}[R_{t+1} + \gamma Q^\pi(S_{t+1}, \pi'(S_{t+1})) \mid S_t = s]$$
$$= \mathbb{E}_{\pi'}[R_{t+1} + \gamma \mathbb{E}[R_{t+2} + \gamma V^\pi(S_{t+2}) \mid S_{t+1}, A_{t+1} = \pi'(S_{t+1})] \mid S_t = s]$$

이 과정을 반복하면 $k \to \infty$에서 $V^{\pi'}(s)$로 수렴한다. $\square$

**정책 반복 알고리즘:** (1) 초기 정책 $\pi_0$에서 시작, (2) 정책 평가(policy evaluation): $V^{\pi_k}$ 계산, (3) 정책 개선(policy improvement): $\pi_{k+1}(s) = \arg\max_a Q^{\pi_k}(s,a)$, (4) 수렴할 때까지 반복. 유한 MDP에서 정책 반복은 유한 단계 내에 수렴한다.

## 예제

**예제 1 (2상태 MDP):** 두 상태 $s_1, s_2$와 두 행동 $a_1, a_2$가 있는 MDP를 고려하자. 전이확률과 보상은 다음과 같다:

$s_1$에서 $a_1$: $s_1$로 전이($p=0.8$, 보상 $+1$) 또는 $s_2$로 전이($p=0.2$, 보상 $0$)
$s_1$에서 $a_2$: $s_2$로 전이($p=1$, 보상 $+2$)
$s_2$에서 $a_1$: $s_1$로 전이($p=0.5$, 보상 $0$) 또는 $s_2$에 체류($p=0.5$, 보상 $+1$)
$s_2$에서 $a_2$: $s_2$에 체류($p=1$, 보상 $+3$)

$\gamma = 0.9$일 때 벨만 방정식을 풀어 최적 정책을 찾아라.

**풀이:** 각 상태-행동 쌍에 대한 벨만 방정식을 세운다.

$Q(s_1, a_1) = 0.8(1 + 0.9V(s_1)) + 0.2(0 + 0.9V(s_2)) = 0.8 + 0.72V(s_1) + 0.18V(s_2)$
$Q(s_1, a_2) = 1(2 + 0.9V(s_2)) = 2 + 0.9V(s_2)$
$Q(s_2, a_1) = 0.5(0 + 0.9V(s_1)) + 0.5(1 + 0.9V(s_2)) = 0.45V(s_1) + 0.5 + 0.45V(s_2)$
$Q(s_2, a_2) = 1(3 + 0.9V(s_2)) = 3 + 0.9V(s_2)$

최적 가치: $V(s_1) = \max(Q(s_1,a_1), Q(s_1,a_2))$, $V(s_2) = \max(Q(s_2,a_1), Q(s_2,a_2))$.

연립방정식을 풀기 위해 $s_1$에서 $a_2$, $s_2$에서 $a_2$가 최적이라고 가정한다:
$$V(s_1) = 2 + 0.9V(s_2)$$
$$V(s_2) = 3 + 0.9V(s_2) \quad \Rightarrow \quad 0.1V(s_2) = 3 \quad \Rightarrow \quad V(s_2) = 30$$
$$V(s_1) = 2 + 0.9 \times 30 = 29$$

검증: $Q(s_1, a_1) = 0.8 + 0.72 \times 29 + 0.18 \times 30 = 0.8 + 20.88 + 5.4 = 27.08 < 29$,
$Q(s_2, a_1) = 0.45 \times 29 + 0.5 + 0.45 \times 30 = 13.05 + 0.5 + 13.5 = 27.05 < 30$.

따라서 최적 정책은 $\pi^*(s_1) = a_2$, $\pi^*(s_2) = a_2$이며, 최적 가치는 $V^*(s_1) = 29$, $V^*(s_2) = 30$이다.

**예제 2 (그리드월드):** $4 \times 4$ 그리드에서 에이전트는 상하좌우로 움직일 수 있다. 각 행동은 의도한 방향으로 $p = 0.8$ 확률로 성공하고, 나머지 $p = 0.2$는 직각 방향(좌우가 섞임)으로 간다. 벽에 부딪히면 제자리에 머문다. 목표 상태 $(4,4)$에 도달하면 보상 $+10$, 구멍 상태 $(2,2)$에 빠지면 보상 $-10$, 나머지는 $-0.1$.

- $\gamma = 0.9$일 때, 가치 반복으로 각 상태의 최적 가치를 수치적으로 구할 수 있다.
- 초기 $V_0(s) = 0$에서 시작하여 $V_{k+1}(s) = \max_a \sum_{s'} P(s'|s,a)[R(s,a,s') + 0.9V_k(s')]$를 반복한다.
- 50회 반복 후 $V^*$가 수렴하며, 각 상태에서 최대 $Q$를 주는 행동이 최적 정책이다.

**예제 3 (가치 반복 수치 예시):** 단일 상태, 두 행동의 MDP. $s_0$에서 $a_1$: $s_0$로 $p=1$, 보상 $+5$. $a_2$: $s_0$로 $p=1$, 보상 $+10$. $\gamma = 0.5$.

$V_{k+1}(s_0) = \max\{5 + 0.5V_k(s_0), 10 + 0.5V_k(s_0)\}$.

$V_0(s_0) = 0$에서 시작:
$V_1 = \max(5, 10) = 10$
$V_2 = \max(5 + 5, 10 + 5) = \max(10, 15) = 15$
$V_3 = \max(5 + 7.5, 10 + 7.5) = \max(12.5, 17.5) = 17.5$
$V_4 = \max(5 + 8.75, 10 + 8.75) = \max(13.75, 18.75) = 18.75$

$V_k$는 진동 없이 단조 증가하며 $V^* = \lim_{k\to\infty} V_k$로 수렴한다. 실제로 $V^* = 10 + 0.5V^*$ → $0.5V^* = 10$ → $V^* = 20$이다.

**예제 4 (정책 반복):** 예제 1의 MDP에서 정책 반복을 수행하라.

**초기 정책:** $\pi_0(s_1) = a_1$, $\pi_0(s_2) = a_1$.

**정책 평가:** $\pi_0$ 하에서 벨만 방정식
$$V^{\pi}(s_1) = 0.8(1 + 0.9V^{\pi}(s_1)) + 0.2(0 + 0.9V^{\pi}(s_2)) = 0.8 + 0.72V^{\pi}(s_1) + 0.18V^{\pi}(s_2)$$
$$V^{\pi}(s_2) = 0.5(0 + 0.9V^{\pi}(s_1)) + 0.5(1 + 0.9V^{\pi}(s_2)) = 0.45V^{\pi}(s_1) + 0.5 + 0.45V^{\pi}(s_2)$$

첫 식: $0.28V^{\pi}(s_1) - 0.18V^{\pi}(s_2) = 0.8$
둘째 식: $-0.45V^{\pi}(s_1) + 0.55V^{\pi}(s_2) = 0.5$

연립방정식 풀이 → $V^{\pi}(s_1) \approx 10.87$, $V^{\pi}(s_2) \approx 10.70$.

**정책 개선:** $Q^{\pi}(s_1,a_1) = V^{\pi}(s_1) \approx 10.87$
$Q^{\pi}(s_1,a_2) = 2 + 0.9 \times 10.70 = 11.63 > 10.87$ → $\pi_1(s_1) = a_2$
$Q^{\pi}(s_2,a_1) = 0.45 \times 10.87 + 0.5 + 0.45 \times 10.70 = 4.89 + 0.5 + 4.82 = 10.21$
$Q^{\pi}(s_2,a_2) = 3 + 0.9 \times 10.70 = 12.63 > 10.21$ → $\pi_1(s_2) = a_2$

1회 개선으로 이미 $\pi^*$에 도달했다.

## 연결

- **[확률 행렬·마르코프 체인](markov-chains.html)** : MDP는 마르코프 체인에 행동(agent의 선택)과 보상을 추가한 확장이다. 정책 $\pi$가 고정되면 MDP는 마르코프 체인이 된다(전이확률 $P^\pi(s'|s) = \sum_a \pi(a|s) P(s'|s,a)$).
- **[중요도 샘플링](importance-sampling.html)** : 강화학습에서 off-policy 학습은 행동 정책(behavior policy)과 목표 정책(target policy)이 다를 때 중요도 샘플링으로 가치를 추정한다.
- **[몬테카를로](monte-carlo.html)** : 모델 없이 MDP를 푸는 몬테카를로 방법(MC prediction, TD learning)은 표본 궤적(sample trajectory)을 사용하여 가치함수를 추정한다.
- **[동적 계획법](dynamical-systems.html)** : 가치 반복과 정책 반복은 동적 계획법(dynamic programming)의 예다. 벨만 방정식은 최적성 원리(principle of optimality)의 구체적 표현이다.
