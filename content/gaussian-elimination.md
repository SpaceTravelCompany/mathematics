---
title: 가우스 소거와 RREF
slug: gaussian-elimination
---

## 직관적 설명

연립방정식을 풀 때 우리는 자연스럽게 "변수를 소거한다"는 전략을 사용한다. 두 방정식을 더하거나 빼서 미지수를 하나 줄이고, 그 결과를 다시 다른 방정식에 대입하는 과정을 반복한다. **가우스 소거(Gaussian elimination)** 는 이 과정을 체계적인 알고리즘으로 정형화한 것이다. 모든 선형 문제를 푸는 가장 기본적인 방법이며, 컴퓨터는 이 알고리즘으로 연립방정식을 푼다.

가우스 소거의 핵심은 **행렬의 행을 조작하는 세 가지 연산**으로 모든 연립방정식을 풀 수 있다는 사실에 있다. 이 연산들은 방정식의 해를 바꾸지 않으면서 행렬을 **기약행사다리꼴(RREF, Reduced Row Echelon Form)**이라는 표준형으로 변환한다. RREF에 도달하면 해가 존재하는지, 유일한지, 무한히 많은지가 즉시 드러난다.

회로 해석(키르히호프의 법칙), 구조 역학(트러스 구조의 힘 평형), 항공기 설계(공력 계산) 등 거의 모든 공학 분야에서 연립방정식이 등장하며, 그 풀이는 가우스 소거에 기반한다. 100만 개의 미지수를 가진 연립방정식도 이 알고리즘의 효율적인 구현으로 풀 수 있다.

---
## 정의

**초등 행 연산(elementary row operations):** 행렬의 행에 적용할 수 있는 다음 세 가지 연산을 말한다.

1. **행 교환(Row swap, $R_i \leftrightarrow R_j$):** 두 행의 위치를 바꾼다.
2. **행 스케일링(Row scaling, $R_i \leftarrow c R_i$, $c \neq 0$):** 한 행에 0이 아닌 상수를 곱한다.
3. **행 더하기(Row addition, $R_i \leftarrow R_i + c R_j$, $i \neq j$):** 한 행의 배수를 다른 행에 더한다.

**행동치(row equivalence):** 행렬 $A$에 유한 번의 초등 행 연산을 적용하여 행렬 $B$를 얻을 수 있을 때, $A$와 $B$는 **행동치**라 한다. 행동치인 두 행렬은 동일한 해집합을 가진다.

**사다리꼴(echelon form):** 행렬이 다음 조건을 만족하면 **사다리꼴(또는 행사다리꼴)**이라 한다.

- 모든 영행(zero row)은 영행이 아닌 행 아래에 위치한다.
- 각 영행이 아닌 행의 첫 번째 0이 아닌 원소(**pivot**, 선행 계수)는 위 행의 pivot보다 오른쪽에 있다.
- Pivot 아래의 모든 원소는 0이다.

**기약행사다리꼴(RREF, Reduced Row Echelon Form):** 사다리꼴이면서 다음 추가 조건을 만족하면 RREF라 한다.

- 각 pivot은 1이다.
- 각 pivot이 속한 열에서 pivot 위의 모든 원소도 0이다.

**가우스-조르단 소거(Gauss-Jordan elimination):** 행렬을 RREF로 변환하는 알고리즘 전체를 가우스-조르단 소거라 부른다. (일반적으로 "가우스 소거"는 사다리꼴까지만 만드는 전방 소거(forward elimination)를, "가우스-조르단"은 후방 대입(back substitution)을 포함한 RREF까지를 의미하기도 한다.)

---
## 주요 정리와 증명

### 정리 1: RREF의 유일성

모든 행렬은 유일한 RREF를 가진다. 즉, 어떤 초등 행 연산의 순서를 따르든 최종 RREF는 같다.

**증명 (개요):** $m \times n$ 행렬 $A$의 두 개의 RREF $R_1$과 $R_2$가 존재한다고 가정하자. 둘 다 $A$와 행동치이므로 $R_1$과 $R_2$도 행동치이며, 따라서 동일한 해집합을 가진다. RREF의 구조상 pivot의 위치는 해집합에 의해 유일하게 결정된다는 것을 보일 수 있다. 구체적으로:

- $Ax = 0$의 해집합에서 pivot 열의 위치는 유일하게 결정된다 (pivot 열이 아닌 열에 대응하는 변수가 자유변수).
- 각 pivot 행에서 pivot의 값은 1이어야 하고, 같은 열의 다른 원소는 0이어야 한다 (해집합이 같으므로).
- 귀납법으로 각 열의 pivot 위치와 값이 $R_1$과 $R_2$에서 같음을 보일 수 있다.

### 정리 2: 기본 행 연산의 가역성

