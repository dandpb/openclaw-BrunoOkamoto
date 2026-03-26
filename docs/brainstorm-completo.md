# 🎓 Mini-Course: Build Your Personal AI Agent with OpenClaw

> **Brainstorm & Complete Proposal — v2**
> Created: 02/13/2026 | Updated: 02/13/2026
> Author: Amora (for Bruno Okamoto)
> Estimated duration: 2h30 - 3h

---

## PART 1 — TIMELINE OF OUR JOURNEY (13 days)

### Day 1 (02/01) — Birth of Amora 🍇
**What was done:**
- OpenClaw installation on the VPS
- Initial setup: IDENTITY.md, USER.md, references/bruno-bios.md
- Role definition: organization, emails, content, research, sub-agent coordination

**Key decisions:**
- Amora as COO (Chief Operational Officer), not just a chatbot
- Bootstrap philosophy: small, lean, profitable

**"Aha" moment:**
- The realization that the agent needed deep context about Bruno (business, philosophy, tone of voice) to be truly useful

---

### Day 2 (02/02) — First Integrations & First Bugs
**What was done:**
- LinkedIn login via browser automation ✅
- Twitter/X via RapidAPI (bot detection prevented direct login) ✅
- Reddit monitoring with 30 subreddits + daily cron ✅
- LinkedIn Voice Guide (analysis of 129 Bruno posts) ✅
- WhatsApp TTS configured ✅

**Problems encountered:**
- 🔴 **Token overflow**: Session exceeded 173k+ tokens (limit 160k). Fix: `compaction.mode: "default"` + `reserveTokensFloor: 30000`
- 🔴 **Substack blocked**: CAPTCHA + 2FA magic link expired before entering the code
- 🔴 **X.com bot detection**: Headless login impossible. Solution: RapidAPI as proxy

**Lessons learned:**
- Cloud IPs are blocked by many platforms (YouTube, X, etc.) → RapidAPI solves it
- Compaction needs to be proactive, not reactive
- Bruno prefers 1-paragraph briefs (not long analyses)

---

### Day 3 (02/03) — Skills & Integrations
**Skills installed:** excalidraw-flowchart, capability-evolver, nano-pdf, notion-api, remind-me, auto-updater, granola
**Integrations:** Notion API ✅, Google Calendar ✅, YouTube (RapidAPI transcripts + Data API) ✅

**Decisions:**
- Heartbeat uses Claude Haiku (~90% savings)
- ImageModel: Gemini 2.5 Flash
- Daily auto-update cron at 11 PM

**Lessons:**
- Some skills are redundant (remind-me, auto-updater) — better to do it natively
- WhatsApp audio: OGG Opus 48kHz format works

---

### Day 4 (02/04) — Security, Circle API & Infographics
**What was done:**
- **PERMANENT rule**: all credentials in 1Password, no exceptions
- Hand-draw-graphics skill created (notebook-style infographics)
- VPH Tracking (Views Per Hour) for YouTube
- Circle API skill complete (hot-topics, frequent-questions, trends, digest)
- 11 build ideas documented
- Notion kanban integrated

**Problems:**
- Imagen 4.0 blocked (requires billing) → better model: Gemini 3 Pro
- VidIQ has no public API

**"Aha" moment:**
- Circle API as a content ideas goldmine (150 MVPs in 60 days in the community)

---

### Day 5 (02/05) — Mission Control & Multi-Agent Blueprint
**What was done:**
- **Mission Control MVP built and launched** (Express + React + Supabase + Cloudflare)
  - Kanban Dashboard, Memory Page, Crons Page, Content Page
  - URL: https://amora.empreendedor.vc
- Google Drive integrated via GOG CLI
- YouTube OAuth complete (upload/scheduling)
- YouTube reminder crons (Tue/Thu/Sun 5 PM)
- Multi-Agent Blueprint based on Bhanu Teja's article (10 agents)

**Decisions:**
- Supabase > SQLite (future scalability)
- Thinking mode enabled (low default)
- Desktop-first for MVP, no chat (WhatsApp is enough)

**Problems:**
- Sub-agents run in sandbox → can't access localhost → QA needs to run in main session

**BIG "Aha" moment:**
- Mission Control built while Bruno was sleeping — from spec to working MVP in one session

---

### Day 6 (02/06) — QA & Peter Levels Interview
**What was done:**
- Complete QA Review of Mission Control (RLS, rate limiting, validation, indexes, WebSocket)
- Deep research for Peter Levels interview
- Custom questions (avoiding overdone topics)

**Lesson:**
- Default TTS: always pt-BR

---

### Day 7 (02/07) — Complete Identity Rewrite
**What was done:**
- SOUL.md rewritten from scratch (generic English → customized PT-BR)
- IDENTITY.md updated with entrepreneur background
- AGENTS.md trimmed (200 → 90 lines)
- Upgrade to Claude Opus 4.6
- Config optimized: thinking medium, contextTokens 250k, reserveTokens 50k

