---
title: 집합과 논리
slug: sets-and-logic
---

## 직관적 설명

수학은 대상을 정의하고 그 대상 사이의 관계를 추론하는 학문이다. 이 과정에서 가장 기본이 되는 두 축이 바로 **집합(set)** 과 **논리(logic)** 다. 집합은 "어떤 조건을 만족하는 대상의 모임"을 형식화한 것이고, 논리는 "참과 거짓을 판단하는 규칙"을 다룬다. 모든 수학적 객체는 궁극적으로 집합으로 정의되고, 모든 수학적 주장은 명제 논리(propositional logic)의 규칙 위에 세워진다. 함수(function)는 집합 사이의 대응이고, 관계(relation)는 집합의 곱집합의 부분집합이며, 수(number)조차 집합으로 구성된다. 집합과 논리는 수학의 언어 그 자체인 셈이다.

## 정의

**집합(set)** 은 중복 없이 구별되는 대상(object)을 하나의 단위로 모은 것이다. 각 대상을 **원소(element)** 라 부르고, $a$가 집합 $A$의 원소임을 $a \in A$로 표기한다.

**공집합(empty set)** $\emptyset$은 원소를 하나도 가지지 않는 집합이다.

**부분집합(subset):** $A$의 모든 원소가 $B$에 속할 때 $A \subseteq B$라 쓴다. $A \subseteq B$이고 $A \neq B$이면 **진부분집합(proper subset)** $A \subsetneq B$이다.

**집합 연산:**
- 합집합(union): $A \cup B = \{x \mid x \in A \lor x \in B\}$
- 교집합(intersection): $A \cap B = \{x \mid x \in A \land x \in B\}$
- 차집합(difference): $A \setminus B = \{x \mid x \in A \land x \notin B\}$
- 여집합(complement, 전체집합 $U$가 주어졌을 때): $A^c = U \setminus A$

**멱집합(power set):** $\mathcal{P}(A) = \{X \mid X \subseteq A\}$, 집합 $A$의 모든 부분집합의 집합.

**카디널리티(cardinality):** 유한집합 $A$의 크기 $|A|$는 원소의 개수.

**명제 논리(propositional logic):** **명제(proposition)** 는 참(true) 또는 거짓(false)이 분명한 문장이다.

**기본 논리 연산자:**
- $\neg P$: **부정(negation, not)** — $P$가 거짓이면 참, $P$가 참이면 거짓
- $P \land Q$: **논리곱(logical AND, conjunction)** — "$P$ **그리고** $Q$" — **둘 다 참일 때만 참**
- $P \lor Q$: **논리합(logical OR, disjunction)** — "$P$ **또는** $Q$" — **둘 중 하나라도 참이면 참** (배타적 또는이 아님, 둘 다 참도 허용)
- $P \oplus Q$ (또는 $P \veebar Q$): **배타적 논리합(exclusive OR, XOR)** — "$P$ **또는** $Q$ **중 하나만**" — **둘 중 정확히 하나만 참일 때 참** (둘 다 참이거나 둘 다 거짓이면 거짓)
- $P \Rightarrow Q$: **함의(implication)** — "$P$이면 $Q$이다" — $P$가 참이고 $Q$가 거짓일 때만 거짓
- $P \iff Q$: **동치(equivalence)** — "$P$와 $Q$가 필요충분조건" — $P$와 $Q$가 같은 진리값일 때 참

> **참고:** $\oplus$ 기호는 벡터공간에서 직합(direct sum) 기호로도 쓰이므로 문맥에서 구별해야 한다. 집합론에서 **대칭 차집합(symmetric difference)** $A \triangle B = (A \setminus B) \cup (B \setminus A)$는 배타적 또는에 대응한다 ($x \in A \triangle B \iff x \in A \oplus x \in B$).

**조건부(conditional) 용어:** $P \Rightarrow Q$에서 $P$는 **충분조건(sufficient condition)**, $Q$는 **필요조건(necessary condition)** 이라 부른다.

## 주요 정리와 증명

### 정리 1: 드 모르간 법칙 (De Morgan's Laws)

전체집합 $U$와 부분집합 $A, B \subseteq U$에 대해 다음이 성립한다.

$$(A \cup B)^c = A^c \cap B^c$$
$$(A \cap B)^c = A^c \cup B^c$$

**증명 (첫 번째 법칙):** 두 집합이 같음을 보이려면 $(A \cup B)^c \subseteq A^c \cap B^c$와 $A^c \cap B^c \subseteq (A \cup B)^c$를 각각 보이면 된다.

($\subseteq$) $x \in (A \cup B)^c$라 하자. 여집합의 정의에 의해 $x \notin A \cup B$이다. 합집합의 정의에 의해 $x \notin A$이고 $x \notin B$이다. 따라서 $x \in A^c$이고 $x \in B^c$이므로 $x \in A^c \cap B^c$이다.

($\supseteq$) $x \in A^c \cap B^c$라 하자. 그러면 $x \in A^c$이고 $x \in B^c$이므로 $x \notin A$이고 $x \notin B$이다. 따라서 $x \notin A \cup B$이며, 여집합의 정의에 의해 $x \in (A \cup B)^c$이다.

두 방향의 포함관계가 성립하므로 두 집합은 같다. 두 번째 법칙도 동일한 원소 논증(element-chasing argument)으로 증명할 수 있다.

