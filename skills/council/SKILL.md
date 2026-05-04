---
name: council
description: "This skill should be used when the user wants multiple mentors to discuss a topic in a roundtable format. Use when: /council, 멘토 라운드테이블, council meeting, 종합 자문"
---

# Council

멘토 라운드테이블. 여러 멘토의 관점을 모아 종합적 인사이트를 얻는다.

## 에이전트

- 지정된 멘토 에이전트 N명 (2명 이상)

## Input

```
/council "{주제}" [멘토1 멘토2 ...]
```

- 주제: 라운드테이블 주제
- 멘토 목록: 선택. 생략 시 전체 멘토 참여 (tim, naval, kepano, charlie). 2명 이상 지정 필수.

## 실행 절차

1. 멘토 목록 파싱 — 생략 시 전원, 1명만 지정 시 "/ask 사용" 안내 후 중단
2. 프로젝트 루트에서 `our-situation.md` 탐색 (있으면 읽기, 없으면 스킵)
3. 참여 멘토 순차 호출: 각자 주제에 대한 자기 관점 제시
4. 종합 정리: 각 멘토 핵심 포인트 요약 + 공통 방향 + 상충 지점 + 실행 제안

## 규칙

- 1명만 지정 시 /ask 사용 안내
- 주제 누락 시 확인 요청
