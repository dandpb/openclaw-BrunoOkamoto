# Student Prompt — M06 Lesson 2: Skills — The superpower system

> Use this prompt with your agent after watching the lesson.

---

## 📦 Tip — Install /criar-skill to create skills faster

Not required in this lesson, but if you want to create skills with help from the agent:

```bash
cd ~/seu-workspace/skills/operations
git clone https://github.com/okjpg/skill-creator criar-skill
```

Or ask the agent: *"Install /criar-skill from the repository https://github.com/okjpg/skill-creator in skills/operations/criar-skill/"*

---

## 🎯 What you'll practice

Creating your first skill from scratch, organizing the folder correctly and testing whether the agent can execute the process consistently.

---

## Prompt to use with your agent

```
I want to create my first skill following the correct OpenClaw structure.

The process I want to document is: [describe here the process you repeat frequently — e.g.: "generate weekly metrics report", "create LinkedIn carousel", "respond to support emails"]

Help me:
1. Define the correct skill name in kebab-case
2. Choose the right category (content, analytics, operations, research, or create a new one)
3. Create the SKILL.md with: name, description (with triggers), metadata and the step-by-step execution
4. Create the folder structure at skills/{category}/{skill-name}/

After creating it, I want to test whether you can execute the process just by reading the SKILL.md — without me having to explain anything.
```

---

## Variations by level

**🟢 Beginner — copy an existing skill:**
```
Show me the SKILL.md of a simple skill you already have, and explain each field.
I want to understand the structure before creating my own.
```

**🟡 Intermediate — create an analytics skill:**
```
Create a skill called "weekly-report" in skills/analytics/.
It should: pull the most important metrics from the week (you define which ones make sense for my business),
format them into clean text with the key numbers, and send it to me every Monday morning.
Include the right triggers in the description so I can activate it easily.
```

**🔴 Advanced — create a skill with a script:**
```
I want a skill that automates [process that uses an API or command line].
Create the SKILL.md + a script in scripts/ that handles the technical part.
The skill should fetch credentials from 1Password — never hardcoded.
```

---

## Post-creation checklist

Before considering the skill done, confirm:

- [ ] Folder created at `skills/{category}/{name}/`
- [ ] SKILL.md has: name, description with triggers, metadata, and clear step-by-step
- [ ] Tested by calling the agent with just the trigger — without providing extra context
- [ ] Agent executed correctly reading only the SKILL.md
- [ ] Skill is in Git (backup done)

---

## Reflection question

> "What process do you do more than twice a week that hasn't become a skill yet?"

That's your next candidate.
