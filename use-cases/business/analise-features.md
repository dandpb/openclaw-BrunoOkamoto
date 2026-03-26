# 🔧 Use Case: Feature Analysis and Roadmap

> Turn customer feedback into a prioritized roadmap.

## What it does

Cross-references data from multiple sources to prioritize features:
- Feature requests from support
- Community discussions
- Competitor analysis
- Product usage data
- Churn feedback (why they cancelled)

## Prompt

```
I want you to help me prioritize the roadmap for my product [PRODUCT NAME].

Analyze these sources:
1. Support tickets from the last 60 days — extract feature requests
2. Community posts — what people are asking for
3. Churn reasons — what was missing that made the customer leave
4. Competitors — features they have that I don't
5. [IF AVAILABLE] Usage data — most and least used features

Deliver:
1. **Ranked feature requests** — by frequency × impact
2. **Quick wins** — easy-to-implement features with high impact (< 1 week dev)
3. **Must-have vs nice-to-have** — clearly separated
4. **Competitor comparison** — feature parity, gaps, advantages
5. **Suggested roadmap** — next 4 weeks, prioritized

Format: table with columns (Feature | Frequency | Impact | Effort | Priority).

Use the formula: Priority = (Frequency × Impact) / Effort
```

## Variation: Feature Feedback Loop

```
Set up a monthly cron that:
1. Analyzes new tickets and community posts
2. Updates the feature requests list
3. Compares with the current roadmap
4. Notifies me if any feature has surged in demand
5. Saves the history to track trends over time
```