**Decisions:**
- Amora = COO, not a generic assistant
- HIGH thinking for coding, content and planning. MEDIUM for everything else.
- Each agent will have its own SOUL.md, AGENTS.md, HEARTBEAT.md and crons
- IDENTITY.md separate from SOUL.md (concrete data vs personality)

**"Aha" moment:**
- Generic SOUL.md = generic agent. Investing time in personality makes an ENORMOUS difference in quality

---

### Day 8 (02/08) — Content Squad & Agent Leveling
**What was done:**
- 6 active agents on the gateway (Amora, Content, Orchestrator, Planner, Scraper, ZoM)
- Kevin Simback Rules applied: L1→L4 leveling system
- Shared context: TEAM.md, outputs, lessons
- Scraper Agent + Content Agent created and configured
- LinkedIn posts created with community data (Craft API)
- Public guide: `building-ai-agent-teams.md` (~25k chars)
- Visual architecture infographic

**Decisions:**
- Content Agent starts on Sonnet (evaluate before upgrading to Opus)
- Scraper and Content don't have Telegram binding — Amora coordinates everything
- Score is informational, NOT a blocking filter
- Creators are skills within the Content Agent, not separate agents
- Backup mandatory before structural changes

**Kevin Simback Lessons:**
- Every new agent starts at L1 (Observer) — output reviewed
- Without leveling, agents "rush" and quality degrades
- Shared context eliminates cold starts
- Weekly performance reviews are mandatory

---

### Day 9 (02/09) — Crons & Stabilization
**What was done:**
- Reorganization of 13 crons (topic redirection, new crons)
- Central PROJECTS.md created (12 items in backlog)
- Automatic Weekly Review (Fri 4 PM)
- Biweekly Auto-Evolution (days 1 and 15)

**CRITICAL Problem:**
- 🔴 **Crons don't actually execute**: they fired with `status: "ok"` but `durationMs` ~0ms
- Hypotheses: inadequate wakeMode, inactive session
- Needs investigation of `next-heartbeat` vs `now`

**Lessons:**
- config.patch restarts gateway and kills running crons
- Heartbeat doesn't fire during active conversation
- Don't propose infra before you have the problem

---

### Day 10 (02/10) — Roadmap & Crisp Analysis
**What was done:**
- 2026 Roadmap created (5 phases, 18+ weeks)
- 6 prioritized ideas (Content Waterfall P0)
- Complete Crisp analysis: 187 conversations, 95% WhatsApp, vibe coding dominant
- Cross-referenced Circle API data
- LinkedIn "Matrix/Skills" post (co-created with Bruno, high quality)
- Session on Claude Code vs OpenClaw (clarification for Bruno)

**Content insight from Crisp:**
- Vibe coding DOMINATES (172 mentions in 187 conversations)
- People get stuck at the "last mile" (deploy, config, go-live)
- Demand for complete "zero to deploy" content

**"Aha" moment:**
- Crisp as an ideas goldmine: customer questions reveal exactly what the audience wants to learn

---

### Day 11 (02/11) — Integrations & Metrics
**What was done:**
- ChartMogul integrated (MRR Jan: R$7,367, -8.5%)
- Crisp API complete integration + monthly cron
- Started exploring Notion API
- Social Media metrics: LinkedIn, Instagram (RapidAPI), YouTube, X/Twitter
- Security hardening: dmPolicy allowlist, UFW active
- Skills removed (granola, openai-image-gen, video-frames)

**Lessons:**
- Instagram: long text > reels (21x more ER!)
- Crisp is a sales channel, not support
- Notion API requires pagination

---

### Day 12 (02/12) — Immune System & Feedback Loops
**What was done:**
- Analysis of Eric Siu's article "30 OpenClaw Jobs A Day" → implementations
- Cron Watchdog with 3x auto-retry
- Sonnet/Opus Split (~90% savings on simple crons)
- Universal Feedback Loops (4 domains: content, tasks, recommendations, digest)
- Definitive cron fix: `sessionTarget: isolated` + `agentTurn` + `announce`
- Security: fail2ban, localhost binding, quarterly key rotation
- Categorized lessons with expiration (strategic = permanent, tactical = 30 days)

**Key quote from Eric Siu:**
> "Agents are 30% of the work. The other 70% is the immune system."

**Concepts learned:**
- Ralph Loop (Geoffrey Huntley) vs Feedback Loop — complementary
- Capability Evolver: do NOT run automatically (sub-agents with full autonomy = risk)

---

### Day 13 (02/13) — Consolidation & Mission Control v2
**What was done:**
- All overlapping projects consolidated into Mission Control v2
- 6 modules, ~18 weeks
- Priority: Module 1 — Content HQ (4h/day → 1h15/day)
- Projects absorbed: Content Waterfall, Social Metrics, ChartMogul, Multi-Agent specs, Agent Leveling, Price Monitor
- Automated QA of MC (sub-agent found 5 bugs: 2 critical, 3 medium)
- Notion + Granola + Amie integration as task hub
- Consolidated crons: all on Sonnet (savings)

---

## QUANTITATIVE SUMMARY (13 days)

