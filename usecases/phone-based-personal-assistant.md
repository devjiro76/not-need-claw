> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Phone-Based Personal Assistant

## Pain Point

You want to access your AI agent from any phone without needing a smartphone app or internet browser. You need hands-free voice assistance while driving, walking, or when your hands are occupied.

## What It Does

By integrating a telephony provider (such as Telnyx, Twilio, or Vonage) with your AI agent, you can receive and make phone calls, turning any phone into a gateway to your AI assistant. You can:
- Call a phone number to speak with your AI agent via voice
- Get calendar reminders, Jira updates, and web search results via voice
- Use reliable phone connectivity through a telephony API

SMS support can be added via the same telephony provider.

## Prompts

```
You are available via phone. When I call, greet me and ask how I can help.

For calendar queries: "What's on my calendar today?"
For Jira updates: "Show me my open tickets"
For web search: "Search for latest news on AI agents"
```

## Tools Needed

- A telephony integration (e.g., [Telnyx](https://telnyx.com/), [Twilio](https://www.twilio.com/), or [Vonage](https://www.vonage.com/)) -- connect via their API or an MCP server
- Calendar integration (Google Calendar or Outlook -- via MCP server, npm package, or direct API)
- Jira integration (via MCP server or direct API)
- Web search capability (via MCP server or search API)

## Related Links

- [Telnyx API](https://telnyx.com/)
- [Twilio Voice API](https://www.twilio.com/docs/voice)
- [Vonage Voice API](https://developer.vonage.com/en/voice/voice-api/overview)
