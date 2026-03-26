# Student Prompt — Lesson N-4: Telegram Bot Slowness

**How to use:** Paste this prompt directly into your OpenClaw agent to start an interactive diagnostic and resolution session for bot slowness.

---

## 📋 MAIN PROMPT

```
My Telegram bot is slow — sometimes it takes 30 seconds or more to respond, and sometimes it seems to freeze.

I want to do a complete diagnosis with you. Guide me through the process step by step, like in Lesson N-4 of the course.

For each step:
1. Tell me which command to run or which config to check
2. Explain what to look for in the result
3. Wait for me to paste the output
4. Analyze it and tell me if that's the cause

Let's start with the initial diagnosis. What is the first step?
```

---

## 🔍 DIAGNOSIS PROMPTS BY CAUSE

Use the prompts below as the diagnosis progresses:

### If you suspect a full context:

```
I'll run /status now and show you the result.
[paste the result of /status]

Is it the context? What do you recommend — /compact or /new? Explain the difference before I decide.
```

### If you suspect a heavy model:

```
Show me how to see which model is currently configured and how to switch
to Sonnet for conversations and Haiku for crons.
I want to understand the real impact on response time.
```

### If you suspect a weak VPS:

```
Help me interpret the output of `openclaw status` and `htop`.
What do the numbers tell me about whether my VPS can handle the current load?
```

### If you suspect simultaneous crons:

```
Think through this: if I have 4 crons all at 09:00, what happens
on the server? Show me how to stagger them and how to list the active crons.
```

### If you suspect aggressive heartbeat:

```
My heartbeat is configured to run every X minutes.
What is the ideal interval? And should I use Haiku for it? Why?
```

### To enable partial streaming:

```
I want to enable partial streaming on Telegram to improve the
perception of speed. Show me exactly where and how to configure this in openclaw.json.
```

---

## ✅ FINAL VERIFICATION PROMPT

After implementing the changes:

```
I implemented the changes you suggested. Now let's verify it worked:

1. How do I objectively test whether the bot got faster?
2. What should I monitor over the next 24 hours to confirm it's stable?
3. Are there any "prevention" settings you recommend to avoid having this problem again?

Give me a summary of the changes we made and what each one fixes.
```

---

## 📊 PRACTICAL EXERCISE PROMPT

To practice the diagnosis in a structured way:

```
I'll give you a hypothetical situation and you guide me through the diagnosis:

Situation: Bot working fine for weeks. Suddenly, this afternoon it starts
taking 20-30s for every message. It's the same time I added 3 new
monitoring crons and increased the heartbeat from 30 to 5 minutes.

Without looking at the logs yet — what are the most likely hypotheses?
In what order should I investigate and why?
```

---

## 💡 USAGE TIPS

- **Paste real results:** When the agent asks for command output, paste the real result from your terminal. The diagnosis becomes much more accurate.
- **One problem at a time:** If there are multiple causes, fix one at a time and test before moving to the next.
- **Save the changes:** After each change to `openclaw.json`, reload the gateway with `openclaw gateway restart`.
- **Measure before and after:** Note the average response time before the changes to compare afterwards.

---

*Prompt created for Lesson N-4 of the OpenClaw Course | Level: Intermediate*
