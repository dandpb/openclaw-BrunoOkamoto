# 📋 MASTER PRD — Re-recording & Updating the OpenClaw Course
> Version: 1.0 · Date: 06/03/2026 · Author: Amora (curso-openclaw)
> Status: **AWAITING BRUNO'S APPROVAL**

---

## 1. CONTEXT AND OBJECTIVE

The OpenClaw course was structured in **12 modules (M0-M11)** + **5 extra lessons (A-E)** + **6 troubleshooting lessons (N1-N6)** between 15/02 and 06/03/2026.

Since the first lessons were recorded, OpenClaw has released **3 significant updates** (2026.2.12, 2026.2.21, 2026.3.2) with **critical breaking changes** that invalidate parts of the existing content.

Additionally, **~2000 messages from student groups** were collected (24/02 to 06/03), generating a ranking of the **Top 10 questions** that need to be addressed in the lessons.

**Objective:** Produce a complete plan for re-recording, updating, and creating new lessons, ensuring the course reflects version 2026.3.2+ and covers real student pain points.

---

## 2. COMPLETE LESSON INVENTORY

### 2.1 Main Modules (12)
| # | Module | Duration | Material Status | Recording Status |
|---|--------|---------|-----------------|-----------------|
| M0 | Opening | 10min | ✅ PRD ready | ❓ Check |
| M1 | Setup (VPS + Installation) | 25min | ✅ PRD ready | ✅ **RECORDED** (Lesson 1 — 04/03) |
| M2 | Security | 15min | ✅ PRD ready | ❌ NOT RECORDED |
| M3 | Identity | 25min | ✅ PRD ready | ❌ NOT RECORDED |
| M4 | Memory | 25min | ✅ PRD ready | ❌ NOT RECORDED |
| M5 | Integrations | 25min | ✅ PRD ready | ❌ NOT RECORDED |
| M6 | Skills | 15min | ✅ PRD ready | ❌ NOT RECORDED |
| M7 | Proactivity | 15min | ✅ PRD ready | ❌ NOT RECORDED |
| M8 | Multi-Agents | 20min | ✅ PRD ready | ❌ NOT RECORDED |
| M9 | Immune System | 20min | ✅ PRD ready | ❌ NOT RECORDED |
| M10 | Mission Control | 10min | ✅ PRD ready | ❌ NOT RECORDED |
| M11 | Wrap-up | 10min | ✅ PRD ready | ❌ NOT RECORDED |

### 2.2 Recorded Lessons (04/03/2026)
| # | Actual Recorded Topic | Corresponds to | Needs Re-recording? |
|---|-------------------|---------------|-------------------|
| Lesson 1 | How to install via VPS and remove Docker | M1 Setup | ⚠️ **YES** — missing `tools.profile full` |
| Lesson 2 | How to use Claude/OpenAI subscription in OpenClaw | N-1 OAuth | ⚠️ **PARTIAL** — Anthropic OAuth blocked |
| Lesson 3 | How to configure agents to execute tasks | N-3 Config Set | ✅ OK (covers `config set`) |
| Lesson 4 | What happens when the agent stops responding | N-4/N-5 Debug | ⚠️ **PARTIAL** — missing scenarios |

### 2.3 Extra Lessons (Material ready, not recorded)
| # | Topic | Material | Recording Status |
|---|------|----------|-----------------|
| Extra A | Tool Integration | ✅ PRD + Prompt + HTML + PDF | ❌ NOT RECORDED |
| Extra B | Debug on VPS with Claude Code | ✅ PRD + Prompt + HTML + PDF | ❌ NOT RECORDED |
| Extra C | Telegram Topics | ✅ PRD + Prompt + HTML + PDF | ❌ NOT RECORDED |
| Extra D | Evolutionary Automations | ✅ PRD + Prompt + HTML + PDF | ❌ NOT RECORDED |
| Extra E | Context & Memory | ✅ PRD + Prompt + HTML + PDF | ❌ NOT RECORDED |

