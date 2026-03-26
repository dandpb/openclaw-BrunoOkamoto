# PRD: Debugging on VPS with Claude Code

> Script for recording Extra Lesson B
> Audience: complete beginners — may have never accessed a server before

---

## Lesson Objective

Teach how to access the VPS and use Claude Code (OpenClaw CLI) directly in the terminal to:
1. **Debug problems** when the agent freezes or throws errors
2. **Fix folders and files** in the workspace
3. **Use `openclaw doctor`** for automatic diagnosis
4. **Use `openclaw doctor fix`** for automatic correction

**Premise:** The student may not know how to use a terminal. They will learn by doing.

---

## Estimated time: 18-22 minutes

---

## Lesson Structure

### Block 1: Why learn to debug? (2 min)

**What to show:**
- Agent froze and not responding? That's normal — you'll know how to fix it.
- Strange error appeared? You'll know where to look.
- Autonomy: not depending on support for simple problems.

**Key phrase:**
> "You don't need to be technical. But you need to know how to open the hood when the red light comes on."

**Real scenarios the student will face:**
- Agent stopped responding in Telegram
- Error "token limit exceeded"
- **Agent became VERY slow (responses take 30s+)**
- Messy workspace (too many files)
- Gateway doesn't start after a restart
- Cron doesn't run on schedule

---

### Block 2: How to access the VPS (4 min)

**Option 1: Local terminal (Mac/Linux/Windows Terminal)**

1. **Get the VPS IP and password** (from the Hostinger panel)

2. **Connect via SSH:**
   ```bash
   ssh root@YOUR_IP_HERE
   ```
   Type the password when prompted.

3. **You're in!** The prompt changes:
   ```
   root@vps-12345:~#
   ```

**Option 2: Hostinger panel terminal (easier for beginners)**

1. Go to hPanel → VPS → click the "Terminal" button (top right)
2. Terminal opens in the browser — no setup required
3. Already connected as root

**Show both methods and let the student choose.**

---

### Block 3: Basic survival commands (3 min)

**Before debugging, teach the minimum:**

1. **See where you are:**
   ```bash
   pwd
   ```
   Shows the current path (like `/root`)

2. **List files:**
   ```bash
   ls -la
   ```
   Shows everything, including hidden folders (start with `.`)

3. **Go to the agent workspace:**
   ```bash
   cd ~/.openclaw/workspace-YOUR-AGENT-NAME
   ```
   Example:
   ```bash
   cd ~/.openclaw/workspace-amora-cos
   ```

4. **View file contents:**
   ```bash
   cat AGENTS.md
   ```
   Or for large files:
   ```bash
   less AGENTS.md
   ```
   (press `q` to exit)

5. **View gateway logs in real time:**
   ```bash
   openclaw gateway logs --follow
   ```
   (press Ctrl+C to exit)

**Explain the concept of "path":**
> "Think of the server as a folder tree. You start at the root (`/`) and go down. `~` is a shortcut for the current user's folder (`/root`)."

---

### Block 4: Using Claude Code in the terminal (5 min)

**What Claude Code is:**
> "It's Claude running INSIDE the VPS terminal. You ask, it answers and can execute commands for you."

**How to invoke:**
```bash
claude
```

Opens an interactive session. Now you can chat:

**Example 1 — Diagnose a problem:**
```
You: My agent stopped responding in Telegram. What could it be?

Claude: I'll check. First, gateway status...
[executes: openclaw gateway status]

Claude: Gateway is stopped. Let me check the latest logs...
[executes: openclaw gateway logs --tail 50]

Claude: Token limit error. The problem is too much context.
Want me to clear the old logs and restart?
```

**Example 2 — Clean up workspace:**
```
You: My workspace is full of test files. How do I clean it?

Claude: Let me list what's here...
[executes: ls -lah]

Claude: There are several .txt and .json test files. I can move them to an
/archive folder. Confirm?

You: Confirm.

Claude: [creates folder, moves files, shows result]
Done. Workspace cleaned.
```

**Example 3 — Check disk usage:**
```
You: How much space do I have on the VPS?

Claude: [executes: df -h]
You have 50GB total, 12GB used, 38GB free.
```

**Exit Claude Code:**
- Type `exit` or press Ctrl+D

---

### Block 5: openclaw doctor — Automatic diagnosis (3 min)

**What it does:**
Runs a battery of checks and shows what's wrong.

**Run:**
```bash
openclaw doctor
```

**What it checks:**
- ✅ Gateway running?
- ✅ Node.js at the right version?
- ✅ Disk has space?
- ✅ RAM available?
- ✅ Config valid? (`openclaw.json`)
- ✅ Provider API key works?
- ✅ Channels connected? (Telegram, etc.)
- ⚠️ Logs too large?
- ⚠️ Workspaces with too many files?

**Example output:**
```
✅ Gateway: running
✅ Node.js: v22.22.0
✅ Disk: 38GB free (76%)
✅ Memory: 2.1GB free (52%)
✅ Config: valid
✅ Provider: Anthropic API OK
✅ Telegram: connected
⚠️ Logs: 450MB (consider clearing)
⚠️ Workspace "amora-cos": 2.3GB (review large files)
```

**Explain each line:**
> "Green = everything OK. Yellow = pay attention, could become a problem. Red = needs fixing now."

---

### Block 6: openclaw doctor fix — Automatic correction (2 min)

