# not-need-claw

> OpenClaw 필요 없습니다. 유능한 AI 에이전트만 있으면 됩니다.

[awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases)의 40개 유즈케이스를 분석한 결과, **92.5%가 OpenClaw 없이도 동작** 가능했습니다. 이 레포는 OpenClaw 의존성을 제거한 37개 유즈케이스를 **컨텍스트 효율적인 스킬 구조**로 재구성한 것입니다.

[English README](README.md)

## 왜 만들었나

원본 레포의 유즈케이스들은 "OpenClaw 스킬"로 포장되어 있지만, 실제 의존하는 건:

| "OpenClaw 기능" | 실체 | 아무 에이전트에서 |
|---|---|---|
| `clawhub install reddit-readonly` | Reddit API 래퍼 | WebFetch / MCP / curl |
| OpenClaw 메모리 | 텍스트 저장 + 검색 | 파일 / SQLite / 벡터 DB |
| SSH 접근 | 쉘 커맨드 실행 | Bash / 터미널 |
| `sessions_spawn` | 서브에이전트 | Agent tool / CrewAI / AutoGen |
| `HEARTBEAT.md` | 스케줄링 | cron / launchd |

**OpenClaw 고유 기능은 하나도 없습니다.** 프롬프트 패턴과 워크플로우 아이디어가 가치의 본질입니다.

## 아키텍처: Index Skill 패턴

```
not-need-claw/
├── SKILL.md          # 인덱스 스킬 (~1,200 토큰)
└── usecases/         # 37개 유즈케이스 (온디맨드 로드)
    ├── second-brain.md
    ├── self-healing-home-server.md
    └── ... (35개 더)
```

### 왜 하나의 거대한 파일이 아닌가?

| 방식 | 호출당 컨텍스트 비용 | 실용적? |
|---|---|---|
| 37개를 1파일에 몰아넣기 | **~30,000 토큰** (매번) | No |
| 37개를 개별 스킬로 분리 | 스킬 목록 비대화 + 37개 트리거 설명 | 지저분함 |
| **인덱스 스킬 + 온디맨드 파일** | **~1,200 토큰** (인덱스) + **~800 토큰** (선택 파일) | **Yes** |

**Index Skill 패턴**의 핵심:

1. **SKILL.md는 목차만** — 카테고리별 한줄 설명 + 파일명. ~1,200 토큰.
2. **유즈케이스는 별도 파일** — 사용자가 선택하면 해당 파일 하나만 Read. ~800 토큰.
3. **총 비용 ~2,000 토큰** — monolithic 대비 **93% 절약**.

스킬이 트리거될 때마다 전체 프롬프트가 컨텍스트에 주입되는 구조에서, 이 패턴은 "필요한 것만 로드"를 가능하게 합니다.

## 카테고리

| 카테고리 | 개수 | 예시 |
|---|---|---|
| Social Media | 4 | Reddit/YouTube 다이제스트, X 분석 |
| Creative & Building | 5 | 팟캐스트 파이프라인, 게임 개발, 콘텐츠 팩토리 |
| Infrastructure & DevOps | 2 | 자가복구 서버, n8n 오케스트레이션 |
| Productivity | 18 | 세컨드 브레인, CRM, 회의록, 습관 트래커 |
| Research & Learning | 7 | arXiv 리더, RAG 지식 베이스, 아이디어 검증 |
| Finance | 1 | Polymarket 오토파일럿 |

## 분석 요약

원본 레포: **40개 유즈케이스**

| 분류 | 개수 | 비율 |
|---|---|---|
| **Agent-agnostic** (아무 AI 에이전트에서 동작) | 20 | 50% |
| **Partial** (스킬 하나만 교체하면 동작) | 17 | 42.5% |
| **OpenClaw-dependent** (제외) | 3 | 7.5% |

제외된 3개 (OpenClaw 필수):
- `aionui-cowork-desktop` — OpenClaw 데스크톱 게이트웨이 래퍼
- `local-crm-framework` (DenchClaw) — OpenClaw 프로필/게이트웨이에 결합
- `x-twitter-automation` (TweetClaw) — OpenClaw 플러그인 시스템으로 배포

## 사용법

**Claude Code 스킬**로 사용:
```bash
# 스킬 설정에서 이 디렉토리를 지정
# 호출: /agent-usecases
```

**레퍼런스 라이브러리**로 사용:
```bash
# usecases/ 직접 탐색
cat usecases/second-brain.md
```

## 크레딧

모든 유즈케이스 콘텐츠는 [@hesamsheikh](https://github.com/hesamsheikh)와 커뮤니티 기여자들의 [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases)에서 유래했습니다. 이 레포는 플랫폼 의존성을 제거하고 워크플로우 패턴과 프롬프트를 보존한 적응 버전입니다.

## 라이선스

원본 레포의 라이선스를 따릅니다. [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases)를 참조하세요.
