# PRD: Memory Architecture (Updated March 2026)

> Drop this file into the agent: "Implement this memory architecture"

## Context

AI agents forget everything between sessions. Without structured memory, you repeat context every day. This architecture solves that with a subfolder structure that enables precise semantic search.

**March 2026 Update:** `memory_search` now works natively — without needing an external API key (OpenAI/Gemini). Embedding search is built-in.

**⚠️ Breaking v2026.3.13 — MEMORY.md required in uppercase:** The agent loads only one root memory file. `MEMORY.md` (uppercase) takes priority; `memory.md` (lowercase) is only used when `MEMORY.md` doesn't exist. If you created `memory.md` before v3.13, rename it:

```bash
mv memory.md MEMORY.md
```

**Post-compaction behavior (v2026.3.13):** After automatic compaction, the memory index is reindexed asynchronously. If the agent seems to "forget" something right after a compaction — wait a few seconds and try `memory_search` again. This is normal and temporary.

## What the agent loads vs. searches

| Always loaded in session | Searched on demand |
|---------------------------|---------------------|
| SOUL.md, USER.md, AGENTS.md | memory/context/decisions.md |
| MEMORY.md (index) | memory/context/lessons.md |
| memory/sessions/ (today + yesterday) | memory/projects/*.md |
| | skills/ (any skill) |

## Tasks

### 1. Create subfolder structure

```bash
mkdir -p memory/context memory/projects memory/sessions memory/integrations
```

### 2. Create context files

| File | Purpose |
|---------|-----------|
| `memory/context/decisions.md` | Permanent and irreversible decisions |
| `memory/context/lessons.md` | Lessons learned, mistakes, patterns |
| `memory/context/people.md` | Team, partners, contacts — how to interact with each |
| `memory/context/business-context.md` | Business context, products, customers |

**Lesson retention:**
- 🔒 Strategic = permanent (philosophy, architecture patterns)
- ⏳ Tactical = expire in 30 days (bugs, temporary workarounds)

### 3. Create individual projects

Instead of one giant `projects.md`, one file per project:

```
memory/projects/
├── my-saas.md          ← current MRR, upcoming features, pending items
├── may-launch.md       ← status, checklist, responsible parties
└── product-b.md
```

**Why separate?** Semantic search finds the right project without bringing in context from other projects.

### 4. Create MEMORY.md (index)

In the workspace root. It's the map — doesn't duplicate content, only references:

```markdown
# MEMORY.md

## Context
- Decisions: memory/context/decisions.md
- Lessons: memory/context/lessons.md
- People: memory/context/people.md

## Active projects
- [Project Name]: memory/projects/name.md

## Integrations
- Tool map: memory/integrations/
```

### 5. Configure memory cycle in AGENTS.md

```
Memory rules:
1. Daily notes: create memory/sessions/YYYY-MM-DD.md at each relevant session
2. Projects: one separate file per project in memory/projects/
3. INVIOLABLE: before compacting → extract lessons, decisions and pending items
4. Feedback: when rejecting a suggestion → save reason in memory/feedback/
```

### 6. Configure semantic search

The agent uses two tools:
- `memory_search("term")` — semantic search across all files (~400 tokens/chunk)
- `memory_get("file.md", start_line)` — reads only the relevant section

**Works natively** since March 2026. No external key needed.

### 7. Configure feedback loops (advanced)

```
memory/feedback/
├── content.json    ← approved/rejected content suggestions
├── tasks.json      ← task execution preferences
└── tone.json       ← tone and style adjustments
```

Format:
```json
{
  "entries": [
    {
      "date": "2026-03-14",
      "context": "Suggested LinkedIn post with formal language",
      "decision": "reject",
      "reason": "Too corporate — prefers direct and conversational",
      "tags": ["linkedin", "tone"]
    }
  ]
}
```

## How to ask to save

| ❌ Doesn't work | ✅ Works |
|----------------|------------|
| "Remember this" | "Save in memory/context/decisions.md" |
| "Store this info" | "Add to memory/projects/name.md" |
| "Don't forget that..." | "Record in memory/sessions/today as a lesson" |

## Expected Result

1. Structure created with organized subfolders
2. MEMORY.md as index pointing to everything
3. Test: close session → open new one → ask about something saved → agent finds it via memory_search
