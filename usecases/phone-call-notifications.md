> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Phone Call Notifications

Your agent already monitors things for you — stocks, emails, smart home, calendars — but notifications are easy to ignore. Push notifications pile up. Chat messages get buried. For the stuff that actually matters, you need something you can't swipe away.

This use case gives your agent a phone call as a notification channel. When something is urgent enough, the agent dials your real phone number, tells you what's going on, and you can talk back. Two-way conversation, not a robocall.

## What It Does

- Agent decides something is worth your attention (price alert, urgent email, appointment reminder, anything)
- Agent calls your phone via a voice calling API service — no complex telephony setup needed
- You pick up, hear the alert, and can ask follow-up questions in real time
- Call ends when the conversation is done

The key idea: the agent calls YOU. You don't call the agent. This works with scheduled checks, cron jobs, or any trigger — the agent evaluates whether something is phone-call-worthy and acts on it.

## Why This Works

AI agents already have initiative — scheduled tasks, cron, event triggers. But their output channels are limited to chat platforms you might not be checking. A phone call is the one notification channel that reliably gets your attention, especially when you're away from your desk.

A managed voice calling service handles the telephony infrastructure. You configure the API credentials and the agent gains the ability to call. No phone number provisioning or webhook configuration needed with managed services.

## Skills Needed

A voice calling service. Options include:

- **Managed (easiest setup)**:
  - [Bland.ai](https://www.bland.ai/) — API-first AI phone calls, minimal configuration
  - [Vapi](https://vapi.ai/) — voice AI platform with easy integration
  - [Retell AI](https://www.retellai.com/) — conversational voice API
- **DIY (more control)**:
  - [Twilio Voice](https://www.twilio.com/docs/voice) + [OpenAI Realtime API](https://platform.openai.com/docs/guides/realtime) — requires Twilio account, phone number, and webhook setup

That's it. No other dependencies. Configure the API key and the agent figures out the rest.

## Example: Morning Briefing Call

Set up a cron job that calls you every morning with a personalized briefing:

```text
Every weekday at 7:30 AM, call me with a morning briefing. Include:
- Weather forecast for my city
- My calendar for today
- Any urgent emails that came in overnight
- Top 3 news headlines relevant to my interests

Keep it concise — aim for under 2 minutes. If I ask questions, answer them.
If I don't pick up, don't retry.
```

## Example: Price Alert

Tell the agent what to watch and when to call:

```text
Monitor NVDA stock price. If it drops more than 5% in a single day,
call me immediately and tell me what happened. Include any relevant
news that might explain the drop.
```

## Example: Urgent Email Filter

```text
During business hours, check my inbox every 15 minutes.
If you see an email from my boss or any email marked urgent,
call me with a summary. For everything else, just send a chat message.
```

## Key Insights

- **Don't overuse it.** The whole point is that a phone call means "this actually matters." If your agent calls you 10 times a day, you'll start ignoring it. Set clear thresholds for what's call-worthy vs chat-worthy.
- **Pair with scheduled checks or cron.** The voice service is the delivery channel — you still need a trigger. Scheduled checks (every 30 min) work for monitoring tasks. Cron jobs work for scheduled briefings.
- **Two-way conversation.** Unlike a push notification, you can ask follow-up questions on the call. "Wait, which email?" or "What's the current price now?" — the agent responds in real time.
- **Fast model for calls.** Phone conversations need quick responses. Use a fast model (Haiku-class) for the voice interaction. The thinking sound covers latency, but faster is always better.
- **Privacy.** Check your voice service's data retention policies. Prefer services that don't store recordings or transcripts, with audio encrypted in transit and discarded after processing.

## Related Links

- [Twilio Voice API](https://www.twilio.com/docs/voice)
- [OpenAI Realtime API](https://platform.openai.com/docs/guides/realtime)
- [Bland.ai](https://www.bland.ai/)
- [Vapi](https://vapi.ai/)
- [Retell AI](https://www.retellai.com/)
