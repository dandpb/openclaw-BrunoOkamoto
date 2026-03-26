# Student Prompt — M06 Lesson 3: Create your skills with /criar-skill

> Use this prompt with your agent after watching the bonus lesson.

---

## 📦 Step 1 — Install /criar-skill

The skill is available on GitHub. Install it before using:

```bash
# In your workspace terminal
cd ~/seu-workspace/skills/operations

# Clone the skill
git clone https://github.com/okjpg/skill-creator criar-skill

# Done. The agent can now use it.
```

Or ask the agent to install it:
```
Install the /criar-skill in my workspace.
Repository: https://github.com/okjpg/skill-creator
Place it in skills/operations/criar-skill/
```

---

## 🎯 What you'll practice

Using `/criar-skill` in both modes: capturing a process you've already solved together, and creating a new skill from an idea you don't yet know how to structure.

---

## Path A — You just solved something. Don't let it disappear.

Use it right after a conversation where you solved a problem together:

```
/criar-skill
```

Just that. The agent reads the history, extracts the process and proposes the complete skill.

**When to use:** Whenever a conversation took more than 10 minutes to solve something. If it was hard once, it will be again — unless it becomes a skill.

---

## Path B — You have an idea. You want to structure it.

```
/criar-skill I want to [describe your idea in 1 sentence]
```

**Real examples to test:**

```
/criar-skill I want to generate a weekly summary of my most important metrics
```

```
/criar-skill I want to create meeting briefs before each important call
```

```
/criar-skill I want to respond to Instagram comments while keeping my tone of voice
```

```
/criar-skill I want to analyze competitors and give me the 3 main points
```

The agent will ask questions to understand the process — answer naturally. At the end, it proposes the complete skill and you approve the deploy.

---

## Lesson challenge

Create **at least 2 skills** this week:

1. **One from Path A** — Think of a problem you've already solved with the agent recently. Recreate the conversation and use `/criar-skill` at the end.

2. **One from Path B** — Think of a process you do manually today that you'd like the agent to take over. Use `/criar-skill I want to [your idea]`.

---

## Question for each skill you create

Before approving the deploy, answer:

- Does the trigger make sense? (Can I activate it naturally?)
- Is the output what I expected?
- Is there any important detail that was left out?

If yes to all three — approve. If not, ask the agent to adjust before saving.

---

## Remember

> "Any process you repeat more than twice is a candidate for a skill."

Every time you find yourself explaining something to the agent again — that's a sign a skill is missing.
