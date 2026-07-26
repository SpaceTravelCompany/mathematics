---
title: 텐서 연산
slug: tensor-operations
---

## 직관적 설명

**텐서(tensor)**는 "행렬의 고차원 일반화"로, 스칼라(0차), 벡터(1차), 행렬(2차)을 모두 포함하는 통일된 개념이다. 3차 이상의 텐서는 $T_{ijk}$처럼 세 개 이상의 인덱스를 가지며, 각 인덱스는 하나의 "축(axis)" 또는 "모드(mode)"에 대응한다.

그러나 텐서의 본질은 단순한 다차원 배열 이상이다. 텐서는 **좌표 변환에 대해 특정한 규칙으로 변환되는 다중선형(multilinear) 대상**이다. 즉, 텐서의 성분 값은 좌표계에 의존하지만, 텐서 자체는 좌표계와 무관한 기하학적 실체다. 이 관점은 연속체 역학, 일반상대론, 전자기학에서 필수적이다.

예를 들어 물체 내부의 응력(stress)은 2차 텐서 $\sigma_{ij}$로 표현된다. $i$는 힘이 작용하는 면의 방향, $j$는 힘의 성분 방향을 나타낸다. 좌표계를 회전하면 $\sigma_{ij}$의 값은 변하지만, 물리적 응력 상태는 동일하게 유지된다. 텐서의 변환 법칙이 바로 이 일관성을 보장한다.

텐서 연산의 핵심은 **축 수축(contraction)** — 인덱스의 합 — 이다. 행렬곱 $C_{ik} = A_{ij} B_{jk}$는 두 텐서의 2축 수축이며, $\text{tr}(A) = A_{ii}$는 단일 텐서의 자기 수축이다. 아인슈타인 합 규약(Einstein summation convention)은 이러한 합 연산에서 $\sum$ 기호를 생략하여 표기를 간결하게 한다.

## 정의

**텐서의 대수적 정의 (algebraic definition):** 체 $\mathbb{F}$ 위의 벡터공간 $V$와 그 쌍대공간(dual space) $V^*$에 대해, $(p,q)$형 텐서는 다음 다중선형사상(multilinear map)이다:

$$T: \underbrace{V^* \times \cdots \times V^*}_{p\text{ times}} \times \underbrace{V \times \cdots \times V}_{q\text{ times}} \to \mathbb{F}$$

$p$는 **반변(contravariant)** 계수(rank), $q$는 **공변(covariant)** 계수이며, 총 계수(rank)는 $p+q$이다.

**성분 표기 (component notation):** 기저 $\{e_i\}$와 쌍대기저 $\{\varepsilon^i\}$를 선택하면, $(p,q)$형 텐서는 $p+q$개의 인덱스를 가진 성분 $T^{i_1 \ldots i_p}_{j_1 \ldots j_q}$로 표현된다.

**텐서의 계수와 예시:**

| 계수 | 이름 | 예시 | 성분 수 ($n$차원) |
|------|------|------|-------------------|
| 0 | 스칼라 | 온도, 질량 | $1$ |
| 1 | 벡터 | 속도, 힘 | $n$ |
| 2 | 행렬 | 응력 텐서, 관성 텐서 | $n^2$ |
| 3 | 3차 텐서 | 피에조 전기 텐서 | $n^3$ |
| 4 | 4차 텐서 | 탄성 텐서, 리만 곡률 텐서 | $n^4$ |

**아인슈타인 합 규약 (Einstein summation convention):** 한 항에서 같은 인덱스가 위·아래에 한 번씩 나타나면 그 인덱스에 대해 합한다:

$$T^i_{\,j} S_j^{\,k} := \sum_{j=1}^n T^i_{\,j} S_j^{\,k}$$

이 규약은 텐서 연산에서 합 기호를 생략하여 표기를 크게 단순화한다.

**텐서 곱 (tensor product):** $(p,q)$형 텐서 $T$와 $(r,s)$형 텐서 $S$의 텐서 곱 $T \otimes S$는 $(p+r, q+s)$형 텐서이며:

$$(T \otimes S)(\alpha^1, \ldots, \alpha^{p+r}, v_1, \ldots, v_{q+s}) = T(\alpha^1, \ldots, \alpha^p, v_1, \ldots, v_q) \cdot S(\alpha^{p+1}, \ldots, \alpha^{p+r}, v_{q+1}, \ldots, v_{q+s})$$

