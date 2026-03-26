# 👥 Use Case: Community Analysis

> Understand what your community is talking about, asking for, and feeling.

## What it does

Connects to your community API (Circle, Discord, Slack) and analyzes:
- Hot topics (what is generating the most discussion)
- Frequently asked questions (natural community FAQ)
- Most active and influential members
- Spam and duplicate posts
- Emerging trends
- Overall sentiment

## Prompt

```
I want a complete analysis of my community over the last [30/60] days.

My community is [CIRCLE/DISCORD/SLACK] with [NUMBER] members.

Deliver:

1. **Hot Topics** — the 10 most discussed subjects, with post volume
2. **Frequently Asked Questions** — the 10 questions that appear most often (base for FAQ/content)
3. **Featured members** — top 10 most active and top 10 who help others most
4. **Spam check** — duplicate posts, excessive cross-posting, suspicious patterns
5. **Trends** — topics that are GROWING (not the biggest ones, the ones that are accelerating)
6. **Sentiment** — what is the vibe? Positive? Frustrated? What's the general feeling?
7. **Opportunities** — content ideas, features, or actions based on the data

Format: report with actionable insights, not just numbers.

Tip: cross-reference community data with support tickets to see complete patterns.
```

## Real example

Amora analyzed 345 posts from the Micro-SaaS community (20k members):
- Pure spam: not found
- Attention patterns: cross-posting and repetition
- "150 MVPs in 60 days" — data point that became a viral LinkedIn post
- Cross-referencing with Crisp revealed: vibe coding dominates in both
