> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Event Guest Confirmation

You're hosting an event — a dinner party, a wedding, a company offsite — and you need to confirm attendance from a list of guests. Manually calling 20+ people is tedious: you play phone tag, forget who said what, and lose track of dietary restrictions or plus-ones. Texting works sometimes, but people ignore messages. A real phone call gets a much higher response rate.

This use case has an AI agent call each guest on your list using a voice calling service, confirm whether they're attending, collect any notes, and compile everything into a summary for you.

## What It Does

- Iterates through a guest list (names + phone numbers) and calls each one
- The AI introduces itself as your event coordinator with a friendly persona
- Confirms the event date, time, and location with the guest
- Asks if they're attending, and collects any notes (dietary needs, plus-ones, arrival time, etc.)
- After all calls are complete, compiles a summary: who confirmed, who declined, who didn't pick up, and any notes

## Voice Calling Approach

For automated phone calls, you need a voice AI service that can make outbound calls. Key considerations:

- **Sandboxed persona**: The AI on the call should only have access to the context you provide (persona name, goal, opening line). It should not have access to your main agent, files, or other tools.
- **Safety**: The person on the other end of the call can't manipulate or access your agent through the conversation. There's no risk of prompt injection or data leakage.
- **Better conversations**: Because the AI is scoped to a single focused task (confirm attendance), it stays on-topic and handles the call more naturally than a general-purpose voice agent would.
- **Batch-friendly**: You're making many calls to different people. A sandboxed persona that resets per call is exactly what you want — no bleed-over between conversations.

## Skills You Need

- A voice calling API or service. Options include:
  - [Twilio Voice](https://www.twilio.com/docs/voice) + [OpenAI Realtime API](https://platform.openai.com/docs/guides/realtime) for a DIY solution
  - [Bland.ai](https://www.bland.ai/) — managed AI phone calls API
  - [Vapi](https://vapi.ai/) — voice AI platform for building phone agents
  - [Retell AI](https://www.retellai.com/) — conversational voice API
- A Twilio account with a phone number (for making outbound calls, if using Twilio directly)
- An LLM API key for the voice AI model
- ngrok (for webhook tunneling if needed — free tier works)

## How to Set It Up

1. Choose and configure your voice calling service. Set up API keys, phone numbers, and webhook endpoints as needed.

2. Prepare your guest list. You can paste it directly in chat or keep it in a file:

```text
Guest List — Summer BBQ, Saturday June 14th, 4 PM, 23 Oak Street

- Sarah Johnson: +15551234567
- Mike Chen: +15559876543
- Rachel Torres: +15555551234
- David Kim: +15558887777
```

3. Prompt your AI agent:

```text
I need you to confirm attendance for my event. Here are the details:

Event: Summer BBQ
Date: Saturday, June 14th at 4 PM
Location: 23 Oak Street

Here is my guest list:
<paste your guest list here>

For each guest, use the voice calling API to call them. Use the persona "Jamie, event
coordinator for [your name]". The goal for each call is to confirm whether they're
attending, and note any dietary restrictions, plus-ones, or other comments.

After each call, log the result. Once all calls are done, give me a full summary:
- Who confirmed
- Who declined
- Who didn't answer
- Any notes or special requests from each guest
```

4. The agent will call each guest one by one, then compile the results. You can check in on progress at any time by asking for a status update.

## Key Insights

- **Start with a small test**: Try it with 2-3 guests first to make sure the persona and opening line sound right. You can adjust the tone before calling the full list.
- **Be mindful of calling hours**: Don't schedule calls too early or too late. You can tell the agent to only call between certain hours.
- **Review transcripts**: Most voice AI services log transcripts. Skim through them after the first batch to see how conversations went.
- **No-answer handling**: If someone doesn't pick up, the agent can note it and you can decide whether to retry later or follow up by text.
- **Real phone calls cost money**: Each call uses Twilio minutes (or equivalent service credits). Set appropriate limits, especially for large guest lists.

## Related Links

- [Twilio Voice API](https://www.twilio.com/docs/voice)
- [OpenAI Realtime API](https://platform.openai.com/docs/guides/realtime)
- [Bland.ai](https://www.bland.ai/)
- [Vapi](https://vapi.ai/)
- [Retell AI](https://www.retellai.com/)
- [ngrok](https://ngrok.com)
