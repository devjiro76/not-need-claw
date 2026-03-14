> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Health & Symptom Tracker

Identifying food sensitivities requires consistent logging over time, which is tedious to maintain. You need reminders to log and analysis to spot patterns.

This workflow tracks food and symptoms automatically:

- Message your food and symptoms in a dedicated chat channel and the AI agent logs everything with timestamps
- 3x daily reminders (morning, midday, evening) prompt you to log meals
- Over time, analyzes patterns to identify potential triggers

## Tools you Need

- Cron jobs for reminders
- A messaging channel for logging (Telegram, Slack, Discord, etc.)
- File or database storage for the health log

## How to Set it Up

1. Create a messaging topic/channel called "health-tracker" (or similar).
2. Create a log file: `~/agent-data/health-log.md`
3. Instruct your AI agent:
```text
When I message in the "health-tracker" topic:
1. Parse the message for food items and symptoms
2. Log to ~/agent-data/health-log.md with timestamp
3. Confirm what was logged

Set up 3 daily reminders:
- 8 AM: "Log your breakfast"
- 1 PM: "Log your lunch"
- 7 PM: "Log your dinner and any symptoms"

Every Sunday, analyze the past week's log and identify patterns:
- Which foods correlate with symptoms?
- Are there time-of-day patterns?
- Any clear triggers?

Post the analysis to the health-tracker topic.
```

4. Optional: Add a preferences/triggers file (e.g., `~/agent-data/health-triggers.json`) for the agent to track known triggers and update it as patterns emerge.

> **Note on storage**: Instead of platform-specific memory, use a local markdown file, JSON file, or SQLite database that your agent can read and write to persist health data across sessions.
