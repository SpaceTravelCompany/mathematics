# 수학 로드맵 사이트 구현 계획

## 목표

`topic-pages` 템플릿으로 **수학 학습 사이트**를 구축한다. 기초 수학 8 + 학습 가이드 2 + 선형대수·미적분·확률통계 64 = **74개 토픽 페이지**. 중학교 수학만 안다는 전제에서 시작. 학술적 깊이, 원리 이해 중심, AI 프레임 없이 순수 수학 콘텐츠.

## 범위

- 프로젝트: `/home/lmsd1/projects/mathematics`
- 템플릿: `/home/lmsd1/projects/topic-pages` (npm 로컬 의존성)
- 산출물: `site.json`, `content/*.md` (74개), 빌드된 `dist/`
- **제외**: AI 관련 프레이밍, "쓰임" 독립 섹션, "사고 도구" 보너스

## 결정 사항

### 콘텐츠 톤·구조

- AI 언급 금지. 수학 자체가 목적.
- 각 토픽 페이지 구조 (5섹션):
  1. **직관적 설명** — 개념의 본질 서술 (물리·공학 맥락은 자연스럽게 녹일 수 있음)
  2. **형식적 정의** — Definition, KaTeX 수식
  3. **정리·증명** — 주요 Theorem, 증명 전개 (스케치 아님)
  4. **예제** — 구체적 계산 2~3개
  5. **연결** — 선행/후속 토픽 관계, 사이트 내 상대 링크
- 언어: 한국어 본문 + 영어 수학 용어 혼용 (원문 TXT 톤 유지)
- 수식: KaTeX (`$inline$`, `$$display$$`)

### 사이트 구성

브랜딩:

```json
{
  "title": "Mathematics Roadmap",
  "subtitle": "선형대수 · 미적분 · 확률통계",
  "brandMark": "∑",
  "storagePrefix": "math-roadmap",
  "theme": {
    "light": { "brand": "#1e3a8a", "accent": "#1e3a8a", "link": "#1d4ed8" },
    "dark": { "brand": "#93b4f8", "accent": "#93b4f8", "link": "#7dd3fc" }
  }
}
```

섹션 구성 (14그룹, 74토픽):

| # | 그룹 | 토픽 수 | 슬러그 범위 |
|---|------|---------|-------------|
| 0 | 기초 수학 | 8 | `sets-and-logic` … `coordinate-geometry` |
| 1 | 학습 가이드 | 2 | `learning-path`, `resources` |
| 2 | 행렬과 선형변환 | 7 | `matrix-multiplication` … `vector-space-abstraction` |
| 3 | 내적공간과 직교성 | 3 | `inner-product-norm` … `least-squares` |
| 4 | 고유값과 행렬분해 | 5 | `eigenvalues` … `change-of-basis` |
| 5 | 미분과 고차원 구조 | 5 | `matrix-calculus` … `embedding-geometry` |
| 6 | 미분과 적분 | 5 | `limits-derivatives` … `series-convergence` |
| 7 | 다변수 미분과 최적화 | 9 | `partial-derivatives` … `extrema-saddle` |
| 8 | 푸리에와 벡터 미적분 | 5 | `sigmoid-softmax` … `line-surface-integrals` |
| 9 | 미분방정식과 변분 | 4 | `ode-basics` … `dynamical-systems` |
| 10 | 확률과 분포 | 8 | `counting` … `conditional-traps` |
| 11 | 추정과 정보이론 | 6 | `joint-marginal-conditional` … `monte-carlo` |
| 12 | 검정과 회귀 | 2 | `hypothesis-testing`, `regression-analysis` |
| 13 | 확률과정과 인과 | 6 | `mdp` … `causal-inference` |

기초 수학 토픽 (중학교 수학 → 본 과정 다리):

