> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# arXiv Paper Reader

Reading arXiv papers means downloading PDFs, losing context when switching between papers, and struggling to parse dense LaTeX notation. You want to read, analyze, and compare papers conversationally without leaving your workspace.

This workflow turns your agent into a research reading assistant:

- Fetch any arXiv paper by ID and get clean, readable text (LaTeX flattened automatically)
- Browse paper structure first — list sections to decide what to read before committing to the full text
- Quick-scan abstracts across multiple papers to triage a reading list
- Ask the agent to summarize, compare, or critique specific sections
- Results are cached locally — revisiting a paper is instant

## Skills you Need

- [arxiv-reader](https://github.com/Prismer-AI/Prismer/tree/main/skills/arxiv-reader) skill (3 tools: `arxiv_fetch`, `arxiv_sections`, `arxiv_abstract`)

No Docker or Python required — the skill runs standalone using Node.js built-ins. It downloads directly from arXiv, decompresses the LaTeX source, and flattens includes automatically.

## How to Set it Up

1. Get the `arxiv-reader` skill from the [Prismer repository](https://github.com/Prismer-AI/Prismer/tree/main/skills/arxiv-reader). You can integrate it as:
   - An MCP server added to your agent's MCP config
   - A Node.js tool integrated directly into your agent's toolchain
   - Copy the `skills/arxiv-reader/` directory and configure it for your agent platform

2. The skill is ready to use. Prompt your AI agent:
```text
I'm researching [topic]. Here's my workflow:

1. When I give you an arXiv ID (like 2301.00001):
   - First fetch the abstract so I can decide if it's relevant
   - If I say "read it", fetch the full paper (remove appendix by default)
   - Summarize the key contributions, methodology, and results

2. When I give you multiple IDs:
   - Fetch all abstracts and give me a comparison table
   - Rank them by relevance to my research topic

3. When I ask about a specific section:
   - List the paper's sections first
   - Then fetch and explain the relevant section in detail

Keep a running list of papers I've read and their key takeaways.
```

3. Try it: "Read 2401.04088 — what's the main contribution?"
