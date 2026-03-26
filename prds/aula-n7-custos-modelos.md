# PRD — Lesson N-7: How Much Does It Cost and Which Model to Use

> **Level:** Intermediate
> **Estimated duration:** 15 minutes
> **Prerequisite:** OpenClaw installed and running, at least one provider configured

---

## 🎯 Lesson Objective

By the end of this lesson, the student will be able to:

1. Understand the difference between **subscription** and **API Key** and when to use each
2. Compare the main AI models by **price and capability**
3. Choose the right model for each type of task (saving up to 95%)
4. Configure **different models per function** (heartbeat, chat, analysis)
5. Estimate the **real monthly cost** of their setup
6. Set **spending limits** to never be surprised

---

## 📋 Recording Script — Section by Section

### 🎬 OPENING (0:00 – 1:00)

**[Bruno on screen, direct tone]**

> "Hey, everyone! Lesson N-7 — costs and models. This is the lesson that will save you from a shocking bill."

> "I've seen a student spend $200 in a single day of testing. I've seen another running the same setup for $8/month. The difference? Model choice. In 15 minutes you'll understand everything."

---

### 💳 SECTION 1: Subscription vs API Key — Which to Use? (1:00 – 4:30)

**[Screen: comparison slide]**

> "First decision: are you going to use a monthly subscription or an API Key with pay-per-use?"

**[Show on screen:]**

| | Subscription (Claude Pro) | API Key (Pay-per-use) |
|---|---|---|
| **Fixed cost** | $20/month always | $0 if unused |
| **Spending control** | ❌ None | ✅ Total |
| **Works with OpenClaw** | ❌ Not anymore (OAuth blocked) | ✅ Yes |
| **Ideal for** | Personal use in chat | Agents, automation |
| **Surprise risk** | Low (fixed) | Medium without limits |

> "The answer is almost always: **API Key**. The Pro subscription was designed for human use — you opening the chat and talking. OpenClaw makes programmatic calls, which require an API Key."

> "With an API Key, you pay exactly for what you use. In a month when you travel and barely use the agent, you pay less. In a month with an intensive project, you pay more — but you're in control."

---

### 📊 SECTION 2: Model and Pricing Table (4:30 – 8:00)

**[Screen: comparison table]**

> "Now let's talk real money. Models are charged per tokens — pieces of text of ~4 characters. The price is per 1 million tokens."

| Model | Input Price (M tokens) | Output Price (M tokens) | Speed | Quality |
|--------|----------------------|------------------------|------------|-----------|
| **Claude Opus 4** | $15 | $75 | Slow | ⭐⭐⭐⭐⭐ |
| **Claude Sonnet 4.5** | $3 | $15 | Medium | ⭐⭐⭐⭐ |
| **Claude Haiku 4.5** | $0.80 | $4 | Fast | ⭐⭐⭐ |
| **GPT-4o** | $2.50 | $10 | Medium | ⭐⭐⭐⭐ |
| **Gemini 3.1 Pro** | $1.25 | $5 | Medium | ⭐⭐⭐⭐ |
| **Mistral Small** | $0.10 | $0.30 | Very fast | ⭐⭐ |

> "A typical message uses ~500 input tokens + ~200 output tokens. Let's do the math:"

> "With Opus 4: $15/M × 0.0005M + $75/M × 0.0002M = $0.0075 + $0.015 = **$0.022 per message**"
> "With Haiku 4.5: $0.80/M × 0.0005M + $4/M × 0.0002M = $0.0004 + $0.0008 = **$0.0012 per message**"

> "Difference: **18x cheaper** with Haiku for the same simple task."

---

### 🎯 SECTION 3: Which Model for Each Situation? (8:00 – 11:00)

**[Screen: recommendation cards]**

> "The strategy is: use the MINIMUM model that solves the problem."

**Heartbeats and Crons:**

> "A heartbeat is when the agent wakes up on its own to check emails, calendar, notifications. These tasks are simple — check, categorize, decide if it needs to alert you."
> "**Use Haiku** — $0.005 per execution vs $0.10 with Opus. With 20 heartbeats a day, that's $0.10/day with Haiku vs $2/day with Opus. In a month: $3 vs $60. The same task."

**Daily Interaction (Telegram messages):**

> "When you send a message to the agent and want a useful response — research, organization, light analysis."
> "**Use Sonnet** — the best cost-benefit. Fast enough, smart enough, reasonable price."

**Complex Analysis:**

> "When you need to analyze a long document, make a difficult decision, or write something important."
> "**Use Opus** — but only when you need it. Don't use Opus to check the weather."

**Economical alternatives:**

> "Gemini 3.1 Pro at $1.25/M is an excellent alternative to Sonnet for those wanting to save money. Mistral Small is absurdly cheap and good for very simple classification tasks."

---

### ⚙️ SECTION 4: How to Configure Model per Function (11:00 – 13:00)

**[Screen: Terminal]**

> "OpenClaw allows configuring different models per function. This is powerful."

