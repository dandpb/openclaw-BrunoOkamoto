# PRD: Multi-Agent OS v2.0 — Advanced Architecture

> ⚠️ **Note (02/19/2026):** This PRD describes v2 as it was designed. The actual `shared/` structure was reorganized in Shared Memory v2 (see `shared/projects/PRD-SHARED-V2.md`). Paths like `shared/context/`, `shared/governance/`, `shared/costs/`, `shared/audit/`, `shared/lessons/`, and `TOOLS-SHARED.md` were consolidated into `shared/tools/`, `shared/assets/`, `shared/projects/`, `shared/decisions.md`, and `shared/lessons.md`.

> For when your single agent has become a bottleneck. Drop this into your main agent.

## 1. Context: Why Evolve?

### Problems with the v1 model (1 hub agent + workers)

| Problem | Symptom |
|---------|---------|
| **Central bottleneck** | Main agent coordinates AND executes — gets slow |
| **Context rot** | Long threads = worse responses (degradation before the limit) |
| **Zero governance** | No cost tracking, no audit, no digest |
| **No specialization** | One agent trying to be good at everything = mediocre at everything |
| **Broken scaling** | Adding more workers doesn't help if the hub is the bottleneck |

### The solution: Hierarchy with Bosses

Instead of 1 agent doing everything, you create an **organization**:

```
You (CEO)
    ↓
Main Agent (Chief of Staff) — coordinates, doesn't execute
    ↓
Bosses (by domain) — manage their workers
    ↓
Workers (specialized) — execute tasks
```

---

## 2. v2 Architecture

### Hierarchy

```
You (CEO)
    ↓ talk to
Main Agent (Chief of Staff, L4)
    — Does NOT execute tasks
    — Coordinates bosses
    — Governance + daily digest
    — Translates your priorities
    ↓
┌──────────────┬──────────────┬──────────────┐
│  Boss A      │  Boss B      │  Boss C      │
│  (domain 1)  │  (domain 2)  │  (domain 3)  │
│  Sonnet, L2  │  Sonnet, L2  │  Sonnet, L2  │
│  Own topic   │  Own topic   │  Own topic   │
└──────┬───────┴──────┬───────┴──────┬───────┘
       ↓              ↓              ↓
    Workers         Workers        Workers
    (L1, Haiku/    (L1, Haiku/    (L1, Haiku/
     Sonnet)        Sonnet)        Sonnet)
```

### What changes from v1 to v2

| Aspect | v1 | v2 |
|--------|----|----|
| **Main agent's role** | COO — does everything | CoS — coordinates, doesn't execute |
| **Delegation** | Hub → Workers directly | CoS → Bosses → Workers |
| **Governance** | None | Day 1: cost tracking, audit, digest |
| **Communication** | Everything goes through hub | You talk directly to bosses via topics |
| **Scaling** | Limited (hub = bottleneck) | Each boss is autonomous in their domain |
| **Cost** | Uncontrolled | Kill switch + per-agent tracking |

---

## 3. Defining Your Bosses

### How to decide which bosses to create

Answer: **"What are the 3-5 major domains of my work?"**

**Examples by profile:**

| Profile | Boss A | Boss B | Boss C | Boss D |
|---------|--------|--------|--------|--------|
| **SaaS Founder** | Content | Product/Ops | Dev | Analytics |
| **Freelancer** | Projects | Prospecting | Admin/Finance | — |
| **Creator** | Content | Community | Monetization | Analytics |
| **Startup** | Growth | Engineering | Customer Success | Data |
| **Agency** | Clients | Production | Sales | Ops |

### Rules for creating bosses

1. **Maximum 5 bosses** to start (complexity grows exponentially)
2. **Each boss = 1 clear domain** — if you can't describe it in 1 sentence, it's too big
3. **Boss ≠ Worker** — boss COORDINATES workers, doesn't execute everything alone
4. **Start with 2-3** — add based on real need, not speculative

---

## 4. Workers: Watcher vs Maker

Not every worker needs to be "always on." Two types:

### Watcher (Always on duty)
- Has active heartbeat (30-60 min)
- Reacts to events without the boss asking
- Cost: ~$1-2/month each
- **Example:** Community monitor, data scraper, metrics collector