### 정리 2: 대우 (Contrapositive)

명제 $P \Rightarrow Q$와 그 **대우(contrapositive)** $\neg Q \Rightarrow \neg P$는 논리적으로 동치이다.

**증명 (진리표):**

| $P$ | $Q$ | $\neg Q$ | $\neg P$ | $P \Rightarrow Q$ | $\neg Q \Rightarrow \neg P$ |
|:---:|:---:|:--------:|:--------:|:-----------------:|:--------------------------:|
| T   | T   | F        | F        | T                 | T                          |
| T   | F   | T        | F        | F                 | F                          |
| F   | T   | F        | T        | T                 | T                          |
| F   | F   | T        | T        | T                 | T                          |

두 열이 완전히 일치하므로 $P \Rightarrow Q \equiv \neg Q \Rightarrow \neg P$이다. 이 동치 관계는 간접 증명의 핵심 도구다. 명제를 직접 증명하기 어려울 때 그 대우를 증명해도 동일한 효과를 얻는다.

**필요조건과 충분조건:** $P \Rightarrow Q$가 참일 때, $Q$는 $P$이기 위한 필요조건(necessary condition)이고 $P$는 $Q$이기 위한 충분조건(sufficient condition)이다. $P \iff Q$일 때 $P$와 $Q$는 서로에 대해 필요충분조건(necessary and sufficient condition)이다.

### 정리 3: 귀류법 — $\sqrt{2}$의 무리성

**귀류법(proof by contradiction)** 은 명제가 거짓이라고 가정하고 모순을 이끌어내어 원래 명제가 참임을 증명하는 방법이다.

**정리:** $\sqrt{2}$는 무리수(irrational number)이다. 즉, $\sqrt{2} = p/q$를 만족하는 정수 $p, q$ (단 $q \neq 0$)는 존재하지 않는다.

**증명:** $\sqrt{2}$가 유리수라고 가정하자. 그러면 서로소(coprime)인 두 정수 $p, q$ ($q \neq 0$)에 대해 $\sqrt{2} = p/q$로 쓸 수 있다. 양변을 제곱하면

$$2 = \frac{p^2}{q^2} \quad\Rightarrow\quad p^2 = 2q^2$$

따라서 $p^2$는 짝수(even)이고, 짝수의 제곱만이 짝수이므로 $p$도 짝수이다. $p = 2k$로 두면

$$(2k)^2 = 2q^2 \quad\Rightarrow\quad 4k^2 = 2q^2 \quad\Rightarrow\quad q^2 = 2k^2$$

따라서 $q^2$도 짝수이므로 $q$도 짝수이다. $p$와 $q$가 모두 짝수라는 것은 두 수가 서로소라는 가정에 모순된다. 따라서 $\sqrt{2}$는 유리수가 될 수 없으며, 무리수이다.

## 예제

**예제 1:** $U = \{1, 2, 3, 4, 5, 6\}$, $A = \{1, 2, 3\}$, $B = \{2, 4, 6\}$일 때 다음을 구하라.

(a) $A \cup B$ \quad (b) $A \cap B$ \quad (c) $A \setminus B$ \quad (d) $A^c$ \quad (e) $\mathcal{P}(A \cap B)$

**풀이:**
(a) $A \cup B = \{1, 2, 3, 4, 6\}$
(b) $A \cap B = \{2\}$
(c) $A \setminus B = \{1, 3\}$
(d) $A^c = U \setminus A = \{4, 5, 6\}$
(e) $A \cap B = \{2\}$이므로 $\mathcal{P}(A \cap B) = \{\emptyset, \{2\}\}$

**예제 2:** 다음 명제의 진리값을 판정하고, 필요조건/충분조건을 구분하라.

"자연수 $n$이 4의 배수이면 $n$은 짝수이다."

**풀이:** $P$: "$n$은 4의 배수", $Q$: "$n$은 짝수"라 하자. $P \Rightarrow Q$는 항상 참이다 (4의 배수는 모두 짝수이므로). 따라서 $P$는 $Q$의 충분조건이고, $Q$는 $P$의 필요조건이다. 역 $Q \Rightarrow P$는 거짓이다 (예: $n=2$는 짝수이지만 4의 배수가 아니다).

**예제 3:** 귀류법을 사용하여 "$\sqrt{3}$은 무리수이다"를 증명하라.

**증명:** $\sqrt{3} = p/q$ ($p, q$는 서로소인 정수, $q \neq 0$)라 가정하면 $p^2 = 3q^2$이다. 따라서 $p^2$는 3의 배수이므로 $p$도 3의 배수이다. $p=3k$로 두면 $9k^2 = 3q^2$, 즉 $q^2 = 3k^2$이므로 $q$도 3의 배수이다. $p$와 $q$가 모두 3의 배수이므로 서로소라는 가정에 모순. 따라서 $\sqrt{3}$은 무리수이다.

## 연결

- **[함수](functions.html)** : 함수는 두 집합 사이의 대응 관계를 형식화한 개념이다. 정의역과 공역은 모두 집합이다.
- **[경우의 수](counting.html)** : 유한집합의 카디널리티를 세는 방법으로, 집합론의 직접적인 응용이다.
- **[내적과 노름](inner-product-norm.html)** : 벡터공간도 집합이며, 내적공간은 집합에 추가 구조가 부여된 것이다.
