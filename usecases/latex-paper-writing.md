> Adapted from [awesome-openclaw-usecases](https://github.com/hesamsheikh/awesome-openclaw-usecases). OpenClaw dependency removed.

# LaTeX Paper Writing

Setting up a local LaTeX environment is painful — installing TeX Live takes gigabytes, debugging compilation errors is tedious, and switching between your editor and PDF viewer breaks flow. You want to write and compile LaTeX papers conversationally without any local setup.

This workflow turns your agent into a LaTeX writing assistant with instant compilation:

- Write LaTeX collaboratively with the agent — describe what you want and it generates the source
- Compile to PDF instantly with pdflatex, xelatex, or lualatex (no local TeX installation needed)
- Preview PDFs inline without switching to another app
- Use starter templates (article, IEEE, beamer, Chinese article) to skip boilerplate
- Bibliography support with BibTeX/BibLaTeX — just paste your .bib content

## Skills you Need

- [latex-compiler](https://github.com/Prismer-AI/Prismer/tree/main/skills/latex-compiler) skill (4 tools: `latex_compile`, `latex_preview`, `latex_templates`, `latex_get_template`)
- Prismer workspace container (runs the LaTeX server on port 8080 with full TeX Live)

## How to Set it Up

1. Clone and deploy [Prismer](https://github.com/Prismer-AI/Prismer) with Docker (the LaTeX server with full TeX Live starts automatically):
```bash
git clone https://github.com/Prismer-AI/Prismer.git && cd Prismer
docker compose -f docker/docker-compose.dev.yml up
```

2. Integrate the `latex-compiler` skill into your agent. Options include:
   - Add it as an MCP server in your agent's MCP config
   - Integrate the tools directly into your agent's toolchain
   - The skill is built into the Prismer container — no separate installation needed

3. Prompt your AI agent:
```text
Help me write a research paper in LaTeX. Here's my workflow:

1. Start from the IEEE template (or article/beamer depending on what I need)
2. When I describe a section, generate the LaTeX source for it
3. After each major edit, compile and preview the PDF so I can check formatting
4. If there are compilation errors, read the log and fix them automatically
5. When I provide BibTeX entries, add them to the bibliography and recompile

Use xelatex if I need Chinese/CJK support, otherwise default to pdflatex.
Always run 2 passes for cross-references.
```

3. Try it: "Start a new IEEE paper titled 'A Survey of LLM Agents'. Give me the template with abstract and introduction sections filled in, then compile it."
