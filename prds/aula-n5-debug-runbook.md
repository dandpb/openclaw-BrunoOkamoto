# PRD — Lesson N-5: Step-by-Step Debug — Standard Diagnostic Runbook

**Module:** N — Troubleshooting & Maintenance  
**Lesson:** N-5  
**Estimated duration:** 25–30 minutes  
**Level:** Intermediate / Advanced  
**Format:** Screencast with live terminal + support slides  

---

## Lesson Objective

By the end of this lesson, the student will be able to follow a systematic 5-step runbook to diagnose and resolve any problem in OpenClaw — whether it's a silent bot, invalid credentials, broken configuration, or an unknown error that needs to be escalated.

---

## Recording Script

### [00:00–02:00] Opening

**Script (Bruno speaks):**

> "Hello everyone! In this lesson we're going to talk about something everyone needs at some point: debug. OpenClaw is robust, but things happen — a bot stops responding, an API key expires, the gateway crashes. And when that happens and you don't know where to start... it becomes chaos.
>
> So today I'll give you my personal runbook. Five steps, in order. You follow from start to finish and, in my experience, this resolves 95% of problems. Let's go."

**What to show on screen:**
- Diagram of the 5 steps (opening slide)
- Clean terminal, ready to use

---

### [02:00–06:00] Step 1: Initial Triage — Is the Bot Responding?

**Script:**

> "The first step is triage. Before touching anything, you need to understand _what_ exactly is wrong. There are three distinct scenarios, and each points to a different path.
>
> **Scenario A: The bot is completely silent.** You sent a message, waited, nothing happened. This almost always means the gateway isn't running. The gateway is the process that listens for messages and routes them to the AI model. If it goes down, the bot simply stops existing. The solution is immediate — we'll see it in Step 2.
>
> **Scenario B: The bot responds, but with an error message.** Great! That means the gateway is up. Now you need to _read_ the error message. It seems obvious, but many people panic and start restarting everything without reading what's written. The error usually tells you exactly what to do: invalid key, rate limit hit, config file with a problem.
>
> **Scenario C: The bot responds, but slowly — very slowly.** This is a performance problem, not a configuration one. I covered this in lesson N-4. If your bot is taking 30 seconds to respond, jump there. Here we focus on errors, not slowness.
>
> So before continuing: which of the three scenarios are you experiencing? This defines everything."

**What to show on screen:**
- Decision flowchart: Silent / Error / Slow
- Demo: send a message on Telegram and show each type of response (or lack thereof)

---

### [06:00–12:00] Step 2: Check the Gateway

**Script:**

> "If the bot is silent, start here. The command is simple:"

```bash
openclaw gateway status
```

> "This command tells you if the gateway process is running or not. If the output shows something like `stopped` or `inactive`, you know the problem. Restart:

```bash
openclaw gateway restart
```

> "If the gateway was stopped, it will probably come back and the bot will start working immediately. Quick test — send a 'hello' there.
>
> But what if the gateway restarts but the problem persists? Then you need to look at the logs. OpenClaw logs are at:

```bash
~/.openclaw/logs/gateway.log
```

> "To see the latest lines in real time, use:

```bash
tail -f ~/.openclaw/logs/gateway.log
```

> "Now, what are you looking for in the logs? There are four warning signs I always look for:
>
> **1. `auth error` or `unauthorized`** — Means the API key isn't being accepted. Go directly to Step 3.
>
> **2. `rate limit exceeded`** — You've exhausted the request limit of your plan. It could be a usage spike, an accidental loop, or the plan needing an upgrade. Wait a few minutes and try again.
>
> **3. `context error` or `context length exceeded`** — The conversation got too long for the model to process. You need to clear the session history or adjust the context limit in the configuration.
>
> **4. `connection refused` or `timeout`** — Network problem or the API endpoint is down. Check your connection and the status of your provider's API (Anthropic, OpenAI, etc.).
>
> I'll show live how to read a real log and identify these signals."

**What to show on screen:**
- `openclaw gateway status` with stopped/running output
- `openclaw gateway restart` and output
- `tail -f ~/.openclaw/logs/gateway.log` with examples of each error type highlighted

---

### [12:00–17:00] Step 3: Check Credentials

**Script:**

> "Here we arrive at the most common cause of problems: credentials. The API key expired, was rotated, or was simply copied wrong. Start with the diagnostic:

```bash
openclaw status
```

> "This command lists all configured models and the status of each. You'll see something like:

```
Models configured:
  ✓ anthropic/claude-opus-4   [active]
  ✗ openai/gpt-4o             [auth error]
```

> "If any model shows `auth error`, the key is invalid or missing.
>
> The simplest test is to send a short message — literally 'hello' — and see what happens. If you receive `401 Unauthorized` in the logs, the key is wrong. If you receive `429 Too Many Requests`, it's rate limit.
>
> These two errors seem the same to the user — the bot doesn't respond — but the solution is completely different:
>
> - **401 / auth error:** You need to reauthenticate. The key is invalid.
> - **429 / rate limit:** The key is valid, but you used it too much. Wait and try again.
>
> To reauthenticate, go to your provider's dashboard, generate a new key, and update in OpenClaw:

```bash
openclaw config set api_key <your-new-key>
openclaw gateway restart
```

> "After the restart, test again. In my experience, 60% of problems that reach support are resolved here."

**What to show on screen:**
- `openclaw status` with examples of active and errored models
- Visual comparison: 401 vs 429 in logs
- Demo of how to update the key and restart

---

### [17:00–22:00] Step 4: Check Configuration

**Script:**

