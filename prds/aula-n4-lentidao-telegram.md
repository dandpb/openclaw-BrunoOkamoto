# PRD — Lesson N-4: Bot Slowness on Telegram
## Debug and Performance Optimization

**Module:** N — Troubleshooting  
**Level:** Intermediate / Debug  
**Estimated duration:** 15–20 minutes  
**Instructor:** Bruno  
**Format:** Screenshare + narration (no camera)

---

## 🎯 Lesson Objective

By the end, the student will know:
1. How to diagnose why the bot is slow (model, VPS, or Telegram?)
2. How to identify and resolve the 6 most common causes of slowness
3. How to measure and monitor response time via logs
4. How to configure OpenClaw for optimal speed

---

## 🎬 RECORDING SCRIPT

### INTRO (0:00 – 1:30)

> **[Bruno speaks, screen shows Telegram with bot taking long to respond]**

*"You send a message to your bot on Telegram... and you stare at the blinking cursor. 5 seconds. 10 seconds. 30 seconds. Nothing."*

*"If this has happened to you, you're not alone. It's one of the most common complaints in the course. And the problem almost always has a quick fix — but you need to know where to look."*

*"In this lesson, we'll learn to diagnose slowness systematically. I'll show you the 6 most common causes, how to identify each one, and the exact solution for each situation."*

*"Let's go? Open your terminal along with me."*

---

### BLOCK 1: INITIAL DIAGNOSIS — IS IT THE MODEL, THE VPS, OR TELEGRAM? (1:30 – 4:00)

> **[Screen: terminal with `openclaw status` and then gateway logs]**

*"Before you start tweaking configs, we need to understand what's slow. There's a logical sequence here:"*

**[Show the flowchart mentally while speaking:]**

*"First — did Telegram receive your message? Did the gateway process it? Did the model respond? Did you receive the response?"*

*"Each step can have a different bottleneck. Let's start with the easiest: the `openclaw status` command."*

```bash
openclaw status
```

*"This command shows CPU usage, RAM, and the state of active processes. If CPU is at 100% or RAM is nearly zero — you already have your answer."*

*"Now, to see where the time is being spent, let's look at the gateway logs:"*

```bash
# Real-time logs
openclaw gateway logs --follow

# Or filter by response time
openclaw gateway logs | grep "response_time"
```

*"In the logs, you'll see timestamps. If the time between 'received message' and 'sent to model' is large — it's internal processing. If the time between 'model responded' and 'sent to telegram' is large — it's a network or webhook problem."*

*"If both are fast but the user doesn't receive — the problem is Telegram itself. Rare, but it happens."*

**[Dramatic pause]**

*"Now that we have our diagnostic toolkit, let's get to the causes. I have 6 to show you — from most common to least common."*

---

### BLOCK 2: CAUSE 1 — CONTEXT TOO LARGE (4:00 – 6:00)

> **[Screen: `/status` showing high context, e.g.: 85%]**

*"Cause number 1, and by far the most common: context full."*

*"Remember that Extra Lesson E explains how context works? Here's the practical impact: the more tokens in context, the more the model needs to process each message. A conversation with 80% context used can be 3 to 5 times slower than a new conversation."*

*"It's like a Word document with 500 pages open — every operation becomes heavy."*

*"Quick diagnosis:"*

```
# Any channel (Telegram, WhatsApp, etc.)
/status
```

*"If it shows '75%+' — you've found your cause."*

**Immediate solution:**

*"You have two options:"*

```
/compact   ← summarizes history, frees space, keeps context
/new       ← starts new session (loses history, starts from zero)
```

*"`/compact` is for when you want to continue where you left off. `/new` is for when you want a clean slate."*

*"To prevent this from happening in the future, configure automatic compaction:"*

```json
{
  "sessions": {
    "main": {
      "autoCompact": {
        "enabled": true,
        "thresholdPercent": 75
      }
    }
  }
}
```

---

### BLOCK 3: CAUSE 2 — MODEL TOO HEAVY (6:00 – 8:00)

> **[Screen: config file with model configured]**

*"Cause number 2: you're using a cannon to kill a fly."*

*"Claude Opus is the smartest model. But 'smartest' also means 'slower and more expensive.' If you configured Opus for absolutely everything — to respond to 'hi, how are you?' And to run notification crons — you're paying more and waiting longer than necessary."*

*"The golden rule is:"*

- **Sonnet** → normal conversations, day to day
- **Haiku** → crons, automatic alerts, simple and repetitive tasks  
- **Opus** → deep analysis, complex code, when quality > speed

*"How to configure this in openclaw.json:"*

```json
{
  "sessions": {
    "main": {
      "model": "claude-sonnet-4-6"
    }
  },
  "crons": {
    "defaultModel": "claude-haiku-4-5"
  }
}
```

*"And to switch models on the fly, without editing config:"*

```
/model sonnet    ← switches to Sonnet in this session
/model haiku     ← switches to Haiku
```

*"You'll feel the difference in practice. Haiku responds in 1-2 seconds. Opus can take 10-15s for complex analyses. Use the right one for each job."*

---

### BLOCK 4: CAUSE 3 — WEAK VPS (8:00 – 9:30)

> **[Screen: `openclaw status` showing CPU/RAM, or `htop`]**

*"Cause number 3: the server itself is choking."*

*"Most course students start with an entry-level VPS — 1GB RAM, 1 shared vCPU. That works for the beginning, but when you start stacking: gateway running, active crons, heavy skills, frequent heartbeats — it may not have enough headroom."*

*"How to diagnose:"*

```bash
openclaw status      # OpenClaw overview
htop                 # real-time CPU/RAM usage
free -h              # available memory
df -h                # disk space (swap issue)
```

*"Warning signs:"*
- Available RAM < 200MB
- CPU consistently > 80%
- Swap being used (this is terrible for performance)

