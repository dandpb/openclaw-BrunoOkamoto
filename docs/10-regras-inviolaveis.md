# 🔒 10 Inviolable Rules

> Lessons distilled from 13 days running AI agents in production. Break any one and you'll feel it.

---

## 1. ALWAYS use `isolated` + `agentTurn` for crons

**Rule:** Every cron must use `sessionTarget: "isolated"` + `payload.kind: "agentTurn"` + `delivery: { mode: "announce" }`.

**Why:** `systemEvent` + `main` fires with `status: "ok"` but `durationMs` is ~0ms — meaning nothing actually executes. This bug alone broke our crons for 3 days.

**If broken:** Crons appear to work but nothing happens. You lose confidence in the entire system.

---

## 2. NEVER hardcode credentials

**Rule:** All API keys, tokens and passwords live in `.env` (or 1Password). Zero exceptions.

**Why:** If someone accesses your server (and they will try — 1,000+ brute force/day), they get ALL your keys at once. The `.env` with `chmod 600` is the last line of defense.

**If broken:** One leak = all your accounts compromised.

---

## 3. `dmPolicy: allowlist` from Day 1

**Rule:** Before doing anything else, configure the allowlist with your Telegram ID. Never leave it "open".

**Why:** With dmPolicy "open", anyone who finds your bot can command your agent — read your files, send emails, access your integrations.

**If broken:** Strangers controlling your agent with access to everything it has.

---

## 4. Extract lessons BEFORE each compaction

**Rule:** Before EACH session compaction, the agent must extract: lessons → `lessons.md`, decisions → `decisions.md`, pending items → `pending.md`.

**Why:** Compaction discards 80% of context. If you don't extract first, valuable information is gone forever. It's like formatting a hard drive without backing up.

**If broken:** Agent loses memory of decisions, mistakes and learnings. Goes back to making the same errors.

---

## 5. Every new agent starts at L1 (Observer)

**Rule:** No agent gains autonomy without a track record. L1 = output always reviewed. Promotion via weekly performance review.

**Why:** Agents without supervision "rush" — deliver fast but with low quality. Kevin Simback's Content Agent dropped from L3 → L2 when it started cutting corners.

**If broken:** Agents making wrong decisions without supervision. Silent damage you only discover days later.

---

## 6. Model split: Sonnet for crons, Opus for interaction, Haiku for heartbeats

**Rule:** Not every task needs the most expensive model. Execution crons on Sonnet. Heartbeats on Haiku (or local Ollama). Only direct interaction and strategic analysis on Opus.

**Why:** The difference is dramatic: ~$0.005/heartbeat on Haiku vs ~$0.10 on Opus. With 17 crons/day, the split saves ~75-80% of monthly cost.

**If broken:** API bill shoots up to $100-150/month when it could be $18-36.

---

## 7. Backup before structural changes

**Rule:** Before creating agents, modifying gateway config, or reorganizing workspace: save config + create ROLLBACK.md with rollback instructions.

**Why:** `config.patch` restarts the gateway and kills running crons. A config error can bring everything down. With a backup, you revert in 30 seconds.

**If broken:** Server down with no idea how to get back to the previous state.

---

## 8. Sub-agent stalled → retry 2x → notify human (NEVER silent limbo)

**Rule:** Every spawned sub-agent MUST have follow-up. Success = summary to user. Failure = automatic retry (2x). Failed 2x = immediate alert. Never "fire and forget".

**Why:** Sub-agents can stall silently. Without follow-up, tasks fall into limbo and no one knows. You think it was done, but it wasn't.

**If broken:** Tasks lost in limbo. Discovered days later when it's too late.

---

## 9. Generic SOUL.md = generic agent

**Rule:** Invest REAL time in the agent's personality. Anti-patterns with ❌/✅ examples. Explicit "Never dos". Inspirational anchors. Deep context in USER.md (400+ lines ideal).

**Why:** The difference between a generic and a customized SOUL.md is absurd — it's what separates "chatbot" from "COO". The agent is only as good as the context you give it.

**If broken:** Generic responses, no opinion, no personality. Basically an expensive ChatGPT.

---

## 10. Creators are skills, not agents

**Rule:** LinkedIn Creator, Newsletter Writer, Instagram Caption — these are prompts/skills INSIDE an agent. 1 agent with 8 skills > 8 specialized agents.

**Why:** Each extra agent = more cost, more coordination, more failure points. Skills inside an agent share context, memory and learnings. Separate agents start from scratch.

**If broken:** Multiplied cost, chaotic coordination, constant cold starts, fragmented learning.

---

## Bonus: The 3 operational rules

- **Space crons by 15-30 min** — collision = rate limit
- **`config.patch` at times with no crons** — restarts gateway and kills running crons
- **`systemEvent` does not notify on Telegram** — use `agentTurn` + `message send` for reminders

---

*Distilled from 13 days of real production. Every rule was learned the hard way. 🍇*
