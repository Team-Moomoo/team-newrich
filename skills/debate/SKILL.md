---
name: debate
description: "This skill should be used when the user wants two mentors to debate a topic from different perspectives. Use when: /debate, 멘토 토론, debate mentors, 관점 비교"
---

# Debate

멘토 2명이 주제에 대해 토론하여 다각적 인사이트를 얻는다.

## 에이전트

- 지정된 멘토 에이전트 2명

## Input

```
/debate {멘토A} {멘토B} "{주제}" [라운드수]
```

- 멘토A, 멘토B: 서로 다른 멘토 2명 (약칭 허용)
- 주제: 토론 주제
- 라운드수: 선택. 기본값 1. 범위 1~5 (초과 시 5로 제한)

## 실행 절차

1. 멘토명 파싱 + 검증 — 같은 멘토 2명이면 에러 + 서로 다른 멘토 선택 안내
2. 라운드수 파싱 — 미지정 시 1, 범위 초과 시 5로 클램프
3. 프로젝트 루트에서 `our-situation.md` 탐색 (있으면 읽기, 없으면 스킵)
4. 라운드 반복:
   - 멘토A: 주제에 대한 자기 관점 제시 (첫 라운드) 또는 상대 반론에 대한 재반론
   - 멘토B: A 의견에 대한 반론 + 자기 관점 제시
   - 멘토A: B 의견에 대한 반론
5. 종합 정리: 공통점, 차이점, 실행 가능한 결론

## 규칙

- 지정 라운드 안에 결론까지 도출
- 같은 멘토 2명 지정 시 에러
- 멘토명/주제 누락 시 확인 요청