**What it does:**
Tries to fix common problems automatically.

**Run:**
```bash
openclaw doctor fix
```

**What it can fix on its own:**
- Restart a frozen gateway
- Clear old logs (keeps last 7 days)
- Fix file permissions
- Recreate missing folders
- Update broken dependencies

**What it does NOT do (requires confirmation):**
- Delete workspace files
- Change critical config
- Perform a major version upgrade

**Flow:**
```bash
openclaw doctor fix
```

Output:
```
🔍 Scanning for issues...
⚠️ Found 3 fixable issues:

1. Gateway not responding → restart
2. Logs > 500MB → rotate
3. /tmp full → cleanup

Apply fixes? [y/N]
```

Type `y` and Enter.

```
✅ Gateway restarted
✅ Logs rotated (freed 380MB)
✅ /tmp cleaned (freed 1.2GB)

All checks passed. System healthy.
```

---

### Block 7: Real scenarios + solutions (5 min)

**Show 4 common problems and how to resolve them:**

#### Scenario 1: "Agent not responding in Telegram"

**Step by step:**
1. SSH into the VPS
2. `openclaw gateway status` → if "stopped", run `openclaw gateway start`
3. If it remains stopped, check logs: `openclaw gateway logs --tail 50`
4. If API key error, reconfigure: `openclaw provider update anthropic`
5. If token error, run `openclaw doctor fix`

#### Scenario 2: "Context too large error"

**Symptom:** Error message "context window exceeded"

**Solution:**
1. SSH into the VPS
2. Go to workspace: `cd ~/.openclaw/workspace-YOUR-AGENT`
3. Open Claude Code: `claude`
4. Ask: "My context is too large. Can you compact old memory/YYYY-MM-DD.md files?"
5. Claude will move them to a compacted file and clean up

#### Scenario 3: "Agent became VERY slow (responses take 30s+)"

**Symptom:** Agent takes long to respond, sometimes times out

**Common causes:**

1. **Session context exceeded 100k tokens**
   - User never ran `/new` or `/compact`
   - Session accumulates months of history

   **Solution:**
   ```bash
   # Check session sizes
   cd ~/.openclaw
   du -sh sessions/*.json | sort -h | tail -10
   ```
   If there's a session.json over 5MB:
   - Ask the user to run `/compact` or `/new`
   - Or move to backup: `mv sessions/SESSION.json sessions/backup/`

2. **Corrupted or giant session.json**
   - File can reach 50MB+ if never compacted

   **Solution:**
   ```bash
   # Find the largest session.json
   ls -lh ~/.openclaw/sessions/ | sort -k5 -h | tail -5
   ```
   If you find a file > 10MB, you can archive it:
   ```bash
   mkdir -p ~/.openclaw/sessions/backup
   mv ~/.openclaw/sessions/GIANT-FILE.json ~/.openclaw/sessions/backup/
   ```

3. **Many agents running in parallel**
   - Each agent consumes memory and CPU
   - A small VPS can't handle 5+ simultaneous agents

   **Solution:**
   ```bash
   # Check how many OpenClaw processes are running
   ps aux | grep openclaw | wc -l
   ```
   If there are more than 3-4 on a small VPS (4GB RAM), consider:
   - Stopping unused agents
   - Upgrading the VPS
   - Using `sessionTarget: isolated` with `cleanup: delete` in crons

**Explain in the video:**
> "Context is like the agent's short-term memory. If you never clear it, it's like trying to remember EVERYTHING that happened in the last 6 months — the brain freezes. Use `/compact` every week or `/new` when you need to start fresh."

#### Scenario 4: "VPS out of space"

**Symptom:** "No space left on device"

**Solution:**
1. Run `openclaw doctor` → will show the problem
2. Run `openclaw doctor fix` → clears logs and /tmp
3. If still full, use Claude Code:
   ```
   You: I need to free up space. What's taking up the most?
   Claude: [executes: du -sh ~/.openclaw/* | sort -h]
   Shows the largest workspaces...
   ```
4. Decide what to archive or delete

---

## Lesson Checkpoint

By the end, the student should know:
- [ ] How to connect to the VPS via SSH (local terminal or Hostinger panel)
- [ ] Basic navigation commands (pwd, ls, cd, cat)
- [ ] How to invoke Claude Code in the terminal (`claude`)
- [ ] How to use `openclaw doctor` for diagnosis
- [ ] How to use `openclaw doctor fix` for automatic correction
- [ ] How to solve 4 common problems on their own (not responding, context, slowness, no space)

---

## Security Alerts

🔴 **NEVER** delete files without knowing what they are
🔴 **ALWAYS** back up before major changes
🔴 **BE CAREFUL** with `rm -rf` — it can delete everything

**Golden rule:**
> "If you don't know what a command does, ask Claude Code before running it."

---

## Prompt that goes in the PDF

Will be in the file `prompts/modulo-extra-b-debug.md`.

---

## Common Troubleshooting

### "Permission denied" when trying something
You probably need `sudo`. But as root, this shouldn't happen.

### "Command not found: claude"
```bash
# Reinstall OpenClaw CLI
npm install -g @anthropic-ai/claude-code
```

### "SSH connection refused"
- Check if the IP is correct
- Check if the VPS is on (Hostinger panel)
- Check if port 22 is open (firewall)

---

*This lesson grants autonomy. Before it, the student depends on support. Afterwards, they can solve 80% of problems on their own.*
