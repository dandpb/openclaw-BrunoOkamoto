# PRD: Integrations Setup

> Drop this file into the agent: "Configure these integrations following the PRD"

## Context

An agent without integrations is just a chatbot. These are the most useful integrations by category.

## Level 1 — Essential (do these first)

### Google Calendar
```bash
# Install GOG CLI (recommended — alternative to manual OAuth flow)
npm install -g gog

# Authenticate
gog auth login --client=calendar-client --account=YOUR_EMAIL
```
- Allows: viewing appointments, creating events, reminders
- Suggested cron: check agenda at every heartbeat
- **New in 3.2:** Use the `gog` CLI as the recommended alternative to the manual OAuth flow. Simpler, less configuration, same access to Google Workspace (Calendar, Drive, Gmail).

> 💡 **gog CLI** is the recommended path for Google Workspace: a single command configures OAuth authentication for Calendar, Drive, Gmail, and Docs. No need to manually create a project in Google Cloud Console.

### Telegram (already configured in setup)
- Create a group with topics to organize conversations
- Suggested topics: General, Content, Metrics, Operational
- dmPolicy: ALWAYS allowlist

## Level 2 — Productivity

### Google Drive
```bash
gog drive ls --client=drive-client --account=YOUR_EMAIL
```
- Upload/download files
- Useful for sharing reports, docs, spreadsheets

### Notion API
- Create integration at https://www.notion.so/my-integrations
- Store API key in 1Password
- Useful for: kanban, content base, CRM

### 1Password CLI
```bash
# Install
# See: https://developer.1password.com/docs/cli/get-started/

# Usage
op item get "Item Name" --field credential --reveal
```
- EVERY credential must live in 1Password
- Never hardcode API keys in files

## Level 3 — Content & Metrics

### YouTube (Data API + OAuth)
- Create a project in Google Cloud Console
- Enable YouTube Data API v3
- Generate OAuth credentials
- Allows: listing videos, viewing analytics, scheduling uploads

### Social Media via RapidAPI
- Cloud IPs are blocked by Instagram, X, LinkedIn
- RapidAPI works as a proxy:
  - Instagram Statistics API (50 req/month free)
  - X/Twitter API45 (1000 req/month free)
  - Fresh LinkedIn Scraper
- Sign up: https://rapidapi.com

### Brave Search
- API for web search
- Already comes configured in OpenClaw (verify)

## Level 3.5 — Native PDF (New in 3.2)

### Native PDF Tool
Starting from version 3.2, agents can analyze PDF documents **natively** — without installing anything.

```
# The agent simply does:
Analyze this PDF: /path/to/document.pdf
```

- **Supported by:** Anthropic Claude and Google Gemini (native analysis)
- **Other models:** automatic fallback via text/image extraction
- **Practical use:** contracts, reports, invoices, PDF spreadsheets
- **Limit:** up to 10 PDFs per call
- No extra configuration — already available in the agent

> 💡 Real use cases: the agent analyzes invoices, extracts data from receipts into Notion, automatically summarizes long reports.

## Level 4 — Advanced

### ChartMogul (if you have a SaaS)
- MRR, churn, LTV metrics
- Weekly cron for reporting

### Crisp / Intercom (if you have support)
- Conversation analysis
- Content insights from real user questions

## Essential Crons

After configuring integrations, create crons:

| Cron | Frequency | What it does |
|------|-----------|-----------|
| Check agenda | Every heartbeat | Upcoming appointments |
| Social metrics | Weekly | Pull data from social networks |
| Weekly review | Friday | Review projects and pending items |

**CRITICAL RULE for crons:**
```
sessionTarget: "isolated"
payload.kind: "agentTurn"
delivery: { mode: "announce" }
```
NEVER use `systemEvent` + `main` — triggers but doesn't execute.

## Expected Result

Agent connected to your main tools, with at least 2 crons running.
