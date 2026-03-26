# Student Prompt — Lesson N-2: Bot Without Shell Access

**How to use:** Paste the prompt below directly into the chat with your OpenClaw agent.
The agent will diagnose its own configuration and guide you to the solution.

---

## PROMPT TO PASTE IN THE CHAT

```
I'm going to do a diagnosis of your shell access. Please execute each step in order.

## STEP 0 — Check tools.profile (ALWAYS the first check)

Before anything else, verify that the tools profile is correct:

1. Run: `openclaw config get tools.profile`
2. If the result is NOT "full", run: `openclaw config set tools.profile full`
3. Restart the gateway: `openclaw gateway restart`
4. Test: `echo "TOOLS_PROFILE_CHECK_OK"`

> This is the most common problem: the agent doesn't execute anything because tools.profile is set to "minimal" (default after installation). Without `tools.profile full`, the agent only responds to messages.

If the test above worked → problem solved! 🎉
If it still fails → continue to Step 1.

---

## STEP 1 — Basic access test

Try running this command and tell me exactly what happened:
execute: echo "SHELL_TEST_OK"

If it worked → confirm "OK" and go to Step 3.
If it failed or you received an error → describe the error and continue to Step 2.

---

## STEP 2 — Configuration diagnosis

Now check your current configuration:

1. Read the main configuration file:
   - Try: `cat ~/.openclaw/config.json`
   - Or: `cat openclaw.json` (if in a workspace)

2. Show me the full contents of the file. I'm specifically looking for:
   - The "tools" or "allowlist" key (to verify if "exec" is in the list)
   - The "sandbox" key (possible values: "off", "non-main", "all")
   - The "security" key (possible values: "deny", "allowlist", "full")
   - The "shell" key (shell path, e.g.: "/bin/bash")

3. Also check the gateway logs:
   `openclaw gateway logs --tail 30`

---

## STEP 3 — Identify the cause

Based on what you found, tell me which of these situations applies:

**A) Cause 1 — exec is not in the allowlist**
Symptom: config has "allowlist" but "exec" is not in the list
→ Solution: add "exec" to the tools allowlist

**B) Cause 2 — Sandbox blocking**
Symptom: config has "sandbox": "all" or sandbox configured restrictively
→ Solution: change to "sandbox": "off" (main agent) or "non-main"

**C) Cause 3 — Security mode "deny"**
Symptom: config has "security": "deny"
→ Solution: change to "security": "allowlist"

**D) Cause 4 — Shell not found**
Symptom: path error or shell not found in logs
→ Solution: configure "shell": "/bin/bash" (or the correct path)

**E) Found nothing suspicious in config**
→ Describe the exact error you see and the gateway logs

---

## STEP 4 — Apply the fix

Based on the identified cause, edit the configuration file with the correct fix.

**For Cause 1 (exec not in allowlist):**
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

**For Cause 2 (sandbox blocking):**
```json
{
  "agents": {
    "main": {
      "sandbox": "off"
    }
  }
}
```

**For Cause 3 (security deny):**
```json
{
  "agents": {
    "main": {
      "security": "allowlist"
    }
  }
}
```

**For Cause 4 (shell not found):**
```json
{
  "agents": {
    "main": {
      "shell": "/bin/bash"
    }
  }
}
```

After editing, run:
`openclaw gateway restart`

---

## STEP 5 — Final verification

After restarting, verify everything is working:

1. `echo "FINAL_VERIFICATION_OK"` → should return the text
2. `touch /tmp/teste-openclaw && echo "file created"` → should work
3. `openclaw gateway status` → should show status "running"

If everything passed: **problem solved!** 🎉
If it still fails: copy the exact error and the gateway logs for analysis.
```

---

## NOTES FOR THE STUDENT

### When to use this prompt
- Your agent responds to questions but doesn't execute commands
- You see errors like "exec not available", "permission denied", or "sandbox restriction"
- The agent says "I cannot execute tasks on the system"

### What the prompt does
0. **Checks tools.profile** — most frequent cause #1, resolves 70% of cases
1. Tests shell access with a simple command
2. Reads your current configuration
3. Identifies which of the 4 causes applies to your case
4. Guides you through the specific fix
5. Verifies the fix worked

### Most common cause (check this first!)
In most cases, the problem is simply that `tools.profile` is not set to `full`. Run this in the server terminal:
```bash
openclaw config set tools.profile full
openclaw gateway restart
```

### Important tip
If the agent can't even read the configuration file, you'll need to do it **manually in the terminal** (not through the agent). In that case, open a terminal on the server where OpenClaw is running and edit `config.json` directly.

---

*Prompt for Lesson N-2 · OpenClaw Course · Pixel Educação*
