> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# X Account Analysis

There are many websites designed to give you a qualitative analysis of your X account. While X already gives you an **analytics** section, it's more focused to show your numbers on your performance.

But a qualitative analysis focuses on the quality of your posts, not the performance stats. Some insights you can get from this type of analysis:
- What are the patterns that make my posts go viral?
- What topics I talk about get me most engagement?
- Why do I get posts with 1000+ likes but sometimes posts with <5 likes? What am I doing wrong?

There are many websites and apps designed to give you X analytics, but they focus on the statistics. There are probably 1-2 websites that let you talk with an AI to understand your performance.

But now you can use an AI agent to do this analysis for you, without needing to pay $10-$50 for subscriptions on these websites.

## Skills you Need
An X/Twitter data access method. Options:

- **X API v2** — Apply for a developer account at [developer.x.com](https://developer.x.com). The free tier allows basic read access.
- **Browser cookie-based access** — Provide your `auth-token` and `ct0` cookies from an authenticated X session. This is what the original "Bird" skill uses under the hood.
- **An MCP server for X/Twitter** — Use a community Twitter MCP server if available.
- **Web scraping tools** — Use a scraping MCP server or `web_fetch` to pull your profile data.

## How to Set it Up
Here's the flow:
1. Set up your X data access method (API keys or browser cookies).
2. For security and isolation when using cookie-based access, consider creating a separate browser profile or using a secondary X account for the bot to read from.
3. If using cookie-based auth: log into x.com in Chrome/Brave, and extract the cookie information (`auth-token`, `ct0`) so the agent can access your account data.
4. Ask your AI agent to take a look at your account, fetch the last N tweets, and ask it any questions you like. Alternatively, you can ask it to write you specific analysis scripts.