성분 표기: $(T \otimes S)^{i_1 \ldots i_{p+r}}_{j_1 \ldots j_{q+s}} = T^{i_1 \ldots i_p}_{j_1 \ldots j_q} \cdot S^{i_{p+1} \ldots i_{p+r}}_{j_{q+1} \ldots j_{q+s}}$.

**축 수축 (contraction):** $(p,q)$형 텐서의 $k$번째 반변 인덱스와 $l$번째 공변 인덱스를 수축하면 $(p-1, q-1)$형 텐서를 얻는다. 성분 표기:

$$(\text{Contraction}_{kl}(T))^{i_1 \ldots i_{k-1} i_{k+1} \ldots i_p}_{j_1 \ldots j_{l-1} j_{l+1} \ldots j_q} = T^{i_1 \ldots i_{k-1} s i_{k+1} \ldots i_p}_{j_1 \ldots j_{l-1} s j_{l+1} \ldots j_q}$$

(아인슈타인 규약에 따라 $s$에 대해 합한다.)

## 주요 정리와 증명

### 정리 1: 텐서 곱의 보편 성질 (Universal Property of Tensor Product)

벡터공간 $V, W$에 대해, 다음 성질을 만족하는 쌍 $(V \otimes W, \otimes)$이 동형을 제외하고 유일하게 존재한다:

임의의 벡터공간 $U$와 쌍선형사상(bilinear map) $\varphi: V \times W \to U$에 대해, 선형사상 $\tilde{\varphi}: V \otimes W \to U$가 유일하게 존재하여 $\varphi = \tilde{\varphi} \circ \otimes$, 즉 $\varphi(v,w) = \tilde{\varphi}(v \otimes w)$를 만족한다.

```
V × W ──⊗──→ V ⊗ W
  │              │
  │ φ            │ ∃! φ̃
  ▼              ▼
  U ──────────→ U (linear)
```

**증명 (구성과 유일성):**

**Step 1 — 자유 벡터공간 (free vector space):** 집합 $V \times W$의 원소를 기저로 하는 자유 벡터공간 $\mathcal{F}(V \times W)$를 구성한다. 즉, 모든 유한 형식적 선형결합 $\sum \alpha_{ij} (v_i, w_j)$의 집합이다.

**Step 2 — 부분공간으로 나누기:** 다음 관계로 생성되는 부분공간 $\mathcal{R}$로 $\mathcal{F}$를 나눈다:
$$(v_1 + v_2, w) - (v_1,w) - (v_2,w)$$
$$(v, w_1 + w_2) - (v,w_1) - (v,w_2)$$
$$(\alpha v, w) - \alpha(v,w)$$
$$(v, \alpha w) - \alpha(v,w)$$

**Step 3 — 몫공간 (quotient):** $V \otimes W := \mathcal{F}(V \times W) / \mathcal{R}$라 정의하고, $v \otimes w$를 $(v,w)$의 동치류(equivalence class)로 정의한다. 이 구성에 의해 $v \otimes w$는 자동으로 쌍선형성을 만족한다.

**Step 4 — 보편 성질:** 임의의 쌍선형 $\varphi: V \times W \to U$에 대해, $\mathcal{F}$에서 $\tilde{\varphi}_0(v,w) = \varphi(v,w)$로 정의하면 $\tilde{\varphi}_0$는 $\mathcal{R}$에서 0이므로 선형사상 $\tilde{\varphi}: V \otimes W \to U$를 유도한다. $\otimes$와의 교환성은 구성에서 자명하다. 유일성은 $V \otimes W$가 $v \otimes w$ 꼴의 원소로 생성되므로 $\tilde{\varphi}$가 이 생성원 위에서 강제로 결정되기 때문이다.

**의의:** 보편 성질은 텐서 곱의 본질이 **쌍선형사상의 선형화**임을 말한다. 즉, 모든 쌍선형 문제는 텐서 곱 위의 선형 문제로 일대일 대응된다.

### 정리 2: 축 수축과 행렬곱의 관계

행렬곱 $C = AB$는 두 2차 텐서의 2축 수축과 동일하다.

**증명:** $A$를 $(1,1)$형 텐서 $A^i_{\,j}$, $B$를 $(1,1)$형 텐서 $B^j_{\,k}$로 보자. $A^i_{\,j}$와 $B^j_{\,k}$의 텐서 곱은 $(2,2)$형 텐서 $T^{ij}_{\,jk} = A^i_{\,j} B^j_{\,k}$이다. 이 텐서의 두 번째 반변 인덱스와 첫 번째 공변 인덱스를 수축하면:

