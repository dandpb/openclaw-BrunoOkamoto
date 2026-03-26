# ❓ Q&A — LLM Comparison (Claude, ChatGPT, and others)

> Reference guide: which model to use, how much it costs, what we recommend.

---

## Which model should I use in OpenClaw?

**Our general recommendation:**

| Situation | Recommended model | Why |
|---|---|---|
| Everyday conversation | Claude Sonnet or GPT-4o | Great quality/cost balance |
| Automated tasks (crons, reminders) | Claude Haiku or GPT-4o mini | Very cheap, fast enough |
| Complex analysis, important decisions | Claude Opus | Maximum quality, use sparingly |
| When Claude is blocked | GPT-4o | Excellent alternative |

---

## Price and Plan Comparison

### Claude (Anthropic)

| Plan | Approx. price | What's included |
|---|---|---|
| Claude.ai Free | Free | Limited chat usage (does not work with OpenClaw) |
| Claude.ai Pro | ~$20/month | Chat usage — **does not connect directly to OpenClaw** |
| Claude.ai Max | ~$110/month | Heavy chat usage — **does not connect directly to OpenClaw** |
| **Anthropic API** | Pay-per-use | ✅ **What works with OpenClaw** |

**Real API cost (monthly estimate with moderate use):**
- Haiku (automations): ~$0.40–2/month
- Sonnet (daily use): ~$4–16/month
- Opus (heavy use): ~$20–60/month

> ⚠️ **Note on blocks:** Anthropic is currently blocking some new accounts. We have no control over this. If your account was blocked, use ChatGPT as an alternative — the course teaches both ways and both work very well.

---

### ChatGPT / OpenAI

| Plan | Approx. price | What's included |
|---|---|---|
| ChatGPT Free | Free | Limited chat usage (does not work with OpenClaw) |
| ChatGPT Plus | ~$20/month | GPT-4o in chat — **does not connect directly to OpenClaw** |
| ChatGPT Pro | ~$200/month | Heavy use + o1 pro — **does not connect directly to OpenClaw** |
| **OpenAI API** | Pay-per-use | ✅ **What works with OpenClaw** |

**Real API cost (monthly estimate with moderate use):**
- GPT-4o mini (automations): ~$0.40–1.60/month
- GPT-4o (daily use): ~$3–12/month
- o1 (complex analyses): ~$16–50/month

---

## What's the difference between subscribing to Claude.ai and using the API?

**Simple analogy:**

- **Subscribing to Claude.ai/ChatGPT** = Eating at a restaurant. You use their menu, in their environment.
- **Using the API** = Buying the ingredients and cooking at home. You integrate it wherever you want.

OpenClaw is like your kitchen — it needs the **ingredients** (API), not the ready-made restaurant.

---

## Can I use models other than Claude and ChatGPT?

Yes! OpenClaw supports several providers:

| Model | Provider | Highlight |
|---|---|---|
| Gemini | Google | Great for very long contexts |
| Mistral | Mistral AI | European option, good privacy |
| Llama (local) | Ollama | **Free**, runs on your machine |
| Deepseek | Deepseek | Very cheap, good quality |

**To find out what's available:**
Paste this prompt into your bot:

```
Which AI models does OpenClaw currently support?
Recommend which would be best for my use based on what you know about me.
Consider both quality and cost.
```

---

## How do I change the model my bot uses?

Paste this prompt into your bot:

```
I want to change the model you use to [MODEL YOU WANT].
Guide me:
1. How do I get the API key for the new provider?
2. How do I update the configuration?
3. How do I test if it's working?
Explain step by step without using difficult terminal commands.
```

---

*Last updated: Feb/2026 — Approximate prices, always check the official provider websites.*