*"Solutions, in order of cost:"*

1. **Free:** Optimize what's running (next causes)
2. **~$5/month:** Upgrade to 2GB RAM (Hetzner, DigitalOcean, etc.)
3. **Reorganize:** Move heavy crons to lower-traffic times

---

### BLOCK 5: CAUSE 4 — TOO MANY SIMULTANEOUS CRONS (9:30 – 11:00)

> **[Screen: cron config, several with the same time]**

*"Cause number 4: all your crons wake up at the same time."*

*"Imagine you have 5 crons configured. All at 09:00. The system wakes up, tries to run all 5 at the same time, all make calls to the model, all compete for the same CPU and memory. The main session waits in the queue."*

*"Diagnosis: list your active crons:"*

```bash
openclaw cron list
```

*"If you see several with identical or very close times — you've found the problem."*

*"Solution: stagger the times:"*

```json
{
  "crons": [
    { "name": "daily-summary", "schedule": "0 9 * * *" },
    { "name": "weather-check", "schedule": "5 9 * * *" },
    { "name": "news-digest", "schedule": "10 9 * * *" },
    { "name": "task-reminder", "schedule": "15 9 * * *" }
  ]
}
```

*"Space at least 5 minutes between heavy crons. Or spread them throughout the day — not everything needs to be at 9 AM."*

---

### BLOCK 6: CAUSE 5 — HEAVY SKILLS (11:00 – 12:30)

> **[Screen: AGENTS.md or skills config]**

*"Cause number 5: skills that take long to load on every turn."*

*"Some skills read large files, make network calls, or execute heavy code every time they're invoked. If you have skills like this configured to load automatically on every message — you're paying that cost on every request."*

*"Diagnosis: check your AGENTS.md or skills configuration:"*

```bash
# Which skills are loading automatically?
cat /root/.openclaw/workspace-*/AGENTS.md | grep -i skill
```

*"Solutions:"*

1. **On-demand loading:** Configure the skill to load only when needed, not on every turn
2. **Local cache:** If the skill fetches external data, add caching (e.g., fetch weather only every 30 min)
3. **Review the list:** Do you really need all active skills? Disable the ones you don't use

```json
{
  "skills": {
    "loadOnDemand": true,
    "autoload": ["weather"]
  }
}
```

---

### BLOCK 7: CAUSE 6 — HEARTBEATS TOO FREQUENT (12:30 – 13:30)

> **[Screen: heartbeat configuration]**

*"Cause number 6: heartbeat too fast."*

*"The heartbeat is the periodic check the agent makes — email, calendar, notifications. If you configured it to check every 5 minutes, you have 12 model invocations per hour. In the background. Competing with your conversations."*

*"Diagnosis:"*

```bash
# Check current heartbeat configuration
cat ~/.openclaw/config.json | grep -A 5 heartbeat
```

*"Solution — adjust the interval:"*

```json
{
  "heartbeat": {
    "enabled": true,
    "intervalMinutes": 30,
    "model": "claude-haiku-4-5"
  }
}
```

*"Golden rule: heartbeat every 30 minutes is enough for 95% of cases. And always use Haiku for heartbeat — it's fast and cheap."*

---

### BLOCK 8: WHEN THE PROBLEM IS TELEGRAM (13:30 – 14:30)

> **[Screen: logs showing model response time vs delivery time]**

*"There's a seventh cause that isn't your setup's fault: Telegram itself."*

*"Occasionally — especially in regions farther from Telegram's datacenters, or during platform traffic peaks — messages take long on the network before reaching the webhook. Or before being delivered back."*

*"How to identify: the gateway logs will show normal model response time, but large delivery delay:"*

```
[15:23:01] Message received
[15:23:01] Sent to model
[15:23:04] Model responded (3s) ← normal
[15:23:09] Delivered to Telegram (5s) ← suspicious
```

*"In this case, the short-term solution is to enable partial streaming:"*

```json
{
  "channels": {
    "telegram": {
      "streaming": "partial"
    }
  }
}
```

*"With partial streaming, the user starts seeing the text arriving while the model is still generating. The complete response may take the same time — but the perception of speed improves a lot. It's the difference between 'the bot didn't respond' and 'the bot is typing'."*

---

### RECAP AND CONCLUSION (14:30 – 16:00)

> **[Screen: diagnostic flowchart or summary slides]**

*"Let's recap what we saw today:"*

*"When the bot is slow, follow this order:"*

1. **`openclaw status`** → CPU/RAM OK?
2. **`/status` in chat** → context above 75%? → `/compact` or `/new`
3. **Gateway logs** → where is the delay?
4. **Model** → Opus where it should be Sonnet?
5. **Crons** → too many at the same time?
6. **Heartbeat** → intervals too short?
7. **Skills** → something loading on every turn?
8. **Streaming** → enable `partial` if the problem is perception

*"The good news: in most cases, the problem is full context or wrong model — and both are resolved in under 2 minutes."*

*"Thanks, everyone! In the next lesson we'll talk about how to configure alerts to warn you before the bot gets slow. See you there!"*

---

## 📋 PRE-RECORDING CHECKLIST

- [ ] Terminal open with gateway running
- [ ] Bot configured on Telegram (for demo)
- [ ] Example `openclaw.json` file prepared
- [ ] Gateway logs with real timing examples
- [ ] Screenshare on 1920x1080 resolution monitor
- [ ] Microphone tested, no background noise
- [ ] Screen recording: OBS or Loom

## 📁 REQUIRED ASSETS

- Diagnostic flowchart (included in the lesson HTML)
- Causes/solutions table (included in the lesson HTML)
- Gateway log examples (simulated if necessary)

---

*PRD generated on: 2026-03-04 | Version: 1.0*
