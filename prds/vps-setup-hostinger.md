# PRD: VPS Setup on Hostinger (Bare Metal, no Docker)

> Step-by-step guide for Module 1 of the course.
> Bruno follows this script during recording.
> **Updated for OpenClaw v2026.3.2**

---

## Prerequisites

- Hostinger account (https://www.hostinger.com)
- Anthropic account (https://console.anthropic.com) with active billing
- Telegram installed on your phone

## Estimated time: 15-20 minutes

---

## Step 1: Create the VPS on Hostinger (3 min)

1. Go to https://www.hostinger.com/vps-hosting
2. Choose the cheapest plan (KVM 1 — sufficient for OpenClaw)
   - 1 vCPU, 4GB RAM, 50GB SSD — more than enough
3. **IMPORTANT:** Do NOT use the OpenClaw Docker/One-Click template
4. Select **Ubuntu 24.04** as the operating system
5. Set a strong root password (or SSH key if you know how)
6. Note down the VPS IP

> **Why not the One-Click Docker?**
> Docker isolates the agent in a container — installing skills, integrations and extra tools becomes much more complicated. For non-technical users, it's an unnecessary barrier. Installing directly, everything works as expected.

---

## Step 2: Connect to the VPS via SSH (2 min)

### On Mac/Linux:
```bash
ssh root@YOUR_VPS_IP
```
(enter the password when prompted)

### On Windows:
- Use PuTTY or Windows Terminal
- Host: YOUR_VPS_IP
- User: root

### First time? Hostinger has a terminal in the panel:
- hPanel → VPS → Terminal (button at the top)
- Works directly in the browser, no installation needed

> 💡 **Tip for the course:** Show both options (local terminal + panel terminal) to accommodate those who don't know how to use SSH.

---

## Step 3: Install OpenClaw (3 min)

```bash
# Install OpenClaw (1 command)
curl -fsSL https://openclaw.ai/install.sh | bash
```

This installs Node.js (if needed) and OpenClaw.

Then, run the setup wizard:

```bash
openclaw onboard --install-daemon
```

The wizard will ask:

1. **Gateway mode:** → Choose `Local`
2. **AI Provider:** → Choose `Anthropic`
3. **API Key:** → Paste the Anthropic API key
4. **Model:** → Choose `Claude Sonnet` (good and cheap to start)
5. **Install as service?** → Yes (runs 24/7 automatically)

> 💡 **Tip for the course:** Show where to get the API key on Anthropic (console.anthropic.com → API Keys → Create Key). Explain that billing needs to be active.

---

## ⚠️ Step 3.5: Configure Tools Profile (NEW — v2026.3.2)

> 🔴 **CRITICAL:** This step is MANDATORY starting from version 2026.3.2. Without it, your agent will respond to messages but won't be able to do ANYTHING useful.

Starting from version **2026.3.2**, OpenClaw comes with `tools.profile = messaging` by default. This means the agent can only respond to messages, but **CANNOT** execute commands, read files, use tools, or do anything beyond chatting.

To have a truly functional agent, you NEED to change to the `full` profile:

```bash
openclaw config set tools.profile full
```

Then, validate everything is correct with the new validation command:

```bash
openclaw config validate
```

The output should show something like:

```
✅ tools.profile: full
✅ gateway.mode: local
✅ ai.provider: anthropic
✅ Configuration valid — 0 warnings
```

> 💡 **Why did this default change?** Anthropic and the security community identified that many installations exposed on the internet gave full tool access to anyone who found the bot. The new `messaging` default is safer for those who don't know what they're doing. But **for the course**, we want `full` — hence this step.

> 📺 **Tip for the course:** Show the "before and after" — send a message to the bot without configuring (`tools.profile = messaging`) and see it responding but unable to execute commands. Then configure and show the difference. Very educational!

---

## ⚠️ Step 3.6: Configure Timezone (NEW — v2026.3.13)

> 🕐 **IMPORTANT for those who will use crons:** Without this step, all your crons will fire in UTC time — 3 hours ahead of Brazil. A cron set to "every day at 9am" will fire at 12pm.

```bash
sudo systemctl edit openclaw
```

In the editor that opens, add inside `[Service]`:

```
[Service]
Environment="OPENCLAW_TZ=America/Sao_Paulo"
```

Save and apply:

```bash
sudo systemctl daemon-reload
sudo systemctl restart openclaw
```

Verify the gateway restarted correctly:

```bash
openclaw gateway status
```

> 📺 **Tip for the course:** Demonstrate the effect live — create a test cron, show it firing at the wrong time (UTC), then configure OPENCLAW_TZ and show the correct time. Very educational moment.

---

## Step 4: Verify it's running (30 sec)

```bash
openclaw gateway status
```

Should show: `running` ✅

If you want to see the web panel:
```bash
openclaw dashboard
```
Access: `http://YOUR_IP:18789`

> 📡 **New in v2026.3.2:** Telegram streaming is now enabled by default. When your agent is "thinking", you'll see the "typing..." indicator in Telegram in real time. This is normal and expected — the agent is processing your message live!

---

## Step 5: Create the Bot on Telegram (3 min)

1. Open Telegram on your phone
2. Search for `@BotFather`
3. Send `/newbot`
4. Choose a name (e.g., "My AI Agent")
5. Choose a username (must end in "bot", e.g., "myagentai_bot")
6. **Copy the token** that BotFather gives you

---

## Step 6: Connect Telegram to OpenClaw (2 min)

Back in the VPS terminal:

```bash
openclaw provider add telegram
```

When prompted, paste the bot token.

Then, open the chat with your bot on Telegram and send `/start`.

---

## Step 7: IMMEDIATE Security (2 min)

**BEFORE doing anything else**, harden access:

```bash
# Check current config
cat ~/.openclaw/openclaw.json
```

Make sure `dmPolicy` is set to `allowlist` and that ONLY your Telegram ID is authorized.

To discover your Telegram ID:
- Send any message to the bot
- Check the logs: `openclaw gateway logs`
- The ID appears in received messages

> 🔴 **ALERT in the course:** If dmPolicy is "open", ANYONE who finds your bot can command your agent. This is an extremely serious security risk. Emphasize this in the video.

---

## Step 8: First test (1 min)

Send a message to the bot on Telegram:

> "Hi! Tell me who you are and what you can do."

If the agent responds → **SETUP COMPLETE!** 🎉

> 📱 **New in v2026.3.2:** You'll see "typing..." appear in Telegram while the agent processes. This is active streaming — it's normal and means the agent is working!

---

## Module 1 Checkpoint

- [ ] VPS running on Hostinger (Ubuntu 24.04)
- [ ] OpenClaw installed (bare metal, not Docker)
- [ ] Gateway running as a service (24/7)
- [ ] **`tools.profile = full` configured** ← NEW (v2026.3.2)
- [ ] `openclaw config validate` with no errors ← NEW (v2026.3.2)
- [ ] **`OPENCLAW_TZ=America/Sao_Paulo` configured** ← NEW (v2026.3.13)
- [ ] Telegram bot created and connected
- [ ] dmPolicy = allowlist (basic security)
- [ ] First "hi" responded ✅

---

## Common Troubleshooting

### "Command not found: openclaw"
```bash
# Reload PATH
source ~/.bashrc
# Or reinstall
curl -fsSL https://openclaw.ai/install.sh | bash
```

### "Invalid API key"
- Check if billing is active on Anthropic
- Copy the key again (without extra spaces)

### "Bot not responding on Telegram"
```bash
# Check logs
openclaw gateway logs
# Check status
openclaw gateway status
```

### "Agent responds but can't execute commands" (NEW — v2026.3.2)
```bash
# Symptom: bot responds "I can't do that" for any task
# Cause: tools.profile is still set to 'messaging'
openclaw config set tools.profile full
openclaw gateway restart
```

### "Gateway won't start"
```bash
# Check port
ss -tlnp | grep 18789
# Restart
openclaw gateway restart
```

---

## How much does it cost?

| Item | Monthly cost |
|------|-------------|
| Hostinger VPS (KVM 1) | ~$5-10/month |
| Anthropic API (moderate use) | ~$10-30/month |
| Gemini 3.1 Pro API (alternative) | ~$5-15/month |
| Telegram | Free |
| **Total (Anthropic)** | **~$15-40/month** |
| **Total (Gemini — budget option)** | **~$10-25/month** |

> 💡 **Tip for the course:** "Less than a lunch per week to have a 24/7 AI assistant"

> 💰 **Budget option:** Gemini 3.1 Pro ($1.25/M input tokens) is a viable and cheaper alternative to Claude Sonnet for those who want to start with lower costs. For simple tasks and heartbeats, it works very well!

---

*This is the most technical module. After this, it's just configuring the agent — and that's the fun part.* 🍇
