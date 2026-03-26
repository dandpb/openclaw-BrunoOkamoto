# ❓ Q&A — OpenClaw Architecture (Brain, Arms, Subagents)

> Plain language. No terminal. Paste the prompt into your bot and it handles the rest.

---

## "What's the difference between the agent's brain and its arms?"

**In plain language:**

Think of it this way: you are the **boss**. OpenClaw is your **company**.

- **Brain (Gateway)** = The central office. It receives your requests, makes decisions, coordinates everything.
- **Arms (Tools/Skills)** = The specialized employees. One does web searches, another accesses the calendar, another sends messages.
- **Subagents** = Freelancers hired for specific tasks. They work in parallel and deliver results.

**Full analogy:**
> You say: "Research the best restaurants near me for tonight and put them in my calendar."
> - The **brain** understands the request
> - The **search arm** looks up the restaurants
> - The **calendar arm** creates the event
> - Everything happens in a coordinated way

---

## "What is a subagent and when should I use one?"

**In plain language:** A subagent is like hiring a temporary assistant to do a specific task while you continue doing something else.

**When to use:**
- Tasks that take a long time (long research, analysis of a lot of data)
- Parallel tasks (while one researches, another writes)
- Risky tasks (better to let an "assistant" test before the "boss" executes)

**What to do:**
Paste this prompt into your bot:

```
I want to understand when it's worth using subagents in my case.
Explain:
1. What makes a subagent different from a normal task?
2. For what I use the bot for today, does it make sense to use subagents?
3. If so, give me a practical example of how it would work?
```

---

## "Should I use OpenClaw or n8n for automation?"

**Simple difference:**

| | OpenClaw | n8n |
|---|---|---|
| **Best for** | Tasks that require reasoning and natural language | Fixed, predictable flows (if X then Y) |
| **Example** | "Summarize important emails and alert me about urgent ones" | "When an email with subject X is received, save it to the sheet" |
| **Requires** | VPS + AI API | Server or cloud account |
| **Learning curve** | Medium (you have AI helping you) | Medium (visual interface) |

**Short answer:** Use OpenClaw when you need human judgment. Use n8n when the flow is always the same.

**They can work together:** n8n triggers a webhook → OpenClaw receives it and decides what to do.

---

## "How do I know if my agent is working correctly?"

**What to do:**
Paste this prompt into your bot:

```
Run a full health check on my agent:
1. Is the gateway running correctly?
2. Are all tools working?
3. Is memory being saved correctly?
4. Are there any crons or automations with issues?
5. What do you recommend checking regularly?
Give me a summary of the overall status.
```

---

## "Can I have more than one agent? How does that work?"

**In plain language:** Yes! It's like having a team of specialized assistants.

**Examples:**
- **Main Agent:** Does everything, it's your personal assistant
- **Work Agent:** Only handles emails and professional tasks
- **Content Agent:** Specialized in creating posts and text

**What to do:**
Paste this prompt into your bot:

```
I want to understand how having multiple agents works.
Explain:
1. How is each agent configured?
2. Do they share memory or are they separate?
3. How much does this increase the cost?
4. Does it make sense for my current use case to have more than one?
```

---

*Last updated: Feb/2026*
