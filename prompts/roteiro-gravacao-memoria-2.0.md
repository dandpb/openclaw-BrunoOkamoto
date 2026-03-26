# Recording Script — "Memory 2.0"
**New separate lesson | ~20 min | March 2026 Update**

---

## Setup before recording

- Open terminal with a clean workspace (new session)
- Have open: VS Code with `memory/` visible, side terminal
- Leave `memory/sessions/` with 2–3 visible files (to show the diary)
- Disable notifications

---

## BLOCK 1 — Opening (1:30 min)

**[FRONT CAMERA]**

> "Everyone, Memory 2.0. If you watched the foundation lesson, you'll remember we configured the memory system, the decisions, lessons, pending files… and when testing the memory search, it got stuck asking for an OpenAI API key.
>
> Two things have happened since then. First: that bug was fixed. Memory search now works natively, without needing any external key. Second: I learned — using my own agent every day — that the folder structure we created in the first lesson works, but there are some adjustments that make a huge difference.
>
> This lesson covers both. It's short. About 20 minutes. And you'll come out with your agent's memory system actually running."

---

## BLOCK 2 — What the agent loads vs. searches (4 min)

**[FRONT CAMERA → SHARE SCREEN: terminal]**

> "Before anything else, I need to make this very clear, because it changes how you think about the structure:"

**[SHOW ON SCREEN: type `/status` in the agent and show output]**

> "Every new session, the agent automatically loads 5 things:
> SOUL.md, USER.md, AGENTS.md, MEMORY.md — and today's and yesterday's notes.
>
> Just that. Nothing else.
>
> Everything else — decisions, lessons, projects, integrations — stays OUTSIDE the context. The agent will search for it when needed. That's semantic search, and I'll show you how it works in a moment."

**[SHOW: folder structure in VS Code]**

> "MEMORY.md — the index — is the only file that's always present. And it doesn't store content. It points to where the content is. Look at mine:"

**[SHOW: MEMORY.md open — sections with links to memory files]**

> "It's a map. Not the territory."

---

## BLOCK 3 — Subfolder structure (4 min)

**[SHARE SCREEN: VS Code, memory/ folder tree]**

> "In the foundation lesson we created everything at the root of the memory folder. Decisions.md, lessons.md, pending.md, all together. It works — but when volume grows, semantic search starts bringing mixed context.
>
> What I use today:"

**[SHOW: tree of the memory/ folder in terminal]**

```
memory/
├── context/
│   ├── decisions.md
│   ├── lessons.md
│   ├── people.md
│   └── business-context.md
├── projects/
│   ├── metricaas.md
│   ├── comunidade-ai.md
│   └── mission-control-apis.md
├── content/
│   ├── voice/linkedin.md
│   └── voice/youtube.md
├── integrations/
│   ├── telegram-map.md
│   └── credentials-map.md
└── sessions/
    ├── 2026-03-14.md
    └── 2026-03-12-mission-control.md
```

> "Subfolders by category. The logic is simple: when I ask 'what's the status of Metricaas?', the agent searches in projects/ and finds exactly the right file. If everything were in one giant projects.md, it would bring context from MGM, from AI Community, from everything mixed together.
>
> Separate projects per file. That's the most important change."

**[SHOW: open metricaas.md — real file content]**

> "Each project has: current status, next actions, pending items. The agent updates it when you ask. In the next session, it finds everything here."

---

## BLOCK 4 — How semantic search works (4 min)

**[FRONT CAMERA → SHARE SCREEN: terminal with agent]**

> "Now what really changed. In the old lesson, memory search required an OpenAI API key to work. That caused a lot of confusion. Students would set everything up correctly, reach this part, and get stuck.
>
> Not anymore. It works natively."

**[LIVE DEMO: open new session in terminal]**

> "Let me show you. New session — zeroed context. No project files loaded."

**[TYPE: "what is the current status of Metricaas?"]**

> "The agent will search through the files... look here — it used memory_search, found the file projects/metricaas.md, and brought exactly the relevant section. Without me manually opening anything."

**[SHOW OUTPUT — agent finding the info]**

> "This is semantic search. It's not grep, it's not exact keyword matching. It understands meaning. If I ask 'how is my metrics SaaS doing', it will find the same file.
>
> Two tools under the hood:
> - `memory_search` — searches everything, brings the most relevant chunks
> - `memory_get` — reads only the specific lines it needs
>
> You don't need to call these tools manually. The agent uses them automatically when you ask something."

---

## BLOCK 5 — How to ask it to save (3 min)

**[FRONT CAMERA]**

> "The biggest mistake beginners make: thinking the agent will remember on its own.
>
> It won't. If it's not in a file, it doesn't exist in the next session.
>
> The difference:"

**[SHOW ON SCREEN — simple slide or type in terminal]**

> "❌ 'Remember this' → dies when you close the window
> ✅ 'Save in memory/context/decisions.md' → permanent"

**[LIVE DEMO: type a decision and ask it to save]**

> "I'm going to make a decision now: all new integrations need documentation before going to production. I'll ask it to save:"

**[TYPE: "It's decided: every new integration needs documentation before going to production. Save in memory/context/decisions.md as a permanent decision."]**

**[SHOW: agent opening the file and saving]**

> "Done. New session, that context will be there.
>
> Quick guide on where to save:
> - Decision that doesn't change → context/decisions.md
> - Error that can't repeat → context/lessons.md
> - Project status → projects/name.md
> - Waiting for your input → pending.md"

---

## BLOCK 6 — Closing (1:30 min)

**[FRONT CAMERA]**

> "Recap of what changed:
>
> One — semantic search works natively, no API key needed.
>
> Two — subfolders by category. Projects with one file per project. Context separate from integrations, separate from sessions.
>
> Three — the agent only loads automatically SOUL, USER, AGENTS, MEMORY, and today's and yesterday's sessions. Everything else is on demand.
>
> Four — to save, you need to be explicit. 'Save in memory/context/decisions.md'. Without that, it doesn't exist.
>
> The material for this lesson is on Drive — there's a PDF guide with the full structure, the prompt to ask the agent to reorganize memory, and the updated PRD. Link in the description.
>
> Any questions, post in the group. See you next time."

---

## Pre-recording checklist

- [ ] New session open in terminal (zeroed context)
- [ ] VS Code with `memory/` visible and real files (metricaas.md, decisions.md)
- [ ] MEMORY.md open in another tab
- [ ] Notifications disabled
- [ ] Tested the memory_search demo before recording

## Approximate timings

| Block | Content | Time |
|-------|---------|------|
| 1 | Opening | 1:30 |
| 2 | Loads vs. searches | 4:00 |
| 3 | Subfolder structure | 4:00 |
| 4 | Semantic search (demo) | 4:00 |
| 5 | How to save (demo) | 3:00 |
| 6 | Closing | 1:30 |
| **Total** | | **~18 min** |

## Links to put in the description

- Student material (PDF): Drive → OpenClaw Course → aula-04-memoria → modulo-04-memoria.pdf
- Implementation prompt: Drive → aula-04-memoria → prompts → modulo-04-memoria.md
- Updated PRD: Drive → aula-04-memoria → prd → memory-architecture.md
