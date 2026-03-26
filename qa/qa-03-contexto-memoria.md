# ❓ Q&A — Context & Memory (Token, /compact, /new)

> Plain language. No terminal. Paste the prompt into your bot and it handles the rest.

---

## "My bot got slow and the responses got much worse"

**What probably happened:** The conversation got too long. Imagine trying to remember EVERYTHING you did over the last 6 months all at once — your brain freezes. It's the same for the bot.

**What to do:**
Paste this prompt into your bot:

```
I feel like you've gotten slower and the responses have gotten worse.
Tell me:
1. What is the current context size? (use /status)
2. Is it close to the limit?
3. What do you recommend: /compact or /new?
4. What is the difference between the two so I can decide?
```

---

## "What's the difference between /compact and /new? I'm afraid of losing everything"

**In plain language:**

| | /compact | /new |
|---|---|---|
| **What it does** | Summarizes the current conversation | Starts a fresh conversation |
| **Lose memory?** | No — it summarizes, not deletes | The conversation disappears, but memory files remain |
| **When to use** | Long conversation but want to continue | Want a fresh start |
| **Analogy** | Taking a photo of what happened | Opening a new notebook |

**Short answer:** Use `/compact` first. If it's still slow afterward, use `/new`.

**Important:** Even with `/new`, the bot still remembers you! It has memory files (MEMORY.md, memory/) that persist between conversations.

---

## "The bot 'forgot' something I had told it"

**What happened:** Either the conversation was compacted and that information didn't make it into the summary, or a new session was started.

**What to do:**
Paste this prompt into your bot:

```
You seem to have forgotten [DESCRIBE WHAT IT FORGOT].
Help me recover it:
1. Check your memory files (MEMORY.md, memory/)
2. Is that information saved somewhere?
3. If not, I'll tell you again now: [RESTATE THE INFORMATION]
4. Please save it in the appropriate memory file so you don't forget again.
```

---

## "A 'token limit' or 'context too long' error appeared"

**What happened:** The conversation exceeded the model's memory limit. It's like trying to fit 10 liters into a 2-liter cup.

**What to do immediately:**
Paste this prompt into your bot:

```
A context/token limit error appeared.
I need you to:
1. Run /compact now to summarize the conversation
2. Confirm when you're done
3. Continue from where we left off after the compact
```

**To prevent it from happening again:**
Paste this prompt:

```
I want to configure automatic compaction so you never hit the limit again.
Guide me on how to configure "compaction: { mode: default }" in my openclaw.json.
Explain what each option does before I apply it.
```

---

## "What is vector memory? Do I need it?"

**In plain language:** It's a way for the bot to store a lot of information and find the right part at the right time — like a smart book index.

**Do you need it?** Probably not right now. Most students get along very well using only normal memory files (MEMORY.md). Vector memory is for advanced use cases with a large amount of information.

**If you want to understand more:**
Paste this prompt into your bot:

```
Explain to me in very simple terms:
1. What are the MEMORY.md and memory/ files you use?
2. What is "vector memory" and when does it make sense?
3. For my current use, what do you recommend?
```

---

*Last updated: Feb/2026*
