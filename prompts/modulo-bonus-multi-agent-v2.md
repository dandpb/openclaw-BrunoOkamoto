# Guided Prompt — Bonus Lesson: Multi-Agent OS v2.0

> Attach the files: `prds/multi-agent-v2.md`, `prds/multi-agent-setup.md`, `templates/BOSS-WORKSPACE/` (all 8 files), `templates/WORKER-WORKSPACE/` (all 6 files)
> ⚠️ Note: `TOOLS-SHARED.md` and `shared/lessons/` in PRD v2 were reorganized in v2.1. See the note at the top of the PRD.

---

```
I just watched the bonus lesson on Multi-Agent OS v2.0 — the evolution from a single agent to a complete organization with a Chief of Staff, Bosses, and Workers. Read the PRDs and templates I'm attaching and guide me through the migration.

## WHAT I NEED

### Phase 1: Diagnosis (before changing anything)

1. **Analyze my current setup:**
   - How many agents do I have?
   - Who does what?
   - Where are the bottlenecks? (overloaded agent, context rot, runaway costs)

2. **Identify my domains:**
   - Ask me questions about my work/business
   - Based on the answers, suggest 3-5 domains for bosses
   - Explain WHY each domain makes sense separately

3. **Personalized migration plan:**
   - What is the ideal order for bosses? (start with the most critical)
   - Which workers does each boss need? (Watcher vs Maker)
   - Monthly cost estimate

### Phase 2: Foundation (execute)

4. **Mandatory backup:**
   - Make a full backup of the current workspace
   - Confirm it is restorable before proceeding

5. **Promote CoS:**
   - Update your own SOUL.md: from COO/Hub to Chief of Staff
   - Clearly define what you STOP doing vs. what you continue
   - Update HEARTBEAT.md to focus on governance

6. **Create shared/:**
   - Full structure: context/, governance/, costs/, audit/, templates/, outputs/, lessons/
   - TEAM.md as the source of truth
   - Canonical USER.md that everyone inherits
   - TOOLS-SHARED.md with shared integrations
   - Governance docs: daily digest template, cross-boss protocol, quality gates, escalation rules
   - Scripts: cost tracking, context sync

7. **Activate governance on Day 1:**
   - Cron: daily digest (morning)
   - Cron: kill switch (night)
   - Show me the created crons and explain each one

### Phase 3: First Boss

8. **Create Boss A (the highest priority):**
   - Create workspace using the BOSS-WORKSPACE template
   - Customize SOUL.md with specific domain
   - Configure Telegram binding (dedicated topic)
   - Add to agents.list
   - Cron: boss summary (at a time that makes sense)

9. **Create Boss A's Workers:**
   - For each worker, decide: Watcher or Maker?
   - Watchers: create workspace + heartbeat
   - Makers: create workspace (no heartbeat — spawned on demand)

10. **Critical test:**
    - Test spawn chain: CoS → Boss → Worker
    - Test that the boss responds in their topic
    - Test that the daily digest includes the boss
    - ONLY move on to Boss B after Boss A works 100%

### Phase 4: Expand

11. **Repeat for Boss B and Boss C:**
    - Same process as Boss A
    - Test cross-boss communication
    - Validate that governance keeps up

12. **Hardening:**
    - Automatic context sync (weekly cron)
    - Weekly performance review
    - Adjust workers: remove unused ones, add missing ones
    - Review costs: any agent too expensive vs. the value it delivers?

## RULES

- ALWAYS backup before each step
- NEVER skip the test — if Boss A doesn't work, don't create Boss B
- Governance is Day 1, not "later"
- Start with 2-3 bosses, NEVER 5 at once
- Idle worker (Maker) = $0 — don't be afraid to create, but also don't create without need
- Every new agent starts L1 (Observer) — trust is earned
- If something goes wrong: rollback from backup, breathe, try again

## FORMAT

For each step:
1. Explain WHAT you're going to do and WHY
2. Ask for my confirmation
3. Execute
4. Show the result
5. Confirm whether I can move on

Don't automate everything at once. I want to understand each decision.
```
