> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Personal CRM with Automatic Contact Discovery

Keeping track of who you've met, when, and what you discussed is impossible to do manually. Important follow-ups slip through the cracks, and you forget context before important meetings.

This workflow builds and maintains a personal CRM automatically:

- Daily cron job scans email and calendar for new contacts and interactions
- Stores contacts in a structured database with relationship context
- Natural language queries: "What do I know about [person]?", "Who needs follow-up?", "When did I last talk to [person]?"
- Daily meeting prep briefing: before each day's meetings, researches external attendees via CRM + email history and delivers a briefing

## Tools you Need

- Gmail and Google Calendar access (e.g., `gog` CLI, a Google Workspace MCP server, or direct API integration)
- A CRM database (SQLite, PostgreSQL, or similar)
- A messaging channel for CRM queries (Telegram, Slack, Discord, etc.)

## How to Set it Up

1. Create a CRM database:
```sql
CREATE TABLE contacts (
  id INTEGER PRIMARY KEY,
  name TEXT,
  email TEXT,
  first_seen TEXT,
  last_contact TEXT,
  interaction_count INTEGER,
  notes TEXT
);
```

2. Set up a messaging topic/channel called "personal-crm" for queries.

3. Instruct your AI agent:
```text
Run a daily cron job at 6 AM to:
1. Scan my Gmail and Calendar for the past 24 hours
2. Extract new contacts and update existing ones
3. Log interactions (meetings, emails) with timestamps and context

Also, every morning at 7 AM:
1. Check my calendar for today's meetings
2. For each external attendee, search my CRM and email history
3. Deliver a briefing to the messaging channel with: who they are, when we last spoke, what we discussed, and any follow-up items

When I ask about a contact in the personal-crm topic, search the database and give me everything you know.
```
