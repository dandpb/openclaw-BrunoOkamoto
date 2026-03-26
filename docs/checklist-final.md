# Final Checklist — Complete Course Validation

> Module 11: Wrap-up
> Use this checklist to confirm everything has been configured correctly.

---

## 🎯 How to Use This Checklist

1. Go module by module, checking each item
2. Mark `[x]` as you confirm it works
3. If something fails, go back to the corresponding module and fix it
4. **Don't skip items!** Each one validates something critical
5. At the end, you'll have a fully functional production OpenClaw agent

---

## ✅ Module 1: Setup & Infrastructure

**Goal:** Gateway running, Telegram connected, VPS secured.

- [ ] `openclaw gateway status` returns "running"
- [ ] Gateway is accessible via public URL (if configured)
- [ ] Telegram bot responds in 1:1 chat
- [ ] VPS has a fixed IP and is accessible via SSH
- [ ] Node.js version ≥ 18 installed (`node --version`)
- [ ] Git configured (`git config user.name` and `user.email`)
- [ ] Workspace at `/root/.openclaw/workspace-<name>` exists
- [ ] `.env` exists and contains `TELEGRAM_TOKEN`

**Quick test:**
```bash
curl -I http://localhost:3339/health  # should return 200 OK
```

---

## 🔒 Module 2: Security

**Goal:** Hardened server, secure credentials, allowlist active.

- [ ] UFW installed and active (`ufw status`)
- [ ] Only necessary ports open (22, 80, 443, 3339 if gateway is public)
- [ ] Fail2ban installed and running (`systemctl status fail2ban`)
- [ ] `dmPolicy: "allowlist"` configured in `config.yaml`
- [ ] `.env` contains credentials (not hardcoded in code)
- [ ] `.env` is in `.gitignore`
- [ ] Root login via SSH disabled (or uses SSH key)
- [ ] Automatic backups configured (cron or script)

**Quick test:**
```bash
cat ~/.openclaw/agents/<agent>/config.yaml | grep dmPolicy  # should be "allowlist"
grep ".env" .gitignore  # should exist
```

---

## 🧬 Module 3: Identity

**Goal:** Agent has personality, knows you, has its own name.

- [ ] `SOUL.md` exists and has ≥100 lines
- [ ] `SOUL.md` contains strong personality (not generic)
- [ ] `SOUL.md` has anti-patterns with ❌/✅ examples
- [ ] `USER.md` exists and has ≥200 lines (ideally 400+)
- [ ] `USER.md` contains routine, communication style, business info
- [ ] `USER.md` defines "do not disturb" hours
- [ ] `AGENTS.md` configured with operational rules
- [ ] `IDENTITY.md` exists (name, emoji, own email)
- [ ] `BOOT.md` exists with startup checklist

**Quick test:**
Ask the agent: "Who are you?" and "Who am I?" — the answers should be detailed and personalized.

---

## 🧠 Module 4: Memory

**Goal:** Persistent memory, daily notes, automatic compaction.

