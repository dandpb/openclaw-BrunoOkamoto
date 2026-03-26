# ❓ Q&A — Telegram (Config, Allowlist, Privacy)

> Plain language. No terminal. Paste the prompt into your bot and it handles the rest.

---

## "Anyone can send messages to my bot and it responds"

**What happened:** Your bot is configured as "open" — anyone who discovers its username can use it. It's like leaving the door to your house wide open.

**What to do:**
Paste this prompt into your bot:

```
My bot is responding to anyone. I need to restrict this.
Help me:
1. Find out what my numeric Telegram ID is
2. Configure dmPolicy to "allowlist"
3. Add my ID to the allowed list
4. Confirm it's correct by testing
Explain everything step by step.
```

---

## "My bot stopped responding to me after I configured the allowlist"

**What probably happened:** You set up the allowlist but forgot to include YOUR OWN ID — or you typed it wrong.

**What to do:**
Paste this prompt into your bot (via another channel, such as a direct chat if available):

```
I can no longer send messages to my main bot.
I think I locked myself out of the allowlist.
Help me check:
1. What is my Telegram ID? (tell me how to find out)
2. How do I see who is on the current allowlist?
3. How do I correctly add my ID?
```

**How to find your Telegram ID:** Send `/start` to @userinfobot on Telegram — it will reply with your numeric ID.

---

## "Bot doesn't work in a group / topic"

**What to do:**
Paste this prompt into your bot:

```
My bot is not responding in the Telegram group/topic.
Help me check:
1. Is the bot's Privacy Mode disabled? (it needs to be disabled to work in groups)
2. Is the group ID in the allowed channels configuration?
3. Is there any "allowFrom" or "allowedIds" configuration that needs to be updated?
Guide me step by step.
```

**Quick tip:** In BotFather, send `/mybots` → select your bot → `Bot Settings` → `Group Privacy` → `Turn off`. This fixes 80% of group problems.

---

## "An error appeared with allowedIds or allowFrom — what changed?"

**What happened:** OpenClaw updated the configuration format. Older versions used `allowedIds` or `allowFrom` — the current version uses `dmPolicy: "allowlist"` with `allowedUsers`.

**What to do:**
Paste this prompt into your bot:

```
My Telegram configuration has "allowedIds" or "allowFrom" that seem to be from an older version.
Help me:
1. Identify which format I'm using
2. Migrate to the current format (dmPolicy + allowedUsers)
3. Verify the config is correct
4. Restart the gateway to apply it
```

---

## "How do I add more people who can use my bot?"

**What to do:**
Paste this prompt into your bot:

```
I want to add a new person so they can use my bot.
Their Telegram ID is: [PUT THE ID HERE]
Guide me on how to add them to the allowlist correctly.
```

**How the person finds their ID:** They send `/start` to @userinfobot on Telegram.

---

*Last updated: Feb/2026*
