# not-need-claw

> You don't need OpenClaw. You just need a capable AI agent.

[awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases)의 40개 유즈케이스를 분석한 결과, **92.5%가 OpenClaw 없이도 동작** 가능했습니다. 이 레포는 OpenClaw 의존성을 제거한 37개 유즈케이스를 **컨텍스트 효율적인 스킬 구조**로 재구성한 것입니다.

## Why This Exists

원본 레포의 유즈케이스들은 "OpenClaw 스킬"로 포장되어 있지만, 실제 의존하는 건:

| 기능 | 실체 | 아무 에이전트에서 |
|---|---|---|
| `clawhub install reddit-readonly` | Reddit API 래퍼 | WebFetch / MCP / curl |
| OpenClaw 메모리 | 텍스트 저장 + 검색 | 파일 / SQLite / 벡터 DB |
| SSH 접근 | 쉘 커맨드 실행 | Bash / 터미널 |
| `sessions_spawn` | 서브에이전트 | Agent tool / CrewAI / AutoGen |
| `HEARTBEAT.md` | 스케줄링 | cron / launchd |

**OpenClaw 고유 기능은 하나도 없습니다.** 프롬프트 패턴과 워크플로우 아이디어가 가치의 본질입니다.

## Architecture: Index Skill Pattern

```
not-need-claw/
├── SKILL.md          # Index skill (~1,200 tokens)
└── usecases/         # 37 use cases (loaded on-demand)
    ├── second-brain.md
    ├── self-healing-home-server.md
    └── ... (35 more)
```

### Why not a single giant file?

| Approach | Context cost per invocation | Practical? |
|---|---|---|
| 37개를 1파일에 몰아넣기 | **~30,000 tokens** (every time) | No |
| 37개를 개별 스킬로 분리 | Skill list bloat + 37 trigger descriptions | Messy |
| **Index skill + on-demand files** | **~1,200 tokens** (index) + **~800 tokens** (selected file) | **Yes** |

**Index Skill Pattern**의 핵심:

1. **SKILL.md는 목차만** — 카테고리별 한줄 설명 + 파일명. ~1,200 tokens.
2. **유즈케이스는 별도 파일** — 사용자가 선택하면 해당 파일 하나만 Read. ~800 tokens.
3. **총 비용 ~2,000 tokens** — monolithic 대비 **93% 절약**.

스킬이 트리거될 때마다 전체 프롬프트가 컨텍스트에 주입되는 구조에서, 이 패턴은 "필요한 것만 로드"를 가능하게 합니다.

## Categories

| Category | Count | Examples |
|---|---|---|
| Social Media | 4 | Reddit/YouTube digest, X analysis |
| Creative & Building | 5 | Podcast pipeline, game dev, content factory |
| Infrastructure & DevOps | 2 | Self-healing server, n8n orchestration |
| Productivity | 18 | Second brain, CRM, meeting notes, habit tracker |
| Research & Learning | 7 | arXiv reader, RAG knowledge base, idea validator |
| Finance | 1 | Polymarket autopilot |

## Analysis Summary

Original repo: **40 use cases**

| Classification | Count | % |
|---|---|---|
| **Agent-agnostic** (works with any AI agent) | 20 | 50% |
| **Partial** (swap one skill/tool, works anywhere) | 17 | 42.5% |
| **OpenClaw-dependent** (excluded) | 3 | 7.5% |

Excluded (genuinely require OpenClaw):
- `aionui-cowork-desktop` — OpenClaw desktop gateway wrapper
- `local-crm-framework` (DenchClaw) — OpenClaw profile/gateway coupled
- `x-twitter-automation` (TweetClaw) — OpenClaw plugin system distribution

## Usage

As a **Claude Code skill**:
```bash
# Point your skill config to this directory
# Then invoke: /agent-usecases
```

As a **reference library**:
```bash
# Browse usecases/ directly
cat usecases/second-brain.md
```

## Credits

All use case content originated from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases) by [@hesamsheikh](https://github.com/hesamsheikh) and community contributors. This repo adapts that content by removing platform-specific dependencies while preserving the workflow patterns and prompts that make each use case valuable.

## License

Following the original repo's license. See [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases) for details.