| Metric | Value |
|--------|-------|
| Active integrations | 15+ (1Password, YouTube, LinkedIn, X, Reddit, Circle, Crisp, ChartMogul, Google Drive, Calendar, Notion, Craft, Telegram, WhatsApp, Tella) |
| Skills installed | 19 (after cleanup) |
| Active agents | 6 (Amora, Content, Orchestrator, Planner, Scraper, ZoM) |
| Configured crons | 17+ |
| Completed projects | Mission Control v1, Agent Leveling, Content Squad spec |
| Critical bugs fixed | Token overflow, crons not executing, security hardening |
| Memory files | 40+ (daily notes, topic files, knowledge base) |
| LinkedIn posts co-created | 3+ |
| Documented decisions | 20+ |
| Lessons extracted | 35+ |

---

## PART 2 — MARKET RESEARCH

### What exists today (Feb/2026)

#### 🎥 YouTube — Content about OpenClaw/AI Agents

**Alex Finn** (top creator, Vibe Coding Academy)
- "ClawdBot is the most powerful AI tool I've ever used" — 427K views
- "Open Claw: App Store Moment for AI Agents" — interview with Cailyn (OpenClaw team)
- "AI Co-Pilot for Your Life with Claude Code" — 25 min tutorial (slash commands, sub-agents)
- Focus: vibe coding, content automation, "AI employee 24/7"
- **Gap**: shallow setup, doesn't cover multi-agent management, feedback loops, or structured memory

**Matthew Berman**
- "I Played with Clawdbot all Weekend" — review
- "Openclaw is NUTS" — overview
- "OpenClaw Use Cases that are actually helpful" — practical use cases
- 6 agents running, NocoDB task board
- **Gap**: doesn't show long-term management, agent evolution, "immune system"

**freeCodeCamp**
- "OpenClaw Full Tutorial for Beginners" — complete tutorial
- **Gap**: too technical, no business perspective

**Others:**
- DEV Community articles, Medium, generic SEO blogs about "how to install OpenClaw"
- Bhanu Teja (@pbteja1998): viral thread about 10 agents (3.7M views, 8.1K bookmarks)
- Kevin Simback: guide on agent team management and leveling
- Eric Siu: "30 OpenClaw Jobs A Day" (49K views, 1.3K bookmarks)

#### 📚 Structured Courses (Udemy, Coursera, etc.)

| Course | Platform | Focus | Price |
|--------|----------|-------|-------|
| 2026 Bootcamp: Build Professional AI Agents | Udemy | LangChain, memory, to-do assistant | ~$40 |
| AI Agents For All! No-Code | Udemy | Langflow, no-code | ~$30 |
| AI Agent Developer | Coursera | Custom GPTs, multi-industry | Subscription |
| 5-Day AI Agents Intensive | Kaggle/Google | Fundamentals | Free |

#### 📰 Written Guides

- **Reddit r/ThinkingDeeplyAI**: "The Ultimate Guide to OpenClaw" — viral and comprehensive post covering setup, use cases, and security risks
- **DEV Community**: "Unleashing OpenClaw: The Ultimate Guide for Developers in 2026"
- **o-mega.ai**: "OpenClaw: Ultimate Guide to AI Agent Workforce 2026"

#### 🔑 Gaps NOBODY covers (Bruno's opportunity)

1. **REAL 13-day production experience** — not "I set up something nice in a 20-min video"
2. **Entrepreneur/founder perspective** — not from a dev/AI engineer
3. **Long-term management** — memory, feedback loops, evolution, maintenance
4. **Multi-agents in practice** — leveling, coordination, shared context
5. **"Immune System"** — watchdogs, auto-retry, Sonnet/Opus split, security hardening
6. **Integration with a real business stack** — 1Password, ChartMogul, Crisp, YouTube OAuth, Google Drive, etc.
7. **Crons that ACTUALLY WORK** — real debugging (crons firing but not executing)
8. **Content in Portuguese** — zero courses in PT-BR about OpenClaw
9. **Real cost and savings** — Haiku for heartbeats, Sonnet for execution, Opus for analysis
10. **Agent voice and identity** — SOUL.md, voice guides, not a generic chatbot
11. **Feedback Loops with approve/reject** — nobody teaches how to make the agent learn from your decisions
12. **Real security** — fail2ban, allowlist, UFW, credential rotation (the Reddit Guide mentions risks but nobody shows the solution)
13. **Sub-agents and delegation** — spawning parallel tasks, coordinating output, handling failures

---

## PART 3 — COURSE PROPOSAL (v2 — with applied lessons)

### Title
**"Build Your AI COO: From Zero to Personal Agent in 2 Hours with OpenClaw"**

Subtitle: *How I built an AI assistant that replaced 3-4 people in 13 days — and how you can do the same.*

### Target Audience
- Entrepreneurs and founders (especially solo)
- Content creators
- Professionals who want 10x productivity
- Bruno's Micro-SaaS community
- **NOT** for devs who want to learn LangChain — it's for people who want to USE it

### What makes this course UNIQUE