### 2.4 Troubleshooting Lessons (Material ready, partially recorded)
| # | Topic | Material | Status |
|---|------|----------|--------|
| N-1 | OAuth & API Configuration | ✅ PRD + HTML + PDF | ⚠️ RECORDED (Lesson 2) — needs update |
| N-2 | Bot without Shell (Sandboxing) | ✅ PRD + HTML + PDF | ❌ NOT RECORDED |
| N-3 | Config Set (tools.profile) | ✅ PRD + HTML + PDF | ✅ RECORDED (Lesson 3) |
| N-4 | Telegram Slowness | ✅ PRD + HTML + PDF | ⚠️ PARTIAL (Lesson 4) |
| N-5 | Debug Runbook | ✅ PRD + HTML + PDF | ⚠️ PARTIAL (Lesson 4) |
| N-6 | VPS vs Mac Mini | ✅ PRD + HTML + PDF | ❌ NOT RECORDED |

---

## 3. TOP 10 STUDENT QUESTIONS (24/02 to 06/03/2026)

> Source: ~2000 messages from the "Tira Dúvidas OpenClaw" + "OpenClaw Geral 1" groups

| # | Question | Freq. | Lesson That Covers It | Status |
|---|--------|-------|----------------|--------|
| 1 | 🔑 **OAuth/Anthropic Token — "I can't authenticate"** | ~20x | N-1 (OAuth) | ⚠️ Needs update (Anthropic blocked OAuth for Pro) |
| 2 | 💥 **Context overflow — "Agent promises and disappears"** | ~15x | Extra E (Context) | ✅ Covered in material |
| 3 | 💰 **Subscription vs API — "How much will I spend?"** | ~15x | ❌ NEW LESSON NEEDED | 🆕 Create Costs lesson |
| 4 | 📹 **"Where are the lessons?" — Confusing onboarding** | ~12x | Not a lesson — it's a platform UX issue | 📋 Operational fix |
| 5 | 📱 **Telegram: bot doesn't respond in group** | ~12x | N-2 (Bot without Shell) + Extra C (Topics) | ⚠️ Needs specific section |
| 6 | 🏗️ **Sub-agents vs Sessions — "When to use?"** | ~10x | M8 (Multi-Agents) | ✅ Covered in material |
| 7 | 🖥️ **VPS vs Local — "Do I need a VPS?"** | ~10x | N-6 (VPS vs Mac Mini) | ✅ Covered in material |
| 8 | ⚙️ **Model per task — "Which model to use?"** | ~10x | ❌ NEW SECTION NEEDED | 🆕 Add to M1 or new lesson |
| 9 | 📱 **Google Integration (Drive/Gmail/Calendar)** | ~10x | Extra A (Integrations) + M5 | ⚠️ Needs update with gog |
| 10 | 🔧 **"My agent doesn't execute anything"** (tools.profile) | ~8x | N-3 (Config Set) | ✅ **COVERED — Lesson 3 recorded** |

### 3.1 New Lessons/Sections Derived from Student Questions