| slug | 제목 | 내용 |
|------|------|------|
| `sets-and-logic` | 집합과 논리 | 집합 연산, 명제, 필요·충분조건, 증명 기법(귀류법·대우) |
| `functions` | 함수 | 정의역·공역·치역, 합성함수, 역함수, 일대일·전사 |
| `polynomials-equations` | 다항식·방정식·부등식 | 인수분해, 이차방정식, 절댓값 부등식, 항등식 |
| `exponentials-logarithms` | 지수와 로그 | 지수법칙, 로그 정의·성질, 지수·로그 함수 그래프 |
| `trigonometric-functions` | 삼각함수 | 호도법, 삼각비, 그래프, 덧셈정리, 삼각방정식 |
| `sequences-series` | 수열과 급수 기초 | 등차·등비수열, 시그마, 급수 수렴·발산 직관 |
| `plane-vectors` | 평면벡터 기초 | 벡터 성분, 덧셈·스칼라배, 크기, 방향, 내적 도입 |
| `coordinate-geometry` | 좌표기하와 이차곡선 | 직선의 방정식, 원, 포물선·타원·쌍곡선 개요 |

### 콘텐츠 생산 순서

배치 단위 순차 작성. 각 배치 5~8토픽.

1. **스캐폴딩**: `package.json`, `site.json`, assets
2. **Batch 0**: 기초 수학 (8)
3. **Batch 1**: 학습 가이드 (2) + 행렬과 선형변환 (7) → 4+5 분할
4. **Batch 2**: 내적공간과 직교성 (3) + 고유값과 행렬분해 (5) = 8
5. **Batch 3**: 미분과 고차원 구조 (5)
6. **Batch 4**: 미분과 적분 (5)
7. **Batch 5**: 다변수 미분과 최적화 (9) → 5+4 분할
8. **Batch 6**: 푸리에와 벡터 미적분 (5)
9. **Batch 7**: 미분방정식과 변분 (4)
10. **Batch 8**: 확률과 분포 (8) → 4+4 분할
11. **Batch 9**: 추정과 정보이론 (6)
12. **Batch 10**: 검정과 회귀 (2) + 확률과정과 인과 (6) → 4+4 분할

각 배치 완료 후 `npx topic-pages build`로 빌드 검증.

## 단계별 구현

### Step 1: 프로젝트 스캐폴딩

- `package.json` 생성 (topic-pages 로컬 의존성)
- `site.json` 작성 (전체 74토픽 slug/title/summary/icon)
- `content/` 디렉터리 생성
- `assets/` → topic-pages 기본 assets 사용 (custom.css로 남색 테마 보강 가능)
- 빈 content 파일 74개 생성 (frontmatter만)
- 빌드 테스트

### Step 2~12: 배치별 콘텐츠 작성

각 배치마다 `@coder`에 위임:
- 입력: 토픽 목록 + 원문 TXT 해당 부분 + 페이지 구조 템플릿 + 슬러그
- 산출: `content/<slug>.md` 파일
- 검증: 빌드 성공 + KaTeX 수식 문법 오류 없음

### Step 13: 최종 빌드·검증

- 전체 빌드
- 브라우저에서 랜딩·토픽 페이지 렌더링 확인
- KaTeX 수식 렌더링 확인
- nav 그룹·링크 동작 확인

## 검증 방법

1. `npx topic-pages build` — 에러 없이 완료
2. 생성된 `dist/index.html` + `dist/topics/*.html` 파일 수 = 75 (1 + 74)
3. 브라우저 렌더링 — KaTeX 수식, nav, 검색 동작
4. 콘텐츠 품질 — 각 토픽 5섹션 구조 준수, 증명 전개 포함

## 위임 대상

| 작업 | 에이전트 |
|------|----------|
| 스캐폴딩 (site.json, package.json, 디렉터리) | `@coder` |
| 콘텐츠 작성 (배치별) | `@coder` |
| 최종 리뷰·계획 적합성 검사 | `@review` |
