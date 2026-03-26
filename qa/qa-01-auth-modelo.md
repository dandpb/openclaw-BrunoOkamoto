# ❓ Q&A — Auth & Model (API, Claude, Switching Providers)

> Plain language. No terminal. Paste the prompt into your bot and it handles the rest.

---

## "My bot stopped responding / suddenly got slow"

**What probably happened:** The Claude (Anthropic) service put your account in a temporary cooldown. This is normal — it happens when there are too many calls in a short period of time.

**What to do:**
Paste this prompt into your bot:

```
Check the gateway status for me. I want to know:
1. If the configured model is responding
2. If there are any authentication errors or cooldowns
3. What you recommend doing now
```

**If the bot doesn't respond either:** Wait 5–10 minutes and try again. The cooldown is automatic and clears on its own.

---

## "Error 401 appeared — what does that mean?"

**In plain language:** The bot tried to authenticate with the AI service and the password was wrong or expired. It's like trying to get into a party with an expired invitation.

**What to do:**
Paste this prompt into your bot:

```
A 401 authentication error appeared. Help me diagnose it:
1. Is the API key configured correctly?
2. Is the .env being read by the gateway?
3. Does the systemd service have an old override that might be overwriting the new key?
Tell me what you find and what I should fix.
```

---

## "I don't know if I should use an API key or subscribe to Claude.ai"

**Simple difference:**

| | Claude.ai Subscription | API Key (Anthropic) |
|---|---|---|
| **What it's for** | Using the chat on the website/app | Connecting to OpenClaw |
| **Price** | $20–110/month | Pay per use ($0.02–$1 per 1M tokens) |
| **Works in OpenClaw?** | ❌ Not directly | ✅ Yes |

**Summary:** To use with OpenClaw, you need the **API Key** (console.anthropic.com), not the chat subscription.

**⚠️ Important warning about blocks:** Some Anthropic accounts are currently being blocked. We have no control over this — it's their decision. If your account was blocked, the course teaches how to use **ChatGPT (OpenAI) as an alternative**. Many students are using it this way without any problems.

---

## "I want to switch from Claude to ChatGPT (or vice versa)"

**What to do:**
Paste this prompt into your bot:

```
I want to change the model you use. Guide me step by step:
1. How do I get my API key from OpenAI (or Anthropic)
2. How do I update the .env with the new key
3. How do I configure the model in openclaw.json
4. How do I restart the gateway to apply the change
Explain as if I've never done this before.
```

---

## "How much does it cost to use Claude / ChatGPT in OpenClaw?"

**Price reference (Feb/2026 — always check the official website):**

| Model | Plan | Approx price/month |
|---|---|---|
| Claude Haiku | API | Very cheap (~$0.20–1) |
| Claude Sonnet | API | Moderate (~$3–10) |
| Claude Opus | API | Expensive (~$16–40) |
| GPT-4o mini | API | Very cheap (~$0.20–1) |
| GPT-4o | API | Moderate (~$4–16) |

**Our recommendation:**
- Use **Haiku or GPT-4o mini** for automated tasks (reminders, crons)
- Use **Sonnet or GPT-4o** for everyday conversations
- Save **Opus** for when you really need depth

**Tip:** With optimization, most students spend between $4–16/month.

---

*Last updated: Feb/2026*
