# PRD — Lesson N-1: Configuring Credentials — Anthropic + OpenAI API Key

> **Level:** Beginner / Setup
> **Estimated Duration:** 15–20 minutes
> **Prerequisites:** OpenClaw installed, internet access
> **Updated:** Anthropic blocked OAuth for Pro plans — new recommended flow

---

## 🎯 Lesson Objective

By the end of this lesson, the student will be able to:

1. Understand why Anthropic's OAuth/`setup-token` flow **no longer works** for most students
2. Configure Anthropic via **direct API Key** (correct and recommended flow)
3. Generate and configure API Keys on the **OpenAI Platform** (OAuth still works here)
4. Configure credentials in OpenClaw via `openclaw config`
5. Verify that the configuration is working with `openclaw status`
6. Diagnose and resolve the **most common authentication errors**

---

## 🚨 IMPORTANT WARNING — Read Before Starting

> **Anthropic has blocked OAuth for Pro plans.**

If you have a Claude Pro subscription ($20/month), **the `setup-token` / `openclaw setup-token` flow NO LONGER WORKS for you.** This affects most students and is the course's #1 question (~20 occurrences in the forums).

**Symptom:** You try running `openclaw setup-token` (or the Anthropic OAuth flow in the wizard), it seems to work, but on the first message to the bot you get an error "OAuth flow not supported for Pro plans" or "Unauthorized".

**Solution:** Completely ignore the OAuth flow and use a **direct API Key**, which is what we'll learn in this lesson.

> ⚠️ **This is not an OpenClaw bug.** Anthropic changed their policy. OpenClaw adapted, but the onboarding wizard may still show the OAuth option — **ignore it and use API Key**.

---

## 📋 Recording Script — Section by Section

### 🎬 OPENING (0:00 – 2:00)

**[Bruno on screen, direct tone]**

> "Hey everyone! Lesson N-1 of the OpenClaw course — configuring credentials. This lesson exists because this is where most people get stuck."

> "And I need to warn you about an important change: Anthropic, which makes Claude, has blocked OAuth login for Pro plans. Yes — if you pay $20/month for a Claude subscription, the old flow no longer works. I'm going to show you the right way, which is actually simpler."

> "If you've already tried to configure it, saw some error about 'setup-token' or 'OAuth', or simply never managed to get Claude to respond — this lesson fixes that once and for all."

---

### 📚 SECTION 1: Why the Old Flow Broke (2:00 – 5:00)

**[Screen showing diagram or slide]**

> "Before the change, Anthropic had a flow where you could connect OpenClaw via OAuth — basically, you authorized access through the web interface, without needing an API Key. It seemed more convenient."

> "But in 2026, Anthropic decided that this OAuth flow only works for API plans (pay-per-use). For Pro plans ($20/month) — which most people have — they blocked it. The reason? Abuse prevention and a clear separation between 'subscription to use in chat' vs 'programmatic access via API'."

**[Pause for emphasis]**

> "So the situation today is:"

| Situation | Works? | What to do |
|----------|-----------|-------------|
| Pro plan ($20/month) + OAuth | ❌ Blocked | Create a separate API Key |
| Anthropic free plan + OAuth | ❌ Blocked | Create API Key with billing |
| Direct API Key (any plan) | ✅ Works | What we're going to do |

> "The good news: an API Key is simpler to understand and more flexible. You control exactly how much you spend. Let's configure that now."

---

### 💳 SECTION 1.5: What if I have a Pro subscription? (5:00 – 7:30)

**[Screen: browser at console.anthropic.com]**

> "Before we continue — if you pay for Claude Pro, you need to understand something important."

> "Your Pro subscription ($20/month) and API access are **separate things**. Your subscription gives access to the chat at claude.ai — not to the API. They are different billing systems."

> "To use OpenClaw with Claude, you need:"
> 1. Access console.anthropic.com (different from claude.ai)
> 2. Add a SEPARATE payment method (or credits)
> 3. Create an API Key

> "Yes, it seems unfair to pay twice. But that's how Anthropic has structured it. The good news: with fine-grained model control (Haiku for simple tasks, Sonnet for interaction), actual API spending is usually $5-15/month — much less than the Pro subscription."

> "If you want to AVOID paying extra: you can migrate from Pro to API-only. Cancel Pro, use only the API. You lose access to claude.ai, but OpenClaw actually works better that way."

---

### 🔑 SECTION 2: Generating your Anthropic API Key (7:30 – 11:00)

**[Screen: Browser opening console.anthropic.com]**

> "Let's create the API Key. Go to **console.anthropic.com** — note: it's the **console**, not claude.ai."

