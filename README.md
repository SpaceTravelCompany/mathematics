# Mathematics Roadmap

선형대수 · 미적분 · 확률통계 학습 사이트. 빌더는 [`topic-pages`](https://github.com/SpaceTravelCompany/topic-pages) 패키지를 사용한다.

## 처음부터 공부하기

[수학을 읽는 법 — 숫자에서 수식까지](content/math-language.md)에서 시작한다. 분수·문자·기호·그래프·증명을 읽는 법부터 설명하며, 각 장의 학습 순번과 이전·다음 링크를 따라 이어 읽을 수 있다.

목차는 **기초 → 선형대수 → 미적분 → 확률통계 → 결합 응용** 순서다. 행렬 미분은 편도함수 뒤에, 마르코프 체인은 행렬과 확률 뒤에, 확률미분방정식은 미분방정식과 확률 뒤에 배치했다. [복소수 입문](content/complex-numbers.md)은 고유값과 푸리에 분석에서 복소수가 처음 등장하기 전에 읽는다.

각 장은 다음 흐름으로 읽는다.

1. **작은 예제로 시작하기:** 앞에서 배운 재료를 떠올리고 숫자를 넣어 개념을 계산한다.
2. **본문·증명으로 이어 읽기:** 예제의 계산이 일반적인 기호와 정리로 어떻게 바뀌는지 연결한다.
3. **직관·정의·정리와 증명:** 적용 조건을 읽고, 식이 변하는 이유를 따라간다.
4. **예제와 연결:** 같은 원리를 다른 문제에 적용하고 다음 개념과의 관계를 살핀다.

기존 본문에는 후속 장의 응용이나 일반적인 증명도 포함되어 있다. 아직 배우지 않은 응용 용어는 해당 장의 연결 안내를 통해 돌아올 수 있게 했으며, 첫 예제에서 필요한 재료와 앞으로 확장할 개념을 구분해 설명한다.

## 사용법

```bash
cd mathematics
npm install         # topic-pages 의존성 설치
npm run build       # dist/ 정적 HTML 생성
```

`dist/index.html` + `dist/assets/` 번들로 동작하는 위키 페이지 앱이다.

`assets/`의 이미지·파비콘 등 추가 에셋도 빌드 시 자동으로 `dist/assets/`에 복사된다.

서빙은 사용자 환경의 도구로 (VS Code Live Server, `npx serve`, `python -m http.server` 등).
`content/*.md` 또는 `site.json` 수정 후 `npm run build` 다시 실행 → `dist/` 갱신.

## 구조

- `site.json` — 섹션·주제·참조 링크·테마 정의
- `content/` — 주제별 마크다운 (기초 입문 2개를 포함한 75개 토픽)
- `assets/` — 파비콘 (빌드 시 `dist/assets/`로 복사)
- `package.json` — `topic-pages` 의존성 + 빌드 스크립트
- `docs/` — AI 계획 문서

## 라이선스

[MIT](LICENSE)
