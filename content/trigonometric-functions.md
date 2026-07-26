---
title: 삼각함수
slug: trigonometric-functions
---

## 직관적 설명

**삼각함수(trigonometric functions)** 는 각도를 입력하면 좌표를 출력하는 함수다. 단위원(unit circle) 위를 회전하는 점의 $x$좌표와 $y$좌표가 각각 코사인(cosine)과 사인(sine)이다. 이 관점은 삼각형의 비율이라는 기하학적 기원을 훨씬 넘어서, 주기적인 현상(periodic phenomena)을 기술하는 가장 강력한 언어로 확장된다. 파동(wave), 진동(oscillation), 회전(rotation), 그리고 원운동(circular motion)은 모두 삼각함수로 표현된다. 푸리에 해석(Fourier analysis)은 모든 주기 신호를 삼각함수의 합으로 분해하며, 이는 신호처리와 양자역학의 초석이다.

## 정의

**호도법(radian measure):** 각도를 측정하는 단위로, 반지름 1인 원에서 호(arc)의 길이로 각도를 나타낸다. $360^\circ = 2\pi$ (rad)이다.

**단위원 정의:** 반지름이 1인 원 위의 점이 $x$축 양의 방향에서부터 각 $\theta$만큼 회전한 위치의 좌표를 $(\cos\theta, \sin\theta)$로 정의한다.

**삼각함수의 기본 성질:**
- 정의역: $\mathbb{R}$ (모든 실수)
- 치역: $\cos\theta, \sin\theta \in [-1, 1]$
- 주기(period): $2\pi$, 즉 $\cos(\theta + 2\pi) = \cos\theta$, $\sin(\theta + 2\pi) = \sin\theta$

**탄젠트(tangent):** $\tan\theta = \frac{\sin\theta}{\cos\theta}$, $\cos\theta \neq 0$인 모든 $\theta$에서 정의된다.

**역삼각함수(inverse trigonometric functions):** $\sin^{-1} x$ (또는 $\arcsin x$)는 $\sin\theta = x$를 만족하는 각도를 $[-\pi/2, \pi/2]$ 범위에서 반환한다. 유사하게 $\cos^{-1} x$ ($[0, \pi]$), $\tan^{-1} x$ ($(-\pi/2, \pi/2)$)가 정의된다.

## 주요 정리와 증명

### 정리 1: 피타고라스 항등식 (Pythagorean Identity)

모든 실수 $\theta$에 대해 다음이 성립한다.

$$\sin^2\theta + \cos^2\theta = 1$$

**증명:** 단위원 위의 점 $(\cos\theta, \sin\theta)$는 원점으로부터의 거리가 1이다. 좌표평면에서 두 점 $(0,0)$과 $(\cos\theta, \sin\theta)$ 사이의 거리는

$$\sqrt{(\cos\theta - 0)^2 + (\sin\theta - 0)^2} = \sqrt{\cos^2\theta + \sin^2\theta}$$

그런데 단위원의 정의에 의해 이 거리는 1이다. 따라서

$$\sqrt{\cos^2\theta + \sin^2\theta} = 1 \;\Longrightarrow\; \cos^2\theta + \sin^2\theta = 1$$

**따름정리:** $1 + \tan^2\theta = \sec^2\theta$, $1 + \cot^2\theta = \csc^2\theta$ (여기서 $\sec\theta = 1/\cos\theta$, $\csc\theta = 1/\sin\theta$, $\cot\theta = 1/\tan\theta$).

### 정리 2: 코사인 덧셈정리 (Cosine Addition Formula)

$$\cos(\alpha + \beta) = \cos\alpha \cos\beta - \sin\alpha \sin\beta$$

**증명 (벡터 내적을 이용한 방법):**

단위원 위의 두 점 $P = (\cos\alpha, \sin\alpha)$와 $Q = (\cos\beta, \sin\beta)$를 생각하자. 두 벡터 $\vec{OP}$와 $\vec{OQ}$ 사이의 각은 $|\alpha - \beta|$이다 (단, $\alpha \geq \beta$라 가정).

내적을 두 가지 방법으로 계산한다.

**대수적 방법:** $\vec{OP} \cdot \vec{OQ} = \cos\alpha \cos\beta + \sin\alpha \sin\beta$

**기하학적 방법:** $\vec{OP} \cdot \vec{OQ} = \|\vec{OP}\| \|\vec{OQ}\| \cos(\alpha - \beta) = 1 \cdot 1 \cdot \cos(\alpha - \beta) = \cos(\alpha - \beta)$

