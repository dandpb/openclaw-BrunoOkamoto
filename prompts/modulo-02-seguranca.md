# Prompt — Module 2: Security

> Paste this prompt in your OpenClaw chat after watching Module 2.
> Also attach the file: `prds/security-hardening.md`

---

I just finished watching Module 2 of the course on security. Read the security hardening PRD I'm attaching and guide me step by step.

**Important:**
- Before EACH action, explain WHAT you're going to do and WHY
- Ask for my confirmation before executing any changes on the server
- If something is already configured, let me know and skip to the next step
- At the end, run a security audit and show me the result

**What I expect you to cover:**
1. Telegram allowlist (dmPolicy) — so nobody can command my bot
2. UFW Firewall — block unnecessary ports
3. Fail2ban — protect against SSH brute force
4. Credentials — store API keys with `openclaw secrets` (not in .env or hardcoded). Use `openclaw secrets audit` to check for exposed credentials and `openclaw secrets apply` to migrate. If using 1Password, configure via `op` CLI.
5. Application ports — don't expose anything on 0.0.0.0

Shall we harden my server?