```bash
# Default model for day-to-day interactions
openclaw config set model anthropic/claude-sonnet-4-5

# Specific model for heartbeats (economical)
openclaw config set heartbeat.model anthropic/claude-haiku-4-5

# Model for heavy analysis (optional, use sparingly)
openclaw config set analysis.model anthropic/claude-opus-4
```

> "This way, the agent automatically uses Haiku for the 20 daily heartbeat executions, Sonnet when you send a message, and Opus only when you request a deep analysis."

> "To check the current configuration:"

```bash
openclaw config get model
openclaw config get heartbeat.model
```

---

### 💰 SECTION 5: Real Monthly Cost Example (13:00 – 14:30)

**[Screen: cost breakdown]**

> "Let's build a real setup and calculate:"

| Usage | Quantity/month | Model | Estimated cost |
|-----|---------------|--------|----------------|
| Heartbeats (2x/hour, 16h/day) | ~960 executions | Haiku | ~$5 |
| Daily messages (10/day) | ~300 messages | Sonnet | ~$4 |
| Weekly analyses | ~4 long analyses | Opus | ~$3 |
| Crons and automations | ~200 executions | Haiku | ~$2 |
| **Estimated total** | | | **~$14/month** |

> "Moderate setup, agent running 24/7 with active heartbeats: **$14 to $25/month**. If you use it intensively, it could reach $40. But with model control, it's very hard to exceed that unintentionally."

> "Compare with: Claude Pro ($20/month) without working in OpenClaw. Or a part-time human assistant ($500+/month). For $15-40/month you have an AI agent running 24/7."

---

### 🚨 SECTION 6: Troubleshooting — "My Account Ran Out" (14:30 – 15:00)

**[Screen: how to set limits]**

> "This happens when a code loop or misconfigured skill makes thousands of calls unintentionally. How to protect yourself:"

**At Anthropic:**
```
console.anthropic.com → Settings → Billing → Usage Limits
→ "Monthly spend limit" → Set a value (e.g.: $50)
→ "Notification threshold" → Set an alert (e.g.: $25)
```

**In OpenClaw:**
```bash
# Limit requests per hour (protection against loops)
openclaw config set rateLimit.requestsPerHour 100

# View estimated accumulated spend for the month
openclaw usage report
```

> "Configure these limits **before** you start using it intensively. It's the seatbelt — you hope you won't need it, but you'll be glad it exists."

---

## 🛠️ Recommended Configuration for Beginners

```bash
# Basic and economical setup to get started
openclaw config set model anthropic/claude-sonnet-4-5
openclaw config set heartbeat.model anthropic/claude-haiku-4-5

# Verify configuration
openclaw config get model
openclaw config get heartbeat.model
```

And at console.anthropic.com:
- Monthly spend limit: $50
- Notification at: $25

---

## 📊 Complete Model Table (Quick Reference)

| Model | Input/Output ($/M) | Ideal Use | Avoid For |
|--------|-------------------|-----------|-------------|
| Claude Opus 4 | $15/$75 | Deep analysis, critical decisions | Heartbeats, simple responses |
| Claude Sonnet 4.5 | $3/$15 | Daily interaction, writing, research | High-volume repetitive tasks |
| Claude Haiku 4.5 | $0.80/$4 | Heartbeats, crons, classification | Complex analyses |
| GPT-4o | $2.50/$10 | Alternative to Sonnet, code | — |
| Gemini 3.1 Pro | $1.25/$5 | Economical alternative to Sonnet | — |
| Mistral Small | $0.10/$0.30 | Simple classification, routing | Any task requiring reasoning |

---

## ✅ Student Final Checklist

- [ ] Understands the difference between subscription and API Key
- [ ] Default model configured: `openclaw config set model anthropic/claude-sonnet-4-5`
- [ ] Heartbeat model configured: `openclaw config set heartbeat.model anthropic/claude-haiku-4-5`
- [ ] Spending limit configured at console.anthropic.com
- [ ] Spending notification configured (threshold)
- [ ] `openclaw usage report` tested and working

---

## ❓ Frequently Asked Questions

**1. Can I switch models at any time?**

> Yes. `openclaw config set model NEW-MODEL` and done. Valid from the next message onward.

**2. Mistral is much cheaper — why not always use it?**

> Lower quality for complex reasoning. For simple heartbeats it works; for conversations and analysis, the quality loss is noticeable. Use Haiku as the minimum for interactions.

**3. Is Gemini reliable for use with OpenClaw?**

> Yes, since v2026.3.2. A good economical alternative. It doesn't have the same tool capabilities as Claude for complex cases, but for general use it's excellent.

**4. How do I know exactly how much I've spent?**

> `openclaw usage report` shows a breakdown by model. The Anthropic console shows it in real time with graphs.

**5. Is Haiku "dumb"?**

> No! For structured tasks (checking emails, classifying messages, answering simple questions), Haiku is excellent. It falls behind in multi-step reasoning and creativity. For 80% of automation tasks, it's more than sufficient.
