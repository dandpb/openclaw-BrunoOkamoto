# ❓ Q&A — Basic Infrastructure (Port, SSH, Connection)

> Plain language. No terminal. Paste the prompt into your bot and it handles the rest.

---

## "'address already in use' or 'port in use' appeared"

**What happened:** Another program is using the same port that OpenClaw wants to use. It's like two people trying to sit in the same chair at the same time.

**What to do:**
Paste this prompt into your bot:

```
A "port already in use" or "address already in use" error appeared.
Help me fix it:
1. Which port is in conflict?
2. Which process is using that port?
3. How to resolve it — stop the process that's in the way or change OpenClaw's port?
4. How do I confirm it's resolved?
```

---

## "The bot won't connect / 'localhost refused connection'"

**What happened:** The gateway (the main OpenClaw program) is probably not running, or it's on a different port than the one you're trying to access.

**What to do:**
Paste this prompt into your bot (if you have access via another channel):

```
I have a connection problem — "connection refused" on localhost.
Help me diagnose:
1. Is the OpenClaw gateway running?
2. Which port should it be on?
3. How do I check the status without using the terminal too much?
4. How do I restart the gateway safely?
```

**If you can't access the bot at all:** Try accessing the OpenClaw panel via Mission Control or the link you configured during setup.

---

## "'command not found' appeared when I try to use something"

**What happened:** The program you want to use is not installed, or the path is not configured correctly.

**What to do:**
Paste this prompt into your bot:

```
"command not found" appeared when I tried to use [COMMAND NAME].
Help me:
1. Should this command be installed in OpenClaw?
2. How do I install it if it's not?
3. How do I check if it's in the right path?
```

---

## "I don't know how to access my server remotely"

**What happened:** You need to connect to your VPS from anywhere securely.

**What to do:**
Paste this prompt into your bot:

```
I need to access my server remotely in a secure way.
Explain in very plain terms:
1. What is an SSH tunnel and what is it for?
2. How do I set up secure access via Tailscale or Cloudflare Tunnel?
3. Which one is easier for a beginner?
4. Guide me through the setup process step by step.
```

**Tip:** Tailscale is the simplest option for beginners — it installs in 5 minutes and works like a free personal VPN.

---

## "My VPS is slow / using too much memory"

**What to do:**
Paste this prompt into your bot:

```
My VPS seems slow or is using too much memory/CPU.
Help me diagnose:
1. Which processes are consuming the most resources?
2. Is there any agent or cron running unnecessarily?
3. What can I do to reduce consumption?
4. When does it make sense to upgrade the VPS?
```

---

*Last updated: Feb/2026*
