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

## 전체 37개 유즈케이스

### Social Media (4)
| 유즈케이스 | 파일 | 설명 |
|---|---|---|
| Daily Reddit Digest | [`daily-reddit-digest.md`](usecases/daily-reddit-digest.md) | 즐겨찾는 서브레딧 인기 게시물 일일 요약 |
| Daily YouTube Digest | [`daily-youtube-digest.md`](usecases/daily-youtube-digest.md) | 구독 채널 신규 영상 일일 요약 |
| X Account Analysis | [`x-account-analysis.md`](usecases/x-account-analysis.md) | X 계정 정성 분석 |
| Multi-Source Tech News | [`multi-source-tech-news-digest.md`](usecases/multi-source-tech-news-digest.md) | 109+ 소스에서 기술 뉴스 수집·점수화 |

### Creative & Building (5)
| 유즈케이스 | 파일 | 설명 |
|---|---|---|
| Goal-Driven Tasks | [`overnight-mini-app-builder.md`](usecases/overnight-mini-app-builder.md) | 목표를 쏟아내면 에이전트가 자율적으로 일일 태스크 생성 + 미니앱 빌드 |
| YouTube Content Pipeline | [`youtube-content-pipeline.md`](usecases/youtube-content-pipeline.md) | 영상 아이디어 탐색·리서치·추적 자동화 |
| Content Factory | [`content-factory.md`](usecases/content-factory.md) | 멀티에이전트 콘텐츠 파이프라인 — 리서치·작성·디자인 에이전트가 전용 채널에서 협업 |
| Game Dev Pipeline | [`autonomous-game-dev-pipeline.md`](usecases/autonomous-game-dev-pipeline.md) | 교육용 게임 개발 전체 라이프사이클 + git 워크플로우 |
| Podcast Pipeline | [`podcast-production-pipeline.md`](usecases/podcast-production-pipeline.md) | 팟캐스트 제작 전 과정 — 게스트 리서치, 대본, 쇼노트, 소셜 홍보 |

### Infrastructure & DevOps (2)
| 유즈케이스 | 파일 | 설명 |
|---|---|---|
| n8n Orchestration | [`n8n-workflow-orchestration.md`](usecases/n8n-workflow-orchestration.md) | n8n으로 API 호출 위임 — 에이전트가 직접 자격증명을 다루지 않음 |
| Self-Healing Server | [`self-healing-home-server.md`](usecases/self-healing-home-server.md) | 상시 인프라 에이전트 — SSH, 자동 헬스체크, 자가복구 |