각 초등 행 연산은 가역적(invertible)이다. 즉, 연산을 되돌리는 초등 행 연산이 존재한다.

**증명:**
1. **행 교환:** $R_i \leftrightarrow R_j$를 다시 적용하면 원래대로 돌아온다.
2. **행 스케일링:** $R_i \leftarrow c R_i$ ($c \neq 0$)는 $R_i \leftarrow (1/c) R_i$로 되돌릴 수 있다.
3. **행 더하기:** $R_i \leftarrow R_i + c R_j$는 $R_i \leftarrow R_i - c R_j$로 되돌릴 수 있다.

### 정리 3: 가우스-조르단 알고리즘

임의의 $m \times n$ 행렬 $A$는 다음 알고리즘으로 RREF로 변환할 수 있다.

**알고리즘:**
1. 가장 왼쪽의 0이 아닌 열을 찾는다. 이 열의 가장 위에 있는 0이 아닌 원소를 pivot으로 삼는다.
2. 필요하면 행 교환을 해서 pivot이 첫 번째 행에 오도록 한다.
3. pivot을 1로 만든다 (행 스케일링).
4. pivot 아래의 모든 원소를 0으로 만든다 (행 더하기).
5. pivot이 있는 행을 제외한 나머지 행렬에 대해 1~4를 반복한다.
6. 모든 pivot 열에 대해, pivot 위의 원소들도 0으로 만든다 (후방 소거).

### 정리 4: 해의 존재와 유일성 판정

$m$개의 방정식, $n$개의 미지수를 가진 연립방정식 $Ax = b$에 대해, 첨가행렬(augmented matrix) $(A|b)$의 RREF를 $R$이라 할 때:

- **해가 없음(불능):** $R$의 어떤 행이 $(0\;0\;\cdots\;0\;|\;1)$의 형태이면 (즉, $0 = 1$), 해가 없다.
- **유일해:** 모든 열에 pivot이 있고 ($\text{rank}(A) = n$), 불능 조건이 없으면 유일해가 존재한다.
- **무수히 많은 해:** pivot이 없는 열(자유변수)이 존재하면 ($\text{rank}(A) < n$), 무수히 많은 해가 존재한다.

**증명:** RREF는 원래 연립방정식과 동치이므로, RREF의 각 행은 방정식을 나타낸다. $0 = 1$ 행이 있으면 해가 없다. 그렇지 않으면 각 pivot 변수(pivot에 대응하는 변수)를 자유변수(free variable)로 표현할 수 있으며, 자유변수의 개수가 $\text{nullity}(A) = n - \text{rank}(A)$이다.

### 정리 5: 동차연립방정식 $Ax = 0$

동차연립방정식은 항상 $x = 0$이라는 **자명해(trivial solution)**를 가진다. $\text{rank}(A) < n$일 때(즉, 자유변수가 존재할 때)에만 비자명해가 존재한다.

**증명:** $Ax = 0$은 $b = 0$인 경우이므로, 불능 조건이 발생하지 않는다(우변이 0이므로 $0 = 1$ 형태가 나올 수 없다). 따라서 항상 최소한 하나의 해($x=0$)가 존재한다. RREF에서 pivot의 개수가 $n$보다 작으면 자유변수가 존재하므로 비자명해가 존재한다.

---
## 예제

**예제 1:** 다음 연립방정식을 가우스-조르단 소거로 풀어라.

$$
\begin{cases}
x + 2y + z = 8 \\
2x - y + z = 3 \\
x + y - z = 2
\end{cases}
$$

**풀이:** 첨가행렬을 만들고 RREF로 변환한다.

$$
\left(\begin{array}{ccc|c}
1 & 2 & 1 & 8 \\
2 & -1 & 1 & 3 \\
1 & 1 & -1 & 2
\end{array}\right)
$$

$R_2 \leftarrow R_2 - 2R_1$, $R_3 \leftarrow R_3 - R_1$:

$$
\left(\begin{array}{ccc|c}
1 & 2 & 1 & 8 \\
0 & -5 & -1 & -13 \\
0 & -1 & -2 & -6
\end{array}\right)
$$

$R_2 \leftarrow -\frac{1}{5}R_2$, $R_2 \leftrightarrow R_3$ (pivot을 위로):

$$
\left(\begin{array}{ccc|c}
1 & 2 & 1 & 8 \\
0 & -1 & -2 & -6 \\
0 & 1 & \frac{1}{5} & \frac{13}{5}
\end{array}\right)
$$

$R_2 \leftarrow -R_2$:

$$
\left(\begin{array}{ccc|c}
1 & 2 & 1 & 8 \\
0 & 1 & 2 & 6 \\
0 & 1 & \frac{1}{5} & \frac{13}{5}
\end{array}\right)
$$

