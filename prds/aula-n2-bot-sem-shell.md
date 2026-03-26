# PRD — Lesson N-2: Bot without shell access — identify and fix

**Module:** N — Diagnostics & Troubleshooting  
**Lesson:** N-2  
**Estimated duration:** 15 minutes  
**Level:** Intermediate / Debug  
**Instructor:** Bruno  
**Format:** Screencast with narration + live slides/terminal

---

## Lesson Objective

By the end of this lesson, the student will be able to:
1. Identify when the agent has lost shell access
2. Diagnose the exact cause of the problem
3. Apply the correct fix for each case
4. Verify that access has been restored

---

## Recording Script

### [00:00 – 01:30] — OPENING

> **Bruno (camera or voice-over):**

"Hey everyone! Bruno here. In this lesson we're going to solve one of the most common problems I see happening with people who are starting to use OpenClaw: the agent stops executing commands.

You ask it to install a tool. It says 'I can't do that.' You ask it to create a file. It says 'I don't have permission.' It seems like the agent has turned into just a chatbot — it responds with text but doesn't do anything.

This has a cause. And it has a solution. I'll show you the 5 most common causes — including the new one from version 3.2 that's catching a lot of people. In the next 15 minutes you'll learn to identify and fix each one.

Let's go!"

---

### [01:30 – 03:00] — SYMPTOMS OF THE PROBLEM

> **Bruno (terminal screen + agent open):**

"First, how do you know you have this problem?

The classic symptoms are these:"

**[Show on screen — list of symptoms:]**

```
Symptom 1: You ask the agent to run a command and it says:
  → "I can't execute commands on your system"
  → "I don't have shell access"
  → "This tool is not available"

Symptom 2: The agent responds to text perfectly, but any
  task involving the operating system fails.

Symptom 3: You receive error messages like:
  → "Permission denied"
  → "exec: not in allowlist"
  → "Sandbox restriction"
```

> "If you're seeing any of these, the problem is shell access permissions. Now let's understand why this happens — there are 4 main causes."

---

### [03:00 – 08:30] — THE 5 CAUSES

#### ⚠️ Cause 0 (NEW, MOST COMMON): `tools.profile = messaging` [03:00 – 03:45]

> **Bruno:**

"But before anything else — since OpenClaw version 3.2, the number one cause of 'bot does nothing' has changed. And a lot of people are falling into this now.

When you configure the agent with `tools.profile = messaging`, OpenClaw puts the agent in messaging mode — optimized for responding to text on Telegram or WhatsApp, but without shell access, no exec, no system operations at all.

This is exactly what happens when you copy an example Telegram bot config and don't notice that parameter.

The symptom is clear: the agent responds fluently, seems smart, but when you ask for anything involving the operating system, it says 'I can't do it.'

The fix is simple: remove the `tools.profile` or change it to a profile that includes exec, like `full` or `default`."

**[Show config with the problem:]**
```json
{
  "agents": {
    "main": {
      "tools": {
        "profile": "messaging"
      }
    }
  }
}
```

**[Show the fix:]**
```json
{
  "agents": {
    "main": {
      "tools": {
        "profile": "default"
      }
    }
  }
}
```

> "Or simply remove the `tools.profile` key — the default already includes exec."

#### Cause 1: `exec` tool not in allowlist [03:45 – 04:45]

> **Bruno:**

"The most common cause. OpenClaw controls which tools each agent can use. If the `exec` tool isn't in the list of allowed tools, the agent simply can't run commands.

This happens when someone configures the agent in a restricted way — perhaps for a support agent that shouldn't have system access. That makes sense in that context, but not if you want an agent that executes tasks.

The fix will be in the allowlist configuration. I'll show you how shortly."

#### Cause 2: Sandbox active without correct permissions [04:00 – 05:00]

> **Bruno:**

"The second cause is the sandbox. OpenClaw has a sandbox system that isolates command execution. Depending on how it's configured, the agent may be running in an isolated environment that doesn't let commands through.

The sandbox has three modes:
- `off` — no sandbox, full system access
- `non-main` — sandbox active only for sub-agents
- `all` — sandbox active for all agents, including the main one

If you set `all` without correctly configuring the sandbox permissions, the main agent also gets stuck.