### Productivity (18)
| 유즈케이스 | 파일 | 설명 |
|---|---|---|
| Project Management | [`autonomous-project-management.md`](usecases/autonomous-project-management.md) | STATE.yaml 패턴으로 멀티에이전트 분산 프로젝트 관리 |
| Customer Service | [`multi-channel-customer-service.md`](usecases/multi-channel-customer-service.md) | WhatsApp·Instagram·Email·Google Reviews 통합 AI 고객 응대 |
| Phone Assistant | [`phone-based-personal-assistant.md`](usecases/phone-based-personal-assistant.md) | 전화로 AI 에이전트 접근 — 핸즈프리 음성 비서 |
| Inbox Declutter | [`inbox-declutter.md`](usecases/inbox-declutter.md) | 뉴스레터를 요약해서 일일 다이제스트 이메일로 발송 |
| Personal CRM | [`personal-crm.md`](usecases/personal-crm.md) | 이메일·캘린더에서 연락처 자동 발견 + 자연어 쿼리 |
| Health Tracker | [`health-symptom-tracker.md`](usecases/health-symptom-tracker.md) | 식사·증상 기록으로 트리거 패턴 분석 + 정기 체크인 |
| Multi-Channel Assistant | [`multi-channel-assistant.md`](usecases/multi-channel-assistant.md) | Telegram·Slack·이메일·캘린더를 하나의 비서로 통합 |
| Project State | [`project-state-management.md`](usecases/project-state-management.md) | 이벤트 기반 프로젝트 추적 — 자동 컨텍스트 캡처 |
| Dynamic Dashboard | [`dynamic-dashboard.md`](usecases/dynamic-dashboard.md) | API·DB·소셜미디어를 병렬 수집하는 실시간 대시보드 |
| Todoist Manager | [`todoist-task-manager.md`](usecases/todoist-task-manager.md) | 에이전트 사고 과정과 진행 로그를 Todoist에 동기화 |
| Family Calendar | [`family-calendar-household-assistant.md`](usecases/family-calendar-household-assistant.md) | 가족 캘린더 통합 아침 브리핑 + 가사 재고 관리 |
| Multi-Agent Team | [`multi-agent-team.md`](usecases/multi-agent-team.md) | 전략·개발·마케팅 전문 에이전트를 팀으로 운영 |
| Morning Brief | [`custom-morning-brief.md`](usecases/custom-morning-brief.md) | 맞춤 아침 브리핑 — 뉴스, 태스크, 콘텐츠 초안, AI 추천 액션 |
| Meeting Notes | [`meeting-notes-action-items.md`](usecases/meeting-notes-action-items.md) | 회의 녹취록 → 구조화된 요약 + Jira/Linear 태스크 자동 생성 |
| Habit Tracker | [`habit-tracker-accountability-coach.md`](usecases/habit-tracker-accountability-coach.md) | 능동적 일일 체크인 — 습관 추적, 스트릭 관리, 톤 자동 조절 |
| Second Brain | [`second-brain.md`](usecases/second-brain.md) | 아무거나 텍스트로 기억시키고, 나중에 검색 — 제로 마찰 캡처 |
| Event Confirmation | [`event-guest-confirmation.md`](usecases/event-guest-confirmation.md) | AI 전화로 게스트 참석 확인 + 요약 자동 정리 |
| Phone Notifications | [`phone-call-notifications.md`](usecases/phone-call-notifications.md) | 에이전트 알림을 실제 전화로 — 아침 브리핑, 가격 하락, 긴급 이메일 |

### Research & Learning (7)
| 유즈케이스 | 파일 | 설명 |
|---|---|---|
| Earnings Tracker | [`earnings-tracker.md`](usecases/earnings-tracker.md) | AI·테크 실적 발표 자동 추적 — 프리뷰, 알림, 상세 요약 |
| Knowledge Base (RAG) | [`knowledge-base-rag.md`](usecases/knowledge-base-rag.md) | URL·기사·트윗을 채팅에 던지면 검색 가능한 지식 베이스 구축 |
| Market Research | [`market-research-product-factory.md`](usecases/market-research-product-factory.md) | Reddit·X에서 페인포인트 발굴 → 에이전트가 MVP 빌드 |
| Idea Validator | [`pre-build-idea-validator.md`](usecases/pre-build-idea-validator.md) | 빌드 전 GitHub·HN·npm·PyPI 스캔 — 레드오션이면 중단, 블루오션이면 진행 |
| Semantic Memory | [`semantic-memory-search.md`](usecases/semantic-memory-search.md) | 마크다운 메모리 파일에 벡터 기반 시맨틱 검색 추가 |
| arXiv Reader | [`arxiv-paper-reader.md`](usecases/arxiv-paper-reader.md) | arXiv 논문을 대화형으로 읽기·분석·비교·요약 |
| LaTeX Writing | [`latex-paper-writing.md`](usecases/latex-paper-writing.md) | 대화형 LaTeX 논문 작성 + 즉시 PDF 프리뷰 |

### Finance (1)
| 유즈케이스 | 파일 | 설명 |
|---|---|---|
| Polymarket Autopilot | [`polymarket-autopilot.md`](usecases/polymarket-autopilot.md) | 예측 시장 자동 페이퍼 트레이딩 — 백테스팅 + 일일 리포트 |

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
