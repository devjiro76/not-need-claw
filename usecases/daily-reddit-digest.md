> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# Daily Reddit Digest
Run a daily digest everyday to give you the top performing posts from your favourite subreddits.

What to use it for:

- Browsing subreddits (hot/new/top posts)
- Searching posts by topic
- Pulling comment threads for context
- Building shortlists of posts to manually review/reply to later

> It's read-only. No posting, voting, or commenting.

## Skills you Need
A Reddit API integration. You can use:
- The [Reddit JSON API](https://www.reddit.com/dev/api/) directly (no auth needed for read-only public data — just append `.json` to any subreddit URL)
- An MCP server for Reddit (e.g., a community Reddit MCP server)
- A simple script using `fetch` / `curl` to pull subreddit data

## How to Set it Up
Once you have Reddit data access set up, prompt your AI agent:
```text
I want you to give me the top performing posts from the following subreddits.
<paste the list here>
Create a separate file for the reddit preferences, about the type of posts I like to see and every day ask me if I liked the list you provided. Save my preference as rules in the file to use for a better digest curation. (e.g. do not include memes.)
Every day at 5pm, run this process and give me the digest.
```
