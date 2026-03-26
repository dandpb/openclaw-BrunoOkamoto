# 🚨 Diagnostic Runbook — "My bot is not working"

> Use this guide BEFORE anything else. It resolves 90% of problems.
> No terminal. Just prompts.

---

## Step 1 — Is my bot responding?

**If YES:** Go to Step 2.

**If NO:**
- Wait 2 minutes and try again (could be temporary instability)
- Try sending a simple message: `hi`
- If it still doesn't respond: access the Mission Control panel or restart the gateway via the link you configured during setup

---

## Step 2 — Ask the bot for a diagnosis

Paste this prompt:

```
Run a quick diagnosis for me right now:
1. Is the gateway working? (/status)
2. Are there any recent errors in the logs?
3. Is the AI model responding?
4. Are there any automations or crons with issues?
Tell me what you find in plain language.
```

---

## Step 3 — Identify the symptom and go to the right Q&A

| What is happening | Help file |
|---|---|
| Bot not responding / slow / responses got worse | → qa-03-contexto-memoria.md |
| Error 401, invalid token, API key problem | → qa-01-auth-modelo.md |
| Anyone can use my bot / bot doesn't respond in the group | → qa-02-telegram.md |
| "Port in use", "command not found", won't connect | → qa-04-infra-basica.md |
| Questions about models / cost / Claude blocked | → qa-06-llms-comparativo.md |
| Questions about how the system works | → qa-05-arquitetura.md |

---

## Universal Emergency Prompt

If you don't know what's wrong, paste this:

```
I have a problem with OpenClaw and I don't know exactly what it is.
Symptom: [DESCRIBE WHAT IS HAPPENING]

Please:
1. Help me identify the cause
2. Tell me what to do in plain language
3. Guide me step by step to resolve it
4. Confirm when it's resolved
```

---

## ⚠️ Golden Rule

**Don't try to fix things by guessing.**

The correct sequence is always:
1. Diagnose first (what is wrong?)
2. Understand the cause (why did it happen?)
3. Apply the solution (how to fix it?)
4. Confirm it's resolved (did it work?)

Skipping steps creates new problems on top of the old ones.

---

*If nothing works: describe your problem in detail in the support group with:*
- *What you were trying to do*
- *What happened (screenshot of the error if available)*
- *What you've already tried*

---

*Last updated: Feb/2026*