두 결과가 같으므로

$$\cos(\alpha - \beta) = \cos\alpha \cos\beta + \sin\alpha \sin\beta$$

$\beta$를 $-\beta$로 치환하면 $\cos(\alpha + \beta) = \cos\alpha \cos(-\beta) + \sin\alpha \sin(-\beta) = \cos\alpha \cos\beta - \sin\alpha \sin\beta$ (코사인은 우함수, 사인은 기함수이므로).

**사인 덧셈정리:** $\sin(\alpha + \beta) = \sin\alpha \cos\beta + \cos\alpha \sin\beta$는 $\sin\theta = \cos(\pi/2 - \theta)$ 관계를 이용하면 위 결과에서 유도된다.

### 정리 3: 배각·반각 공식 (Double- and Half-Angle Formulas)

덧셈정리에서 $\beta = \alpha$로 두면 **배각 공식**을 얻는다.

$$\cos(2\alpha) = \cos^2\alpha - \sin^2\alpha = 2\cos^2\alpha - 1 = 1 - 2\sin^2\alpha$$
$$\sin(2\alpha) = 2\sin\alpha\cos\alpha$$

배각 공식에서 $\cos^2\alpha$ 또는 $\sin^2\alpha$에 대해 정리하면 **반각 공식**을 얻는다.

$$\cos^2\alpha = \frac{1 + \cos(2\alpha)}{2}, \quad \sin^2\alpha = \frac{1 - \cos(2\alpha)}{2}$$

또는 $\alpha = \theta/2$로 치환하여

$$\cos\frac{\theta}{2} = \pm\sqrt{\frac{1 + \cos\theta}{2}}, \quad \sin\frac{\theta}{2} = \pm\sqrt{\frac{1 - \cos\theta}{2}}$$

여기서 부호는 $\theta/2$가 위치한 사분면에 따라 결정된다.

## 예제

**예제 1:** 삼각방정식 $\sin x = \frac{1}{2}$를 $0 \leq x < 2\pi$ 범위에서 풀어라.

**풀이:** 단위원에서 $\sin x = 1/2$인 각도는 $x = \pi/6$와 $x = 5\pi/6$이다. 사인 함수의 주기성을 고려하면 일반해는

$$x = \frac{\pi}{6} + 2n\pi \quad\text{또는}\quad x = \frac{5\pi}{6} + 2n\pi \quad (n \in \mathbb{Z})$$

주어진 범위 $[0, 2\pi)$에서는 $x = \pi/6$, $x = 5\pi/6$가 해이다.

**예제 2:** $\cos 75^\circ$의 값을 덧셈정리를 이용하여 구하라. (단, $75^\circ = 45^\circ + 30^\circ$)

**풀이:**

$$\cos 75^\circ = \cos(45^\circ + 30^\circ) = \cos 45^\circ \cos 30^\circ - \sin 45^\circ \sin 30^\circ$$

$$= \frac{\sqrt{2}}{2} \cdot \frac{\sqrt{3}}{2} - \frac{\sqrt{2}}{2} \cdot \frac{1}{2} = \frac{\sqrt{6} - \sqrt{2}}{4}$$

**예제 3:** 함수 $y = 2\cos(3x - \pi/4) + 1$의 진폭(amplitude), 주기(period), 평행이동(phase shift)을 구하고 기본 파형과의 차이를 설명하라.

**풀이:** 표준형 $y = A\cos(B(x - C)) + D$와 비교한다.
- 진폭 $A = 2$ (최댓값 $2+1=3$, 최솟값 $-2+1=-1$)
- 주기 $T = \frac{2\pi}{|B|} = \frac{2\pi}{3}$
- 수평 이동(phase shift) $C = \pi/12$ (우측)
- 수직 이동 $D = 1$ (상향)

기본 $\cos x$에 비해 진폭이 2배, 주기가 $1/3$로 줄고, $\pi/12$만큼 우측으로, 1만큼 위로 이동했다.

## 연결

- **[푸리에 급수](topics/fourier.html)** : 모든 주기함수는 삼각함수의 무한급수로 분해된다.
- **[평면벡터 기초](topics/plane-vectors.html)** : 단위원 위의 점 $(\cos\theta, \sin\theta)$는 벡터이며, 덧셈정리는 벡터 회전과 연결된다.
- **[극한과 도함수](topics/limits-derivatives.html)** : 삼각함수의 미분 $\frac{d}{dx}\sin x = \cos x$는 극한 $\lim_{x\to 0} \frac{\sin x}{x} = 1$에서 출발한다.