$$C^i_{\,k} = T^{ij}_{\,jk} = A^i_{\,j} B^j_{\,k}$$

이는 정확히 행렬곱 $C = AB$의 성분 표기이며, $j$에 대해 합산된다.

**일반화:** 더 일반적으로, $m$차 텐서 $T_{i_1 \ldots i_m}$과 $n$차 텐서 $S_{j_1 \ldots j_n}$의 $k$축 수축은 다음과 같다:
$$(T \cdot_k S)_{i_1 \ldots i_{m-1} j_1 \ldots j_{n-1}} = \sum_{p=1}^d T_{i_1 \ldots i_{a-1} p i_a \ldots i_{m-1}} \cdot S_{j_1 \ldots j_{b-1} p j_b \ldots j_{n-1}}$$

즉, 두 텐서의 공통 축을 따라 성분을 곱하고 합한다.

### 정리 3: 좌표 변환에서 텐서 성분의 변환 법칙

벡터공간 $V$의 기저가 $\{e_i\}$에서 $\{e'_i\}$로 변환된다고 하자. 변환 행렬 $Q$를 $e'_i = Q^j_{\,i} e_j$로 정의한다. $(1,0)$형 텐서(벡터) $v = v^i e_i = v'^i e'_i$의 성분 변환 법칙은:

$$v'^i = (Q^{-1})^i_{\,j} v^j$$

이는 반변(contravariant) 변환이라 불린다. 반면 $(0,1)$형 텐서(코벡터) $\omega = \omega_i \varepsilon^i = \omega'_i \varepsilon'^i$의 성분은:
$$\omega'_i = Q^j_{\,i} \omega_j$$

이는 공변(covariant) 변환이다.

일반적인 $(p,q)$형 텐서의 변환 법칙은 각 반변 인덱스에 $(Q^{-1})$을, 각 공변 인덱스에 $Q$를 적용한다:

$$T'^{i_1 \ldots i_p}_{j_1 \ldots j_q} = (Q^{-1})^{i_1}_{\,k_1} \cdots (Q^{-1})^{i_p}_{\,k_p} \cdot Q^{l_1}_{\,j_1} \cdots Q^{l_q}_{\,j_q} \cdot T^{k_1 \ldots k_p}_{l_1 \ldots l_q}$$

**증명 (직교 변환의 경우):** $Q$가 직교 행렬($Q^T = Q^{-1}$)인 경우, 반변 벡터와 공변 벡터의 구분이 사라진다. 직교 좌표계에서 $Q^{-1} = Q^T$이므로:

$$v'_i = Q_{ij} v_j, \quad T'_{ij} = Q_{ip} Q_{jq} T_{pq}$$

**증명:** $T = T_{pq} \varepsilon^p \otimes \varepsilon^q$라 하자. 새 기저에서 $\varepsilon'^i = Q^i_{\,p} \varepsilon^p$이므로:
$$\begin{aligned}
T &= T_{pq} \varepsilon^p \otimes \varepsilon^q \\
&= T_{pq} (Q^{-1})^p_{\,i} \varepsilon'^i \otimes (Q^{-1})^q_{\,j} \varepsilon'^j \\
&= (Q^{-1})^p_{\,i} (Q^{-1})^q_{\,j} T_{pq} \, \varepsilon'^i \otimes \varepsilon'^j
\end{aligned}$$

따라서 $T'_{ij} = (Q^{-1})^p_{\,i} (Q^{-1})^q_{\,j} T_{pq}$이다. 직교 변환이면 $(Q^{-1})^p_{\,i} = Q_{ip}$이므로 $T'_{ij} = Q_{ip} Q_{jq} T_{pq}$가 된다.

**의의:** 이 변환 법칙이 텐서를 단순한 다차원 배열과 구분 짓는 핵심이다. 같은 물리량이라도 좌표계에 따라 성분값이 이 법칙에 따라 변해야 텐서라 할 수 있다.

## 예제

**예제 1 (2차 텐서의 대칭·반대칭 분해):** 임의의 2차 텐서 $T_{ij}$는 대칭(symmetric) 부분과 반대칭(antisymmetric) 부분으로 유일하게 분해된다:
$$T_{ij} = S_{ij} + A_{ij}$$
$$S_{ij} = \frac{1}{2}(T_{ij} + T_{ji}), \quad A_{ij} = \frac{1}{2}(T_{ij} - T_{ji})$$

**확인:** $S_{ij} = S_{ji}$, $A_{ij} = -A_{ji}$이며 이 분해는 유일하다. 이는 모든 행렬이 대칭 성분과 반대칭 성분으로 분해된다는 선형대수의 결과와 일치한다.

**예제 2 (응력 텐서의 주응력):** Cauchy 응력 텐서 $\sigma_{ij}$는 2차 대칭 텐서이다. 주응력(principal stress)은 $\sigma$의 고유값이며, 주축(principal axis)은 고유벡터이다.

응력 텐서의 고유값 문제:
$$\sigma_{ij} n_j = \lambda n_i \quad \Longleftrightarrow \quad (\sigma - \lambda I)n = 0$$

주응력 $\lambda_1, \lambda_2, \lambda_3$은 실수(대칭 텐서이므로)이며, 직교하는 주축 방향을 결정한다. 이는 재료의 파괴 조건(Tresca, von Mises)의 기초가 된다.

**예제 3 (아인슈타인 규약 전개):** 다음 표현을 아인슈타인 규약 없이 전개하라:
$$R^i_{\,jkl} v^j w^k u_l$$

**풀이:** $i$는 자유 인덱스(결과의 성분 인덱스), $j,k,l$은 합 인덱스:
$$R^i_{\,jkl} v^j w^k u_l = \sum_{j=1}^n \sum_{k=1}^n \sum_{l=1}^n R^i_{\,jkl} v^j w^k u_l$$

**예제 4 (행렬식을 텐서 표기로):** $n \times n$ 행렬 $A$의 행렬식은 레비-치비타 기호(Levi-Civita symbol) $\varepsilon$를 사용하여 텐서 축 수축으로 표현된다:
$$\det(A) = \varepsilon_{i_1 \ldots i_n} A^{i_1}_{\,1} \cdots A^{i_n}_{\,n}$$

또는 완전히 수축된 형태:
$$\det(A) = \frac{1}{n!} \varepsilon^{i_1 \ldots i_n} \varepsilon_{j_1 \ldots j_n} A^{j_1}_{\,i_1} \cdots A^{j_n}_{\,i_n}$$

**예제 5 (탄성 텐서):** 등방성(isotropic) 선형 탄성 재료의 응력-변형률 관계는 4차 탄성 텐서 $C_{ijkl}$로 표현된다:
$$\sigma_{ij} = C_{ijkl} \varepsilon_{kl}$$

등방성 재료에서 $C_{ijkl}$는 두 개의 Lamé 상수 $\lambda, \mu$로 결정된다:
$$C_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk})$$

