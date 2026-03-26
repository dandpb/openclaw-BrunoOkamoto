# Prompt — Module 5: Integrations, Tools and Crons

> Paste this prompt in your OpenClaw chat after watching Module 5.
> Also attach the files: `prds/integrations-setup.md`, `configs/cron-examples.md`

---

I just finished watching Module 5 of the course on integrations and crons. Read the integrations PRD and guide me.

**What I need you to do:**

1. **Analyze my profile** — based on what you already know about me (USER.md), recommend the 3-5 most useful integrations to start with

2. **Guide me through the installation** of each integration, one at a time:
   - Explain what it does and why it's useful
   - Help me configure the API key securely
   - Test whether it worked

3. **Configure at least 2 crons:**
   - A reminder/calendar alert (so I can see it working)
   - An automatic report (daily briefing or metrics)
   - ALWAYS use: `sessionTarget: isolated` + `agentTurn` + `announce` (this is critical for it to work!)

4. **Explain common errors:**
   - Why `systemEvent` in the main session doesn't work as expected
   - Why crons at the same time cause problems
   - How config.patch affects running crons

**Rules:**
- Start with simple integrations (calendar, weather) before the complex ones
- If a cloud IP blocked error occurs, explain the solution (RapidAPI as proxy)
- ALL credentials go in 1Password — zero hardcoding in files
- Warning: systemd override overwrites .env — update BOTH when changing credentials
- At the end, show me the active crons and when they will run

**Production tip:**
- Use Telegram with a group + topics as the central hub
- Each cron delivers to the right topic — zero noise
- Split model: Sonnet for execution crons (sync, watchdog, reminders), Opus for analysis and strategy (~90% savings)

**Useful commands:**
```
openclaw channels status --probe
openclaw models fallbacks add <model>
openclaw models aliases add <alias> <model>
```

Shall we connect to the real world?
