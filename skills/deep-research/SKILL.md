---
name: deep-research-protocol
description: >
  Structured deep research protocol with multiple sources, synthesis and actionable
  report. Use when Bruno asks for detailed research, market analysis, topic investigation
  or benchmarking. Trigger when: "research on", "deep research", "investigate",
  "analyze the market for", "benchmark", "I want to better understand", "deep research",
  "give me an overview of", "competitor analysis". For complex research (>30min),
  spawn as sub-agent.
metadata:
  author: amora-cos
  version: 1.0.0
  domain: shared
  owner: main
---

# Deep Research Protocol — Deep Research Skill

## What it is

Structured protocol for deep research. Combines multiple sources, synthesizes findings, and delivers an actionable report.

## Research Protocol

### 1. Framing (2 min)
- What is the exact question?
- What decision will this research inform?
- What depth level? (Quick scan vs Deep dive)

### 2. Multi-source Collection

**Primary sources (use in this order):**
1. `web_search` — general search (Brave)
2. `web_fetch` — extract content from relevant URLs
3. **Perplexity** — search with AI-powered answers and citations (API key in 1Password: "Perplexity API")
   ```bash
   PERPLEXITY_API_KEY=$(op item get "Perplexity API" --vault "Amora Vault" --field credential --reveal)
   node /root/.openclaw/workspace/skills/perplexity/scripts/search.mjs "query"
   ```
4. Knowledge Base — if there is relevant content already ingested

**Specialized sources:**
- Reddit/HackerNews — technical community opinion
- Twitter/X — real-time signals
- YouTube — long-form analyses and tutorials
- GitHub — open source repos and projects

### 3. Synthesis

For each source:
- **Fact** — what is confirmable
- **Opinion** — what is interpretation
- **Signal** — what suggests a trend

### 4. Report

**Standard format:**

```markdown
# [Topic] — Deep Research
Date: DD/MM/YYYY

## TL;DR (3-5 bullets)

## Context
[Why we are researching this]

## Findings
### [Subtopic 1]
- Finding + source
### [Subtopic 2]
- Finding + source

## Analysis
[Cross-referencing findings, identified patterns]

## Recommendation
[What to do with this information]

## Sources
[List of consulted URLs]
```

### 5. Saving
- Save in `memory/research-YYYY-MM-DD-[slug].md`
- If relevant to Knowledge Base → ingest

## Depth Levels

| Level | Time | Sources | Output |
|-------|------|---------|--------|
| Quick scan | 5-10 min | 3-5 URLs | 1 paragraph + bullets |
| Standard | 15-30 min | 8-12 URLs | 1-2 page report |
| Deep dive | 30-60 min | 15-20+ URLs | 3-5 page report |

## When to spawn a sub-agent

If research is deep dive (>30min) or Bruno wants to keep working while the research runs:
- Spawn via `sessions_spawn` with detailed task
- Sub-agent delivers report when ready
- Amora reviews and sends to Bruno

## Biases to avoid

- Confirmation bias — actively seek counter-arguments
- Recency bias — verify if trends are real or hype
- Survivorship bias — look for failure cases, not only success
- Authority bias — expert said it ≠ it is true
