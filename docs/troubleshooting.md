# 🔧 Troubleshooting — FAQ for Common Problems

> 35+ lessons learned in 13 days of production. If you got an error, the answer is probably here.

---

## 🔴 Critical (breaks everything if not resolved)

### My cron fires but doesn't execute anything
**Symptom:** Cron shows `status: "ok"` but `durationMs` is ~0ms. Nothing happens.
**Cause:** Using `systemEvent` + `sessionTarget: main`
**Solution:**
```json
{
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "your instruction here"
  }
}
```
**Rule:** ALWAYS use `isolated` + `agentTurn` + `announce` for crons.

---

### Token overflow — session overflowed
**Symptom:** Agent stops responding, context errors, truncated responses.
**Cause:** Context exceeded the limit without compaction configured.
**Solution:**
```json
{
  "compaction": { "mode": "default" },
  "contextTokens": 160000,
  "reserveTokensFloor": 30000
}
```
**Tip:** The `reserveTokensFloor` ensures the agent finishes its reasoning before compacting.

---

### Anyone can command my bot
**Symptom:** Strangers messaging your bot and it responding.
**Cause:** `dmPolicy` configured as `"open"`.
**Solution:** Change to `"allowlist"` and add only your Telegram ID:
```json
{
  "dmPolicy": "allowlist",
  "allowedUsers": ["YOUR_TELEGRAM_ID"]
}
```
**How to find your ID:** Send `/start` to @userinfobot on Telegram.

---

### I locked myself out of SSH
**Symptom:** Can't access the server after configuring the firewall.
**Cause:** UFW blocked the SSH port before allowing it.
**Solution:** Access via the web console of your Hostinger panel (or your VPS) and run:
```bash
sudo ufw allow ssh
sudo ufw allow 22/tcp
```
**Prevention:** ALWAYS run `sudo ufw allow ssh` BEFORE `sudo ufw enable`.

---

## 🟠 Important (works but with problems)

### Reminder/cron doesn't notify on Telegram
**Symptom:** Cron runs but no message appears on Telegram.
**Cause:** `systemEvent` doesn't send to channels — it's an internal event.
**Solution:** Use `agentTurn` + `delivery: { mode: "announce" }`. The agent needs to use the `message` tool to send.

---

### Multiple crons failing at the same time
**Symptom:** Some crons execute, others time out or fail.
**Cause:** Schedule collision — many crons at the same minute cause rate limiting.
**Solution:** Space crons at least 15-30 minutes apart.

---

### config.patch killed my crons
**Symptom:** Crons stopped after changing the config.
**Cause:** `config.patch` restarts the gateway and kills running crons.
**Solution:** Apply patches at times when no crons are running. Check schedule before changing.

---

### Cloud IP blocked by YouTube/Instagram/X
**Symptom:** Errors when trying to access YouTube transcripts, social media scraping.
**Cause:** Cloud IPs (AWS, Hetzner, DigitalOcean) are blocked by platforms.
**Solution:** Use **RapidAPI** as a proxy:
- YouTube Transcripts: Apify actor (~$0.007/video)
- Instagram: RapidAPI Instagram Statistics
- X/Twitter: RapidAPI API45
- Generous free tiers on most

---

### yt-dlp doesn't work on VPS
**Symptom:** Bot detection error when downloading videos.
**Cause:** YouTube blocks downloads from cloud IPs.
**Solution:** Use Tella.tv to record (automatic sync) or Apify for transcriptions.

---

### Agent loading 50KB of history every session
**Symptom:** Tokens burning fast, slow responses, high cost.
**Cause:** Session initialization without a loading rule.
**Solution:** Configure session initialization rule:
- Load ONLY: SOUL.md, USER.md, IDENTITY.md, memory/YYYY-MM-DD.md
- Use `memory_search()` on demand for the rest
- Reduces from 50KB → 8KB per session

---

## 🟡 Moderate (inconveniences)

### systemd override overwrites .env
**Symptom:** I changed the API key in .env but the agent uses the old one.
**Cause:** The systemd override takes precedence over .env.
**Solution:** Update BOTH: `.env` AND `systemctl edit openclaw` (override).

---

### Brave Search intermittent
**Symptom:** Searches fail sometimes.
**Cause:** Brave API has occasional instability.
**Solution:** Have a fallback with `web_fetch` directly to the URL.

---

### Sub-agent returns empty history
**Symptom:** Sub-agent spawn brings no result.
**Cause:** Sub-agents run in isolated sandbox — they don't access localhost.
**Solution:** Have a manual fallback. Sub-agent QA should run in the main session.

---

### Notion API only returns part of the data
**Symptom:** Pages/databases listing is incomplete.
**Cause:** Notion API uses pagination — without paginating, it only returns the first page.
**Solution:** Always implement pagination (`has_more` + `start_cursor`).

---

### Agent forgets to extract lessons before compacting
**Symptom:** After compaction, important information is gone.
**Cause:** Even with an "inviolable" rule, the agent sometimes forgets.
**Solution:**
1. Reinforce in AGENTS.md as an inviolable rule
2. Configure periodic consolidation (every 15 days) that reviews daily notes
3. This consolidation is the safety net — catches what slipped through

---

### trash-cli not found
**Symptom:** Error `trash: command not found`.
**Cause:** Not installed by default on Ubuntu.
**Solution:** `sudo apt install trash-cli`

---

## 💡 Production Tips

### Token savings
- **Heartbeat:** Haiku (~$0.005) or local Ollama (free)
- **Execution crons:** Sonnet (~90% savings vs Opus)
- **Interaction:** Opus (when quality matters)
- **Session initialization:** 8KB startup vs 50KB (~80% savings)

### Security
- Credentials ALWAYS in 1Password — zero hardcoding
- Quarterly API key rotation
- Weekly security audit (cron)
- `openclaw security-audit` + `openclaw doctor fix`
- App ports: `127.0.0.1` + Cloudflare Tunnel

### Memory
- MEMORY.md getting too large? Break it into topic files
- Strategic lessons = permanent, tactical = expire in 30 days
- Feedback loops in JSON: agent consults before repeating mistakes

### Multi-agents
- Every new agent starts L1 (Observer) — no automatic trust
- Hub model > Mesh model (central coordination)
- Agents that don't need Opus should not use Opus
- Sub-agent stalled? → retry 2x → if it fails → notify human (NEVER silent limbo)

---

*Based on 13 days of real production with Amora 🍇*