$R_3 \leftarrow R_3 - R_2$:

$$
\left(\begin{array}{ccc|c}
1 & 2 & 1 & 8 \\
0 & 1 & 2 & 6 \\
0 & 0 & -\frac{9}{5} & -\frac{17}{5}
\end{array}\right)
$$

$R_3 \leftarrow -\frac{5}{9}R_3$:

$$
\left(\begin{array}{ccc|c}
1 & 2 & 1 & 8 \\
0 & 1 & 2 & 6 \\
0 & 0 & 1 & \frac{17}{9}
\end{array}\right)
$$

후방 소거: $R_2 \leftarrow R_2 - 2R_3$, $R_1 \leftarrow R_1 - R_3$:

$$
\left(\begin{array}{ccc|c}
1 & 2 & 0 & \frac{55}{9} \\
0 & 1 & 0 & \frac{20}{9} \\
0 & 0 & 1 & \frac{17}{9}
\end{array}\right)
$$

$R_1 \leftarrow R_1 - 2R_2$:

$$
\left(\begin{array}{ccc|c}
1 & 0 & 0 & \frac{15}{9} \\
0 & 1 & 0 & \frac{20}{9} \\
0 & 0 & 1 & \frac{17}{9}
\end{array}\right)
$$

따라서 $x = \frac{15}{9} = \frac{5}{3}$, $y = \frac{20}{9}$, $z = \frac{17}{9}$이다.

**예제 2:** 다음 연립방정식의 해를 구하라 (해가 무수히 많은 경우).

$$
\begin{cases}
x + y + z = 1 \\
2x + 2y + 2z = 2 \\
x - y + z = 3
\end{cases}
$$

**풀이:** 첨가행렬:

$$
\left(\begin{array}{ccc|c}
1 & 1 & 1 & 1 \\
2 & 2 & 2 & 2 \\
1 & -1 & 1 & 3
\end{array}\right)
$$

$R_2 \leftarrow R_2 - 2R_1$, $R_3 \leftarrow R_3 - R_1$:

$$
\left(\begin{array}{ccc|c}
1 & 1 & 1 & 1 \\
0 & 0 & 0 & 0 \\
0 & -2 & 0 & 2
\end{array}\right)
$$

$R_2 \leftrightarrow R_3$, $R_2 \leftarrow -\frac{1}{2}R_2$:

$$
\left(\begin{array}{ccc|c}
1 & 1 & 1 & 1 \\
0 & 1 & 0 & -1 \\
0 & 0 & 0 & 0
\end{array}\right)
$$

$R_1 \leftarrow R_1 - R_2$:

$$
\left(\begin{array}{ccc|c}
1 & 0 & 1 & 2 \\
0 & 1 & 0 & -1 \\
0 & 0 & 0 & 0
\end{array}\right)
$$

Pivot 변수는 $x$와 $y$이고, $z$는 자유변수이다. 해는:

$$x = 2 - z,\quad y = -1,\quad z = z$$

즉, $x = \begin{pmatrix} 2 \\ -1 \\ 0 \end{pmatrix} + t \begin{pmatrix} -1 \\ 0 \\ 1 \end{pmatrix}$, $t \in \mathbb{R}$.

**예제 3:** 다음 연립방정식이 해를 가지는지 판정하라.

$$
\begin{cases}
x + y = 1 \\
2x + 2y = 3
\end{cases}
$$

**풀이:** 첨가행렬:

$$
\left(\begin{array}{cc|c}
1 & 1 & 1 \\
2 & 2 & 3
\end{array}\right)
\xrightarrow{R_2 \leftarrow R_2 - 2R_1}
\left(\begin{array}{cc|c}
1 & 1 & 1 \\
0 & 0 & 1
\end{array}\right)
$$

두 번째 행이 $0 = 1$을 의미하므로 해가 없다 (불능).

---
## 연결

- **[rank·열공간·널공간](rank-nullspace.html)** : RREF에서 pivot의 개수는 rank와 같으며, 자유변수의 개수는 nullity와 같다.
- **[역행렬과 기저 변환](inverse-change-of-basis.html)** : 가우스-조르단 소거는 역행렬을 계산하는 가장 기본적인 방법이다.
- **[행렬곱과 선형변환](matrix-multiplication.html)** : 연립방정식 $Ax = b$는 선형변환 $T_A$에 의한 $x$의 상(image)이 $b$임을 의미한다.
- **[행렬식의 기하학](determinant.html)** : $\det A = 0$이면 가우스 소거 중에 pivot이 0이 되는 열이 발생한다.
- **[최소제곱법](least-squares.html)** : 해가 존재하지 않는 연립방정식의 근사해를 구한다.
