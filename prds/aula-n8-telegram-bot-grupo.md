# PRD — Lesson N-8: Telegram: Bot Not Responding in Group

> **Level:** Intermediate / Troubleshooting
> **Estimated duration:** 10 minutes
> **Prerequisite:** OpenClaw configured, Telegram bot working in DM

---

## 🎯 Lesson Objective

By the end of this lesson, the student will be able to:

1. Understand why the bot works in DM but not in the group
2. Fix the privacy mode in BotFather
3. Configure `groupPolicy` in OpenClaw
4. Find the chat ID of any group
5. Understand the difference between `dmPolicy` and `groupPolicy`
6. Systematically diagnose group issues

---

## 🎬 OPENING (0:00 – 0:45)

**[Bruno on screen, direct tone]**

> "Hey! Lesson N-8 — one of the most common questions in the course: 'I added my bot to the group, but it doesn't respond'. In 10 minutes you'll understand why this happens and how to fix it."

> "Spoiler: it's almost always 3 causes. I'll show you all 3 and the diagnosis to find out which one is yours."

---

## 📚 SECTION 1: Why the Bot Doesn't Talk in the Group (0:45 – 3:00)

**[Screen: slide with 3 causes]**

> "The bot works in DM but not in the group? There are 3 possible causes, and they are independent — any one of them is enough to make the bot go silent:"

**Cause 1: Privacy Mode ENABLED in BotFather (most common)**

> "By default, Telegram creates bots with 'privacy mode' ENABLED. This means the bot DOES NOT RECEIVE group messages — it only receives messages that start with `/command` or that directly mention the bot with @username."

> "It's a privacy measure from Telegram. But for an AI agent that should participate in conversations, this is a problem."

**Cause 2: `groupPolicy` not configured in OpenClaw**

> "Even if the bot receives the messages, OpenClaw has its own security layer: by default, it doesn't process group messages unless you explicitly configure it."

**Cause 3: Group chat ID is not in the allowlist**

> "If you used `groupPolicy = allowlist`, you need to add the specific group's chat ID. Without the correct ID, OpenClaw ignores the messages even with everything configured."

---

## 🔧 FIX 1: BotFather — Disable Privacy Mode (3:00 – 5:00)

**[Screen: Telegram open in BotFather]**

> "Let's fix Cause 1. Open Telegram and talk to **@BotFather**."

```
1. Open the chat with @BotFather
2. Send: /setprivacy
3. BotFather will list your bots — select yours
4. Choose: Disable
5. Confirmation: "Success! Privacy mode is disabled."
```

> "Now the bot will receive ALL group messages, not just commands. This is necessary for the agent to participate in conversations normally."

> "**Attention:** After changing the privacy mode, you need to **remove the bot from the group and add it back**. Telegram only applies the new configuration when the bot enters the group. If the bot was already in the group, the change won't work until you do this."

---

## 🔧 FIX 2: Configure groupPolicy in OpenClaw (5:00 – 7:30)

**[Screen: Terminal]**

> "Now let's fix Causes 2 and 3 together. In the VPS terminal:"

```bash
# Configure policy for groups
# allowlist = only responds in specific groups (recommended)
openclaw config set channels.telegram.groupPolicy allowlist

# Add the group chat ID to the allowlist
# (See the section below to find the chat ID)
openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXXXXX]"
```

> "If you have more than one group:"
```bash
openclaw config set channels.telegram.groupAllowlist "[-100111111111, -100222222222]"
```

> "To allow any group without allowlist (less secure):"
```bash
openclaw config set channels.telegram.groupPolicy open
```

> "I recommend `allowlist` — you control exactly which groups the agent acts in."

---

## 🔍 How to Find the Group Chat ID (7:30 – 8:30)

**[Screen: Terminal + Telegram]**

> "To find your group's chat ID, follow these steps:"

```bash
# 1. Add the bot to the group (if you haven't already)
# 2. Send any message in the group
# 3. Check OpenClaw logs
openclaw gateway logs | grep "chat_id"
# or
openclaw gateway logs | tail -50
```

> "In the logs you'll see something like:"
```
Received message from chat_id: -1001234567890, user: John
```

> "Group chat IDs start with `-100` followed by numbers. Note this ID — it's the one that goes in the allowlist."

> "Alternative tip: add the bot @userinfobot to the group, send `/start`, it also returns the group ID."

---

## 📘 SECTION 5: dmPolicy vs groupPolicy — The Difference (8:30 – 9:30)

**[Screen: comparison]**

> "This is a common source of confusion. Let me clarify it once and for all:"

