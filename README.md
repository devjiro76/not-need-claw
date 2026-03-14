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

## All 37 Use Cases

### Social Media (4)
| Use Case | File | Description |
|---|---|---|
| Daily Reddit Digest | [`daily-reddit-digest.md`](usecases/daily-reddit-digest.md) | Curated daily summary of top posts from your favorite subreddits |
| Daily YouTube Digest | [`daily-youtube-digest.md`](usecases/daily-youtube-digest.md) | Daily summaries of new videos from channels you follow |
| X Account Analysis | [`x-account-analysis.md`](usecases/x-account-analysis.md) | Qualitative analysis of your X/Twitter account performance |
| Multi-Source Tech News | [`multi-source-tech-news-digest.md`](usecases/multi-source-tech-news-digest.md) | Aggregate and score tech news from 109+ sources (RSS, X, GitHub, web) |

### Creative & Building (5)
| Use Case | File | Description |
|---|---|---|
| Goal-Driven Tasks | [`overnight-mini-app-builder.md`](usecases/overnight-mini-app-builder.md) | Brain dump goals, agent autonomously generates daily tasks and builds mini-apps overnight |
| YouTube Content Pipeline | [`youtube-content-pipeline.md`](usecases/youtube-content-pipeline.md) | Automate video idea scouting, research, and tracking for a YouTube channel |
| Content Factory | [`content-factory.md`](usecases/content-factory.md) | Multi-agent content pipeline — research, writing, and design agents in dedicated channels |
| Game Dev Pipeline | [`autonomous-game-dev-pipeline.md`](usecases/autonomous-game-dev-pipeline.md) | Full lifecycle management of educational game development with git workflow |
| Podcast Pipeline | [`podcast-production-pipeline.md`](usecases/podcast-production-pipeline.md) | End-to-end podcast production — guest research, outlines, show notes, social promo |

### Infrastructure & DevOps (2)
| Use Case | File | Description |
|---|---|---|
| n8n Orchestration | [`n8n-workflow-orchestration.md`](usecases/n8n-workflow-orchestration.md) | Delegate API calls to n8n workflows via webhooks — agent never touches credentials |
| Self-Healing Server | [`self-healing-home-server.md`](usecases/self-healing-home-server.md) | Always-on infrastructure agent with SSH, automated health checks, and self-healing |

### Productivity (18)
| Use Case | File | Description |
|---|---|---|
| Project Management | [`autonomous-project-management.md`](usecases/autonomous-project-management.md) | Decentralized multi-agent project coordination via STATE.yaml pattern |
| Customer Service | [`multi-channel-customer-service.md`](usecases/multi-channel-customer-service.md) | Unified AI inbox across WhatsApp, Instagram, Email, and Google Reviews |
| Phone Assistant | [`phone-based-personal-assistant.md`](usecases/phone-based-personal-assistant.md) | Access your AI agent via phone calls — hands-free voice assistance |
| Inbox Declutter | [`inbox-declutter.md`](usecases/inbox-declutter.md) | Summarize newsletters into a daily digest email |
| Personal CRM | [`personal-crm.md`](usecases/personal-crm.md) | Auto-discover and track contacts from email and calendar with natural language queries |
| Health Tracker | [`health-symptom-tracker.md`](usecases/health-symptom-tracker.md) | Track food intake and symptoms to identify triggers, with scheduled check-ins |
| Multi-Channel Assistant | [`multi-channel-assistant.md`](usecases/multi-channel-assistant.md) | Route tasks across Telegram, Slack, email, and calendar from a single assistant |
| Project State | [`project-state-management.md`](usecases/project-state-management.md) | Event-driven project tracking with automatic context capture |
| Dynamic Dashboard | [`dynamic-dashboard.md`](usecases/dynamic-dashboard.md) | Real-time dashboard with parallel data fetching from APIs, databases, and social media |
| Todoist Manager | [`todoist-task-manager.md`](usecases/todoist-task-manager.md) | Sync agent reasoning and progress logs to Todoist for transparency |
| Family Calendar | [`family-calendar-household-assistant.md`](usecases/family-calendar-household-assistant.md) | Aggregate family calendars into morning briefings and manage household inventory |
| Multi-Agent Team | [`multi-agent-team.md`](usecases/multi-agent-team.md) | Run specialized agents (strategy, dev, marketing) as a coordinated team |
| Morning Brief | [`custom-morning-brief.md`](usecases/custom-morning-brief.md) | Customized daily briefing — news, tasks, content drafts, AI-recommended actions |
| Meeting Notes | [`meeting-notes-action-items.md`](usecases/meeting-notes-action-items.md) | Turn meeting transcripts into structured summaries and auto-create tasks in Jira/Linear |
| Habit Tracker | [`habit-tracker-accountability-coach.md`](usecases/habit-tracker-accountability-coach.md) | Proactive daily check-ins that track habits, maintain streaks, and adapt their tone |
| Second Brain | [`second-brain.md`](usecases/second-brain.md) | Text anything to remember, search everything later — zero-friction capture system |
| Event Confirmation | [`event-guest-confirmation.md`](usecases/event-guest-confirmation.md) | AI phone calls to confirm guest attendance and compile summary |
| Phone Notifications | [`phone-call-notifications.md`](usecases/phone-call-notifications.md) | Turn agent alerts into real phone calls — morning briefings, price drops, urgent emails |

### Research & Learning (7)
| Use Case | File | Description |
|---|---|---|
| Earnings Tracker | [`earnings-tracker.md`](usecases/earnings-tracker.md) | Track tech/AI earnings reports with automated previews, alerts, and summaries |
| Knowledge Base (RAG) | [`knowledge-base-rag.md`](usecases/knowledge-base-rag.md) | Build a searchable knowledge base by dropping URLs, tweets, and articles into chat |
| Market Research | [`market-research-product-factory.md`](usecases/market-research-product-factory.md) | Mine Reddit and X for real pain points, then have your agent build MVPs |
| Idea Validator | [`pre-build-idea-validator.md`](usecases/pre-build-idea-validator.md) | Scan GitHub, HN, npm, PyPI before building — stop if crowded, proceed if open |
| Semantic Memory | [`semantic-memory-search.md`](usecases/semantic-memory-search.md) | Add vector-powered semantic search to your agent's markdown memory files |
| arXiv Reader | [`arxiv-paper-reader.md`](usecases/arxiv-paper-reader.md) | Read and analyze arXiv papers conversationally — fetch, browse, compare, summarize |
| LaTeX Writing | [`latex-paper-writing.md`](usecases/latex-paper-writing.md) | Write and compile LaTeX papers conversationally with instant PDF preview |

### Finance (1)
| Use Case | File | Description |
|---|---|---|
| Polymarket Autopilot | [`polymarket-autopilot.md`](usecases/polymarket-autopilot.md) | Automated paper trading on prediction markets with backtesting and daily reports |

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