```markdown
# HEARTBEAT.md (Watcher)
1. Read WORKING.md — has a task? Yes → execute. No → HEARTBEAT_OK
2. Check [data source] for news
3. If found something relevant → record in shared/outputs/
```

### Maker (Only exists when there's work)
- No heartbeat — boss uses `sessions_spawn` when needed
- Cost when idle: **$0**
- **Example:** Writer, editor, dev, data analyst

```
Boss receives request → spawns Maker with briefing → Maker delivers → Boss reviews
```

### Decision rule

> "Does this worker need to react to something without the boss asking?"
> → **Yes** = Watcher | **No** = Maker

---

## 5. Governance (FROM DAY 1)

> Governance is not "after it's working." It's the **foundation**.
> Without it, the system grows without visibility and costs explode.

### 5.1 Cost Tracking

```
shared/costs/
├── YYYY-MM-DD.csv       ← daily log (agent_id, model, tokens_in, tokens_out, cost_usd)
└── monthly-summary.md   ← monthly consolidation
```

### 5.2 Audit Log

```
shared/audit/
└── YYYY-MM-DD.jsonl     ← {timestamp, agent, api, endpoint, operation: read|write}
```

### 5.3 Daily Digest (automatic cron)

The CoS sends every morning:

```
🍇 Daily Digest — DD/MM/YYYY

✅ Yesterday: [X tasks per boss]
⚠️ Blockers: [list]
💰 Cost: $X.XX day | $X.XX month
🔔 Alerts: [anomalies]

Boss A: [1 line status]
Boss B: [1 line status]
Boss C: [1 line status]
```

### 5.4 Kill Switch

| Threshold | Action |
|-----------|--------|
| 2x expected cost | ⚠️ Alert on Telegram |
| 3x expected cost | 🚨 Notify you and ASK before pausing |

**NEVER auto-kill** — always ask for human confirmation.

### 5.5 Escalation Rules

| Situation | Who decides |
|-----------|-------------|
| Task within boss's domain | Boss decides alone |
| Involves real money (payments, refunds) | **Always asks for approval** |
| Cross-boss (needs another domain) | CoS coordinates |
| Urgent outside business hours | Notifies you |
| Error/rollback needed | Boss records + notifies CoS |

---

## 6. Shared Structure

```
shared/
├── TEAM.md                     ← Registry: who does what, level, status
├── context/
│   ├── USER.md                 ← Canonical — all inherit from here
│   ├── TOOLS-SHARED.md         ← Shared integrations
│   └── business-context.md     ← Business context
├── governance/
│   ├── DAILY-DIGEST-TEMPLATE.md
│   ├── CROSS-BOSS-PROTOCOL.md
│   ├── QUALITY-GATES.md
│   ├── ESCALATION-RULES.md
│   └── APPROVAL-LOG.md
├── costs/
│   └── YYYY-MM-DD.csv
├── audit/
│   └── YYYY-MM-DD.jsonl
├── templates/
│   ├── BOSS-WORKSPACE/         ← Template for new boss (8 files)
│   └── WORKER-WORKSPACE/       ← Minimum template for worker
├── outputs/                    ← Agent deliveries
└── lessons/                    ← Cross-agent lessons
```

### TEAM.md (Source of Truth)

```markdown
# 🏢 Team Registry

| Agent | Role | Level | Model | Type | Status |
|-------|------|-------|-------|------|--------|
| [name] | CoS / Hub | L4 | Sonnet | Main | Active |
| [boss-a] | Boss [domain] | L2 | Sonnet | Boss | Active |
| [boss-b] | Boss [domain] | L2 | Sonnet | Boss | Active |
| [worker-1] | [function] | L1 | Haiku | Watcher | Active |
| [worker-2] | [function] | L1 | Sonnet | Maker | Idle |
```

---

## 7. Communication

### You → Bosses (Direct Access)

Each boss has its own topic on Telegram. You talk **directly** with any boss:
- Boss A's topic → Boss A responds
- Boss B's topic → Boss B responds

The CoS **does NOT intercept** messages from the bosses' topics.

### Boss → Boss (Cross-Domain)

When a boss needs another:
1. Creates a card/record mentioning @[other-boss]
2. Reports in the daily digest
3. CoS coordinates in the next window
4. If urgent → boss mentions CoS directly

