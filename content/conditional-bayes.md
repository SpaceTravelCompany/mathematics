---
title: 확률·조건부확률·베이즈 정리
slug: conditional-bayes
---

## 직관적 설명

**확률(probability)**은 불확실성을 숫자로 측정하는 도구다. "내일 비가 올 확률 70%"라는 말은 10번 중 7번꼴로 비가 온다는 경험적 해석(빈도주의, frequentist)일 수도 있고, "비가 온다는 믿음의 강도가 0.7"이라는 주관적 해석(베이지안, Bayesian)일 수도 있다. 어느 쪽이든 확률은 0에서 1 사이의 숫자로 표현된다.

**조건부확률(conditional probability)** $P(A|B)$는 "사건 $B$가 발생했다는 정보를 알게 되었을 때, 사건 $A$의 확률"이다. 이는 우리가 새로운 정보를 얻었을 때 믿음을 어떻게 갱신해야 하는지를 수량화한다.

**베이즈 정리(Bayes' theorem)**는 이 조건부확률을 뒤집는 공식이다. $P(B|A)$(증거를 본 후 가설의 확률)를 $P(A|B)$(가설 하에서 증거가 관측될 확률)로 표현한다. 이는 의료 진단, 법정 증거 해석, 기계의 고장 진단 등 불확실한 상황에서 추론하는 모든 영역의 핵심이다.

## 정의

**확률 공간(probability space)** $(\Omega, \mathcal{F}, P)$는 다음 세 요소로 구성된다.
- **표본공간(sample space)** $\Omega$: 가능한 모든 결과의 집합.
- **사건(event)**들의 $\sigma$-대수 $\mathcal{F}$: $\Omega$의 부분집합들로, 확률을 할당할 대상.
- **확률측도(probability measure)** $P: \mathcal{F} \to [0, 1]$: 다음 세 공리를 만족하는 함수.

**콜모고로프 공리(Kolmogorov axioms):**
1. **비음성(non-negativity):** 모든 사건 $A \in \mathcal{F}$에 대해 $P(A) \geq 0$.
2. **정규화(normalization):** $P(\Omega) = 1$.
3. **가산 가법성(countable additivity):** 서로 배타적인(countably many) 사건 $A_1, A_2, \ldots$에 대해 $P(\bigcup_{i=1}^\infty A_i) = \sum_{i=1}^\infty P(A_i)$.

**조건부확률(conditional probability):** $P(B) > 0$일 때, $B$가 주어졌을 때 $A$의 조건부확률은

$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

**쌍대독립(pairwise independence) vs 상호독립(mutual independence):** 사건 $A_1, \ldots, A_n$이 **상호독립(mutually independent)**이라는 것은 임의의 부분집합 $I \subseteq \{1,\ldots,n\}$에 대해

$$P\left(\bigcap_{i \in I} A_i\right) = \prod_{i \in I} P(A_i)$$

이다. 쌍대독립은 $|I| = 2$인 경우만 만족하는 것으로, 상호독립보다 약한 조건이다.

**독립(independence):** 두 사건 $A$와 $B$가 **독립(independent)**이라는 것은

$$P(A \cap B) = P(A)P(B)$$

이다. 이는 $P(A|B) = P(A)$와 동치다 ($P(B) > 0$일 때).

**전확률 법칙(law of total probability):** 표본공간 $\Omega$의 분할 $\{B_1, B_2, \ldots, B_n\}$(서로 배타적이고 합집합이 $\Omega$인 사건들)에 대해

$$P(A) = \sum_{i=1}^n P(A|B_i) P(B_i)$$

**베이즈 정리(Bayes' theorem):** 위와 같은 분할 $\{B_i\}$에 대해

$$P(B_j|A) = \frac{P(A|B_j) P(B_j)}{\sum_{i=1}^n P(A|B_i) P(B_i)}$$

## 주요 정리와 증명

### 정리 1: 베이즈 정리의 유도

**증명:** 조건부확률의 정의에 의해

$$P(B_j|A) = \frac{P(A \cap B_j)}{P(A)}$$

분자는 다시 조건부확률로 $P(A \cap B_j) = P(A|B_j)P(B_j)$이다. 분모는 전확률 법칙에 의해 $P(A) = \sum_i P(A|B_i)P(B_i)$이다. 따라서

$$P(B_j|A) = \frac{P(A|B_j)P(B_j)}{\sum_i P(A|B_i)P(B_i)}$$

$\square$

### 정리 2: 독립과 조건부확률의 불변성

$A$와 $B$가 독립이고 $P(B) > 0$이면 $P(A|B) = P(A)$이다.

**증명:** 독립의 정의 $P(A \cap B) = P(A)P(B)$를 조건부확률 정의에 대입하면

$$P(A|B) = \frac{P(A \cap B)}{P(B)} = \frac{P(A)P(B)}{P(B)} = P(A)$$

$\square$

이 역시 성립한다: $P(A|B) = P(A)$이고 $P(B) > 0$이면 $P(A \cap B) = P(A|B)P(B) = P(A)P(B)$이므로 $A$와 $B$는 독립이다. 따라서 $P(A|B) = P(A)$는 독립의 필요충분조건이다.

### 정리 3: 연쇄법칙 (Chain Rule, 곱셈법칙)

유한개의 사건 $A_1, A_2, \ldots, A_n$에 대해

$$P(A_1 \cap A_2 \cap \cdots \cap A_n) = P(A_1) \cdot P(A_2|A_1) \cdot P(A_3|A_1 \cap A_2) \cdots P(A_n|A_1 \cap \cdots \cap A_{n-1})$$

**증명 (수학적 귀납법):** $n=2$일 때는 조건부확률의 정의 $P(A_2|A_1) = P(A_1 \cap A_2)/P(A_1)$에서 자명하다.

$n$일 때 성립한다 가정하자. $n+1$일 때:

$$
\begin{aligned}
P(A_1 \cap \cdots \cap A_{n+1}) &= P((A_1 \cap \cdots \cap A_n) \cap A_{n+1}) \\
&= P(A_1 \cap \cdots \cap A_n) \cdot P(A_{n+1} | A_1 \cap \cdots \cap A_n)
\end{aligned}
$$

귀납 가정을 $P(A_1 \cap \cdots \cap A_n)$에 적용하면 원하는 결과를 얻는다. $\square$

### 정리 4: 확률의 기본 성질

콜모고로프 공리로부터 다음이 유도된다.

(a) $P(\emptyset) = 0$.
(b) $P(A^c) = 1 - P(A)$.
(c) $A \subseteq B$이면 $P(A) \leq P(B)$.
(d) $P(A \cup B) = P(A) + P(B) - P(A \cap B)$.

**증명:**
(a) $\Omega = \Omega \cup \emptyset \cup \emptyset \cup \cdots$에서 가산 가법성과 정규화를 적용하면 $1 = P(\Omega) = P(\Omega) + P(\emptyset) + P(\emptyset) + \cdots$이므로 $P(\emptyset) = 0$.

(b) $\Omega = A \cup A^c$이고 $A \cap A^c = \emptyset$이므로 $1 = P(A) + P(A^c)$, 따라서 $P(A^c) = 1 - P(A)$.

(c) $B = A \cup (B \setminus A)$이고 $A \cap (B \setminus A) = \emptyset$이므로 $P(B) = P(A) + P(B \setminus A) \geq P(A)$.

(d) $A \cup B = A \cup (B \setminus A)$이고 $A \cap (B \setminus A) = \emptyset$이므로 $P(A \cup B) = P(A) + P(B \setminus A)$. 한편 $B = (A \cap B) \cup (B \setminus A)$이므로 $P(B) = P(A \cap B) + P(B \setminus A)$. 두 식에서 $P(B \setminus A) = P(B) - P(A \cap B)$를 대입하면 $P(A \cup B) = P(A) + P(B) - P(A \cap B)$. $\square$

### 정리 5: 체비셰프 부등식의 확률 버전

확률측도 $P$에 대해 $X$가 확률변수이고 $g: \mathbb{R} \to [0, \infty)$일 때

$$P(g(X) \geq \epsilon) \leq \frac{\mathbb{E}[g(X)]}{\epsilon}$$

**증명 (마르코프 부등식, Markov's inequality):** 사건 $A = \{X : g(X) \geq \epsilon\}$의 지표함수 $\mathbf{1}_A$를 생각하자. $g(X) \geq \epsilon$이므로 $\mathbf{1}_A \leq g(X)/\epsilon$이다. 양변의 기댓값을 취하면

$$P(g(X) \geq \epsilon) = \mathbb{E}[\mathbf{1}_A] \leq \mathbb{E}\left[\frac{g(X)}{\epsilon}\right] = \frac{\mathbb{E}[g(X)]}{\epsilon}$$

$\square$

이 부등식은 대수의 법칙 증명의 핵심 도구로 사용된다.

## 예제

**예제 1 (의료 검사):** 어떤 희귀병의 유병률(prevalence)이 1%이다. 검사의 민감도(sensitivity, $P(+|D)$)는 99%, 특이도(specificity, $P(-|\bar{D})$)는 95%이다. 검사 결과 양성이 나왔을 때 실제로 환자일 확률은?

**풀이:** 베이즈 정리를 적용한다.

$$
\begin{aligned}
P(D|+) &= \frac{P(+|D)P(D)}{P(+|D)P(D) + P(+|\bar{D})P(\bar{D})} \\
&= \frac{0.99 \times 0.01}{0.99 \times 0.01 + 0.05 \times 0.99} \\
&= \frac{0.0099}{0.0099 + 0.0495} = \frac{0.0099}{0.0594} \approx 0.1667
\end{aligned}
$$

양성 판정을 받았더라도 실제 환자일 확률은 약 16.7%에 불과하다. 이는 유병률이 낮아 위양성(false positive)이 전체 양성 결과에서 큰 비중을 차지하기 때문이다.

**예제 2 (몬티 홀 문제, Monty Hall problem):** 세 개의 문 뒤에 하나는 자동차, 둘은 염소가 있다. 참가자가 문을 하나 고르면, 사회자가 나머지 두 문 중 염소가 있는 문을 열어 보여준다. 그런 다음 참가자는 선택을 바꿀 기회를 얻는다. 선택을 바꾸는 것이 유리한가?

**풀이:** 처음 고른 문에 자동차가 있을 확률은 $1/3$이다. 사회자는 항상 염소가 있는 문을 열어주므로, 참가자가 처음에 염소를 골랐다면($2/3$ 확률) 남은 문에는 반드시 자동차가 있다. 따라서 선택을 바꾸면 당첨 확률이 $2/3$로 두 배가 된다.

조건부확률로 엄밀히: 사건 $C_i$를 "$i$번 문에 자동차가 있음", 사건 $H$를 "사회자가 3번 문을 열어 염소를 보여줌"이라고 하자. (참가자가 1번을 골랐다고 가정.)

$$P(C_1|H) = \frac{P(H|C_1)P(C_1)}{P(H|C_1)P(C_1) + P(H|C_2)P(C_2) + P(H|C_3)P(C_3)}$$

$P(H|C_1) = 1/2$ (사회자가 2번이나 3번 중 하나를 무작위로 선택), $P(H|C_2) = 1$ (2번에 차가 있으면 3번에는 염소가 있으므로 반드시 3번을 열음), $P(H|C_3) = 0$이므로

$$P(C_1|H) = \frac{1/2 \times 1/3}{1/2 \times 1/3 + 1 \times 1/3 + 0 \times 1/3} = \frac{1/6}{1/2} = \frac{1}{3}$$

따라서 바꾸지 않으면 $1/3$, 바꾸면 $2/3$의 확률로 당첨된다.

**예제 3 (거짓말 탐지기):** 어떤 회사에서 거짓말 탐지기를 도입했다. 탐지기는 거짓말을 할 때 90%의 확률로 양성(거짓말이라고 판단)을, 진실을 말할 때 10%의 확률로 양성을 보인다. 전체 직원 중 5%가 거짓말을 했다고 할 때, 탐지기가 양성이라고 판단했을 때 실제로 거짓말을 한 직원일 확률은?

**풀이:** 사건 $L$을 "거짓말을 함", $+$를 "탐지기 양성"이라 하자.

$$
P(L|+) = \frac{0.9 \times 0.05}{0.9 \times 0.05 + 0.1 \times 0.95} = \frac{0.045}{0.045 + 0.095} = \frac{0.045}{0.14} \approx 0.321
$$

약 32.1%로, 직관보다 낮다.

**예제 4 (신뢰할 수 있는 두 증인):** 어떤 사건에 두 명의 증인이 있다. 증인 A는 90%의 확률로 정확히 말하고, 증인 B는 80%의 확률로 정확히 말한다. 두 증인이 독립적으로 같은 진술(사건이 일어났음)을 했다면, 실제로 사건이 일어났을 확률은? (사전 확률 $P(E) = 0.01$이라 가정.)

**풀이:** $E$를 "사건 발생", $S_A$, $S_B$를 각 증인의 "사건 발생 진술"이라 하자. 증인이 정확할 때 진술과 일치하므로 $P(S_A|E) = P(S_A^c|E^c) = 0.9$, $P(S_B|E) = P(S_B^c|E^c) = 0.8$이다. 두 증인은 조건부 독립이라 가정한다.

$$
\begin{aligned}
P(E|S_A,S_B) &= \frac{P(S_A,S_B|E)P(E)}{P(S_A,S_B|E)P(E) + P(S_A,S_B|E^c)P(E^c)} \\
&= \frac{0.9 \times 0.8 \times 0.01}{0.9 \times 0.8 \times 0.01 + 0.1 \times 0.2 \times 0.99} \\
&= \frac{0.0072}{0.0072 + 0.0198} \approx 0.267
\end{aligned}
$$

두 증인이 일치해도 실제 확률은 26.7%로, 직관보다 훨씬 낮다.

**예제 5 (간단한 사례 — $P(A \cup B)$ 계산):** $P(A) = 0.4$, $P(B) = 0.3$, $P(A \cap B) = 0.1$일 때 $P(A \cup B)$를 구하라.

**풀이:** $P(A \cup B) = P(A) + P(B) - P(A \cap B) = 0.4 + 0.3 - 0.1 = 0.6$

**예제 6 (독립 판정):** 다음 조건이 주어졌을 때 $A$와 $B$가 독립인지 판정하라.
- $P(A) = 0.5$, $P(B) = 0.4$, $P(A \cap B) = 0.2$

**풀이:** $P(A)P(B) = 0.5 \times 0.4 = 0.2 = P(A \cap B)$이므로 $A$와 $B$는 독립이다.

**예제 7 (연쇄법칙 활용):** 항아리에서 공을 비복원 추출하는 상황을 생각하자. 항아리에 빨간 공 5개, 파란 공 3개가 있다. 세 개의 공을 연속으로 뽑을 때, 순서대로 (빨간 공, 파란 공, 빨간 공)이 나올 확률은?

**풀이:** $R_i$를 "$i$번째에 빨간 공", $B_i$를 "$i$번째에 파란 공"이라 하자. 연쇄법칙에 의해

$$
\begin{aligned}
P(R_1 \cap B_2 \cap R_3) &= P(R_1) \cdot P(B_2|R_1) \cdot P(R_3|R_1 \cap B_2) \\
&= \frac{5}{8} \cdot \frac{3}{7} \cdot \frac{4}{6} = \frac{60}{336} = \frac{5}{28} \approx 0.179
\end{aligned}
$$

## 연결

- **[경우의 수](topics/counting.html)** : 확률의 분모는 표본공간의 크기다. $P(A) = |A|/|\Omega|$로, 모든 확률 계산은 경우의 수에서 출발한다.
- **[베이지안 추론](topics/bayesian-inference.html)** : 베이즈 정리는 사전확률(prior)을 사후확률(posterior)로 갱신하는 프레임워크로 확장된다. $P(\theta|D) \propto P(D|\theta)P(\theta)$.
- **[확률변수](topics/random-variables.html)** : 사건을 숫자로 매핑하는 확률변수는 조건부확률을 조건부 기댓값으로 일반화한다.