1. **Real experience, not theory** — Bruno shows Amora running in production, with real bugs and how they were solved
2. **CEO/founder perspective** — no other course teaches how to set up an agent from the perspective of someone running a business
3. **13 documented days** — real timeline with problems, decisions, and breakthroughs
4. **Multi-agents** — not just "a chatbot" but a team of 6 coordinated agents
5. **Immune System** — nobody teaches feedback loops, watchdogs, auto-retry
6. **In Portuguese** — first mini-course in PT-BR about OpenClaw
7. **Real stack** — 1Password, YouTube, LinkedIn, Telegram, ChartMogul, not toy examples
8. **Evolution framework** — the agent improves on its own over time

---

### COURSE STRUCTURE (v3 — reordered + kit per module)

> **New order:** Setup → Security → Personality → Memory → Integrations → Skills → Multi-agents → Immune System → Mission Control
> **Each module delivers:** 📹 Video + 📦 Kit (PRDs, templates, prompts, skills)

---

#### Module 0 — Opening & Context (10 min)
**Format:** Slides + talking head

- Why personal AI agents are the "next big thing"
- The Matrix analogy (Trinity + skills = superpowers)
- What Amora does today: quick demo (1 min, Telegram, showing real commands)
- Course map: what we'll build together
- **Introduce the Kit:** "Each module comes with ready-to-copy files — just drop them into your agent"

📦 **Kit:** None (slides only)

---

#### Module 1 — Setup: From Zero to First "Hi" (25 min)
**Format:** Live coding (screen + face cam)