### Boss → Workers

- **Watcher:** Boss updates the worker's `WORKING.md` → worker picks it up on next heartbeat
- **Maker:** Boss uses `sessions_spawn` with complete briefing

---

## 8. Model Economics

| Tier | Suggested model | Estimated cost/month |
|------|----------------|---------------------|
| CoS (1x) | Sonnet | ~$30-50 |
| Bosses (3-5x) | Sonnet, active heartbeat | ~$5-8 each |
| Watchers (3-5x) | Haiku, heartbeat 30-60min | ~$1-2 each |
| Makers (5-10x) | Sonnet/Haiku, on demand | ~$0 when idle |
| **Estimated total (3 bosses)** | | **~$60-80/month** |
| **Estimated total (5 bosses)** | | **~$80-120/month** |

### Economics rules
- Worker that doesn't need Sonnet → **Haiku** (90% cheaper)
- Worker heartbeat → **Haiku** (even if the worker uses Sonnet for tasks)
- CoS does NOT need Opus — Sonnet coordinates well
- Maker idle = **$0** — no cost if not spawned

---

## 9. Leveling System

| Level | Name | Autonomy | Review |
|-------|------|----------|--------|
| L1 | Observer | Zero — output always reviewed | Every delivery |
| L2 | Contributor | Low — executes within guidelines | Weekly |
| L3 | Operator | Medium — autonomy with guardrails | Weekly |
| L4 | Trusted | High — almost total | Biweekly |

**Rules:**
- Every new agent starts at **L1**
- Promotion via weekly performance review
- Demotion is possible (if quality drops)
- **NEVER** rush an agent to L3+ without history

### Performance Review (weekly, automatic)

CoS runs review every Sunday with criteria:
1. **Responsiveness** — responded within SLA?
2. **Quality** — outputs needed correction?
3. **Cost** — within budget?
4. **Autonomy** — made good decisions independently?

---

## 10. Migration: v1 → v2 (Step by Step)

### Step 0: Backup (1 hour)
- [ ] Full backup of current workspace
- [ ] Verify backup is restorable
- [ ] Document current state (which agents, which crons)

### Step 1: Foundation (1 day)
- [ ] Promote main agent: COO → Chief of Staff
- [ ] Update SOUL.md with new role
- [ ] Create `shared/` with full structure
- [ ] Create Boss and Worker templates
- [ ] Activate governance: daily digest + kill switch

### Step 2: First Boss (2-3 days)
- [ ] Create Boss A workspace (use template)
- [ ] Configure Telegram binding (own topic)
- [ ] Add to agents.list
- [ ] Create 1-2 initial workers
- [ ] Test spawn chain: CoS → Boss → Worker
- [ ] Validate it works before advancing

### Step 3: Second Boss (2-3 days)
- [ ] Repeat Boss A process
- [ ] Test cross-boss communication
- [ ] Validate daily digest with 2 bosses

### Step 4: Remaining Bosses (1 day each)
- [ ] Follow the same pattern
- [ ] Maximum 1 new boss per day
- [ ] Always test before advancing

### Step 5: Hardening (ongoing)
- [ ] Automatic context sync (weekly cron)
- [ ] Memory lifecycle (cleanup of old notes)
- [ ] Weekly performance reviews
- [ ] Adjust workers based on actual usage

---

## 11. Emergency Restoration

If something goes wrong during migration:

```bash
openclaw gateway stop
cp -r ~/.openclaw/workspace ~/.openclaw/workspace-failed-v2/
cd ~/.openclaw
tar -xzf workspace-pre-v2-backup.tar.gz
openclaw gateway start
```

**Rule:** ALWAYS backup before each step. Paranoia is a feature, not a bug.

---

## 12. Expected Result

After v2 implementation, you will have:

- ✅ CoS coordinating (not executing)
- ✅ 3-5 autonomous Bosses by domain
- ✅ Specialized Workers (Watchers + Makers)
- ✅ Complete governance from Day 1
- ✅ Cost tracking with kill switch
- ✅ Automatic daily digest
- ✅ Weekly performance reviews
- ✅ Direct access to any boss via topic
- ✅ Controlled cost (~$60-120/month)

---

*"Agents are 30% of the work. The other 70% is the immune system + governance."*