**[Show navigation in the panel]**

> "After you log in, click on **'API Keys'** in the side menu (or Settings → API Keys)."

> "Click on **'Create Key'**."

**[Show the form]**

> "Give your key a name — I recommend `openclaw-personal`. This helps with management later."

> "**ATTENTION now!** The key will appear on the screen. It looks like `sk-ant-api03-XXXXXX...`"

**[WARNING box on screen]**

> "**COPY IT NOW.** This is your only chance to see the full key. After this, Anthropic doesn't show it again. Save it in a password manager (1Password, Bitwarden) or a secure place."

> "But before you leave happily — check if billing is active. Go to **Settings → Billing** and confirm that you have a card on file or credits. Without billing, the key works but every call returns error 402."

---

### 🔑 SECTION 3: Generating your OpenAI API Key (11:00 – 13:30)

**[Screen: Browser opening platform.openai.com]**

> "Now let's go to OpenAI. Here it's more straightforward — OAuth still works, but API Key also works. Let's use API Key for consistency."

> "Go to **platform.openai.com/api-keys** and click **'Create new secret key'**."

> "Give it a name, confirm, and copy the key. It starts with `sk-proj-` or `sk-`."

> "Same rule: **copy it now**, it won't appear again."

> "Check credit at **Billing → Usage**. OpenAI needs credit or an active free trial to work."

---

### ⚙️ SECTION 4: Configuring OpenClaw with `openclaw config` (13:30 – 17:00)

**[Screen: Terminal open]**

> "Now that we have the keys, let's configure. Open the terminal and type:"

```bash
openclaw config
```

> "This opens the interactive wizard. Select Anthropic, paste your API Key when prompted."

> "Then select OpenAI (if you've set that up too) and paste the key."

**[IMPORTANT — show this]**

> "Attention: if the wizard shows an 'OAuth' or 'Setup Token' option for Anthropic — **ignore it**. Always choose 'API Key'. I know it seems contradictory that OpenClaw itself shows this option, but it no longer works for most accounts."

---

### ✅ SECTION 5: Testing with `openclaw status` (17:00 – 19:00)

**[Screen: Terminal]**

> "To check that everything is correct, run:"

```bash
openclaw status
```

> "You'll see something like this:"

```
✅ OpenClaw Status
─────────────────────────────
Provider: Anthropic (Claude)
Model:    claude-sonnet-4-5
API Key:  sk-ant-...api03 (valid)
Status:   Connected

Provider: OpenAI
Model:    gpt-4o
API Key:  sk-proj-...XxXx (valid)
Status:   Connected
─────────────────────────────
All providers configured ✓
```

> "If 'Connected' appears — perfect! If an error appears, see the next section."

---

### 🔧 SECTION 6: Common Errors and How to Fix Them (19:00 – 22:00)

**[Screen: Slides with errors]**

**[Error 1 — TOP 1 of the course]**

> "**'OAuth flow not supported' or 'setup-token only'** — this is the #1 error in the forum. Cause: you used the OAuth flow or `openclaw setup-token`. Solution: run `openclaw config` again, choose 'API Key' (not OAuth), paste your key from console.anthropic.com."

**[Error 2]**

> "**'Invalid API Key'** — the key is wrong, expired, or was revoked. Go to the provider's console, create a new one, reconfigure."

**[Error 3]**

> "**'HTTP 402 — Payment Required'** — you have the right key but don't have billing active. Anthropic: go to console.anthropic.com → Billing → add a card. OpenAI: platform.openai.com → Billing → add credit."

**[Error 4]**

> "**Rate limit (HTTP 429)** vs invalid credential (HTTP 401) — these are different things! Rate limit is temporary, wait a few minutes. Invalid credential is permanent, you need to reconfigure."

---

### 🎯 CLOSING (22:00 – 23:00)

> "Lesson summary: Anthropic's OAuth flow no longer works for Pro plans — always use API Key. OpenAI still works with OAuth but API Key is simpler. We configured with `openclaw config`, verified with `openclaw status`."

> "If you have a Pro subscription — you'll need separate billing on the API to use OpenClaw. It's worth it: with smart model usage, you spend less than Pro and have much more control."

> "In the next lesson, we start using it for real. But first, do the practical exercise!"

---

## 🛠️ Detailed Technical Step-by-Step

### 1. Generate API Key — Anthropic

