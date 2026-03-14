> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Multi-Agent Content Factory

You're a content creator juggling research, writing, and design across multiple platforms. Each step — finding trending topics, writing scripts, generating thumbnails — eats hours of your day. What if a team of specialized agents handled all of it overnight?

This workflow sets up a multi-agent content factory inside Discord, where different agents handle research, writing, and visual assets in dedicated channels.

## What It Does

- **Research Agent** scans trending stories, competitor content, and social media for the best content opportunities each morning
- **Writing Agent** takes the top ideas and writes full scripts, threads, or newsletter drafts
- **Thumbnail Agent** generates AI thumbnails or cover images for the content
- Each agent works in its own Discord channel, keeping everything organized and reviewable
- Runs automatically on a schedule (e.g., daily at 8 AM) so you wake up to finished content

## Pain Point

Content creation has three phases — research, writing, and design — and most creators are doing all three manually. Even with AI writing tools, you still have to prompt them one at a time. This system chains agents together in a pipeline where one agent's output feeds the next, completely hands-free.

## Skills You Need

- Discord integration with multiple channels
- Sub-agent / parallel task orchestration for multi-agent pipelines
- X/Twitter research integration (e.g., a custom MCP tool or API wrapper)
- Local image generation (e.g., Nano Banana) or an image generation API
- Knowledge-base / RAG skill (optional, for retrieval-augmented research)

> **Note:** The original workflow references `clawhub.ai` skills (`x-research-v2`, `knowledge-base`). You can replace these with any equivalent X/Twitter search API wrapper and any RAG/vector-search tool.

## How to Set It Up

1. Set up a Discord server (or ask the AI agent to do it for you — just say "Set up a Discord for us").

2. Create channels for each agent:
   - `#research` — trending topics and content opportunities
   - `#scripts` — written drafts and outlines
   - `#thumbnails` — generated images and cover art

3. Prompt the AI agent:
```text
I want you to build me a content factory inside of Discord.
Set up channels for different agents:

1. Research Agent (#research): Every morning at 8 AM, research top trending
   stories, competitor content, and what's performing well on social media
   in my niche. Post the top 5 content opportunities with sources.

2. Writing Agent (#scripts): Take the best idea from the research agent
   and write a full script/thread/newsletter draft. Post it in #scripts.

3. Thumbnail Agent (#thumbnails): Generate AI thumbnails or cover images
   for the content. Post them in #thumbnails.

Have all their work organized in different channels.
Run this pipeline automatically every morning.
```

4. Customize for your platform:
```text
I focus on X/Twitter threads, not YouTube. Change the writing agent
to produce tweet threads instead of video scripts.
```

## Key Insights

- The power is in the **chained agents** — research feeds writing, writing feeds thumbnails. You don't prompt each step individually.
- Discord channels make it easy to review each agent's work separately and give feedback like "scripts are too long" or "focus more on AI news."
- You can adapt this for any content format: tweets, newsletters, LinkedIn posts, podcast outlines, blog articles.
- Running a local model for image generation (like Nano Banana on a Mac Studio) keeps costs down and gives you more control.

## Based On

Inspired by [Alex Finn's video on life-changing AI agent use cases](https://www.youtube.com/watch?v=41_TNGDDnfQ).

## Related Links

- [Claude Code Subagent Patterns](https://github.com/anthropics/claude-code)
- [Discord Bot Setup](https://discord.com/developers/docs)