> "If you've gotten here and still haven't resolved it, the problem is in the configuration. OpenClaw has a new command that I strongly recommend using _before_ any restart:

```bash
openclaw config validate
```

> "This command reads your `openclaw.json`, checks the syntax, and points out exactly where the error is — with line number and everything. Much better than restarting and staring at a blank screen trying to guess.
>
> The most common errors I see in `openclaw.json`:
>
> **1. Extra or missing comma** — JSON is unforgiving. One extra comma at the end of an object breaks everything.
>
> **2. Missing required field** — `model`, `channel`, or `token` missing from the config block.
>
> **3. Reference to non-existent file** — The `openclaw.json` pointing to an AGENTS.md at a path that doesn't exist.
>
> Speaking of AGENTS.md: this file can also cause problems. The most common errors are:
>
> - **Broken indentation** — AGENTS.md uses markdown. A badly closed code block can mess up the parsing.
> - **Circular reference** — A skill that imports another that imports the first.
> - **Conflicting instructions** — Two rules that contradict each other. The model gets stuck trying to obey both.
>
> Skills can also have conflicts. If you added a new skill and the bot started behaving strangely, test by removing the skill temporarily to isolate the problem.
>
> After fixing anything in the configuration file, always validate before restarting:

```bash
openclaw config validate && openclaw gateway restart
```

> "The `&&` ensures that the restart only happens if validation passes. Good practice."

**What to show on screen:**
- `openclaw config validate` with success and error output
- Examples of broken vs correct `openclaw.json` (side-by-side diff)
- Example of AGENTS.md with formatting problem

---

### [22:00–27:00] Step 5: Escalate the Problem

**Script:**

> "If you've gotten here and still couldn't resolve it, the problem is more complex. There's no shame in that — what matters now is asking for help the right way.
>
> There's a specific tool for that:

```bash
openclaw doctor
```

> "The `doctor` does a complete environment check: OpenClaw version, config file integrity, model status, file permissions, environment variables. It generates a report you can share.
>
> But before posting in the support group, there's an important etiquette: **never share your API keys.** The `openclaw doctor` automatically masks credentials in the output, but if you're copying logs manually, review first.
>
> What to collect before asking for help:
>
> **1. OpenClaw version:**

```bash
openclaw --version
```

> **2. Output of `openclaw doctor`** (already with credentials masked)
>
> **3. Last 50 gateway logs:**

```bash
tail -50 ~/.openclaw/logs/gateway.log
```

> **4. Your config without credentials:**

```bash
openclaw config export --mask-secrets
```

> "With these four things, anyone in support can help you in minutes. Without this, the conversation becomes an interrogation and takes much longer.
>
> In the support group, paste everything in a single code block, describe what you did before the problem appeared, and which of the 5 runbook steps you've already executed. This saves everyone's time."

**What to show on screen:**
- `openclaw doctor` with complete output
- `openclaw --version`
- `openclaw config export --mask-secrets`
- Support group post template

---

### [27:00–30:00] Closing — Error Table & First Aid

**Script:**

> "Before finishing, two resources you'll want to always have at hand.
>
> The first is the most common errors table — it's in the supplementary material for this lesson. Bookmark it.
>
> The second is the first aid checklist: five commands that resolve 80% of problems. When the bot stops working, run these five in order, and most of the time one of them already solves it:

```bash
# 1. Check overall status
openclaw status

# 2. Check gateway status
openclaw gateway status

# 3. Restart gateway
openclaw gateway restart

# 4. Validate configuration
openclaw config validate

# 5. Complete diagnostic
openclaw doctor
```

> "Save this. Print it if needed. It's your debug toolkit.
>
> See you in the next lesson. If you have questions, the support group is there."

---

## Most Common Errors Table

| Error | Symptom | Cause | Solution |
|-------|---------|-------|----------|
| `401 Unauthorized` | Bot silent or error in response | Invalid or expired API key | Generate new key, `openclaw config set api_key <new>`, restart |
| `429 Too Many Requests` | Bot silent for a period | Rate limit hit | Wait 1-5 minutes, reduce usage frequency |
| `Gateway stopped` | Bot completely silent | Gateway process froze or crashed | `openclaw gateway restart` |
| `Context length exceeded` | Error after long conversation | Conversation history too extensive | Clear history or adjust `max_context` in config |
| `Connection refused` | Connection error in logs | Unstable network or endpoint down | Check internet, check provider status |
| `JSON parse error` | Gateway fails to start | `openclaw.json` with syntax error | `openclaw config validate`, fix JSON |
| `File not found` | Gateway fails to start | Non-existent file path in config | Check all paths in `openclaw.json` |
| `Skill conflict` | Bot erratic behavior | Two skills with conflicting instructions | Remove recently added skill, isolate problem |
| `AGENTS.md parse error` | Bot ignores instructions | Badly formatted AGENTS.md (open code block) | Close all code blocks in AGENTS.md |
| `Model not found` | Error processing message | Incorrect model name in config | Check exact naming in `openclaw status` |

---

## First Aid Checklist

- [ ] `openclaw status` — check overall state of models
- [ ] `openclaw gateway status` — confirm if gateway is running
- [ ] `openclaw gateway restart` — restart the gateway
- [ ] `openclaw config validate` — validate the configuration file
- [ ] `openclaw doctor` — complete environment diagnostic

---

## Production Notes

- **Recording environment:** Terminal with large font (16px+), dark theme
- **Show real errors:** Prepare intentionally broken configuration files for demonstration
- **Pause at key moments:** After each command, wait for the output to appear completely before speaking
- **Support material:** HTML for this lesson should be linked in the video description
- **Thumbnail:** Image with "5 steps" and bug/tools icon
