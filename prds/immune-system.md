# PRD: Immune System

> "Agents are 30% of the work. The other 70% is the immune system." — Eric Siu
> Drop into the agent: "Implement this immune system"

## Context

Agents break silently. Crons fail without warning. Sub-agents get stuck in limbo. Without monitoring, you discover problems days later.

## 1. Cron Watchdog

Create a cron that monitors other crons:

**Logic:**
1. List all active crons
2. Check the last run of each one
3. If any failed → automatic retry (up to 3x)
4. If it failed 3x → alert the user in Telegram

**Configuration:**
```json
{
  "name": "Watchdog - Cron Monitor",
  "schedule": { "kind": "cron", "expr": "0 8 * * *", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Check the health of all crons. List those that failed in the last 24h. Retry the ones that failed. If any fails 3 times, alert via Telegram."
  },
  "delivery": { "mode": "announce" }
}
```

## 2. Feedback Loops

Continuous learning system: the agent learns from your decisions (approve/reject).

### Setup

Create `memory/feedback/` with JSON files by domain:

- `content.json` — feedback about content, drafts, suggestions
- `tasks.json` — feedback about task deliveries
- `recommendations.json` — feedback about tool/process suggestions

### Format

```json
{
  "entries": [
    {
      "date": "2026-02-13",
      "context": "Suggested thread about X for LinkedIn",
      "decision": "approve",
      "reason": "Spot-on tone, specific data",
      "tags": ["linkedin", "thread", "tone"]
    }
  ]
}
```

### Rules
- Max 30 entries per file (FIFO — removes the oldest ones)
- Agent MUST consult feedback before suggesting → avoids repeating mistakes
- Consolidate patterns in `lessons/` monthly
- Cycle: Feedback (granular, JSON) → Lessons (curated, prose) → Decisions (permanent)

## 3. Cost Monitoring

### Model split
| Usage | Model | Relative cost |
|-----|--------|---------------|
| Direct interaction | Opus | $$$ |
| Crons and automation | Sonnet | $ |
| Heartbeats | Haiku | ¢ |

### Rule
- ALL crons must run on Sonnet (never Opus)
- Heartbeats on Haiku
- Only direct interaction uses Opus

## 4. Sub-agents: Never "Fire and Forget"

Every spawned sub-agent MUST have a follow-up:

1. **When spawning:** inform what it will do
2. **Follow-up:** check status in 15-30 min
3. **Success:** summarize result in human language
4. **Failure:** immediate retry → if it fails 2x → notify the user
5. **Never** let it fall into silent limbo

## 5. Backup Before Changes

Before creating agents, modifying config, or reorganizing workspace:

```bash
mkdir -p backups/$(date +%Y-%m-%d)
cp /root/.openclaw/openclaw.json backups/$(date +%Y-%m-%d)/
```

## 6. Secrets Audit

### openclaw secrets audit (new in 3.2)

Version 3.2 brings a dedicated command to audit exposed secrets:

```bash
# Audit all workspace files for leaked secrets
openclaw secrets audit

# Audit specific directory
openclaw secrets audit --path /root/.openclaw/workspace-my-agent

# Output with detailed report
openclaw secrets audit --report
```

The command detects:
- API keys hardcoded in `.json`, `.md`, `.env` files
- Tokens in git history
- Credentials in SOUL.md, AGENTS.md or TOOLS.md
- Known patterns (OpenAI, Stripe, Telegram, AWS, etc.)

> ⚠️ Run `openclaw secrets audit` before sharing any workspace files or backing up to the cloud.

### openclaw doctor — Improved in 3.2

The `openclaw doctor` command was expanded in 3.2 and now checks:

```bash
openclaw doctor
```

Checks added in 3.2:
- ✅ `tools.profile` compatibility (detects profile incompatible with tasks)
- ✅ ACP dispatch status
- ✅ Quick secrets audit (most critical files)
- ✅ Node.js version and dependencies
- ✅ Connectivity with configured channels (Telegram, WhatsApp, Slack)
- ✅ Crons with invalid configuration (`systemEvent` + `main` = problem)

> 💡 Tip: run `openclaw doctor` after any version update or when something feels "off". It's the starting point for diagnosis.

## 7. Exec Approvals — Never Disable

OpenClaw can execute commands on your server. The approvals system is your last line of defense: when the agent wants to execute something outside the standard, it pauses and asks for your confirmation before proceeding.

**Why this exists:** In March/2026, 7 ways to bypass this system were found and fixed — attackers tried to hide dangerous commands using invisible Unicode characters, backslash-newline breaks, and wrappers for common tools (pnpm, npm, Perl). The system exists precisely to block this.

**Verify configuration:**
```bash
openclaw config get exec.approvals
# Should return: ask
```

**Never use `allow`** (executes everything without confirmation). Always keep it as `ask`.

> 📺 **Course tip:** Show the system pausing and requesting approval live. Students tend to think it's bureaucracy — showing the security context changes their perception.

## Checklist

- [ ] Cron watchdog active
- [ ] Feedback loops configured (at least 1 domain)
- [ ] Model split applied
- [ ] Sub-agent rule documented in AGENTS.md
- [ ] Automatic backup before changes
- [ ] `openclaw secrets audit` run — zero leaks confirmed
- [ ] `openclaw doctor` run with no critical errors
- [ ] `exec.approvals = ask` (never `allow`!) ← v2026.3.13

## Expected Result

A resilient system that self-monitors, learns from decisions, and doesn't let anything fall into limbo.
