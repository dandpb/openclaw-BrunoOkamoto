# 🎓 Final Course Structure

**"Build Your AI COO: From Zero to Personal Agent with OpenClaw"**

> 11 modules, ~3h30 of content. From zero to agent in production.
> Each module delivers: 🎥 Video + 📄 PDF + 💬 Prompt for the agent

---

## Module 0 — Opening & Context (10 min)
**Format:** Slides + talking head

**Content:**
- Why personal AI agents are the "next big thing"
- The Matrix analogy (Trinity + skills = superpowers)
- Quick demo of Amora on Telegram (1 min, real commands)
- Course map: what we'll build together
- Introduce the Kit: "Each module comes with ready-to-use files to send to your agent"

**Module kit:** None (slides only)

---

## Module 1 — Setup: From Zero to First "Hi" (25 min)
**Format:** Live coding (screen + face cam)

**Content:**
1. What is OpenClaw and how it works (architecture: gateway + agent + channel)
2. Creating the VPS on Hostinger (KVM 1 plan, Ubuntu 24.04)
   - Docker vs Bare Metal — why bare metal is better for non-developers
3. Connect via SSH (local terminal + Hostinger panel)
4. Install OpenClaw:
   ```bash
   curl -fsSL https://openclaw.ai/install.sh | bash
   openclaw onboard --install-daemon
   ```
5. Configuration wizard (provider, model, service)
6. Create bot on Telegram (BotFather → /newbot → token)
7. Connect Telegram + first "Hi" 🎉

**How much it costs:**
| Item | Cost/month |
|------|-----------|
| VPS Hostinger (KVM 1) | ~$5-10 |
| Anthropic API (moderate use) | ~$10-30 |
| Telegram | Free |
| **Total** | **~$15-40** |

**Checkpoint:** Agent responding on Telegram ✅

**Kit:**
- `prds/vps-setup-hostinger.md`
- `configs/modelo-config.md`
- `prompts/modulo-01-setup.md`

---

## Module 2 — Security: Hardening Your Agent (15 min)
**Format:** Live coding

**Content:**
1. Why now? Show real log: 1,015+ brute force attempts in 24h
2. Telegram Allowlist (dmPolicy) — from "open" to "allowlist" with your ID
3. UFW Firewall:
   ```bash
   sudo ufw default deny incoming
   sudo ufw allow ssh
   sudo ufw --force enable
   ```
4. Fail2ban (SSH protection): 5 attempts → ban 1h
5. Secure credentials: 1Password CLI or environment variables (NEVER hardcode)
6. Application ports: 127.0.0.1 (not 0.0.0.0) + Cloudflare Tunnel

**Checkpoint:** Hardened server ✅

**Kit:**
- `prds/security-hardening.md`
- `prompts/modulo-02-seguranca.md`

---

## Module 3 — Identity: Giving the Agent Personality (25 min)
**Format:** Demo + slides

**Content:**
1. SOUL.md: the agent's soul
   - Show diff: generic vs Amora's personalized version
   - Concrete anti-patterns: ❌/✅ examples
   - Explicit "Never dos"
   - Inspirational anchors (speak like X, never like Y)
2. USER.md: who are you?
   - Deep context > surface level
   - Tone of voice by platform
   - Tip: import CLAUDE.md if you already use Claude Code
3. IDENTITY.md: concrete data vs personality
   - Name, own email, own password vault
   - "Treat as a person, not a robot"
4. AGENTS.md: operational rules
   - What it can do alone vs ask about
5. Choosing model: Opus vs Sonnet vs Haiku
   - Real savings: Haiku for heartbeats (90% savings)
6. Thinking mode: when to rev the engine and how much it costs

**Day 7 Insight:** Amora rewrote her own SOUL.md — the difference was enormous.

**Exercise:** Student takes templates, fills in [fields], sends to agent.

**Checkpoint:** Agent with personality and context ✅

**Kit:**
- `templates/SOUL-template.md`
- `templates/USER-template.md`
- `templates/AGENTS-template.md`
- `templates/IDENTITY-template.md`
- `prompts/modulo-03-identidade.md`
- `prompts/onboarding.md`
- `prompts/interview-your-agent.md`

---

## Module 4 — Memory: The Secret Nobody Teaches (25 min) ⭐
**Format:** Demo + diagrams

**Content:**
1. The problem: agents forget everything each session (Alzheimer reset)
2. Layered memory architecture:
   - Session → Daily note → Topic files → MEMORY.md (index)
3. Specialized topic files:
   - `decisions.md` — permanent decisions
   - `lessons.md` — categorized (strategic permanent, tactical 30 days)
   - `projects.md` — current state
   - `people.md` — contacts, team
   - `pending.md` — awaiting input
4. INVIOLABLE rule: extract lessons/decisions BEFORE each compaction
   - "If you don't extract before compacting, you lose 80% of the value"
5. Compaction: context tokens, reserve, avoid overflow
   - Real case: token overflow of 173k+ on Day 2
