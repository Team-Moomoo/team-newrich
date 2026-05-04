# team-newrich

내 상황을 아는 멘토에게 자문을 구하는 [Claude Code](https://claude.com/claude-code) 플러그인.

찰리 멍거, 나발 라비칸트, 팀 페리스, 케파노, 안드레이 카파시 — 5명의 가상 멘토에게 1명/2명/N명 단위로 질문할 수 있다. 모든 멘토는 프로젝트 루트의 `our-situation.md`를 읽고 너의 맥락에 맞춰 답한다.

- `/ask` — 멘토 1명에게 질문
- `/debate` — 멘토 2명이 토론
- `/council` — 멘토 N명 라운드테이블
- 한국 맥락 보정 내장 (미국발 조언을 한국 환경에 맞게 변환)
- `our-situation.md` 없어도 동작 — 단, 답변이 일반론에 머문다

## Installation

### Marketplace

```
/plugin marketplace add Team-Moomoo/team-newrich
/plugin install team-newrich@team-newrich
```

### Manually

```bash
git clone https://github.com/Team-Moomoo/team-newrich.git \
  ~/.claude/plugins/team-newrich
```

## 사용 시나리오

### 1) `our-situation.md` 작성

이 플러그인의 핵심은 멘토가 **너의 상황을 알고** 답하는 것. `our-situation.md`가 없으면 그냥 멍거 흉내·나발 흉내일 뿐이다.

프로젝트 루트(또는 작업하려는 폴더 루트)에 `our-situation.md`를 만들고, 멘토가 알아야 너에게 의미 있는 조언을 할 수 있는 정보를 적는다. 정해진 양식 없음 — 아래는 무엇을 적으면 좋은지에 대한 가이드.

**적으면 좋은 것**

- **현재 상황** — 가족 구성, 거주, 핵심 관계 (조언이 너의 일상과 맞물려야 한다)
- **경력 / 역량 / 성향** — 무엇을 잘하고 무엇을 싫어하는지. 누구와 함께 일하는지, 그 사람의 강점은 무엇인지
- **현재 진행 중인 프로젝트 / 일** — 무엇을, 왜, 어디까지 와 있는지
- **재무 상황** — 자산, 월간 고정비, 월간 수입, 런웨이. 멘토가 "그건 너무 위험해" 또는 "그건 충분히 안전해"를 판단할 수 있는 수준
- **목표** — 단기(3개월) / 중기(1년) / 장기(3~5년). 모르면 "모르겠다"고 적는 것도 괜찮음
- **제약** — 시간, 육아, 건강, 자금, 법적/계약상 제약 등 멘토가 무시하면 안 되는 것
- **강점·자산** — 동원 가능한 자원 (멘토가 "그 자산을 써라" 같은 조언을 할 수 있도록)
- **세계관·가치관** — 우선순위, 포기 못 하는 것, 멘토 조언이 충돌하면 안 되는 라인

**작성 팁**

- 길어도 된다. 멘토는 다 읽는다.
- 정직하게 적는다. "잘해요"가 아니라 실제 데이터 (예: MAU, 월 매출, 런웨이 개월 수)
- 가치관·우선순위는 명문화한다 — 멘토가 너에게 안 맞는 조언을 하지 않도록
- 상황이 바뀌면 이 파일만 업데이트하면 된다

### 2) 멘토 세팅

기본 5명을 그대로 써도 되고, 본인의 멘토를 추가/교체해도 된다.

**기본 멘토**

| 약칭 | 에이전트 | 전문 영역 |
|------|----------|-----------|
| `tim` | tim-ferriss | 시간/장소 독립, 효율, 실험 설계 |
| `naval` | naval-ravikant | 부, 행복, 지혜, 레버리지 |
| `kepano` | kepano | 도구, 사고, 미니멀리즘 |
| `charlie` | charlie-munger | 의사결정, 멘탈 모델, 역발상 |
| `karpathy` | andrej-karpathy | AI/SW 패러다임, 바이브 코딩, 기술적 직관 |

**본인의 멘토 추가하기**

플러그인 디렉토리(`~/.claude/plugins/team-newrich/`)의 `agents/` 폴더에 `<mentor-name>.md`를 추가한다. 형식은 기존 멘토 파일(`agents/charlie-munger.md` 등) 참고. frontmatter + Role + Frameworks + 응답 절차 구성. 추가 후 새 세션 시작하면 자동 인식.

### 3) 호출

```
/ask charlie 지금 회사 그만두고 창업할지 말지
/ask naval 프리랜서 vs 풀타임 중 나에게 맞는 쪽이 어디인지

/debate naval charlie "사이드 프로젝트 키울지, 본업에 더 집중할지"
/debate tim kepano "도구를 더 늘릴지, 줄일지" 3

/council "이번 분기 무엇을 가장 우선해야 할지"
/council "이 프로젝트 접을지" naval charlie kepano
```

자연어로 불러도 된다 — `"멍거한테 이번 결정 어떻게 보는지 물어봐줘"` 같은 식. Claude가 적절한 스킬을 골라서 실행.

## 한계

- 멘토는 실제 인물의 발언을 학습한 가상 페르소나. 실존 인물의 의견과 다를 수 있다
- `our-situation.md`가 없거나 부실하면 답변도 일반론에 그친다
- 멘토 추가는 수동 (`agents/` 폴더에 직접 .md 추가)

## 구조

```
.claude-plugin/
├── marketplace.json   # 마켓플레이스 메타
└── plugin.json        # 플러그인 메타
agents/
├── tim-ferriss.md     # 멘토 에이전트 (frontmatter + Role + Frameworks + 응답 절차)
├── naval-ravikant.md
├── kepano.md
├── charlie-munger.md
├── andrej-karpathy.md
└── references/        # 멘토별 deep reference (에이전트 호출 시 참조)
skills/
├── ask/SKILL.md
├── debate/SKILL.md
└── council/SKILL.md
docs/specs/            # 스킬·에이전트 SSOT
```

자세한 동작은 [SKILL.md](./skills/ask/SKILL.md) / [agents.md](./docs/specs/agents.md) / [skills.md](./docs/specs/skills.md).

## 라이선스

[MIT](./LICENSE)

## 크레딧

- 원작 컨셉 & 멘토 큐레이션: [@lazyyoyo](https://github.com/lazyyoyo), [@jojo-dan](https://github.com/jojo-dan)
- Team Moomoo (lazyyoyo + jojo) 공동 운영
