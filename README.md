# not-need-claw

> You don't need OpenClaw. You just need a capable AI agent.

We analyzed all 40 use cases from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases) and found that **92.5% work without OpenClaw**. This repo extracts those 37 agent-agnostic use cases into a **context-efficient skill structure**.

[한국어 README](README_KR.md)

## Why This Exists

The original use cases are packaged as "OpenClaw skills", but here's what they actually depend on:

| "OpenClaw Feature" | What It Really Is | Any Agent Can Do It |
|---|---|---|
| `clawhub install reddit-readonly` | Reddit API wrapper | WebFetch / MCP / curl |
| OpenClaw memory | Text storage + search | Files / SQLite / Vector DB |
| SSH access | Shell command execution | Bash / terminal |
| `sessions_spawn` | Sub-agents | Agent tool / CrewAI / AutoGen |
| `HEARTBEAT.md` | Scheduling | cron / launchd |

**None of these are OpenClaw-specific.** The real value is in the prompt patterns and workflow ideas — and those are platform-agnostic.

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
| All 37 in one file | **~30,000 tokens** (every time) | No |
| 37 individual skills | Skill list bloat + 37 trigger descriptions | Messy |
| **Index skill + on-demand files** | **~1,200 tokens** (index) + **~800 tokens** (selected) | **Yes** |

The **Index Skill Pattern** works because:

1. **SKILL.md is just a table of contents** — one-line descriptions + filenames. ~1,200 tokens.
2. **Use cases live in separate files** — only the selected file gets loaded via Read. ~800 tokens.
3. **Total cost ~2,000 tokens** — **93% savings** vs monolithic.

In skill systems where the entire prompt is injected into context on every trigger, this pattern enables "load only what you need".

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
