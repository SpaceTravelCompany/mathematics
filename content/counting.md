---
title: 경우의 수·순열·조합
slug: counting
---

## 직관적 설명

**경우의 수(counting)**는 "몇 가지 경우가 있는가"라는 질문에서 출발한다. 확률(probability)은 "모든 경우가 같은 정도로 일어난다"는 가정 위에 세워지므로, 먼저 가능한 결과의 전체 개수를 세는 법을 알아야 한다. 이때 단순히 손가락으로 세는 것을 넘어, **순서를 고려하는가(순열, permutation)**와 **순서를 무시하는가(조합, combination)**라는 두 축이 모든 계산을 관통한다.

가령 3개의 문자 A, B, C에서 2개를 뽑는 상황을 생각해보자. 순서를 고려하면 (A,B), (A,C), (B,A), (B,C), (C,A), (C,B)의 6가지가 나오고, 순서를 무시하면 {A,B}, {A,C}, {B,C}의 3가지가 나온다. 이 차이를 일반화한 것이 순열 $P(n,r)$과 조합 $\binom{n}{r}$이다.

이 개념들은 확률론의 기초일 뿐 아니라 이항정리(binomial theorem), 파스칼의 삼각형(Pascal's triangle), 포함-배제 원리(inclusion-exclusion principle) 등 수학 전반의 중요한 결과로 이어진다.

## 정의

**곱의 법칙(multiplication principle):** 어떤 사건이 $m$가지 방법으로 일어나고, 각 방법에 대해 다른 사건이 $n$가지 방법으로 일어날 때 두 사건이 **연속해서** 일어나는 경우의 수는 $m \times n$이다.

**합의 법칙(addition principle):** 두 사건이 **동시에** 일어나지 않을 때, 사건 A가 $m$가지, 사건 B가 $n$가지 방법으로 일어나면 A 또는 B가 일어나는 경우의 수는 $m + n$이다.

**순열(permutation):** $n$개의 서로 다른 원소에서 $r$개를 **순서를 고려하여** 선택하는 방법의 수.

$$P(n,r) = \frac{n!}{(n-r)!}$$

여기서 $n! = n \times (n-1) \times \cdots \times 1$이며, $0! = 1$로 정의한다.

**조합(combination):** $n$개의 서로 다른 원소에서 $r$개를 **순서 없이** 선택하는 방법의 수.

$$\binom{n}{r} = \frac{n!}{r!(n-r)!}$$

**중복순열(permutation with repetition):** $n$개의 서로 다른 원소에서 **중복을 허용하여** $r$개를 순서대로 나열하는 방법의 수.

$$n^{\overline{r}} = n^r$$

**중복조합(combination with repetition):** $n$개의 서로 다른 원소에서 **중복을 허용하여** $r$개를 선택하는 방법의 수. "별과 막대(stars and bars)" 문제와 동일하다.

$$\binom{n+r-1}{r}$$

**원순열(circular permutation):** $n$개의 서로 다른 원소를 원형으로 배열하는 방법의 수.

$$(n-1)!$$

원순열에서 회전하여 같은 배열은 동일한 것으로 본다. 예를 들어 4명이 원탁에 앉는 방법은 $(4-1)! = 6$가지다.

**이항계수(binomial coefficient)** $\binom{n}{k}$(또는 $_nC_k$, $C(n,k)$)는 위에서 정의한 조합과 같으며, 파스칼의 삼각형(Pascal's triangle)으로 시각화할 수 있다.

파스칼의 삼각형:
```
        1
       1 1
      1 2 1
     1 3 3 1
    1 4 6 4 1
   1 5 10 10 5 1
```

각 항은 바로 위 두 항의 합이며, $n$번째 행의 항들은 $(a+b)^n$의 전개 계수와 일치한다.

## 주요 정리와 증명

### 정리 1: 이항정리 (Binomial Theorem)

음이 아닌 정수 $n$에 대해 다음이 성립한다.

$$(a+b)^n = \sum_{k=0}^{n} \binom{n}{k} a^{n-k}b^k$$

**증명 (조합론적 방법):** $(a+b)^n = (a+b)(a+b)\cdots(a+b)$를 전개하면 각 항은 $n$개의 괄호에서 $a$ 또는 $b$를 하나씩 골라 곱한 결과다. $a$가 $n-k$번, $b$가 $k$번 선택된 항 $a^{n-k}b^k$는 $n$개의 괄호 중 $b$를 선택할 $k$개의 괄호를 고르는 문제와 같다. 따라서 $a^{n-k}b^k$의 계수는 $\binom{n}{k}$다. $\square$

**증명 (수학적 귀납법):** $n=0$일 때 $(a+b)^0 = 1 = \binom{0}{0}a^0b^0$이므로 성립.

$n$일 때 성립한다 가정하고 $n+1$일 때를 보이자.

$$
\begin{aligned}
(a+b)^{n+1} &= (a+b)(a+b)^n = (a+b)\sum_{k=0}^n \binom{n}{k} a^{n-k}b^k \\
&= \sum_{k=0}^n \binom{n}{k} a^{n+1-k}b^k + \sum_{k=0}^n \binom{n}{k} a^{n-k}b^{k+1}
\end{aligned}
$$

첫 번째 합에서 $a^{n+1-k}b^k$의 계수는 $\binom{n}{k}$이고, 두 번째 합에서 $a^{n-k}b^{k+1} = a^{n+1-(k+1)}b^{k+1}$의 계수는 $\binom{n}{k}$다.

$a^{n+1-k}b^k$ 항의 총 계수: 첫 번째 합에서 $\binom{n}{k}$, 두 번째 합에서 $k-1$번째 항 $\binom{n}{k-1}$이므로 파스칼 항등식에 의해

$$\binom{n}{k} + \binom{n}{k-1} = \binom{n+1}{k}$$

따라서 $n+1$일 때도 성립한다. $\square$

### 정리 2: 파스칼 항등식 (Pascal's Identity)

음이 아닌 정수 $n \geq k \geq 1$에 대해

$$\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$$

**증명 (조합론적):** $\binom{n}{k}$는 $n$개의 원소에서 $k$개를 선택하는 방법의 수다. 특정 원소 하나를 고정하고 생각하자.

- 이 원소를 **포함**하는 경우: 나머지 $n-1$개에서 $k-1$개를 선택해야 하므로 $\binom{n-1}{k-1}$가지.
- 이 원소를 **포함하지 않는** 경우: 나머지 $n-1$개에서 $k$개를 선택해야 하므로 $\binom{n-1}{k}$가지.

두 경우는 서로 배타적이므로 합의 법칙에 의해 $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$이다. $\square$

**증명 (대수적):** 조합의 정의를 직접 대입한다.

$$
\begin{aligned}
\binom{n-1}{k-1} + \binom{n-1}{k}
&= \frac{(n-1)!}{(k-1)!(n-k)!} + \frac{(n-1)!}{k!(n-k-1)!} \\
&= \frac{(n-1)!}{(k-1)!(n-k-1)!} \left( \frac{1}{n-k} + \frac{1}{k} \right) \\
&= \frac{(n-1)!}{(k-1)!(n-k-1)!} \cdot \frac{k + (n-k)}{k(n-k)} \\
&= \frac{(n-1)!}{(k-1)!(n-k-1)!} \cdot \frac{n}{k(n-k)} \\
&= \frac{n!}{k!(n-k)!} = \binom{n}{k}
\end{aligned}
$$

$\square$

### 정리 3: 포함-배제 원리 (Inclusion-Exclusion Principle)

유한집합 $A_1, A_2, \ldots, A_n$에 대해

$$\left| \bigcup_{i=1}^n A_i \right| = \sum_{i=1}^n |A_i| - \sum_{1 \leq i < j \leq n} |A_i \cap A_j| + \sum_{1 \leq i < j < k \leq n} |A_i \cap A_j \cap A_k| - \cdots + (-1)^{n-1} |A_1 \cap \cdots \cap A_n|$$

**증명 (지표함수, indicator function):** 집합 $S$의 지표함수 $\mathbf{1}_S(x)$를 $x \in S$일 때 1, 아니면 0으로 정의하자. 합집합의 지표함수는

$$\mathbf{1}_{\bigcup A_i}(x) = 1 - \prod_{i=1}^n (1 - \mathbf{1}_{A_i}(x)) = 1 - \prod_{i=1}^n (1 - \mathbf{1}_{A_i})$$

우변을 전개하면

$$1 - \left(1 - \sum \mathbf{1}_{A_i} + \sum_{i<j} \mathbf{1}_{A_i}\mathbf{1}_{A_j} - \cdots + (-1)^n \mathbf{1}_{A_1}\cdots\mathbf{1}_{A_n}\right)$$

$$= \sum \mathbf{1}_{A_i} - \sum_{i<j} \mathbf{1}_{A_i \cap A_j} + \sum_{i<j<k} \mathbf{1}_{A_i \cap A_j \cap A_k} - \cdots + (-1)^{n-1} \mathbf{1}_{A_1 \cap \cdots \cap A_n}$$

양변의 합 $\sum_{x \in U}$를 취하면 각 지표함수의 합이 카디널리티가 되므로 포함-배제 원리가 증명된다. $\square$

### 정리 4: 이항계수의 합

$$\sum_{k=0}^n \binom{n}{k} = 2^n$$

**증명 1 (멱집합):** $n$개 원소 집합의 부분집합의 개수는 각 원소를 포함하거나 포함하지 않는 2가지 선택이 $n$번 반복되므로 $2^n$이다. 한편 크기가 $k$인 부분집합의 수는 $\binom{n}{k}$이므로 그 합은 $2^n$이다.

**증명 2 (이항정리):** 이항정리 $(a+b)^n = \sum \binom{n}{k}a^{n-k}b^k$에 $a = b = 1$을 대입하면

$$(1+1)^n = 2^n = \sum_{k=0}^n \binom{n}{k}$$

$\square$

### 정리 5: 다항계수 (Multinomial Coefficient)

$n$개의 서로 다른 원소를 $k$개의 그룹으로 나누는 방법의 수. 각 그룹의 크기가 $n_1, n_2, \ldots, n_k$ ($\sum n_i = n$)일 때

$$\binom{n}{n_1, n_2, \ldots, n_k} = \frac{n!}{n_1! n_2! \cdots n_k!}$$

**조합론적 해석:** $n$개의 위치 중 $n_1$개는 첫 번째 종류, $n_2$개는 두 번째 종류, ...로 채우는 방법의 수와 같다. 이항계수 $\binom{n}{k}$는 $k=2$인 특수한 경우다.

**다항정리(multinomial theorem):**

$$(x_1 + x_2 + \cdots + x_k)^n = \sum_{n_1 + \cdots + n_k = n} \binom{n}{n_1, \ldots, n_k} x_1^{n_1} \cdots x_k^{n_k}$$

### 정리 6: 야코브슈탈-칸델의 항등식 (간단한 버전)

$$\binom{n}{k} = \frac{n}{k}\binom{n-1}{k-1}$$

**증명:** 정의에서 직접 유도된다.

$$\binom{n}{k} = \frac{n!}{k!(n-k)!} = \frac{n}{k} \cdot \frac{(n-1)!}{(k-1)!(n-k)!} = \frac{n}{k}\binom{n-1}{k-1}$$

$\square$

## 예제

**예제 1 (로또):** 한국 로또 6/45는 1부터 45까지의 숫자 중 6개를 순서 없이 선택하는 방식이다. 총 가능한 번호 조합의 수는

$$\binom{45}{6} = \frac{45!}{6!39!} = \frac{45 \times 44 \times 43 \times 42 \times 41 \times 40}{6 \times 5 \times 4 \times 3 \times 2 \times 1} = 8,\!145,\!060$$

1등에 당첨될 확률은 약 814만 분의 1이다.

**예제 2 (중복조합 — 별과 막대):** 3가지 종류의 과일(사과, 배, 귤)에서 5개를 선택하는 방법은 몇 가지인가? (같은 종류는 구별하지 않고, 각 종류는 충분히 있다고 가정.)

이는 $\binom{3+5-1}{5} = \binom{7}{5} = 21$가지다. 일반적으로 $n$가지에서 $r$개를 중복 선택하는 방법은 $\binom{n+r-1}{r}$이다.

**별과 막대 해석:** $r$개의 별(*)을 $n-1$개의 막대(|)로 $n$개의 구역으로 나눈다. 예를 들어 **|*|****는 "사과 2개, 배 1개, 귤 2개"를 의미한다. $r$개의 별과 $n-1$개의 막대를 일렬로 배열하는 총 방법의 수가 $\binom{n+r-1}{r}$이다.

**예제 3 (포커 핸드 분류):** 52장의 표준 카드에서 5장을 뽑을 때 다음 각 핸드의 경우의 수를 구하라.

(a) **원페어(one pair):** 같은 숫자가 2장, 나머지 3장은 모두 다른 숫자.
(b) **플러시(flush):** 5장 모두 같은 무늬.

**풀이:**
(a) 먼저 페어가 될 숫자 1개 고르기: $\binom{13}{1}$가지. 그 숫자에서 2장 고르기: $\binom{4}{2}$가지. 나머지 3개 숫자를 다른 숫자 12개에서 고르기: $\binom{12}{3}$가지. 각 숫자에서 1장씩 고르기: $4^3$가지.

$$\binom{13}{1}\binom{4}{2}\binom{12}{3}4^3 = 13 \times 6 \times 220 \times 64 = 1,\!098,\!240$$

(b) 무늬 하나 고르기: 4가지. 해당 무늬에서 5장 고르기: $\binom{13}{5}$.

$$4 \times \binom{13}{5} = 4 \times 1287 = 5,\!148$$

**예제 4 (포함-배제 — 3집합):** 100명의 학생 중 수학을 듣는 학생이 60명, 물리를 듣는 학생이 50명, 화학을 듣는 학생이 40명이다. 수학과 물리를 모두 듣는 학생은 30명, 수학과 화학은 20명, 물리와 화학은 15명, 세 과목을 모두 듣는 학생은 10명이다. 적어도 한 과목을 듣는 학생은 몇 명인가?

**풀이:** 포함-배제 원리에 의해

$$
\begin{aligned}
|M \cup P \cup C| &= |M| + |P| + |C| - |M \cap P| - |M \cap C| - |P \cap C| + |M \cap P \cap C| \\
&= 60 + 50 + 40 - 30 - 20 - 15 + 10 = 95
\end{aligned}
$$

따라서 95명이 적어도 한 과목을 듣는다.

## 연결

- **[집합과 논리](topics/sets-and-logic.html)** : 집합의 카디널리티와 연산(합집합, 교집합)은 포함-배제 원리의 기초다. 멱집합(power set)의 크기가 $2^n$임은 이항계수 합의 조합론적 해석이다.
- **[확률·조건부확률·베이즈 정리](topics/conditional-bayes.html)** : 경우의 수는 확률 계산의 분모 역할을 한다. $P(A) = |A|/|\Omega|$로, 모든 확률은 경우의 수에서 출발한다.
