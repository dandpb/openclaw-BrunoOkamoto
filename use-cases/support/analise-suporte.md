# 🎧 Use Case: Intelligent Support Analysis

> Identify patterns, recurring bugs, and opportunities in tickets.

## What it does

Connects to your support tool (Crisp, Intercom, Zendesk) and analyzes:
- Ticket patterns (which problems appear most often)
- Customer sentiment (satisfaction, frustration)
- Response and resolution time
- Feature suggestions based on complaints
- Content opportunities (FAQ that becomes a post)

## Prompt

```
I want you to analyze my support tickets from the last [30/60/90] days.

My support tool is [CRISP/INTERCOM/ZENDESK].

Deliver:
1. **Top 10 most reported problems** — grouped by category
2. **Sentiment analysis** — % of positive/neutral/negative tickets
3. **Recurring bugs** — issues that appear more than 3 times
4. **Feature suggestions** — what customers are asking for
5. **Content opportunities** — frequently asked questions that can become tutorials/posts
6. **Time patterns** — when tickets come in (peak times)
7. **Average resolution time** — and where it is slow

Format: structured report with concrete actions for each insight.

Amora's insight: "Crisp is a sales channel, not just support. Analyze pre-sale questions too."
```

## Real example

Amora analyzed 187 Crisp conversations:
- 95% via WhatsApp
- "Vibe coding" dominated (172 mentions)
- People get stuck at the "last mile" (deploy, config, go-live)
- Generated 6 content ideas directly from tickets
