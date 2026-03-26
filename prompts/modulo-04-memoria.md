# Prompt — Module 4: Memory System (Updated March 2026)

> Paste this prompt in your OpenClaw chat after watching Module 4.
> Also attach the files: `prds/memory-architecture.md`, `templates/MEMORY-template.md`, `templates/HEARTBEAT-template.md` and the folder `templates/memory/`

---

I just finished watching Module 4 of the course on memory. Read the memory architecture PRD and guide me through the implementation.

**What I need you to do:**

1. **Explain how your memory works** — I want to understand the problem (Alzheimer between sessions) and the solution (layered memory)

2. **Create the memory structure** organized into subfolders:
   ```
   memory/
   ├── MEMORY.md              ← general index (the only file always loaded)
   ├── context/
   │   ├── decisions.md       ← permanent and irreversible rules
   │   ├── lessons.md         ← mistakes and learnings
   │   ├── people.md          ← team, partners, contacts
   │   └── business-context.md
   ├── projects/              ← one file per active project
   ├── sessions/              ← diary: one file per day (YYYY-MM-DD.md)
   └── integrations/          ← tool map, IDs, access credentials
   ```

3. **Configure the extraction rule before compaction** — NEVER compact without first extracting lessons, decisions and pending items. This is NON-NEGOTIABLE.

4. **Explain what is loaded vs. searched on demand:**
   - Always loaded: `SOUL.md`, `USER.md`, `AGENTS.md`, `MEMORY.md`, today's + yesterday's sessions
   - Searched on demand: all other files via `memory_search`

5. **Configure memory search** — native semantic search (no external API key needed):
   - `memory_search()` for meaning-based search across all files
   - `memory_get()` to pull only a specific excerpt (token-efficient)
   - Works natively since March 2026 — no OpenAI/Gemini embedding required

6. **Teach how to save correctly** — show practical examples:
   - ❌ "Remember this" (mental note — dies in the next session)
   - ✅ "Save in memory/context/decisions.md as a permanent decision"
   - ✅ "Log in memory/projects/my-project.md"

7. **Configure feedback loops** — JSONs in `memory/feedback/` that capture approve/reject:
   - The agent checks BEFORE suggesting again
   - Doesn't repeat mistakes — real evolution

**Rules:**
- Explain each file and WHAT IT'S FOR before creating it
- Show me a practical example of how a decision becomes permanent memory
- NON-NEGOTIABLE rule: before EACH compaction, run the extraction checklist (lessons, decisions, people, projects, pending)
- Test the semantic search: close the session, open a new one and ask about something that was saved

**Quick reference — what goes where:**

| What it is | File |
|---------|---------|
| Decision that cannot change | `memory/context/decisions.md` |
| Mistake that cannot be repeated | `memory/context/lessons.md` |
| Project status | `memory/projects/project-name.md` |
| Awaiting your input | `memory/pending.md` |
| What happened today | `memory/sessions/YYYY-MM-DD.md` |

Shall we create your memory?