The difference between these modes matters. I'll show you in the configuration."

#### Cause 3: Security mode "deny" [05:00 – 06:00]

> **Bruno:**

"The third cause is the security mode. OpenClaw has a parameter called `security` that controls how the agent handles command execution. When this parameter is set to `deny`, the agent blocks any attempt to execute commands on the system.

This mode exists for a reason: security. In some cases you want an agent that only reads, not one that executes. But if you configured this by mistake on the wrong agent, it will get stuck.

The solution is simple: change the security mode to `allowlist` or `full`."

#### Cause 4: BotFather privacy mode — bot doesn't respond in group [06:00 – 07:00]

> **Bruno:**

"This cause is specific to those who use the agent in Telegram groups. You add the bot to the group, send a message — nothing. The bot responds in DM normally, but in the group, total silence.

The culprit is the **Group Privacy Mode** from BotFather. By default, when you create a bot in BotFather, it comes with privacy mode ACTIVE. This means the bot only receives messages that start with `/command` — normal messages in the group are invisible to it.

How to fix:"

**[Show step by step:]**
```
1. Open @BotFather on Telegram
2. Send: /mybots
3. Select your bot
4. Click "Bot Settings"
5. Click "Group Privacy"
6. Click "Turn off"
7. Confirmation: "Privacy mode is disabled"

IMPORTANT: remove and re-add the bot to the group
for the new permissions to take effect.
```

> "After disabling privacy mode and re-adding the bot, it starts receiving all messages from the group. Simple as that."

#### Cause 5: Shell path not found [07:00 – 08:00]

> **Bruno:**

"The fifth cause is less common but happens especially on VPS — OpenClaw can't find the system shell.

In standard Linux environments, the shell is at `/bin/bash` or `/bin/sh`. But in some minimal distributions, Docker containers, or poorly configured VPS, the path may be different. Or the user running OpenClaw doesn't have permission to use the shell.

The fix is to configure the correct shell path in the agent configuration."

---

### [08:00 – 08:30] — DIAGNOSTIC FLOWCHART

> **Bruno:**

"Before diving into the step-by-step diagnosis, let me show you the mind map. When the bot does nothing, follow this order:"

**[Show flowchart on screen:]**

```
Bot doesn't execute commands?
         │
         ▼
┌─────────────────────────────────┐
│  tools.profile = messaging?    │ ──YES──▶ Remove or change to "default"
└─────────────────────────────────┘
         │ NO
         ▼
┌─────────────────────────────────┐
│  Bot in group and not responding? │ ──YES──▶ BotFather → disable Group Privacy
└─────────────────────────────────┘
         │ NO
         ▼
┌─────────────────────────────────┐
│  sandbox = "all" ?             │ ──YES──▶ Change to "off" or "non-main"
└─────────────────────────────────┘
         │ NO
         ▼
┌─────────────────────────────────┐
│  security = "deny" ?           │ ──YES──▶ Change to "allowlist"
└─────────────────────────────────┘
         │ NO
         ▼
┌─────────────────────────────────┐
│  "exec" in allowlist?          │ ──NO───▶ Add "exec" to allowlist
└─────────────────────────────────┘
         │ YES
         ▼
    openclaw gateway restart
         │
         ▼
    echo "SHELL_TEST_OK"
         │
    ┌────┴────┐
   OK?      Failed?
    │           │
  Resolved   Check gateway
              logs
```

> "Test in this order. Cause 0 — the tools.profile — resolves 60% of cases that appear in the group."

---

### [08:30 – 09:00] — QUICK TEST

> **Bruno (showing terminal):**

"Before diving into the diagnosis, there's a quick test you can do. Ask your agent to execute this:"

**[Show on terminal/chat:]**
```
execute: echo test
```

> "If the agent responds with 'test', it has shell access. If it errors, you have one of the problems we just saw. Simple as that."

---

### [08:00 – 10:30] — HOW TO DIAGNOSE

> **Bruno (terminal screen):**

"Now let's go to the diagnosis. Step by step:"

#### Step 1: Check the gateway logs

```bash
openclaw gateway logs --tail 50
```

> "Look for messages like `exec blocked`, `not in allowlist`, `sandbox restriction` or `permission denied`. The log will tell you exactly what's blocking."

