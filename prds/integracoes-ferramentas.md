# PRD: How to Integrate Your Tools — Skills & APIs

> Script for recording Extra Lesson A
> Audience: complete beginners — never dealt with an API or skill before

---

## Lesson Objective

Teach how to connect the agent to tools the student already uses (Notion, Google Calendar, Stripe, etc.) through:
1. **Ready-made skills** from ClawHub
2. **Direct APIs** (when there's no skill available)
3. **Turning knowledge into a custom skill**

**Premise:** The student doesn't know how to program. Everything must be explained as if it's the first time.

---

## Estimated time: 20-25 minutes

---

## Lesson Structure

### Block 1: Why integrate? (3 min)

**What to show:**
- Isolated agent vs connected agent
- Visual example: "Without integration, the agent is blind. With integration, it sees everything."
- Real case: MGM Boss (Stripe + ChartMogul + Notion) and FLG Boss (YouTube + Instagram + Notion)

**Key phrase:**
> "The agent is only useful if it has access to your data. Without that, it's just a glorified chatbot."

---

### Block 2: ClawHub Skills — The easy way (7 min)

**What a skill is:**
"A skill is like an app you install on your agent. Someone already did the heavy lifting — you just install and use it."

**Live demonstration:**

1. **Search available skills**
   ```bash
   clawhub search notion
   ```
   Explain: "ClawHub is like an App Store of skills for agents."

2. **Install a skill**
   ```bash
   clawhub install notion
   ```
   Explain what happens:
   - Downloads the skill code
   - Registers it in OpenClaw
   - Now the agent knows how to use Notion

3. **View installed skills**
   ```bash
   clawhub list
   ```

4. **Test the skill** — send a message to the agent:
   > "List the tasks from database [database ID] that have status 'In Progress'"

**Recommended skills to show:**
- `notion` — project management
- `1password` — secure credentials
- `weather` — simple example to test with
- `github` — for those with a repo

---

### Block 2.5: gog CLI — Google Workspace made simple (2 min)

**New in 3.2 — recommended alternative to manual OAuth flow:**

```bash
# Install gog CLI
npm install -g gog

# Authenticate (one command for everything: Calendar, Drive, Gmail, Docs)
gog auth login

# Use
gog calendar list --account=YOUR_EMAIL
gog drive ls
gog gmail inbox --limit 10
```

**Why use gog instead of the manual OAuth flow?**
- No need to create a project in Google Cloud Console
- No need to manually configure OAuth credentials
- A single `gog auth login` authenticates all Google services
- Calendar, Drive, and Gmail skills already use gog by default

> 💡 If you use Google Calendar, Drive, Gmail or Docs — install gog first. It's the fastest path.

---

### Block 3: Direct APIs — When there's no skill (8 min)

**Scenario:** "What if there's no ready-made skill for Stripe? Or for your internal CRM?"

**Real case: Integrating Stripe in MGM Boss**

**Step by step (show the process, not just the result):**

1. **Get the API key**
   - Go to dashboard.stripe.com → Developers → API Keys
   - Copy the "Secret key" (starts with `sk_live_` or `sk_test_`)
   - **NEVER** put it directly in code or config

2. **Store in 1Password** (security!)
   ```bash
   # If you have the 1Password CLI installed
   op item create --category=api-credential \
     --title="Stripe MGM" \
     --vault="Amora Vault" \
     secret_key="sk_live_..."
   ```
   Or manually through the app/web.

3. **Retrieve when the agent needs it** — show how the agent does this:
   > "Agent, get the Stripe key from 1Password and show me my current MRR."

   Behind the scenes, the agent will:
   ```bash
   STRIPE_KEY=$(op item get "Stripe MGM" --vault "Amora Vault" --field secret_key --reveal)
   curl https://api.stripe.com/v1/balance \
     -u "$STRIPE_KEY:"
   ```

4. **Register in TOOLS.md** — document the integration:
   ```markdown
   ### Stripe (MGM Payments)
   - **1PW Item:** `Stripe MGM`
   - **Vault:** Amora Vault
   - **Access:** Read freely, Write = Bruno's approval
   ```

**Explain the flow:**
> "1Password → Agent retrieves credential → Uses API → Returns result. Your password is never exposed."

---

### Block 3.5: Native PDF Tool — already available in your agent (1 min)

**No installation needed — it already works:**

> "Since version 3.2, your agent can analyze PDFs directly. No skill, no configuration."

**Demonstrate live:**
- Drag a PDF into the chat (or mention the path)
- Ask: "Analyze this contract and tell me the critical points"
- Show the agent extracting information from the PDF in real time

**Practical use cases:**
- Analyzing bills and invoices
- Summarizing long reports
- Extracting data from PDF spreadsheets
- Reviewing contracts (with a warning: the agent is not a lawyer!)

**Technical details (brief):**
- Native support: Claude (Anthropic) and Gemini (Google)
- Other models: automatic text/image extraction as fallback
- Limit: up to 10 PDFs per message

---

### Block 4: Turning knowledge into a skill (5 min)

**Scenario:** "What if you use a niche tool that nobody else uses? Like an internal CRM from your company?"

**Show the concept (no need to implement live):**

A skill is just a folder with:
- `SKILL.md` — instructions for the agent
- Helper scripts (if needed)

**Simple example — "Company X CRM" Skill:**

Create folder:
```bash
mkdir -p ~/.openclaw/skills/company-x-crm
```

Create `SKILL.md`:
```markdown
# Skill: Company X CRM

Access to the internal CRM API.

## Credentials
- API Key: 1Password → "Company X CRM API Key"
- Base URL: https://crm.companyx.com/api/v1

## Main endpoints

### List leads
GET /leads?status=active
Header: Authorization: Bearer {API_KEY}

### Create lead
POST /leads
Body: {"name": "...", "email": "...", "phone": "..."}

## How to use
The agent should:
1. Get the API key from 1Password
2. Make calls via curl or fetch
3. Parse the JSON response
```

**Register the skill:**
```bash
openclaw skills register ~/.openclaw/skills/company-x-crm
```

**Test:**
> "Agent, list the active leads in the CRM."

**Explain:**
> "You don't need to know how to program. You just need to know where the API documentation is and copy it into SKILL.md. The agent does the rest."

---

### Block 5: Real cases — FLG and MGM (3 min)

**Show both workspaces side by side:**

**MGM Boss (`workspace-mgm-boss`):**
- **TOOLS.md open** — show the documented integrations:
  - Supabase (database)
  - Stripe (payments)
  - ChartMogul (SaaS metrics)
  - PostHog (analytics)
  - Notion (sprint board)
  - Google Analytics + Search Console (SEO)

**FLG Boss (`workspace-flg-boss`):**
- **TOOLS.md open** — show:
  - YouTube Data API + Analytics API
  - Instagram via RapidAPI
  - LinkedIn via RapidAPI
  - Twitter/X Bearer Token
  - Tella.tv (recordings)
  - Figma (design)
  - Notion (editorial calendar)

**Key phrase:**
> "These two agents see EVERYTHING that happens in my businesses. And I don't need to open 15 tabs every day."

---

### Block 6: Practical checklist for integrating any tool (2 min)

**Roadmap the student can follow:**

1. ✅ Does the tool have an API? (search "API documentation" on Google)
2. ✅ Is there a ready-made skill on ClawHub? (`clawhub search tool-name`)
3. ✅ If yes → install and test
4. ✅ If not → follow the flow:
   - Get API key from the tool
   - Store in 1Password
   - Document in TOOLS.md
   - Test with the agent
5. ✅ If it's recurring → create a custom skill

---

## Security Alerts (emphasize)

🔴 **NEVER** put API keys directly in code or config
🔴 **NEVER** commit credentials to Git
🔴 **ALWAYS** use 1Password (or similar)
🔴 **ALWAYS** define permissions (read-only when possible)

**Real MGM example:**
> "In MGM Boss, the agent can READ Stripe data freely. But to issue a refund or cancel a subscription, it MUST ask for my approval. This is documented in TOOLS.md and it respects that."

---

## Lesson Checkpoint

By the end, the student should know:
- [ ] What a skill is and where to find one
- [ ] How to install a skill from ClawHub
- [ ] How to integrate an API directly (without a ready-made skill)
- [ ] Where to store credentials (1Password)
- [ ] How to document integrations in TOOLS.md
- [ ] How to create a custom skill (concept)

---

## Prompt that goes in the PDF

Will be in the file `prompts/modulo-extra-a-integracoes.md`.

---

## Common Troubleshooting

### "clawhub: command not found"
```bash
npm install -g clawhub
```

### "Skill installed but agent doesn't know how to use it"
```bash
# Check if it was registered
openclaw skills list
# If it doesn't appear, register manually
openclaw skills register ~/.openclaw/skills/skill-name
# Restart gateway
openclaw gateway restart
```

### "API returns 401 Unauthorized"
- Check if the API key is correct
- Check if it has expired
- Check if it has sufficient permissions

---

*This lesson is the turning point: before it, the student has an isolated agent. Afterwards, they have an agent that sees everything.*
