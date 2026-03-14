> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Inbox De-clutter

Newsletters can take up the inbox like nothing else. Often times they pile-up without being opened at all.

## Tools you Need

Gmail access via one of:
- A Gmail MCP server (e.g., [gmail-mcp](https://github.com/anthropics/anthropic-cookbook/tree/main/misc/gmail_mcp))
- A Gmail npm package or Python library with OAuth
- Direct Gmail API integration

## How to Set it Up

1. [optional] Create a new Gmail account specifically for your AI agent.
2. [optional] Unsubscribe from all newsletters from your main email and subscribe to them using the new email.
3. Set up the Gmail integration and make sure it works.
4. Instruct your AI agent:
```txt
I want you to run a cron job everyday at 8 p.m. to read all the newsletter emails of the past 24 hours and give me a digest of the most important bits along with links to read more. Then ask for my feedback on whether you picked good bits, and update your preferences file (e.g., ~/agent-data/newsletter-prefs.json) based on my preferences for better digests in the future jobs.
```

> **Note on memory/storage**: Instead of platform-specific memory, store user preferences in a local JSON or YAML file, a SQLite database, or any persistent storage your agent can read/write.