#### Step 2: Check the agent configuration

```bash
cat ~/.openclaw/config.json
```

or, if it's in a specific workspace:

```bash
cat openclaw.json
```

> "You need to check three things in this file: the tools `allowlist`, the `sandbox` parameter, and the `security` mode. I'll show you how each should be configured."

#### Step 3: Use the interactive diagnostic

> "You can also paste the diagnostic prompt we provided with this lesson — it will guide the agent to check its own configuration and identify the problem automatically."

---

### [10:30 – 13:00] — HOW TO FIX EACH CAUSE

> **Bruno (code editor open with config):**

"Now the good part — the fixes. I'll show you each one."

#### Fix 1: Add `exec` to the allowlist

```json
{
  "agents": {
    "main": {
      "tools": {
        "allowlist": ["exec", "read", "write", "edit", "web_search", "web_fetch"]
      }
    }
  }
}
```

> "Simple. Add `exec` to the list. If the `tools` key didn't exist, create it. Save the file and restart the gateway."

#### Fix 2: Adjust sandbox configuration

```json
{
  "agents": {
    "main": {
      "sandbox": "off"
    }
  }
}
```

> "For the main agent, use `sandbox: off`. If you want sandboxing in sub-agents but not the main one, use `non-main`. Only use `all` if you understand the implications well and have correctly configured the sandbox permissions."

**Explanation table:**

| Value       | Behavior |
|-------------|----------|
| `off`       | No sandbox — full system access |
| `non-main`  | Sandbox only on sub-agents |
| `all`       | Sandbox on all — **includes main agent** |

#### Fix 3: Adjust security mode

```json
{
  "agents": {
    "main": {
      "security": "allowlist"
    }
  }
}
```

> "Change from `deny` to `allowlist`. With `allowlist`, only commands and tools in your allowed list will work — it's secure and functional. `full` disables restrictions but only use if you know what you're doing."

#### Fix 4: Configure shell path

```json
{
  "agents": {
    "main": {
      "shell": "/bin/bash"
    }
  }
}
```

> "If the shell isn't being found, specify the full path. On Ubuntu/Debian it's `/bin/bash`, on some Alpine/containers it may be `/bin/sh`. Run `which bash` or `which sh` in the terminal to confirm the correct path."

---

### [13:00 – 14:30] — POST-FIX VERIFICATION CHECKLIST

> **Bruno:**

"After applying any fix, follow this checklist:"

**[Show on screen:]**

```
POST-FIX CHECKLIST

□ 1. Restart the gateway:
     openclaw gateway restart

□ 2. Check gateway status:
     openclaw gateway status

□ 3. Test basic access — ask the agent:
     execute: echo "shell working"

□ 4. Test file creation:
     execute: touch /tmp/test-openclaw && echo "OK"

□ 5. Check logs for residual errors:
     openclaw gateway logs --tail 20

□ 6. Test a simple real task:
     "list the files in the current directory"
```

---

### [14:30 – 15:00] — CLOSING

> **Bruno:**

"Done! Now you know how to identify and fix the five types of problems that remove shell access from your agent.

To recap:
- Cause 0 (most common!): `tools.profile = messaging` → remove or change to `default`
- Cause 1: `exec` not in allowlist → add to the tools list
- Cause 2: Misconfigured sandbox → adjust the sandbox mode
- Cause 3: Security mode `deny` → change to `allowlist`
- Cause 4: Bot in group not responding → disable Group Privacy in BotFather
- Cause 5: Shell not found → configure the correct path

Use the diagnostic prompt we made available to do this process interactively with the agent itself.

Any questions, drop them in the group. See you next time!"

---

## Production Notes

- **Show live terminal** when explaining logs and config
- **Code editor** open when showing JSON fixes
- **Highlight** relevant lines in the config with zoom or highlight
- **Demonstrate** the quick test (`echo test`) live to show the agent working after the fix
- **Add captions/subtitles** on the technical parts

## Required Assets

- [ ] Example `openclaw.json` file (with deliberate error)
- [ ] Fixed version of `openclaw.json`
- [ ] Screenshot of logs with error message
- [ ] GIF/video of the `echo test` working

---

*PRD generated on 2026-03-04 · OpenClaw Course · Pixel Educação*
