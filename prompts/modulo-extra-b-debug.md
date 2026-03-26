# Prompt — Extra Lesson B: Debugging on the VPS with Claude Code

> Paste this prompt in your agent chat **inside the VPS** (via `claude` in the terminal) after watching Extra Lesson B.

---

I just watched the lesson on VPS debugging. Now I want you to help me ensure my environment is healthy and teach me how to solve problems when they arise.

**What I need to do:**

## 1. Full Health Check

Run a complete system diagnostic:
1. Gateway status (`openclaw gateway status`)
2. Available disk space
3. RAM memory usage
4. Log size
5. My workspace size
6. Active connections (Telegram, etc.)
7. Last time the gateway restarted

Show me everything clearly and tell me:
- ✅ What's OK
- ⚠️ What needs attention
- 🔴 What needs to be fixed now

## 2. Clean up what's necessary

If there's something to clean up (old logs, temporary files, messy workspace):
1. Show me WHAT will be cleaned and HOW MUCH space will be freed
2. Ask for my confirmation
3. Perform the cleanup
4. Show me the before/after

**Cleanup rules:**
- ❌ NEVER delete workspace files without my explicit approval
- ✅ Can compress/archive `memory/YYYY-MM-DD.md` files older than 30 days
- ✅ Can clean logs older than 7 days
- ✅ Can clean `/tmp`

## 3. Review my workspace

Go to my main workspace and tell me:
- How many files do I have?
- What is the total size?
- Are there any large or duplicate files?
- Are there any forgotten test files?
- Is the structure organized?

If you find anything unusual, suggest what to do.

## 4. Teach useful commands

Teach me 5 commands I'll always use:
1. View gateway logs in real time
2. Restart the gateway
3. View disk space
4. View running processes
5. Navigate to my workspace quickly

For each one, explain:
- What the command does
- When to use it
- How to interpret the output

## 5. Simulate 3 common problems

Explain what to do in each scenario:

**Scenario A:** Agent stopped responding on Telegram
- Step 1: ...
- Step 2: ...
- How to know if resolved: ...

**Scenario B:** "context window exceeded" error
- What it means: ...
- How to resolve: ...
- How to prevent: ...

**Scenario C:** VPS ran out of disk space
- How to identify: ...
- What to clean first: ...
- How to avoid in the future: ...

## 6. Configure preventive alerts (if possible)

Help me set up a system that warns me BEFORE problems occur:
- If disk passes 80% full
- If logs exceed 1GB
- If gateway goes down
- If session context exceeds 80% of the limit

If it's not possible natively through OpenClaw, suggest alternatives (cron job, simple script).

---

**At the end, give me a summary like:**

```
✅ System healthy
📊 Disk: XX% used (XGB free)
💾 Memory: XX% used
📝 Logs: XMB (last 7 days)
📁 Workspace: XMB
🔗 Telegram: connected
⏱️ Uptime: X days

Next recommended maintenance: [date]
```

Let's start with the health check. Show me everything.
