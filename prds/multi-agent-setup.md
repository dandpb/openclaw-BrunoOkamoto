# PRD: Multi-Agent Setup

> ⚠️ **Note (02/19/2026):** References to `shared/TEAM.md` reflect the original v2. In the actual structure, the team is in `shared/people.md` and agents in workspace files.

> For when one agent is not enough. Drop this into your main agent.

## Context

When responsibilities grow, a single agent becomes overwhelmed. The solution: multiple specialized agents, coordinated by a main one (hub).

## Architecture

```
Gateway (1 server)
├── Main Agent (Opus) ← hub, coordinates everything
├── Content Agent (Sonnet) ← production, drafts
├── Scraper Agent (Sonnet) ← data collection
└── [Others as needed]
```

## Leveling System (Kevin Simback)

Every new agent starts at L1 and levels up as it gains trust:

| Level | Name | Autonomy | Review |
|-------|------|-----------|--------|
| L1 | Observer | Zero — output always reviewed | Every delivery |
| L2 | Contributor | Low — can suggest, not execute | Weekly |
| L3 | Operator | Medium — executes within guidelines | Weekly |
| L4 | Trusted | High — near total autonomy | Biweekly |

**Rules:**
- Promotion via weekly performance review
- Demotion is possible (if quality drops)
- NEVER rush an agent to L3+ without history

## Shared Context

Create a `shared/` folder accessible by all agents:

```
shared/
├── TEAM.md          ← Registry: who does what, level, status
├── outputs/         ← Shared results
└── lessons/         ← Team learnings
```

**TEAM.md example:**
```markdown
| Agent | Role | Level | Model | Status |
|--------|-------|-------|--------|--------|
| Amora | COO / Hub | L4 | Opus | Active |
| Content | Production | L1 | Sonnet | Active |
| Scraper | Collection | L1 | Sonnet | Active |
```

## Economics

- **Main agent:** Opus (interaction, decisions)
- **Execution agents:** Sonnet (crons, routine tasks)
- **Heartbeats:** Haiku (~90% savings)
- Rule: an agent that doesn't need Opus should NOT use Opus

## Coordination

- Main agent is the HUB — user only talks to it
- Secondary agents don't have Telegram binding
- Hub model > Mesh model (cross-domain learning doesn't work well)
- Sub-agents (sessions_spawn) for parallel tasks
- **After spawning sub-agents: use `sessions_yield`** to cleanly end the turn and receive results in the next message (v2026.3.12+)

## What's New in 3.13

### sessions_yield — New Orchestration Tool

Version 2026.3.13 added the `sessions_yield` tool, which allows the main agent to **immediately end the current turn** after spawning sub-agents, receiving results as the next message.

```json
// Flow before (3.12 and earlier):
// 1. Agent spawns sub-agent
// 2. Agent keeps "running" (waiting, processing)
// 3. Sub-agent finishes and announces

// Flow with sessions_yield (3.13+):
// 1. Agent spawns sub-agent
// 2. Agent calls sessions_yield → turn ends
// 3. Sub-agent finishes → next turn starts with result
```

**Why it matters:** The orchestrator can now cleanly end the session without getting "stuck" while sub-agents work. Reduces token consumption and improves coordination.

**Practical example:**
```
After spawning 3 sub-agents for parallel tasks, the hub calls
sessions_yield to exit the turn. Results arrive as
the next message — everything organized.
```

> ✅ **No extra config needed.** The `sessions_yield` tool is available after updating to v2026.3.13.

## What's New in 3.2

### ACP Dispatch — Enabled by Default
Starting from version 3.2, ACP (Agent Communication Protocol) dispatch is **enabled by default**. No longer needs to be manually enabled in config.

```json
// BEFORE (3.1 and earlier):
{
  "acp": {
    "dispatch": true
  }
}

// NOW (3.2+): this config is no longer needed
// ACP dispatch is already active automatically
```

> ✅ If you have this old config, you can remove it — it doesn't cause issues, but it's redundant.

### sessions_spawn with Attachments
`sessions_spawn` now supports sending **attachments** (files, images, buffers) directly when spawning a sub-agent:

```json
{
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Analyze this report and give me an executive summary.",
    "attachments": [
      {
        "type": "file",
        "path": "/workspace/monthly-report.pdf"
      }
    ]
  }
}
```

Use cases: passing PDFs for analysis, images for processing, data files for transformation — all in a single call without extra steps.

## Tasks

1. Define which agents you need (max 2-3 to start)
2. Create config for each agent with its own SOUL.md
3. Configure shared/TEAM.md
4. Define models (Opus vs Sonnet)
5. Take it for a first test drive with a simple task
6. Review after 1 week → decide on promotion

## Expected Result

A coordinated team of 2-3 agents, each with a clear role and defined level.