| | dmPolicy | groupPolicy |
|---|---|---|
| **Controls** | Direct messages (DM/private) | Messages in groups |
| **Default** | allowlist | not configured |
| **Scope** | 1-on-1 with you | Multiple users in the same chat |
| **Risk** | Someone commanding your agent | Agent active in unauthorized groups |

> "They are two independent gatekeepers. `dmPolicy` guards your private conversation with the bot. `groupPolicy` guards when the bot is in groups."

> "You can have: open DM (just you) + groups in the allowlist. Or DM only for you + no active groups. The combination depends on your use case."

---

## 🗺️ SECTION 6: Step-by-Step Diagnosis (Flowchart)

```
Bot added to group but not responding
│
├── [1] Privacy mode is ACTIVE?
│   → Test: send /start or /help in the group
│   → If the bot RESPONDS to commands but ignores regular messages → Privacy mode ACTIVE
│   → FIX: BotFather → /setprivacy → Disable → Remove and re-add bot to group
│
├── [2] groupPolicy configured?
│   → Test: openclaw config get channels.telegram.groupPolicy
│   → If it returns empty or "none" → not configured
│   → FIX: openclaw config set channels.telegram.groupPolicy allowlist
│
├── [3] Chat ID in allowlist?
│   → Test: openclaw config get channels.telegram.groupAllowlist
│   → Check if the group ID is in the list
│   → FIX: openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXX]"
│
└── [4] Still not working?
    → openclaw gateway logs | tail -100
    → Look for error messages related to the chat
    → openclaw gateway restart
```

---

## 💡 SECTION 7: Topics (Forum Mode) — Reference

> "If your group uses **topics** (groups with forum mode enabled), there's an additional configuration. The bot needs to be an admin of the group to have access to all topics, and you may need to configure which topics the agent monitors."

> "For detailed topic configuration, refer to **Extra Lesson C** — it covers the full forum mode with practical examples."

---

## 📋 Full Configuration (Quick Reference)

```bash
# 1. BotFather: /setprivacy → Disable (in Telegram)
# 2. Remove and re-add the bot to the group

# 3. Configure groupPolicy
openclaw config set channels.telegram.groupPolicy allowlist

# 4. Add group chat ID
openclaw config set channels.telegram.groupAllowlist "[-100XXXXXXXXXX]"

# 5. Verify configuration
openclaw config get channels.telegram.groupPolicy
openclaw config get channels.telegram.groupAllowlist

# 6. Restart gateway
openclaw gateway restart

# 7. Check logs
openclaw gateway logs | tail -30
```

---

## ✅ Student Final Checklist

- [ ] Privacy mode disabled in BotFather (`/setprivacy → Disable`)
- [ ] Bot removed and re-added to the group after privacy mode change
- [ ] Group chat ID found (starts with `-100...`)
- [ ] `groupPolicy = allowlist` configured
- [ ] Chat ID added to `groupAllowlist`
- [ ] Gateway restarted
- [ ] Test: message sent in group → bot responded ✅

---

## 🚨 Common Errors

| Symptom | Cause | Solution |
|---------|-------|---------|
| Bot responds `/start` but ignores messages | Privacy mode ENABLED | BotFather → /setprivacy → Disable |
| Bot doesn't respond at all in group | groupPolicy not configured | `openclaw config set channels.telegram.groupPolicy allowlist` |
| groupPolicy configured but still not responding | Chat ID not in allowlist | Add the correct ID to groupAllowlist |
| Bot works in DM, silent in group | Any of the 3 causes | Follow the diagnosis flowchart |
| After privacy mode change, still silent | Bot still in group with old config | Remove bot from group and add back |
| Invalid chat ID | Copied wrong ID | Check logs: `openclaw gateway logs | grep chat_id` |

---

## ❓ Frequently Asked Questions

**1. Do I need to remove the bot and add it back every time I change the privacy mode?**

> Yes. Telegram processes the privacy mode configuration at the moment the bot enters the group. Retroactive changes don't apply — it needs to leave and rejoin.

**2. Can I have groupPolicy = open?**

> Yes, but I don't recommend it for general use. With `open`, the agent responds in any group it's been added to — anyone who adds the bot to a group can use it. Prefer `allowlist`.

**3. Can the bot be a group admin?**

> Yes, and it's required for some features (deleting messages, accessing all topics in forum mode). For basic response usage, being a regular member is sufficient.

**4. Does it work with large groups (hundreds of people)?**

> Technically yes. But think about the cost: every message in the group goes to the agent. With 200 people in the group and many messages per day, the token cost can be high. Configure `groupPolicy` well and consider using `groupMentionOnly` (the bot only responds when @mentioned) for large groups.

**5. Do topics (forum mode) require extra configuration?**

> Yes. Refer to Extra Lesson C for full forum mode configuration with topics.
