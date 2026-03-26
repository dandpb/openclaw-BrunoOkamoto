# Prompt — Module 1: OpenClaw Setup

> Paste this prompt in your OpenClaw chat after watching Module 1.

---

I just finished watching Module 1 of the "Build Your AI COO" course. I need you to guide me through the initial OpenClaw setup.

**What I need to do:**

1. **Check my environment** — Verify that Node.js, npm and dependencies are installed correctly. If anything is missing, explain what it is and help me install it.

2. **Configure the provider** — Help me configure the Anthropic (Claude) API key. Explain where to get the key and how to configure it.

3. **Activate the tools profile** — Run `openclaw config set tools.profile full` and explain why this is mandatory. Without it, you don't execute commands — you only respond to messages. Then run `openclaw config validate` to confirm the configuration is valid.

4. **Choose the model** — Explain the difference between Sonnet, Opus and Haiku. Recommend which one to start with (considering cost vs quality). Configure the failover chain (Opus → Sonnet → Cooldown).

5. **Connect to Telegram** — Guide me step by step to create a bot in BotFather and connect it to OpenClaw. Explain why Telegram with topics is better than WhatsApp (single session vs multiple). Use `openclaw channels login` and `openclaw channels status --probe` to validate.

6. **First test** — After everything is configured, run a health check and confirm everything is working. Include a command execution test (e.g.: `echo "SHELL_TEST_OK"`) to prove that tools.profile full is active.

7. **Initial token optimization** — Configure the session initialization rule to avoid loading 50KB of history with every message:
   - Load ONLY: SOUL.md, USER.md, IDENTITY.md, memory/YYYY-MM-DD.md
   - Do NOT load automatically: MEMORY.md, session history, previous outputs
   - Use `memory_search()` on demand when prior context is needed

**Rules:**
- Explain the WHY behind each step before executing
- If something goes wrong, explain what happened and how to fix it
- At the end, tell me approximately how much this will cost per month
- Cost reference: before optimization ~$2-3/day, after ~$0.10/day

8. **Timezone (REQUIRED if you'll use crons)** — Configure the gateway timezone so your crons fire at the correct time for Brazil. Without this, a cron configured for "9am" will fire at 12pm (UTC):

```bash
sudo systemctl edit openclaw
# Add inside [Service]:
# Environment="OPENCLAW_TZ=America/Sao_Paulo"
sudo systemctl daemon-reload && sudo systemctl restart openclaw
```

**Useful commands for this module:**
```
openclaw gateway start --mode local
openclaw config set tools.profile full
openclaw config validate
openclaw channels login
openclaw channels status --probe
openclaw models list --all
openclaw models set <model>
```

Shall we begin?