6. Periodic consolidation (every 15 days)
7. Feedback Loops: approve/reject → agent evolution
   - 4 domains: content, tasks, recommendations, digest
   - Agent consults BEFORE suggesting → avoids repeating mistakes

**Live demo:** Show how Amora remembers a decision from Day 4 on Day 13.

**This is the differentiator module.** Nobody covers structured memory + feedback loops.

**Checkpoint:** Memory system configured ✅

**Kit:**
- `prds/memory-architecture.md`
- `templates/MEMORY-template.md`
- `templates/HEARTBEAT-template.md`
- `templates/memory/` (5 files)
- `prompts/modulo-04-memoria.md`

---

## Module 5 — Integrations & Crons: Connecting to the Real World (25 min)
**Format:** Live coding + demo

**Content:**
1. 1Password: credential security (NEVER hardcode)
   - Caution: systemd override overwrites .env — update BOTH
2. Google Calendar & Drive via GOG CLI
3. YouTube: Data API + OAuth
4. RapidAPI as universal proxy:
   - Cloud IPs blocked by YouTube, X, Instagram → RapidAPI solves it
   - APIs: Instagram Statistics, X/Twitter API45, YouTube Transcripts
5. Telegram as operational hub:
   - Topics = organized war room
   - Why not WhatsApp (single session vs multiple)
6. Crons — automate recurring tasks:
   - **The bug EVERYONE will hit:**
     - systemEvent + main = fires but does NOT execute (durationMs ~0ms)
     - **Solution:** `sessionTarget: isolated` + `agentTurn` + `announce`
   - Schedule collision → space 15-30min
   - config.patch restarts gateway and kills crons → do it at times with no crons
   - Reminders: systemEvent does NOT notify → use agentTurn + message send

**Checkpoint:** At least 1 integration + 1 cron working ✅

**Kit:**
- `prds/integrations-setup.md`
- `configs/cron-examples.md`
- `prompts/modulo-05-integracoes.md`

---

## Module 6 — Skills: Instant Superpowers (15 min)
**Format:** Demo

**Content:**
1. What skills are and how to install them (ClawHub + GitHub)
2. Essential skills by profile:
   - Entrepreneur: nano-pdf, excalidraw, perplexity
   - Creator: hand-draw-graphics, video-frames, openai-image-gen
   - Dev: github, coding-agent, tmux
3. Creating your first custom skill
4. Skill security:
   - Reference: study on vulnerabilities in third-party skills
   - Always review before installing
5. Redundant skills: remind-me ≈ native cron → audit
6. Creators as skills, not agents:
   - 1 agent with 8 skills > 8 specialized agents

**Matrix analogy:** "Tank, I need a pilot program"

**Checkpoint:** 2-3 skills installed and tested ✅

**Kit:**
- `skills/skills-by-profile.md`
- `prompts/modulo-06-skills.md`

---

## Module 7 — Proactivity: Heartbeats & Automations (15 min)
**Format:** Demo + slides

**Content:**
1. Heartbeats: what they are and how to configure
   - HEARTBEAT.md: periodic checklist (emails, calendar, projects)
   - Economic model: Haiku for heartbeats (~$0.005 vs ~$0.10 on Opus)
2. What to check automatically:
   - Urgent emails
   - Events in the next 24-48h
   - Projects stalled for >5 days
   - Business metrics
3. When to speak vs stay quiet:
   - Quiet hours (11pm-8am)
   - Nothing new = HEARTBEAT_OK
4. Proactive work without asking:
   - Organize memory
   - Git status of projects
   - Update documentation
5. Real examples from Amora:
   - Daily social media briefing
   - Schedule alerts
   - Weekly project review

**Checkpoint:** Heartbeat configured + 2 active automations ✅

**Kit:**
- `templates/HEARTBEAT-template.md`
- `prompts/proactive-mandate.md`

---

## Module 8 — Multi-Agents: From Solo to Team (20 min)
**Format:** Slides + demo

**Content:**
1. When one agent isn't enough (and when it IS — less is more)
2. Architecture: single gateway + agents.list
3. Leveling System (Kevin Simback): L1→L4
   - L1 Observer → L2 Contributor → L3 Operator → L4 Trusted
   - Promotion via weekly performance review
   - Real case: Content Agent dropped from L3 → L2 when it started "rushing"
4. Creating agents with the Orchestrator:
   - Agent that creates agents (SOUL, AGENTS, USER, memory)
5. Shared Context:
   - TEAM.md → registry (who does what)
   - shared/outputs/ → shared results
   - shared/lessons/ → team learnings
6. Coordination: hub model > mesh model
   - Main agent curates > everyone reads everything
   - Agents without Telegram binding — communicate via main
7. Real savings:
   - Sonnet for execution/crons, Opus for interaction/analysis
   - "Agents that don't need Opus should not use Opus"
8. Sub-agents and delegation:
   - sessions_spawn for parallel tasks
   - Retry + notify user (NEVER silent limbo)