1. Access [console.anthropic.com](https://console.anthropic.com) (**not** claude.ai)
2. Log in or create an account
3. In the side menu: **Settings → API Keys** (or click the key icon)
4. Click **"Create Key"**
5. Give it a descriptive name (e.g.: `openclaw-personal`)
6. **COPY THE KEY IMMEDIATELY** — it starts with `sk-ant-api03-`
7. Save it in a password manager (e.g.: 1Password, Bitwarden)
8. Check billing: Settings → Billing → card on file ✅

> ⚠️ **If you have a Pro plan:** You still need to do these steps. The Pro subscription and the API are separate billing systems.
> ⚠️ **Anthropic only displays the full key once.** After closing the modal, it's not possible to view it again.

### 2. Generate API Key — OpenAI

1. Access [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
2. Log in to your OpenAI account
3. Click **"Create new secret key"**
4. Give it a name (e.g.: `openclaw`)
5. **COPY THE KEY IMMEDIATELY** — it starts with `sk-proj-` or `sk-`
6. Check credit at **Billing → Usage**

### 3. Configure OpenClaw

```bash
# Start the configuration wizard
openclaw config

# When OAuth/setup-token option appears for Anthropic → IGNORE
# Always choose "API Key"
# Paste your key when prompted
```

### 4. Verify the Configuration

```bash
# Check status of all providers
openclaw status

# Expected output:
# ✅ Provider: Anthropic — Status: Connected
# ✅ Provider: OpenAI — Status: Connected
```

### 5. Where Credentials are Stored

| Operating System | Path |
|--------------------|---------|
| Linux / macOS | `~/.openclaw/config.json` |
| Windows | `C:\Users\<YourName>\.openclaw\config.json` |

> 🔒 **Security:** This file has restricted permissions (mode 600 on Linux/Mac). **Never commit this file to git.**

---

## 🚨 Common Error Table + Solution

| Error | Cause | Solution |
|------|-------|---------|
| `OAuth flow not supported` / `setup-token only` | ⭐ **TOP 1** — Used OAuth with Pro plan | Run `openclaw config`, choose "API Key", paste key from console.anthropic.com |
| `Invalid API Key` | Wrong, expired, or revoked key | Check/recreate the key in the console. Run `openclaw config` again. |
| `HTTP 401 Unauthorized` | Invalid credential | Same solution as Invalid API Key. |
| `HTTP 402 Payment Required` | No active billing on Anthropic | console.anthropic.com → Billing → add card/credits |
| `HTTP 429 Too Many Requests` | Rate limit reached (not a key issue) | Wait 1-5 minutes. Consider plan upgrade if recurring. |
| `Insufficient credits` | No credit on OpenAI | platform.openai.com → Billing → add credit. |
| `API Key not configured` | Never ran `openclaw config` | Run `openclaw config` and configure the keys. |
| Key works but agent doesn't respond | tools.profile = messaging (v2026.3.2) | `openclaw config set tools.profile full` |
| `model_not_available` | Model not available on tier | Switch to claude-haiku-4-5 or claude-sonnet-4-5 |

---

## ✅ Student Final Checklist

- [ ] Account created/accessed at console.anthropic.com (**not** claude.ai)
- [ ] Anthropic API Key generated and saved securely
- [ ] Active billing on Anthropic (card or credits)
- [ ] (Optional) OpenAI API Key generated and saved
- [ ] (Optional) OpenAI: credit verified in Billing
- [ ] `openclaw config` run — chose "API Key" (not OAuth)
- [ ] `openclaw status` showing "Connected" for configured providers
- [ ] File `~/.openclaw/config.json` is NOT in git (checked .gitignore)
- [ ] First tests completed successfully

---

## ❓ Frequently Asked Questions

**1. I have Claude Pro — do I need to pay extra?**

> Yes, unfortunately. Your Pro subscription gives access to claude.ai (the web interface), not to the API. To use OpenClaw, you need separate billing at console.anthropic.com. The good news: with economical models (Haiku for simple tasks), actual spending is usually $5-15/month.

**2. Can I cancel Pro and use only the API?**

> Yes! For use with OpenClaw, API-only is actually the ideal setup. You lose access to claude.ai (the nice web interface), but OpenClaw replaces it with much more power.

**3. Why does the OAuth option still appear in OpenClaw?**

> OpenClaw still keeps the option for compatibility with legacy API plans. But for the vast majority of students with Pro plans or new accounts, **it doesn't work**. Always use API Key.

**4. Do I need to configure both providers (Anthropic AND OpenAI)?**

> It's not mandatory. Configure only the ones you intend to use. For the course, we recommend at least Anthropic (Claude).

**5. How do I change the key after it's been configured?**

> Run `openclaw config` again and enter the new key. The previous value is overwritten.

**6. Does OpenClaw store my keys in the cloud?**

> No. The keys are stored only locally in `~/.openclaw/config.json`. OpenClaw does not send your credentials to any external server.
