> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Daily YouTube Digest

Start your day with a personalized summary of new videos from your favorite YouTube channels — no more missing content from creators you actually want to follow.

## Pain Point

YouTube notifications are unreliable. You subscribe to channels, but their new videos never show up in your home feed. They're not in notifications. They just... disappear. This doesn't mean you don't want to see them — it means YouTube's algorithm buried them.

Plus: it's fun to start the day with curated content insights instead of doom-scrolling a recommendation feed.

## What It Does

- Fetches the latest videos from a list of your favorite channels
- Summarizes or extracts key insights from each video's transcript
- Delivers a digest to you daily (or on demand)

## Skills You Need

A YouTube transcript/data integration. Options:

- **TranscriptAPI.com** — Sign up at [TranscriptAPI.com](https://transcriptapi.com) for a clean HTTP API. You get **100 free credits on signup**, no credit card required. Use the API key directly in your agent's environment or scripts.
- **yt-dlp** — Free CLI tool, but can be flaky (gets blocked by YouTube, verbose output).
- **YouTube Data API** — Google's official API for channel/video metadata (free tier available).
- **An MCP server** — Use a community YouTube MCP server if available.

> Note: Store your API keys in environment variables or a secure config file so the agent can access them across sessions.

### Why TranscriptAPI.com over yt-dlp?

| CLI tools (yt-dlp, etc.) | TranscriptAPI |
|--------------------------|---------------|
| Verbose logs flood agent context | Clean JSON responses |
| Doesn't work on cloud/remote setups | Works everywhere, fast |
| Gets blocked randomly by YouTube | Powers [YouTubeToTranscript.com](https://youtubetotranscript.com) serving millions. Cached and reliable. |
| Requires binary installation | No binaries, just HTTP |

## How to Set It Up

### Option 1: Channel-based digest

Prompt your AI agent:

```text
Every morning at 8am, fetch the latest videos from these YouTube channels and give me a digest with key insights from each:

- @TED
- @Fireship
- @ThePrimeTimeagen
- @lexfridman

For each new video (uploaded in the last 24-48 hours):
1. Get the transcript
2. Summarize the main points in 2-3 bullets
3. Include the video title, channel name, and link

If a channel handle doesn't resolve, search for it and find the correct one.
Save my channel list to a file (e.g., youtube-channels.txt) so I can add/remove channels later.
```

### Option 2: Keyword-based digest

Track new videos about a specific topic:

```text
Every day, search YouTube for new videos about "AI agents" (or "Claude Code", "LLM tools", etc).

Maintain a file called seen-videos.txt with video IDs you've already processed.
Only fetch transcripts for videos NOT in that file.
After processing, add the video ID to seen-videos.txt.

For each new video:
1. Get the transcript
2. Give me a 3-bullet summary
3. Note anything relevant to my work

Run this every morning at 9am.
```

This way you never waste credits re-fetching videos you've already seen.

## Tips

- `channel/latest` and `channel/resolve` are **free** (0 credits) on TranscriptAPI — checking for new uploads costs nothing
- Only transcripts cost 1 credit each
- Ask for different digest styles: key takeaways, notable quotes, timestamps of interesting moments
- This already exists as a product - [Recapio - Daily YouTube Recap](https://recapio.com/features/daily-recaps)
