# Student Prompt: Extra Lesson E — Context & Memory Management

> **Paste this prompt in the chat with your OpenClaw agent to practice the lesson concepts.**

---

Hello! I'm going to practice context and memory management with you.

**Goal:** Learn how to use `/status`, `/compact`, `/new`, understand automatic compaction, and how memory works between sessions.

Please guide me through the following exercises:

---

## Exercise 1: Understanding `/status`

1. Show me how to use the `/status` command
2. Explain what each piece of information means:
   - Current model
   - Context usage (tokens and %)
   - Cost (if available)
   - Session time
3. Tell me: at what % of context should I start to be concerned?

---

## Exercise 2: Simulating Context Growth

Let's have a long conversation to fill up the context (doesn't need to be useful, just for practice):

1. Tell me a story about how you were created (use lots of text)
2. Then explain how an LLM works in technical detail (again, lots of text)
3. After that, run `/status` again and show me how much the context grew

**Reflective question:** Why do long conversations increase the context so much?

---

## Exercise 3: Manual Compaction

1. Show me how to use the `/compact` command
2. Run `/status` before and after so I can see the difference
3. Explain:
   - What was preserved?
   - What was summarized?
   - Do you still remember our previous conversation?

---

## Exercise 4: Difference Between `/compact` and `/new`

1. Explain the difference between:
   - Compacting the session (`/compact`)
   - Starting a new session (`/new`)

2. Give me examples of when to use each:
   - 3 situations for `/compact`
   - 3 situations for `/new`

---

## Exercise 5: Testing `/new`

**Before doing `/new`:**
1. Help me create a file `memory/teste-aula-e.md` with:
   - Summary of what we've practiced so far
   - An important fictional decision: "Project X should use Python 3.11"
   - Current date and time

**Now do `/new`**

**After `/new`:**
1. Do you still remember me?
2. Do you remember what we talked about before?
3. Can you access the file `memory/teste-aula-e.md`?
4. Explain what happened: what did you lose and what did you retain?

---

## Exercise 6: Automatic Compaction

Explain how to configure automatic compaction in OpenClaw:

1. Which file do I need to edit?
2. Which parameters should I configure?
3. Which threshold do you recommend? (70%, 75%, 80%?)
4. What are the advantages and disadvantages of enabling it?

---

## Exercise 7: Memory Hierarchy

Draw me (in text/ASCII) the memory hierarchy of OpenClaw:

1. Session context (temporary)
2. Recent memory (memory/*.md)
3. Long-term memory (MEMORY.md)

And explain:
- What happens to each level when I use `/compact`?
- What happens to each level when I use `/new`?
- How do you decide what to save at each level?

---

## Exercise 8: Troubleshooting

Help me solve these fictional problems:

**Problem 1:** "I did `/new` and the agent doesn't remember the project we started yesterday"
- What might have happened?
- How do I fix it?

**Problem 2:** "My context is at 95% and `/compact` only freed up 10%"
- What should I do?
- How do I prevent this in the future?

**Problem 3:** "After compacting, the agent forgot an important decision"
- Why does this happen?
- How do I ensure important decisions are not lost?

---

## Exercise 9: Personal Strategy

Based on my usage (you can ask me how I plan to use OpenClaw), recommend:

1. Should I enable auto-compact? With what threshold?
2. How often should I use `/new`?
3. Should I actively monitor context or leave it on automatic?
4. Specific tips for saving API costs

---

## Exercise 10: Final Checklist

Create a personalized checklist of context management best practices that I can print and keep next to my computer. Something like:

**Before starting:**
- [ ] ...

**During work:**
- [ ] ...

**When finishing:**
- [ ] ...

---

## Final Reflection

After completing all these exercises, answer me:

1. What is the practical difference between `/compact` and `/new`?
2. Why is automatic compaction important?
3. How does memory work between sessions?
4. What is the biggest lesson you learned about context management?

---

**Thank you for guiding me! 🚀**

Now I know:
✅ Use `/status`, `/compact`, `/new` with confidence
✅ Configure automatic compaction
✅ Understand the memory hierarchy
✅ Manage context proactively
✅ Save API costs

---

*If you have additional questions during the exercises, feel free to ask!*