**Topics:**
1. What is OpenClaw and how it works (architecture: gateway + agent + channel)
2. **Creating the VPS on Hostinger** (KVM 1 plan, Ubuntu 24.04)
   - **Docker vs Bare Metal:** "Hostinger has One-Click Docker, but we'll install directly because it's more flexible — skills, integrations, and everything we'll do later works better this way"
   - Docker = isolation that gets in the way (skills don't install easily, sub-agents limited, debugging difficult)
   - Bare Metal = everything works as expected, direct access
3. **Connecting via SSH** (show local terminal + Hostinger panel terminal)
4. **Installing OpenClaw:**
   ```bash
   curl -fsSL https://openclaw.ai/install.sh | bash
   openclaw onboard --install-daemon
   ```
5. **Configuration wizard:**
   - Gateway mode: Local
   - Provider: Anthropic (show where to get the API key at console.anthropic.com)
   - Model: Claude Sonnet (good and cheap to start)
   - Install as service: Yes (runs 24/7)
6. **Creating a Telegram bot** (BotFather → /newbot → copy token)
7. **Connecting Telegram:**
   ```bash
   openclaw provider add telegram
   ```
8. **First test:** Send "Hi" on Telegram → agent responds 🎉

**🆕 Practical checkpoint:** Student has agent responding on Telegram ✅

**How much it costs to run:**
| Item | Cost/month |
|------|-----------|
| Hostinger VPS (KVM 1) | ~$5-10 |
| Anthropic API (moderate use) | ~$10-30 |
| Telegram | Free |
| **Total** | **~$15-40** |

> "Less than a lunch per week to have a 24/7 AI assistant"

📦 **Module kit:**
- `prds/vps-setup-hostinger.md` — complete step-by-step
- `configs/modelo-config.md` — recommended settings

---

#### Module 2 — Security: Hardening Your Agent (15 min)
**Format:** Live coding

> ⚡ Security BEFORE everything else. Exposed servers receive 1,000+ attacks/day.

**Topics:**
1. **Why now?** Show real log: 1,015 brute force attempts in 24h
2. **Telegram Allowlist (CRITICAL):**
   - dmPolicy "open" = anyone can command your agent
   - Change to "allowlist" with your Telegram ID
   - Show how to find the ID
3. **Firewall (UFW):**
   ```bash
   sudo apt install -y ufw
   sudo ufw default deny incoming
   sudo ufw allow ssh
   sudo ufw --force enable
   ```
4. **Fail2ban (SSH protection):**
   ```bash
   sudo apt install -y fail2ban
   ```
   - Configure: 5 attempts → ban 1h
5. **Secure credentials:**
   - NEVER hardcode API keys
   - 1Password CLI or environment variables
6. **Application ports:**
   - If you have web apps: 127.0.0.1 (not 0.0.0.0)
   - Cloudflare Tunnel for remote access

**Checkpoint:** Server hardened ✅

📦 **Module kit:**
- `prds/security-hardening.md` — copy-paste PRD (drop it in the agent, it hardens itself)

---

#### Module 3 — Personality and Context (25 min)
**Format:** Demo + slides

**Topics:**
1. **SOUL.md: the agent's soul** — show diff of generic vs Amora's customized version
   - Concrete anti-patterns: ❌/✅ examples inside SOUL.md
   - Explicit "never dos": things the agent should NEVER do
   - Inspirational anchors: give the agent tone references ("speak like X, never like Y")
2. **USER.md: who are you?** — context that makes the agent useful
   - Deep context > superficial: business, philosophy, schedule, communication style
   - Tone of voice per platform (if creating content)
3. **IDENTITY.md: concrete data vs personality** — separate "who I am" from "how I act"
4. **AGENTS.md: operational rules** — what's allowed, what's not, how to operate
5. **Choosing your model:** Opus vs Sonnet vs Haiku (and when to use each)
   - Real savings: Haiku for heartbeats (90% savings), Sonnet for crons, Opus for interaction
6. **Thinking mode:** when to turn on turbo and how much it costs

**Practical exercise:** Student takes the templates, fills in the [fields] and drops them in the agent

**Day 7 Insight:**
- Show how Amora rewrote its own SOUL.md from scratch — the difference was absurd
- "SOUL.md can't be rushed" — Kevin Simback

📦 **Module kit:**
- `templates/SOUL-template.md` — with [FILL IN HERE] fields
- `templates/USER-template.md`
- `templates/AGENTS-template.md`
- `templates/IDENTITY-template.md`
- `prompts/onboarding.md` — first conversation with the configured agent
- `prompts/proactive-mandate.md` — activates proactive mode
- `prompts/interview-your-agent.md` — discover hidden capabilities

---

#### Module 4 — Memory: The Secret Nobody Teaches (25 min)
**Format:** Demo + diagrams

**Topics:**
1. The problem: agents forget everything every session
2. Amora's memory architecture: daily notes → topic files → MEMORY.md (index)
3. **🆕 Specialized topic files:**
   - `decisions.md` — permanent decisions (never lose these)
   - `lessons.md` → `lessons/` categorized (integrations, crons, content, infra)
   - `projects.md` — current state of all projects
   - `people.md` — contacts, team, partners
   - `pending.md` — awaiting user input
4. **🆕 Smart lesson retention:**
   - 🔒 Strategic = permanent (patterns, philosophy)
   - ⏳ Tactical = expire in 30 days (bugs, workarounds)
   - Monthly review: delete expired tactical lessons
5. Auto-compaction: how to configure to avoid token overflow
   - 🆕 **Token overflow is real:** we showed exceeding 173k+ tokens on Day 2
6. **🆕 Mandatory extraction on compaction:**
   - RULE: Before EVERY compaction, extract lessons → lessons, decisions → decisions, etc.
   - "If you don't extract before compacting, you lose 80% of the value"
7. **🆕 Feedback Loops: approve/reject → agent evolution**
   - 4 domains: content, tasks, recommendations, digest
   - JSON with {date, context, decision, reason, tags}
   - Agent checks BEFORE suggesting → avoids repeating mistakes
   - Max 30 entries/file (FIFO) → consolidate into lessons monthly

**🆕 Live demo:**
- Show how Amora remembers a decision from Day 4 on Day 13
- "Bruno prefers 1-paragraph briefs" → noted decision → automatically respected
- Feedback loop: "I rejected this post format → agent no longer suggests it"

**This is the differentiating module.** No other course covers structured memory + feedback loops.

📦 **Module kit:**
- `templates/MEMORY-template.md`
- `templates/HEARTBEAT-template.md`
- `templates/memory/` (decisions, lessons, projects, people, pending)
- `prds/memory-architecture.md` — copy-paste PRD

---

#### Module 5 — Integrations: Connecting to the Real World (25 min)
**Format:** Live coding + demo

**Topics:**
1. **1Password:** credential security (rule #1 — NEVER hardcode)
   - 🆕 **Careful:** systemd override overwrites .env — update BOTH
2. **Google Calendar & Drive** via GOG CLI
3. **YouTube:** Data API + OAuth (list videos, analytics)
4. **🆕 RapidAPI as universal proxy:**
   - Cloud IPs blocked by YouTube, X, Instagram → RapidAPI solves EVERYTHING
   - Specific APIs: Instagram Statistics, X/Twitter API45, YouTube Transcripts
   - Generous free tiers
5. **🆕 Telegram as operational hub:**
   - Topics in the group = organized war room (content, metrics, operational, projects)
   - dmPolicy allowlist = security
   - Bot with inline buttons for quick interactions
6. **Crons: automating recurring tasks**
   - 🆕 **The bug EVERYONE will encounter:**
     - systemEvent + main = cron fires but DOESN'T execute (durationMs ~0ms)
     - 🆕 **Definitive fix:** `sessionTarget: isolated` + `agentTurn` + `announce`
     - This fix alone is worth the entire course
   - 🆕 **Schedule collision:** multiple crons at the same minute = rate limit → space 15-30min apart
   - 🆕 **config.patch restarts gateway** and kills running crons → do it at times without crons
   - 🆕 **Reminders:** systemEvent does NOT notify on Telegram → use agentTurn + message send

**Practical checkpoint:** Student has at least 1 integration + 1 cron working ✅

**Lessons from the trenches:**
- yt-dlp doesn't work from cloud → Tella.tv or alternative API
- Brave Search API unstable → have a fallback
- Notion API requires pagination

📦 **Module kit:**
- `prds/integrations-setup.md` — PRD with integrations by level
- `configs/cron-examples.md` — 4 ready crons (schedule, watchdog, review, reminder)

---

#### Module 6 — Skills: Instant Superpowers (15 min)
**Format:** Demo

**Topics:**
1. What skills are and how to install (ClawHub)
2. Essential skills: excalidraw, nano-pdf, hand-draw-graphics
3. Creating your first custom skill
4. 🆕 **Community skills: be careful!**
   - Reference: Cisco study — significant percentage of skills with vulnerabilities
   - Always review before installing
   - Redundant skills exist (remind-me ≈ native cron) → audit
5. 🆕 **Creators as skills, not agents:**
   - LinkedIn Creator, Newsletter Creator, etc. = prompts/skills WITHIN an agent
   - 1 agent with 8 skills > 8 specialized agents (less cost, less coordination)

**Matrix analogy:**
- "Tank, I need a pilot program" — Bruno's viral LinkedIn post

📦 **Module kit:**
- `skills/skills-by-profile.md` — curation by profile (entrepreneur, creator, dev, ops)

---

#### Module 7 — Multi-Agents: From Solo to Team (20 min)
**Format:** Slides + demo

**Topics:**
1. When one agent isn't enough
2. Architecture: single gateway + agents.list
3. **Leveling System (Kevin Simback): L1→L4**
   - L1 Observer → L2 Contributor → L3 Operator → L4 Trusted
   - 🆕 **Promotion via weekly performance review** — demotion is possible
   - 🆕 **Real case:** Kevin's Content Agent dropped from L3 → L2 when it started "rushing"
4. Amora's Squad: 6 agents, each with a defined role
5. **🆕 Shared Context:**
   - `shared/TEAM.md` → registry of all agents (who does what)
   - `shared/outputs/` → shared results
   - `shared/lessons/` → team learnings
   - "Last updated by" header — know who touched the file
   - 🆕 Shared context eliminates cold starts → new agent already knows who the others are
6. Coordination: Amora as hub, agents behind the scenes
   - 🆕 **Hub model > Mesh model:** cross-learning between distinct domains doesn't make sense
   - 🆕 Content agents without Telegram binding — Bruno only talks to Amora
7. **🆕 Real economics:**
   - Sonnet for execution/crons, Opus for interaction/analysis
   - All 17 crons on Sonnet = massive savings
   - 🆕 **Agents that don't need Opus should NOT use Opus**

**Sub-agents and delegation:**
- sessions_spawn for parallel tasks (3 sub-agents running simultaneously)
- Failure handling: retry + notify user (NEVER leave in silent limbo)
- Sub-agent stuck? → immediate retry → if fails 2x → notify

📦 **Module kit:**
- `prds/multi-agent-setup.md` — complete PRD with leveling + shared context

---

#### Module 8 — The Immune System: Keeping Everything Running (20 min)
**Format:** Slides + demo

**Topics:**
1. **"Agents are 30% of the work. The other 70% is the immune system."** — Eric Siu
2. **🆕 Watchdog with auto-retry (3x before alerting)**
   - Monitors crons, detects failures, auto-retry
   - If fails 3x → alert human
3. **Universal Feedback Loops (recap of Module 4 applied)**
   - Cycle: Feedback (granular, JSON) → Lessons (curated, prose) → Decisions (permanent)
4. **🆕 REAL security hardening (not just theory):**
   - fail2ban: 1,015+ brute force attempts/24h → automatic ban
   - UFW firewall active
   - Telegram allowlist (dmPolicy)
   - SSH hardening (ideal: key-only, no password)
   - Application ports: 0.0.0.0 → 127.0.0.1 (only Cloudflare Tunnel accesses)
   - 🆕 **Quarterly credential rotation** — schedule on calendar
5. **🆕 Real cost monitoring:**
   - Sonnet/Opus split (crons: Sonnet, interaction: Opus)
   - Heartbeat with Haiku (~$0.005/heartbeat vs ~$0.10/heartbeat on Opus)
   - Breakdown: how much it costs to run 17 crons/day + daily interaction
6. **🆕 Backup before structural changes:**
   - Save config + ROLLBACK.md with instructions
   - Especially before: creating agents, modifying gateway config, reorganizing workspace
7. **🆕 Sub-agents with autonomy = risk:**
   - Capability Evolver: do NOT run automatically
   - Any sub-agent with "fire and forget" can cause damage
   - Always review output before approving

**🆕 Ralph Loop vs Feedback Loop:**
- Ralph Loop (Geoffrey Huntley): code execution loop (agent runs until complete)
- Feedback Loop: cross-session learning via approve/reject
- They're complementary: Ralph for coding, Feedback for decisions

**This module is what separates "playing around" from "running in production."**

📦 **Module kit:**
- `prds/immune-system.md` — complete PRD (watchdog, feedback loops, costs, backups)

---

#### Module 9 — Mission Control: Your Operations Dashboard (10 min)
**Format:** Demo

**Topics:**
1. Why a visual UI helps (even with Telegram)
2. Overview of Amora's Mission Control (Kanban, Memory, Crons, Content HQ)
   - 🆕 **Content HQ:** 229 packs, 773 pieces, platform filters, approve/reject
   - 🆕 **File Manager** with security (path traversal blocked)
3. How to build yours (Express + React + Supabase + Cloudflare Tunnel)
4. Simpler alternatives: NocoDB, Notion, Google Sheets
5. **Automated QA:** sub-agent tested 23 endpoints, found 5 bugs in 7 minutes

📦 **Module kit:**
- `reports/report-templates.md` — design guidelines + report structure

---

#### Module 10 — Wrap-up & Next Steps (10 min)
**Format:** Talking head + slides

**Topics:**
1. Recap: what we built together
2. **🆕 Mistakes I made (real consolidation):**
   - Token overflow on Day 2 (not configuring compaction)
   - Crons not executing for 3 days (systemEvent vs agentTurn)
   - Sub-agent that got stuck and nobody noticed (silent limbo)
   - Security "open" in the first days (anyone could command it)
   - Proposing infra before having the problem (premature optimization)
3. **🆕 How much does it cost to run an AI agent? (REAL breakdown)**
   - API costs: ~$X/day with Sonnet/Opus/Haiku split
   - VPS: $5-10/month
   - RapidAPI: generous free tiers
   - Estimated total: $XX/month for complete operation
4. Community: where to get help, awesome-skills, ClawHub
5. The future: agent-to-agent, MCP, Claude Code integration
6. CTA: Micro-SaaS community + immersion

---

### TIMELINE PER MODULE

| Module | Time | Format | Kit delivered |
|--------|------|--------|-------------|
| 0 - Opening | 10 min | Slides + talking head | — |
| 1 - VPS Setup | 25 min | Live coding | PRD setup + configs |
| 2 - Security | 15 min | Live coding | PRD security |
| 3 - Personality | 25 min | Demo + slides | 4 templates + 3 prompts |
| 4 - Memory | 25 min | Demo + diagrams | MEMORY + memory/ + PRD |
| 5 - Integrations | 25 min | Live coding | PRD integrations + crons |
| 6 - Skills | 15 min | Demo | Curation by profile |
| 7 - Multi-agents | 20 min | Slides + demo | PRD multi-agent |
| 8 - Immune System | 20 min | Slides + demo | PRD immune system |
| 9 - Mission Control | 10 min | Demo | Report templates |
| 10 - Wrap-up | 10 min | Talking head | Complete kit (zip) |
| **TOTAL** | **~3h20** | | **24+ files** |

---

### 🆕 LESSONS APPLIED TO THE COURSE (v2)

These are lessons we lived through the 13 days that became teachable content:

#### Infrastructure Lessons
| Lesson | Module | What to teach |
|--------|--------|---------------|
| Real token overflow (173k+ tokens) | M3 | Configure compaction + reserveTokens BEFORE you need it |
| systemd override overwrites .env | M4 | Update BOTH when changing credentials |
| Intermittent Brave Search | M4 | Have a fallback for web_fetch |
| Sub-agents may return empty history | M6 | Have a manual fallback |
| trash-cli not installed by default | M1 | `apt install trash-cli` in setup |

#### Cron Lessons
| Lesson | Module | What to teach |
|--------|--------|---------------|
| systemEvent crons don't execute | M4 | Use isolated + agentTurn (ALWAYS) |
| systemEvent doesn't notify | M4 | Use agentTurn + message send for reminders |
| config.patch kills crons | M4 | Plan patches at times without crons |
| Schedule collision = rate limit | M4 | Space 15-30 min apart |
| Crons without agentId fail | M6 | Always create from the main session |

#### Content & Integration Lessons
| Lesson | Module | What to teach |
|--------|--------|---------------|
| Cloud IPs blocked | M4 | RapidAPI as universal proxy |
| yt-dlp doesn't work | M4 | Tella.tv or Whisper as alternative |
| Instagram text > reels | M4 | Real data that surprises |
| Crisp = sales channel | M4 | Use for content insights |
| Notion API requires pagination | M4 | Always paginate |

#### Agent & Management Lessons
| Lesson | Module | What to teach |
|--------|--------|---------------|
| Generic SOUL.md = generic agent | M2 | Invest time in personality |
| Every agent starts at L1 | M6 | No trust = no autonomy |
| Shared context eliminates cold starts | M6 | TEAM.md + shared outputs |
| Creators are skills, not agents | M5/M6 | 1 agent with N skills > N agents |
| Hub > Mesh for learning | M6 | Amora curation > everyone reads everything |

#### Security Lessons
| Lesson | Module | What to teach |
|--------|--------|---------------|
| dmPolicy open = critical risk | M1/M7 | Allowlist from Day 1 |
| 1,015+ brute force attempts/day | M7 | fail2ban MANDATORY |
| 0.0.0.0 → 127.0.0.1 + Cloudflare | M7 | Never expose ports directly |
| Credentials in 1Password | M4/M7 | NEVER hardcode |
| Sub-agent with autonomy = risk | M7 | Always review output |

---

### FORMAT SUGGESTIONS

#### Option A: YouTube (Free) — Maximum Reach
- 1 long video (~3h) divided into chapters
- Or series of 9 episodes → playlist
- **Pros:** Massive reach, SEO, first in PT-BR
- **Cons:** Doesn't monetize directly

#### Option B: Community Mini-course (Paid) — Monetization
- Exclusive access for Micro-SaaS PRO members
- Live sessions with Q&A
- **Pros:** Added value to community, indirect monetization
- **Cons:** Limited reach

#### Option C: Hybrid (RECOMMENDED) ⭐
- **YouTube:** Modules 0-2 free (attract audience — ~60 min)
  - "How I built an AI assistant that replaced 3-4 people"
  - Setup + personality = immediate value, but want more
- **Paid (Community/course):** Modules 3-9 (memory, integrations, multi-agents, immune system)
  - The advanced content nobody else has
- **Pros:** Natural funnel, differentiated premium content
- **Cons:** More production work

#### Option D: Live Workshop + Recording
- 1 live session (Zoom/YouTube Live) of 3h with screen share
- Participants build along in real time
- Recording becomes the product
- **Pros:** Interaction, Q&A, urgency
- **Cons:** One chance to get it right

---

### PRODUCTION SUGGESTIONS

1. **Record on Tella.tv** → automatic transcription → content waterfall
2. **Split screen:** terminal + Telegram + face cam
3. **Diagrams:** Excalidraw (we already have the skill) for architecture
4. **Infographics:** Hand-draw-graphics for visual summaries
5. **Before/after:** Show day 1 vs day 13 (what changed)
6. **Live bugs:** DON'T hide errors — show and resolve = authenticity

---

### SUPPLEMENTARY MATERIAL

1. **Setup checklist** (PDF/Notion) — reproducible step-by-step
2. **Templates:** SOUL.md, USER.md, AGENTS.md, MEMORY.md model
3. **Integration list** with links and instructions
4. **Awesome skills list** curated for entrepreneurs
5. **Cost spreadsheet** (how much each model costs per month)
6. **GitHub repo** with example configs (no credentials, of course)
7. **🆕 Lessons learned table** (the 35+ categorized lessons)
8. **🆕 Feedback loop template** (ready-to-use JSONs)
9. **🆕 Security checklist** (fail2ban, UFW, allowlist, SSH, key rotation)

---

### ALTERNATIVE TITLES TO TEST

1. "Build Your AI COO: From Zero to Personal Agent in 2 Hours"
2. "How I Built An AI Assistant That Replaced 3-4 People (And You Can Too)"
3. "OpenClaw in Practice: 13 Days Building a Real AI Agent"
4. "From Chatbot to COO: The Definitive Guide to the Personal AI Agent"
5. "Your First AI Agent: Complete Setup with OpenClaw (Without Knowing How to Code)"

---

### DIFFERENTIATORS vs COMPETITION (Updated Summary)

| Aspect | Other courses/guides | Our course |
|--------|---------------------|-------------|
| Perspective | Dev/engineer | CEO/founder |
| Experience | "I just installed it" | 13 days in production |
| Memory | Don't cover | Entire module + feedback loops |
| Multi-agents | Superficial | Leveling system + shared context |
| Real bugs | Hidden | Shown and resolved live |
| Immune system | Doesn't exist | Dedicated module (watchdog, retry, security) |
| Language | EN | PT-BR (first!) |
| Integrations | Toy examples | Real business stack (15+ APIs) |
| Cost | Don't discuss | Real breakdown with Sonnet/Opus/Haiku split |
| Evolution framework | Doesn't exist | Feedback loops + categorized lessons |
| Security | "Be careful with this" | Complete solution (fail2ban, UFW, allowlist, rotation) |
| Sub-agents | Don't cover | Parallel delegation + failure handling |
| Crons | Basic setup | Real debugging + definitive fix (isolated) |

---

### DERIVED CONTENT IDEAS (Content Waterfall)

From the mini-course, we can extract:
1. **5-7 LinkedIn posts** (one per module, isolated insights)
2. **3-5 Reels/Shorts** (live bugs, Matrix analogy, Telegram demo)
3. **1 X Thread** ("13 days building an AI COO — complete thread")
4. **1 Newsletter** (behind the scenes, what went wrong)
5. **Infographic** (Amora's architecture, hand-drawn style)
6. **Podcast/Audio** (Tella transcription → editing)

---

### 🆕 REFERENCES USED

- **Kevin Simback:** "My Complete Guide to Managing OpenClaw Agent Teams" — leveling L1-L4, shared context, performance reviews
- **Bhanu Teja** (@pbteja1998): 10-agent blueprint — staggered heartbeat, Mission Control as hub
- **Eric Siu:** "I Run 30 OpenClaw Jobs A Day" — immune system, 70% is maintenance
- **Geoffrey Huntley:** Ralph Loop — infinite coding agent loop
- **Lenny's Newsletter:** Context engineering — progressive disclosure, context rot
- **Reddit Ultimate Guide:** r/ThinkingDeeplyAI — complete setup + security risks (https://www.reddit.com/r/ThinkingDeeplyAI/comments/1qsoq4h/)
- **Alex Finn / Vibe Coding Academy:** Use cases, proactive mandate
- **Simon Willison:** Security research — 900+ exposed servers

---

*File created on 02/13/2026, updated 02/13/2026 (v2) by Amora 🍇*
*Base for brainstorm with Bruno — next step: review, prioritize, decide format and recording date.*
