# Student Prompt — Lesson N-1: Configure API Key

> **How to use:** Copy the prompt below and paste it in the chat with your OpenClaw agent after watching the lesson.
>
> ⚠️ **Note:** This lesson uses **API Key** directly — not OAuth. You will need your Anthropic (or other provider) API key on hand.

---

## 📋 Main Prompt

```
Hello! I just watched lesson N-1 of the OpenClaw course on API Key configuration.

I need your help to:
1. Verify that my configuration is correct
2. Complete the practical exercises from the lesson
3. Fix any issues I encounter

Let's start with a complete diagnosis of my configuration?
```

---

## 🧪 Exercise 1 — Configuration Diagnosis

```
Please do a complete diagnosis of my current OpenClaw configuration:

1. Run `openclaw status` and show me the result
2. Identify which providers are configured (Anthropic, OpenAI, Google, etc.)
3. For each provider, check if the status is "Connected"
4. Tell me if there are any problems or warnings

After the diagnosis, explain what each part of the output means.
```

---

## 🔑 Exercise 2 — Configure API Key (main flow)

```
I want to configure my API Key in OpenClaw using the correct flow.

Please guide me through the process:
1. Explain the difference between API Key and setup-token — when do I use each?
2. Guide me to obtain my Anthropic API Key (console.anthropic.com)
3. Configure the key in OpenClaw:
   - First try: `openclaw config set providers.anthropic.apiKey <my-key>`
   - Or via file: edit `~/.openclaw/config.json` and add the key in the correct field
4. Confirm it's working with `openclaw status`

Important: Do not hardcode the key in any code file or .env — use the OpenClaw config or `openclaw secrets`.
```

---

## 🔍 Exercise 3 — Credentials Security Check

```
I want to verify that my credentials are stored securely.

Please:
1. Run `openclaw secrets audit` to check for exposed credentials
2. Check the permissions of the file ~/.openclaw/config.json (should be 600)
3. If in a git project, check if config.json is in .gitignore
4. Confirm there are NO hardcoded API keys in code files or .env

If there is any problem, use `openclaw secrets apply` to migrate credentials to the correct location.
```

---

## 🔗 Exercise 4 — Real Connectivity Test

```
Now let's test whether the credentials actually work, not just whether they are configured.

Please do a real test:
1. Try a simple call to the Anthropic API (if configured)
2. Confirm which model is being used
3. Show me the result — whether success or a specific error

If the test fails, help me diagnose the problem in detail.
```

---

## 🚨 Exercise 5 — Guided Troubleshooting (use if you have problems)

```
I'm having a problem with my configuration.

[DESCRIBE YOUR ERROR HERE — for example:]
- "It shows 'Invalid API Key' when I try to use Claude"
- "openclaw status shows 'Not configured'"
- "It shows 'Unauthorized' or '401' when testing"
- "The key was accepted but the model doesn't respond"

I need help resolving this step by step. Please:
1. Explain what this error means
2. Give me the exact steps to fix it
3. Help me verify it worked after each step
```

---

## 📊 Exercise 6 — Understanding Rate Limits vs Invalid Credentials

```
I want to understand the difference between rate limit and invalid credentials in practice.

Please explain:
1. How to identify a rate limit error (what message, what HTTP status)
2. How to identify an invalid credentials error (what message, what HTTP status)
3. What to do in each case
4. How to check my current plan/quota at the providers I configured

I also want to know: is there any OpenClaw command to see my current token/request usage?
```

---

## 🔄 Exercise 7 — Reconfiguration (if you need to change the key)

```
I want to practice the reconfiguration process, as if I needed to swap my API Key.

Please guide me through the complete process:
1. How to rotate (replace) an API Key without interrupting the service
2. Which command to use to update credentials in OpenClaw
3. How to verify the new key is working
4. Best practices: use `openclaw secrets` to store, never put in .env or code

No need to actually execute — just explain the process step by step.
```

---

## ✅ Final Learning Check

```
To close the exercises for lesson N-1, give me a quick quiz with 5 questions about:
- Difference between API Key and setup-token
- Where credentials should be stored (spoiler: openclaw secrets or config)
- How to interpret openclaw status
- How to distinguish rate limit from invalid credentials
- Security best practices with API Keys

After I answer, give me detailed feedback on what I got right and what I need to review.
```

---

## 💡 Usage Tip

> If you haven't configured your credentials yet and are seeing errors, use this more direct prompt:

```
I need to configure my OpenClaw API Key from scratch.
I have my Anthropic API Key on hand (obtained from console.anthropic.com).

Please guide me step by step through the complete process, from the terminal to verifying it works. I'm using [Linux/Mac/Windows — choose one].

Remember: I want to use API Key directly, not OAuth.
```

---

*Prompt for Lesson N-1 · OpenClaw Course · Pixel Educação*
