# 🔬 Use Case: Deep Research

> In-depth research on any topic with multiple sources.

## What it does

Spawns sub-agents that research in parallel and consolidates everything:
- Web search (Brave, Perplexity)
- Analysis of papers and long articles
- Competitor monitoring
- Comparison of tools/solutions
- Executive summary with recommendations

## Prompt

```
Do in-depth research on [TOPIC].

I want you to:
1. Research at least 5 different sources (web, papers, articles, discussions)
2. Analyze different points of view (pros, cons, debates)
3. Identify trends and what is changing
4. Compare the main solutions/approaches
5. Give me a recommendation based on my context

Output format:
- **Executive summary** (3 paragraphs, for those in a hurry)
- **Detailed analysis** (by source, with links)
- **Comparison** (table if applicable)
- **Recommendation** (what I should do, considering my profile)
- **Sources** (links so I can dive deeper if I want)

Use thinking mode for this — I want quality, not speed.
```

## Variations

### Competitor research
```
Research my competitors: [LIST].
For each one, tell me: price, features, strengths, weaknesses, what they posted recently, and where I have an advantage.
```

### Interview/podcast preparation
```
I'm going to interview [PERSON]. Research everything about them: background, projects, controversial opinions, recent content. Give me 10 questions that NOBODY has asked yet.
```

### Trend analysis
```
What are the emerging trends in [NICHE] for the next 6 months? Research newsletters, Twitter, Reddit, and HN. Give me the 5 trends with the strongest signal.
```