**Checkpoint:** 1-2 extra agents configured with leveling ✅

**Kit:**
- `prds/multi-agent-setup.md`
- `prompts/modulo-07-multiagentes.md`

---

## Module 9 — The Immune System: Keeping Everything Running (20 min) ⭐
**Format:** Slides + demo

**Content:**
1. "Agents are 30% of the work. The other 70% is the immune system." — Eric Siu
2. Watchdog with auto-retry (3x before alerting):
   - Monitors crons, detects failures, automatic retry
3. Universal Feedback Loops:
   - Cycle: Feedback (JSON) → Lessons (curated) → Decisions (permanent)
4. Advanced security hardening:
   - Weekly security audit (cron)
   - `openclaw security-audit` + `openclaw doctor fix`
   - Quarterly credential rotation
5. Cost monitoring:
   - Sonnet/Opus/Haiku split
   - Real breakdown: how much it costs to run 17 crons/day + interaction
6. Backup before structural changes:
   - Config + ROLLBACK.md with instructions
7. Sub-agents with autonomy = risk:
   - Capability Evolver: DO NOT run automatically
   - Always review output before approving
8. Ralph Loop vs Feedback Loop:
   - Ralph (coding loop) vs Feedback (learning between sessions)

**This module separates "just playing around" from "in production".**

**Checkpoint:** Watchdog + feedback loops + audit configured ✅

**Kit:**
- `prds/immune-system.md`
- `prompts/modulo-08-immune-system.md`

---

## Module 10 — Mission Control: Your Operational Panel (10 min)
**Format:** Demo

**Content:**
1. Why a visual UI helps (even with Telegram)
2. Overview of Amora's Mission Control:
   - Task Kanban
   - Memory Page
   - Crons Page
   - Content HQ (229 packs, 773 pieces)
3. How to build yours:
   - Stack: Express + React + Supabase + Cloudflare Tunnel
   - Automated QA: sub-agent ran 23 endpoints, found 5 bugs in 7min
4. Simpler alternatives:
   - NocoDB (self-hosted, free)
   - Notion (integrates with skill)
   - Google Sheets (simple and functional)

**Checkpoint:** At least one visual alternative configured ✅

**Kit:**
- `reports/report-templates.md`

---

## Module 11 — Wrap-up & Next Steps (10 min)
**Format:** Talking head + slides

**Content:**
1. Recap: what we built together (visual checklist)
2. Mistakes I made (real consolidation):
   - Token overflow on Day 2
   - Crons that weren't executing for 3 days
   - Sub-agent stuck in limbo
   - Security "open" in the first days
3. How much does it cost to run an AI agent? (REAL breakdown)
   - API costs with Sonnet/Opus/Haiku split
   - VPS + tools + external APIs
4. 10 inviolable rules (consolidation)
5. Community: Discord OpenClaw, ClawHub, awesome-skills
6. The future: agent-to-agent, MCP, Claude Code integration
7. CTA: Community + upcoming content

**Kit:**
- Final validation checklist
- Resource links
- `docs/custos.md` (detailed breakdown)

---

## Summary by Module

| # | Module | Time | Format | Kit |
|---|--------|-------|---------|-----|
| 0 | Opening & Context | 10 min | Slides + face | — |
| 1 | Setup: From Zero to "Hi" | 25 min | Live coding | PRD + config + prompt |
| 2 | Security | 15 min | Live coding | PRD + prompt |
| 3 | Identity & Personality | 25 min | Demo + slides | 4 templates + 3 prompts |
| 4 | Memory ⭐ | 25 min | Demo + diagrams | PRD + templates + prompt |
| 5 | Integrations & Crons | 25 min | Live coding | PRD + config + prompt |
| 6 | Skills | 15 min | Demo | Curated list + prompt |
| 7 | Proactivity | 15 min | Demo + slides | Template + prompt |
| 8 | Multi-Agents | 20 min | Slides + demo | PRD + prompt |
| 9 | Immune System ⭐ | 20 min | Slides + demo | PRD + prompt |
| 10 | Mission Control | 10 min | Demo | Templates |
| 11 | Wrap-up | 10 min | Talking head | Checklist + costs |
| **Total** | | **~3h35** | | **~50 files** |

---

## References

- **Kevin Simback:** Agent team management, leveling L1-L4
- **Bhanu Teja (@pbteja1998):** Blueprint of 10 agents (3.7M views)
- **Eric Siu:** "30 OpenClaw Jobs A Day" — immune system
- **Geoffrey Huntley:** Ralph Loop
- **Lenny's Newsletter:** Context engineering
- **Reddit Ultimate Guide:** r/ThinkingDeeplyAI
- **Alex Finn / Vibe Coding Academy:** Use cases, proactive mandate
- **Simon Willison:** Security research — 900+ exposed servers

---

*Final structure v1 — 02/16/2026*
*Curated by the curso-openclaw agent 🍇*
