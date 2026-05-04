---
name: ask
description: "This skill should be used when the user wants to ask a specific mentor for advice or insight. Use when: /ask, 멘토에게 질문, ask mentor, 조언 구하기"
---

# Ask

멘토 1명에게 질문하여 해당 멘토의 관점에서 인사이트를 얻는다.

## 에이전트

- 지정된 멘토 에이전트 1명

## Input

```
/ask {멘토명} {질문}
```

- 멘토명: tim, naval, kepano, charlie (약칭 허용). tim-ferriss 등 풀네임도 가능.
- 질문: 자유 텍스트. 인자가 없으면 대화에서 파악.

## 실행 절차

1. 멘토명 파싱 — 약칭을 풀네임으로 변환 (tim→tim-ferriss, naval→naval-ravikant, kepano→kepano, charlie→charlie-munger)
2. 존재하지 않는 멘토명이면 에러 + 사용 가능 멘토 목록 출력 후 중단
3. 프로젝트 루트에서 `our-situation.md` 탐색 (있으면 읽기, 없으면 스킵)
4. 해당 멘토 에이전트 호출 (질문 + context 전달)
5. 멘토 관점 답변 출력 — 적용한 프레임워크 명시

## 규칙

- 멘토명 누락 시 어떤 멘토에게 질문할지 확인
- 질문 누락 시 무엇을 질문할지 확인
