> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Multi-Source Tech News Digest

Automatically aggregate, score, and deliver tech news from 109+ sources across RSS, Twitter/X, GitHub releases, and web search — all managed through natural language.

## Pain Point

Staying updated across AI, open-source, and frontier tech requires checking dozens of RSS feeds, Twitter accounts, GitHub repos, and news sites daily. Manual curation is time-consuming, and most existing tools either lack quality filtering or require complex configuration.

## What It Does

A four-layer data pipeline that runs on a schedule:

1. **RSS Feeds** (46 sources) — OpenAI, Hacker News, MIT Tech Review, etc.
2. **Twitter/X KOLs** (44 accounts) — @karpathy, @sama, @VitalikButerin, etc.
3. **GitHub Releases** (19 repos) — vLLM, LangChain, Ollama, Dify, etc.
4. **Web Search** (4 topic searches) — via Brave Search API

All articles are merged, deduplicated by title similarity, and quality-scored (priority source +3, multi-source +5, recency +2, engagement +1). The final digest is delivered to Discord, email, or Telegram.

The framework is fully customizable — add your own RSS feeds, Twitter handles, GitHub repos, or search queries in 30 seconds.

## Prompts

**Set up a daily digest:**
```text
Set up a daily tech digest at 9am to Discord #tech-news channel. Also send it to my email at myemail@example.com.

Use the following data sources:
- RSS feeds: fetch from a list of tech blog RSS URLs (I'll provide the list)
- Twitter/X: monitor key accounts using the X API
- GitHub: check releases for repos I follow using the GitHub API
- Web search: use Brave Search API to find trending tech topics

Deduplicate articles by title similarity, score them by relevance, and format a clean digest.
```

**Add custom sources:**
```text
Add these to my tech digest sources:
- RSS: https://my-company-blog.com/feed
- Twitter: @myFavResearcher
- GitHub: my-org/my-framework
```

**Generate on demand:**
```text
Generate a tech digest for the past 24 hours and send it here.
```

## Tools / Services Needed

Instead of a single bundled skill, set up the individual components:

- **RSS parsing** — Use `web_fetch` or an RSS parser library to pull feeds. No special tool needed.
- **Twitter/X monitoring** — Requires `X_BEARER_TOKEN` (X API v2 developer account). Alternatively, use a Twitter MCP server.
- **GitHub releases** — Use the GitHub API directly (or `gh` CLI). A `GITHUB_TOKEN` helps with rate limits.
- **Web search** — Use Brave Search API (`BRAVE_API_KEY`), or any web search MCP server.
- **Delivery** — Discord webhook, email (via Gmail API / SMTP), or Telegram bot API.

## Environment Variables

- `X_BEARER_TOKEN` — Twitter/X API bearer token for KOL monitoring
- `BRAVE_API_KEY` — Brave Search API key for web search layer
- `GITHUB_TOKEN` — GitHub token for higher API rate limits

## Related Links

- [GitHub Repository (original)](https://github.com/draco-agent/tech-news-digest)