- [ ] `memory/` folder exists in the workspace
- [ ] `memory/YYYY-MM-DD.md` being created automatically every day
- [ ] `MEMORY.md` exists and contains curated insights (not raw logs)
- [ ] `memory/decisions.md` or similar exists (optional but recommended)
- [ ] Compaction configured (weekly or monthly cron)
- [ ] Agent extracts lessons BEFORE compacting (doesn't lose context)
- [ ] Compaction workflow documented in `AGENTS.md`

**Quick test:**
```bash
ls -la memory/  # should have a file with today's date
wc -l MEMORY.md  # should have at least 50 lines if used for a few days
```

---

## 🔌 Module 5: Integrations

**Goal:** At least 1 external integration working + 1 isolated cron.

- [ ] At least 1 integration configured (Gmail, Calendar, GitHub, etc.)
- [ ] Integration credentials in `.env` or 1Password
- [ ] Tested the integration manually (e.g.: "list my emails")
- [ ] At least 1 cron job configured
- [ ] Cron uses `sessionMode: "isolated"` + `notifyMode: "agentTurn"`
- [ ] **Never** `systemEvent` + `main` (this breaks context)
- [ ] Cron ran at least 1x and worked (check logs)
- [ ] Cron notifications arrive in the correct channel

**Quick test:**
```bash
openclaw cron list  # should list at least 1 cron
openclaw cron logs <id>  # should show recent executions
```

---

## 🛠️ Module 6: Skills

**Goal:** 2-3 skills installed and working.

- [ ] At least 2 skills installed (`openclaw skill list`)
- [ ] Skills were **reviewed** before installing (security)
- [ ] Skills manually tested and working
- [ ] Skill configurations documented in `TOOLS.md`
- [ ] No redundant skills (e.g.: 3 image generators)
- [ ] I understand when to use a skill vs when to create a cron vs when to ask the main agent

**Quick test:**
```bash
openclaw skill list --enabled  # should list active skills
```
Ask the agent to use a skill and confirm it works.

---

## 💓 Module 7: Proactivity

**Goal:** Heartbeats configured, agent checks things periodically.

- [ ] `HEARTBEAT.md` exists and contains a short checklist
- [ ] Heartbeat configured in `config.yaml` (interval ~30min)
- [ ] Heartbeat uses a cheap model (Haiku or Sonnet, not Opus)
- [ ] `heartbeat-state.json` exists in `memory/` (tracking checks)
- [ ] Agent checks email/calendar/notifications several times a day
- [ ] Agent knows when to stay quiet (HEARTBEAT_OK) vs when to notify
- [ ] Does not disturb late at night (11pm-8am) unless urgent

**Quick test:**
Wait for a heartbeat (or force one manually) and see if the agent takes any proactive action or returns `HEARTBEAT_OK`.

---

## 🤝 Module 8: Multi-Agents (Optional)

**Goal:** Agent team configured, with leveling and hierarchy.

If you configured multi-agents:

- [ ] `TEAM.md` exists with team description
- [ ] Each agent has its own `SOUL.md`
- [ ] Levels system (L1-L5) documented
- [ ] New agents start at L1 (Observer)
- [ ] Promotions based on performance (not automatic)
- [ ] Main agent knows when to delegate vs do it alone
- [ ] Subagents don't try to be the main agent

**Quick test:**
Ask the main agent to spawn a subagent and execute a delegated task. Confirm that the subagent reports back to main.

---

## 🛡️ Module 9: Immune System

**Goal:** Watchdog, feedback loops, model split, automatic backups.

- [ ] Watchdog configured (detects stuck agent/infinite loop)
- [ ] Retry policy: 2x retry → notify human (never silent limbo)
- [ ] Model split: Sonnet for crons, Opus for interaction, Haiku for heartbeats
- [ ] Feedback loops: agent learns from errors and updates docs
- [ ] Automatic backup before structural changes
- [ ] Error logs monitored (manually or via cron)
- [ ] Rollback plan documented (if something goes wrong)

**Quick test:**
Simulate an error (e.g.: a failing cron) and confirm that:
1. Retry happens
2. You are notified after 2 failures
3. Error is logged in `memory/`

---

## 📊 Module 10: Mission Control (Optional)

**Goal:** Visual panel to see system state.

If you configured Mission Control:

- [ ] Tool chosen (NocoDB/Notion/Sheets/Custom) running
- [ ] Tables created (Tasks, Memory, Crons, Health)
- [ ] Agent can write to the panel
- [ ] Crons update panel automatically
- [ ] Dashboard accessible via browser
- [ ] Credentials in `.env` (not hardcoded)
- [ ] Setup documented in `docs/mission-control-setup.md`

**Quick test:**
Ask the agent to log a task in the panel. Open the panel and confirm it appeared.

---

## 🎓 Final Validation

**Meta-checklist — confirm you master:**

- [ ] I know how to restart the gateway (`openclaw gateway restart`)
- [ ] I know where the logs are (`~/.openclaw/logs/`)
- [ ] I know how to create an isolated cron with agentTurn
- [ ] I know when to use Sonnet vs Opus vs Haiku
- [ ] I know how to manually back up the workspace
- [ ] I know how to review a skill's code before installing
- [ ] I know how to edit `config.yaml` without breaking the agent
- [ ] I know how to use `.env` for credentials
- [ ] I know when the agent should ask me vs do it alone
- [ ] I've read the 10 Inviolable Rules and understand why each one matters

---

## 🚀 Next Steps

If you checked everything above, **congratulations!** You have a production OpenClaw agent running.

**Now:**
1. **Use it for 7 days** — let it work, see what works and what doesn't
2. **Iterate** — adjust SOUL.md, HEARTBEAT.md, crons based on real usage
3. **Expand** — add more skills, integrations, automations as needs arise
4. **Document** — your `AGENTS.md` and `TOOLS.md` should grow over time
5. **Share** — teach someone, contribute to the community, create skills

**Remember the 10 Inviolable Rules** (see `docs/10-regras-inviolaveis.md`).

---

## 📝 Validation Log

Record when you completed this checklist:

```
Date: _______________
Completed items: ___ / 70+
Time since course start: ___ days
Next review: _______________ (recommended: 30 days)
```

---

**You didn't complete a course. You built a system.** 🎉
