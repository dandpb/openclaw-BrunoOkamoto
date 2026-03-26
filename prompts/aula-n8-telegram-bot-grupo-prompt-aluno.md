# Student Prompt — Lesson N-8: Telegram Bot Not Responding in a Group

> **How to use:** Copy the prompt below and paste it in the chat with your OpenClaw agent after watching the lesson.

---

## 📋 Main Prompt

```
Hello! I watched lesson N-8 on configuring a bot in Telegram groups.

I'm trying to get my bot to work in a group, but [it doesn't respond / only responds to commands / responds sometimes].

Help me:
1. Diagnose the specific problem in my case
2. Apply the necessary fixes
3. Verify it worked

Let's start with the diagnosis?
```

---

## 🔍 Exercise 1 — Complete Diagnosis

```
Please do a complete diagnosis of my bot setup for groups:

1. Check the current configuration:
   - `openclaw config get channels.telegram.groupPolicy`
   - `openclaw config get channels.telegram.groupAllowlist`

2. Tell me which of the 3 causes is most likely:
   - Privacy mode enabled in BotFather
   - groupPolicy not configured
   - Chat ID is not in the allowlist

3. Check the logs for group messages:
   `openclaw gateway logs | tail -50`

After the diagnosis, tell me exactly what I need to do.
```

---

## 🤖 Exercise 2 — Privacy Mode Fix

```
I need to check and fix my bot's privacy mode.

Please guide me through the complete process:
1. How to check if privacy mode is enabled (signal in bot behavior)
2. Step-by-step to disable it via BotFather:
   - Which command to send to BotFather
   - What to select when it asks
   - How to confirm it was disabled
3. Why I need to remove and re-add the bot to the group
4. How to confirm the change worked

(If you've already checked and privacy mode is disabled, confirm that and let's move to the next step)
```

---

## ⚙️ Exercise 3 — Configure groupPolicy

```
I want to configure the OpenClaw groupPolicy correctly.

Please:
1. Explain the difference between groupPolicy = "allowlist" and "open"
2. Configure the allowlist (recommended for security):
   `openclaw config set channels.telegram.groupPolicy allowlist`
3. Help me find the chat ID of my group:
   - Run `openclaw gateway logs | grep -i "chat_id"`
   - Or tell me another method if it doesn't appear
4. After finding the ID, configure the allowlist:
   `openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXXXXX]"`
5. Restart the gateway: `openclaw gateway restart`
6. Test: send a message in the group and check the logs

(My group is: [DESCRIBE YOUR GROUP — e.g.: "family group of 5 people"])
```

---

## 📍 Exercise 4 — Finding Chat ID in Practice

```
I need to find the chat ID of my Telegram group.

Please guide me through ALL available methods:

Method 1 — Via OpenClaw logs:
- How to send a test message in the group
- Where exactly the chat ID appears in the logs
- The correct command format to filter

Method 2 — Via @userinfobot:
- How to use this bot to find the ID
- What to do with the information it returns

Method 3 — Via Telegram API (if necessary):
- How to use the API URL to see recent updates

Which method is easiest for beginners?
```

---

## 🔄 Exercise 5 — dmPolicy vs groupPolicy in Practice

```
I want to fully understand the difference between dmPolicy and groupPolicy.

Please:
1. Show my current configuration of both:
   - `openclaw config get channels.telegram.dmPolicy`
   - `openclaw config get channels.telegram.groupPolicy`

2. Explain what each current setting means in practice:
   - Who can send a private message to the bot?
   - In which groups does the bot respond?

3. Recommend the ideal configuration for security:
   - dmPolicy for personal use (just me)
   - groupPolicy for a specific group I want

4. If I need to adjust, give me the exact commands.
```

---

## 🗺️ Exercise 6 — Diagnostic Flowchart (use if you still have problems)

```
I still can't get the bot to work in the group. Let's be systematic.

Please take me through the diagnostic flowchart step by step:

Step 1: Does the bot respond in the group when you send /start?
[Yes → Step 2] [No → Privacy mode or bot is not in the group]

Step 2: Is groupPolicy configured?
[Yes → Step 3] [No → configure groupPolicy]

Step 3: Is the group's chat ID in the allowlist?
[Yes → Step 4] [No → add chat ID]

Step 4: Was the gateway restarted after the changes?
[Yes → check logs] [No → openclaw gateway restart]

For each step, run the diagnosis and tell me the result. Let's solve this together.
```

---

## ✅ Final Learning Check

```
To close the exercises for lesson N-8, give me a quick quiz with 5 questions about:
- What privacy mode is and when it causes problems
- Difference between dmPolicy and groupPolicy
- How to find the chat ID of a group
- Why you need to remove and re-add the bot when changing privacy mode
- When to use groupPolicy "open" vs "allowlist"

After I answer, give me feedback on what I got right and what I need to review.
```

---

## 💡 Emergency Prompt (if nothing works)

> If you've tried everything and the bot still doesn't respond in the group:

```
My bot is NOT responding in the group and I've already tried everything. Help me with a complete debug:

1. Run `openclaw gateway logs | tail -100` and analyze everything
2. Check if there are Telegram-related errors
3. Check if the webhook is working: `openclaw provider status telegram`
4. Show me ALL the current Telegram channel configuration:
   `openclaw config get channels.telegram`
5. Based on what you find, give me the specific solution

I'm willing to follow any step — I just need the bot to work in the group.
```
