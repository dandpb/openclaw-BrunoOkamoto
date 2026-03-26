# Prompt — Module 7: Multi-Agents

> Paste this prompt in your OpenClaw chat after watching Module 7.
> Attach the file: `prds/multi-agent-setup.md`
> ⚠️ Note: `shared/lessons/` referenced below = `shared/lessons.md` in the actual structure.

---

I just watched Module 7 of the course on multi-agents. Read the PRD and guide me through creating my first agent team.

**What I need you to do:**

1. **Assess whether I need multi-agents right now** — if my usage is still simple, tell me honestly that it's too early. Multi-agents without a foundation = chaos.

2. **If it makes sense, help me create 1-2 extra agents:**
   - Ask me about which tasks I want to delegate
   - Create the SOUL.md and AGENTS.md for each agent
   - Configure in the gateway (agents.list)

3. **Implement the leveling system:**
   - L1 Observer → L2 Contributor → L3 Operator → L4 Trusted
   - Every new agent starts at L1 (output reviewed by me)
   - Explain how to promote and demote

4. **Configure shared context:**
   - TEAM.md — registry of all agents
   - shared/outputs/ — shared results
   - shared/lessons/ — team learnings

5. **Define the economics and demonstrate the full cycle:**
   - Which model for each agent (not every agent needs Opus)
   - When to spawn sub-agents vs. doing it in the main session
   - Demonstrate the orchestration cycle live with sessions_yield:
     1. Spawn a sub-agent with sessions_spawn for a simple task
     2. Call sessions_yield to cleanly close the turn
     3. Show the result arriving in the next message
   - Explain the token difference with and without sessions_yield

**Rules:**
- Less is more — 2 well-built agents > 6 messy agents
- I (the human) am always in the loop for important decisions
- At the end, show me the full team and who does what

Shall we build the team?