크로네커 델타(Kronecker delta) $\delta_{ij}$를 사용한 이 표현은 등방성(모든 방향에서 동일한 성질) 조건을 자동으로 만족시킨다.

**예제 6 (관성 텐서):** 강체의 관성 모멘트는 2차 텐서 $I_{ij}$이다:
$$I_{ij} = \int_V \rho(r) (\delta_{ij} \|r\|^2 - r_i r_j) \, dV$$

각운동량 $L_i = I_{ij} \omega_j$는 관성 텐서와 각속도 벡터의 축 수축이다. 좌표계를 회전하면 관성 텐서의 성분은 변환 법칙 $I'_{ij} = Q_{ip} Q_{jq} I_{pq}$를 따라 변한다.

**예제 7 (텐서 곱의 차원):** $m$차원 벡터공간 $V$와 $n$차원 벡터공간 $W$에 대해, $V \otimes W$의 차원은 $mn$임을 보여라.

**풀이:** $\{e_1, \ldots, e_m\}$이 $V$의 기저, $\{f_1, \ldots, f_n\}$이 $W$의 기저라 하자. $\{e_i \otimes f_j \mid i=1,\ldots,m,\; j=1,\ldots,n\}$이 $V \otimes W$의 기저를 이룬다. 이 집합이 일차독립이고 $V \otimes W$를 생성함을 보일 수 있다. 기저 원소의 개수가 $mn$이므로 $\dim(V \otimes W) = mn$이다.

## 연결

- **[행렬곱과 선형변환](matrix-multiplication.html)** : 행렬곱은 2차 텐서의 축 수축이며, 텐서 개념의 가장 친숙한 예시다.
- **[발산·회전](div-curl.html)** : 응력 텐서 $\sigma_{ij}$의 발산 $\partial_j \sigma_{ij}$는 연속체 역학의 운동방정식에 나타난다.
- **[SVD](svd.html)** : 2차 텐서(행렬)의 특이값 분해는 텐서 분해(Tucker, CP, Tensor Train)로 일반화된다.
