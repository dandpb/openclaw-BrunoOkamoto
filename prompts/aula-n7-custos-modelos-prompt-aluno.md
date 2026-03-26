# Student Prompt — Lesson N-7: How Much It Costs and Which Model to Use

> **How to use:** Copy the prompt below and paste it in the chat with your OpenClaw agent after watching the lesson.

---

## 📋 Main Prompt

```
Hello! I just watched lesson N-7 of the OpenClaw course on AI costs and models.

I need your help to:
1. Check which models are configured in my setup
2. Optimize the configuration to save without losing quality
3. Understand how much I'm spending (or will spend)

Let's start with a diagnosis of my model configuration?
```

---

## 🧪 Exercise 1 — Diagnosis of Configured Models

```
Please check my current model configuration:

1. Run `openclaw config get model` — what is the default model?
2. Run `openclaw config get heartbeat.model` — is there a specific model for heartbeat?
3. Tell me if I'm using the right model or if I should optimize
4. Calculate the estimated cost per message with the current model

Based on the pricing table:
- Haiku 4.5: $0.80/$4 per M tokens
- Sonnet 4.5: $3/$15 per M tokens
- Opus 4: $15/$75 per M tokens
- Gemini 3.1 Pro: $1.25/$5 per M tokens
```

---

## 💰 Exercise 2 — Calculate Estimated Monthly Spend

```
I want to estimate how much I'll spend per month. Help me with this calculation:

My estimated usage:
- Heartbeats: [X] times per hour, [Y] hours per day
- Direct messages: [Z] per day
- Long analyses: [W] per week

For each type of usage:
1. Which model should I use?
2. What is the estimated cost per execution?
3. What is the total monthly cost for that item?

At the end, add everything up and give me an estimated monthly total.
(Fill in the values above with your real or estimated usage)
```

---

## ⚙️ Exercise 3 — Configure Optimized Models

```
I want to configure different models for different situations in my OpenClaw.

Please guide me through the commands to:
1. Configure Claude Sonnet 4.5 as the default model for interactions
2. Configure Claude Haiku 4.5 for heartbeats (economical)
3. Verify the configurations are set correctly
4. Tell me the estimated impact on monthly cost from this change

Execute the commands and confirm each step.
```

---

## 🛡️ Exercise 4 — Configure Spending Limits

```
I need to configure protections to avoid surprises on my bill.

Please:
1. Tell me how to configure the monthly spending limit at console.anthropic.com (step-by-step instructions)
2. Configure the rateLimit in OpenClaw: `openclaw config set rateLimit.requestsPerHour 100`
3. Teach me how to check current spending with `openclaw usage report`
4. Suggest an appropriate spending limit for my usage profile

We want to ensure that if something goes wrong (infinite loop, skill bug), the financial damage is limited.
```

---

## 📊 Exercise 5 — Real Cost Comparison: Haiku vs Sonnet vs Opus

```
I want to see in practice the cost difference between models.

Please give me a demonstration:
1. Create a simple heartbeat task (e.g.: "check if there are urgent emails and respond in 1 line")
2. Estimate the cost of this task in each model: Haiku, Sonnet, and Opus
3. Calculate what this means over 30 days with 2 heartbeats per hour

Show the detailed calculation so I understand why Haiku is so important for repetitive tasks.
```

---

## 🔍 Exercise 6 — Real Usage Analysis (if you've been using it for a while)

```
I've been using OpenClaw for some time and I want to analyze my real usage.

Please:
1. Run `openclaw usage report` and show me the result
2. Identify which model I'm using the most
3. Calculate whether I would be spending less with a more optimized configuration
4. Suggest adjustments to my configuration based on real usage

If `openclaw usage report` is not available, explain how to see usage in the Anthropic/OpenAI console.
```

---

## ✅ Final Learning Check

```
To close the exercises for lesson N-7, give me a quick quiz with 5 questions about:
- When to use Haiku vs Sonnet vs Opus
- How pricing per token works in practice
- How to configure different models per function
- How to protect yourself from unexpected spending
- Difference between subscription and API Key

After I answer, give me feedback on what I got right and what I need to review.
```

---

## 💡 Quick Tip

> If you want a quick analysis of your current setup:

```
Do a complete diagnosis of my cost setup:
1. Currently configured models
2. Frequency of active heartbeats
3. Estimated monthly cost with current configuration
4. Optimization suggestion if applicable
5. Alert if any configuration may cause excessive cost
```
