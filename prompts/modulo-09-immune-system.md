# Prompt — Module 8: Immune System

> Paste this prompt in your OpenClaw chat after watching Module 8.
> Attach the file: `prds/immune-system.md`

---

I just watched Module 8 of the course on the immune system. "Agents are 30% of the work. The other 70% is the immune system." Read the PRD and guide me.

**What I need you to do:**

1. **Cron watchdog** — Set up a cron that monitors whether other crons are running. If any fail, automatic retry up to 3x. If it fails 3x, notify me.

2. **Feedback Loops** — Help me configure an approve/reject system:
   - When you suggest something and I reject it, note the reason
   - Consult those notes before suggesting again
   - Show me how this works in practice

3. **Cost monitoring:**
   - Configure the model split (Haiku for heartbeats, Sonnet for crons, Opus for interaction)
   - Configure rate limits and budgets to prevent runaway costs
   - Show me how much I'm spending per day/week
   - Goal: from ~$2-3/day to ~$0.10/day with optimizations

4. **Periodic security audit:**
   - Set up a weekly security audit cron
   - Run one now so I can see the result

5. **Backup before changes:**
   - Create a rule: before any structural change, save a backup + ROLLBACK.md
   - Show me how to roll back if something goes wrong

**Rules:**
- This module is what separates "I'm just playing" from "I'm in production"
- Explain each protection and what problem it prevents
- At the end, run a full health check and give me the score

Shall we build the immunity?