| Question | Action | Priority |
|--------|------|-----------|
| **Costs & Models** (#3 + #8) | Create new lesson: "How much it costs and which model to use" | 🔴 HIGH |
| **Onboarding** (#4) | Not a lesson — it's a direct link on the landing page + welcome message | 🟡 OPERATIONAL |
| **Telegram group** (#5) | Expand N-2 with section "Bot doesn't respond in group" (BotFather privacy) | 🔴 HIGH |
| **Google Integration** (#9) | Update Extra A with gog CLI step by step | 🟡 MEDIUM |

---

## 4. CHANGE ANALYSIS — OpenClaw Feb/Mar 2026

### 4.1 Releases Analyzed
- **2026.2.12** (12/02)
- **2026.2.21** (21/02) — Gemini 3.1, Telegram Streaming, Discord Voice, Apple Watch
- **2026.3.2** (03/03) — **CRITICAL BREAKING CHANGES**

### 4.2 Changes That Affect the Course

| Change | Release | Impact | Affected Lessons |
|---------|---------|---------|----------------|
| 🚨 **`tools.profile` default = messaging** | 3.2 | **CRITICAL** — new installs don't execute anything | M1, N-2, N-3 |
| 🔑 **`openclaw secrets` (64 targets)** | 3.2 | **HIGH** — replaces manual .env management | M2, M9 |
| ✅ **`openclaw config validate`** | 3.2 | **MEDIUM** — useful new command to teach | M1, M3 |
| 📺 **Telegram streaming = partial (default)** | 3.2 | **MEDIUM** — students see "typing" live | M1 (mention) |
| 🔒 **WebSocket loopback-only** | 3.2 | **MEDIUM** — remote panel without tunnel breaks | M2, Extra B |
| 🔒 **CVE CVSS 8.8 — 30k exposed instances** | 2.12 | **HIGH** — gateway on 0.0.0.0 without firewall | M2 (motivation) |
| 📄 **Native PDF tool** | 3.2 | **LOW** — new feature, nothing breaks | M5 (mention) |
| 🧠 **Ollama embeddings for memory** | 3.2 | **LOW** — local alternative | M4 (mention) |
| 🤖 **ACP dispatch enabled by default** | 3.2 | **LOW** — sub-agents routing | M8 (mention) |
| 📱 **Gemini 3.1 support** | 2.21 | **LOW** — more model option | M1 (model table) |
| ⌚ **Apple Watch companion** | 2.21 | **INFO** — new feature | M10 (mention) |
| 🎙️ **Audio echo transcript** | 3.2 | **INFO** — new config | Extra C (mention) |

### 4.3 Impact per Lesson — What Changed

| Lesson | Current Status | What needs to change |
|------|-------------|---------------------|
| **M1 Setup** | ⚠️ RE-RECORD | + `openclaw config set tools.profile full` (MANDATORY) · + `config validate` · + mention visual streaming · + updated model table (Gemini 3.1) |
| **M2 Security** | ⚠️ RE-RECORD | + `openclaw secrets audit/apply` replaces manual .env · + CVE 30k instances as motivation · + WebSocket loopback · + correct order: dmPolicy BEFORE UFW |
| **M3 Identity** | ✅ KEEP | + Just add `config validate` as a tip |
| **M4 Memory** | ✅ KEEP | + Mention Ollama embeddings as local option |
| **M5 Integrations** | ⚠️ UPDATE | + Native PDF tool · + gog CLI step by step |
| **M6 Skills** | ✅ KEEP | No relevant changes |
| **M7 Proactivity** | ✅ KEEP | No relevant changes |
| **M8 Multi-Agents** | ⚠️ UPDATE | + ACP dispatch default · + sessions_spawn attachments |
| **M9 Immune System** | ⚠️ UPDATE | + `openclaw secrets audit` in checklist · + improved `openclaw doctor` |
| **M10 Mission Control** | ✅ KEEP | + Mention Apple Watch |
| **M11 Wrap-up** | ✅ KEEP | No changes |
| **N-1 OAuth** | ⚠️ UPDATE | + Anthropic blocked OAuth for Pro · + new flow via API Key |
| **N-2 Bot without Shell** | ⚠️ UPDATE | + `tools.profile full` as cause #1 · + BotFather privacy mode |
| **N-3 Config Set** | ✅ KEEP | ✅ Already covers what's needed |
| **N-4 Slowness** | ✅ KEEP | No changes |
| **N-5 Debug Runbook** | ✅ KEEP | No changes |
| **N-6 VPS vs Mac Mini** | ✅ KEEP | No changes |
| **Extra A Integrations** | ⚠️ UPDATE | + gog CLI · + native PDF tool |
| **Extra B Debug VPS** | ✅ KEEP | No changes |
| **Extra C Topics** | ✅ KEEP | + Mention audio echo transcript |
| **Extra D Automations** | ✅ KEEP | No changes |
| **Extra E Context** | ✅ KEEP | No changes |

---

## 5. RE-RECORDING DECISION

### 🔴 RE-RECORD (content outdated or incomplete)
| Lesson | Reason | Priority |
|------|--------|-----------|
| **M1 Setup** (Lesson 1) | Missing `tools.profile full` — students get stuck | 🔴 P0 |
| **M2 Security** | `openclaw secrets` changes the entire flow + CVE | 🔴 P0 |
| **N-1 OAuth** (Lesson 2) | Anthropic OAuth blocked, needs new flow | 🔴 P1 |

### 🟡 UPDATE MATERIAL (optional re-recording, but docs need updating)
| Lesson | What to change in the material | Re-record? |
|------|------------------------|-----------|
| **M5 Integrations** | PDF tool + gog CLI | Optional |
| **M8 Multi-Agents** | ACP dispatch + attachments | Optional |
| **M9 Immune System** | `openclaw secrets audit` | Optional |
| **N-2 Bot without Shell** | tools.profile + BotFather | Recommended |
| **Extra A Integrations** | gog CLI | Optional |

### ✅ KEEP (no changes needed)
M0, M3, M4, M6, M7, M10, M11, N-3, N-4, N-5, N-6, Extra B, Extra C, Extra D, Extra E

### 🆕 CREATE NEW LESSON
| Lesson | Topic | Justification | Priority |
|------|------|--------------|-----------|
| **N-7** | **Costs & Models — "How much will I spend?"** | Top 3 student question (~15x). Clear table: Subscription vs API, cost per model, recommendation by use case, cheap model config for heartbeat/crons | 🔴 P1 |
| **N-8** | **Telegram: Bot doesn't respond in group** | Top 5 question (~12x). BotFather privacy, allowlist, dmPolicy vs groupPolicy, step-by-step diagnosis | 🔴 P1 |

---

## 6. EXECUTION PLAN — TASKS

### PHASE 1: Update Existing Material (Amora does)
> ⏱️ Estimate: 2-3 hours

| Task | Description | Depends on | Output |
|------|-----------|-----------|--------|
| T1.1 | Update M1 Setup PRD with `tools.profile full` + `config validate` + streaming | — | Updated PRD |
| T1.2 | Update M2 Security PRD with `openclaw secrets` + CVE + WebSocket | — | Updated PRD |
| T1.3 | Update N-1 OAuth PRD with new flow post-Anthropic block | — | Updated PRD |
| T1.4 | Update N-2 PRD with tools.profile as cause #1 + BotFather privacy | — | Updated PRD |
| T1.5 | Create N-7 PRD (Costs & Models) from scratch | — | New PRD |
| T1.6 | Create N-8 PRD (Telegram Bot in Group) from scratch | — | New PRD |
| T1.7 | Update M5, M8, M9, Extra A PRDs with minor changes | — | Updated PRDs |

### PHASE 2: Bruno's Approval
> ⏱️ Estimate: 30 min review

| Task | Description | Depends on |
|------|-----------|-----------|
| T2.1 | Bruno reviews change list (section 4.3 above) | T1.* |
| T2.2 | Bruno approves/rejects each item | T2.1 |
| T2.3 | Bruno defines recording order | T2.2 |

### PHASE 3: Generate Deliverables (Amora does)
> ⏱️ Estimate: 3-4 hours

| Task | Description | Depends on | Output |
|------|-----------|-----------|--------|
| T3.1 | Generate updated HTML for each modified lesson | T2.2 | HTMLs |
| T3.2 | Generate PDF for each modified lesson | T3.1 | PDFs |
| T3.3 | Generate/update student prompts for each modified lesson | T3.1 | Prompts .md |
| T3.4 | Generate consolidated HTML+PDF document (v2) with all lessons | T3.2 | curso-openclaw-completo-v2.html/pdf |
| T3.5 | Update Notion Knowledge Base with new Q&A | T3.1 | Updated Notion |

### PHASE 4: Recording (Bruno does)
> ⏱️ Estimate: depends on Bruno

| Task | What to record | Reference PRD | Priority |
|------|-------------|-------------------|-----------|
| T4.1 | **M1 Setup** (re-record) — include `tools.profile full` | Updated M1 PRD | 🔴 P0 |
| T4.2 | **M2 Security** (record from scratch) — `openclaw secrets` + CVE | Updated M2 PRD | 🔴 P0 |
| T4.3 | **N-1 OAuth** (re-record) — new post-block flow | Updated N-1 PRD | 🔴 P1 |
| T4.4 | **N-7 Costs & Models** (new) — cost table, model config | New N-7 PRD | 🔴 P1 |
| T4.5 | **N-8 Telegram Bot in Group** (new) — BotFather + allowlist | New N-8 PRD | 🔴 P1 |
| T4.6 | **N-2 Bot without Shell** (record) — tools.profile + diagnosis | Updated N-2 PRD | 🟡 P2 |
| T4.7 | **Remaining M3-M11** (record from scratch) | Existing PRDs | 🟡 P2 |
| T4.8 | **Extras A-E** (record) | Existing PRDs | 🟢 P3 |

### PHASE 5: Post-Production
| Task | Description | Depends on |
|------|-----------|-----------|
| T5.1 | Upload videos to the platform | T4.* |
| T5.2 | Link material (PDF/HTML/Prompt) to each video | T5.1 |
| T5.3 | Create welcome message with direct links to videos | T5.1 |
| T5.4 | Update landing page / Google Drive | T5.1 |

---

## 7. EXECUTIVE SUMMARY

| Metric | Value |
|---------|-------|
| **Total lessons in course** | 23 (12 modules + 5 extras + 6 troubleshooting) |
| **Already recorded lessons** | 4 (Lessons 1-4 on 04/03) |
| **Lessons that need RE-RECORDING** | 2 (M1 Setup, N-1 OAuth) |
| **Lessons that need to be recorded from scratch** | 19 |
| **New lessons to CREATE** | 2 (N-7 Costs, N-8 Telegram Group) |
| **Final total** | **25 lessons** |
| **Material that needs UPDATING** | 7 PRDs + HTMLs + PDFs |
| **Material OK (no changes)** | 16 lessons |
| **Top questions covered by course** | 9/10 (after creating N-7 and N-8) |
| **Question #4 (onboarding)** | Operational fix, not a lesson |

---

## 8. IMMEDIATE NEXT STEP

**Bruno needs to:**
1. ✅ or ❌ each item in section 4.3 (What changed per lesson)
2. Confirm creation of the 2 new lessons (N-7 and N-8)
3. Define recording order

**Once approved, I will:**
1. Update all PRDs (Phase 1)
2. Generate HTML + PDF + Prompt for each (Phase 3)
3. Deliver complete package ready to record

---

## 9. MISSING ITEMS IDENTIFIED IN DOUBLE CHECK

### 9.1 Existing Material Not Mentioned in the Original PRD

| Item | Status | Action |
|------|--------|------|
| **Bonus Module: Multi-Agent v2** | ✅ PRD + Prompt + HTML ready (`prds/multi-agent-v2.md`, `prompts/modulo-bonus-multi-agent-v2.md`, `pdfs/modulo-bonus-multi-agent-v2.html`) | Missing from inventory — add as **Bonus 1** |
| **Ebook 20 Use Cases** | ✅ v7 ready (`pdfs/ebook-20-use-cases-v7.html/pdf`) | Support material — not a lesson, it's a marketing/sales bonus |
| **PDFs per module (M0-M11)** | ✅ All generated (`pdfs/modulo-00-abertura.pdf` through `modulo-11-wrapup.pdf`) | Ready — check if they need updating with 3.2 changes |
| **Templates (6 files)** | ✅ SOUL, USER, AGENTS, IDENTITY, MEMORY, HEARTBEAT templates | Support material for modules M3-M7 |
| **Use Cases (6 categories)** | ✅ business, community, content, productivity, research, support | Support material — complements ebook |
| **Example configs** | ✅ `configs/cron-examples.md` + `configs/modelo-config.md` | Support material for modules M5 and M1 |
| **10 Inviolable Rules** | ✅ `docs/10-regras-inviolaveis.md` | Support material for M11 (Wrap-up) — **check if rule #2 needs updating** (now it's `openclaw secrets`, not `.env`) |
| **Troubleshooting doc** | ✅ `docs/troubleshooting.md` (35+ problems) | Support material — **check if it needs updating** |
| **Costs doc** | ✅ `docs/custos.md` | Support material for M11 — **check if values are still accurate** |
| **Automatic Setup Guide** | ✅ `docs/guia-setup-automatico.md` | Alternative speed run — **check if it needs `tools.profile`** |
| **Survival Guide** | ✅ `docs/guia-sobrevivencia-openclaw.html/pdf` | New — check content |
| **YouTube Agenda (Rony podcast)** | ✅ Complete agenda generated (23/02) | Not a course lesson — it's marketing content |
| **N-3 Config Set** | ⚠️ **HAS NO OWN PRD** — only exists in `memory/2026-03-04-config-set.md` | Create a dedicated PRD if it becomes a separate lesson, or keep as part of the already recorded Lesson 3 |
| **Notion Knowledge Base** | ✅ 14 published sections | **Needs updating** with 3.2 changes |

### 9.2 Identified Gaps

| Gap | Impact | Recommended Action |
|-----|---------|-----------------|
| **N-3 has no formal PRD** | Low (Lesson 3 already recorded and working) | Document the `config set` flow in the updated M1 PRD |
| **M0-M11 module PDFs may be outdated** | Medium (students may download PDFs with old info) | Regenerate after updating PRDs in Phase 1 |
| **10 Inviolable Rules — rule #2 outdated** | Medium (mentions .env, now it's `openclaw secrets`) | Update doc in Phase 1 |
| **`docs/custos.md` may have outdated values** | Medium (model prices change) | Check and update with current prices |
| **`docs/guia-setup-automatico.md` missing `tools.profile full`** | High (student follows speed run and gets stuck) | Update in Phase 1 |
| **`configs/modelo-config.md` may be missing Gemini 3.1 and MiniMax** | Low | Update with new models |
| **Notion Base outdated with 3.2 changes** | High (students consult and receive old info) | Add task T1.8 in Phase 1 |
| **No lesson about WhatsApp** | Medium (question #5 includes WhatsApp) | Consider section in N-8 or separate lesson |

### 9.3 Additional Tasks (complement Phase 1)

| Task | Description | Priority |
|------|-----------|-----------|
| T1.8 | Update Notion Knowledge Base (14 sections) with 3.2 changes | 🔴 HIGH |
| T1.9 | Update `docs/10-regras-inviolaveis.md` (rule #2: .env → openclaw secrets) | 🟡 MEDIUM |
| T1.10 | Update `docs/guia-setup-automatico.md` with `tools.profile full` | 🔴 HIGH |
| T1.11 | Check and update `docs/custos.md` with current prices | 🟡 MEDIUM |
| T1.12 | Update `configs/modelo-config.md` with Gemini 3.1 + MiniMax | 🟢 LOW |
| T1.13 | Regenerate M0-M11 PDFs after PRD updates | 🟡 MEDIUM (Phase 3) |
| T1.14 | Add Bonus Module (Multi-Agent v2) to official inventory | 🟢 LOW |
| T1.15 | Update `docs/troubleshooting.md` with new 3.2 problems | 🟡 MEDIUM |

### 9.4 Updated Count

| Metric | Before | After Double Check |
|---------|-------|----------------------|
| Total lessons | 25 | **26** (+1 Bonus Multi-Agent v2) |
| Support docs to update | 0 | **6** (10 rules, costs, setup guide, model config, troubleshooting, Notion Base) |
| Phase 1 tasks | 7 | **15** (+8 support material update tasks) |
| Marketing/bonus material | not listed | Ebook 20 Use Cases + YouTube Agenda |

---

## 10. FINAL EXECUTIVE SUMMARY (POST DOUBLE CHECK)

**Everything that needs to happen, in order:**

### 🔴 URGENT (before recording anything)
1. Update `guia-setup-automatico.md` with `tools.profile full`
2. Update Notion Base with 3.2 changes
3. Update PRDs M1 + M2 + N-1 + N-2

### 🟡 IMPORTANT (before publishing material)
4. Create PRDs N-7 (Costs) + N-8 (Telegram Group)
5. Update 10 Inviolable Rules
6. Update custos.md + troubleshooting.md
7. Regenerate all PDFs

### 🟢 NICE TO HAVE
8. Add Bonus Module to inventory
9. Update modelo-config.md
10. Check ebook use cases

---

*PRD generated by Amora · curso-openclaw · 06/03/2026*
*Double check performed: +8 tasks, +1 lesson, +6 support docs identified*
