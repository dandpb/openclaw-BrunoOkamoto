# Skills by User Profile

> Curated guide of OpenClaw skills organized by profile. Copy the install command and go.

---

## ⚠️ Important Warnings

### Security First
**Always review the code before installing a skill!** Skills have access to your workspace, credentials, and can execute commands. Only install from trusted sources (verified ClawHub, official repositories).

```bash
# Before installing, inspect the code:
git clone <repo> /tmp/skill-review
cat /tmp/skill-review/SKILL.md
```

### Avoid Redundancies
- **remind-me ≈ native cron** — OpenClaw already has a built-in cron. Only install remind-me if you need extra features (complex recurrence, snooze)
- **multiple weather skills** — choose one (built-in weather is sufficient)
- **duplicate creators** — one image generator is enough (built-in openai-image-gen or stable-diffusion)

### Creators Are Skills, Not Agents
❌ **Wrong:** 8 specialized agents (ImageAgent, VideoAgent, WriterAgent...)
✅ **Right:** 1 main agent + 8 skills (image-gen, video-edit, grammar-check...)

**Why?** One agent with unified context and multiple tools > multiple disconnected agents. Agents should have *purposes*, not *functions*.

---

## Essential Skills (All Profiles)

Regardless of your work, these are fundamental:

### 1. **github** (built-in)
- **What it does:** Creates issues, PRs, searches code, manages repos
- **Why it's essential:** Your workspace is on Git. This is version control for your agent.
- **Installation:** `openclaw skill enable github`

### 2. **1password** (built-in)
- **What it does:** Reads/creates/updates credentials in 1Password via CLI
- **Why it's essential:** Never hardcode credentials. Your agent needs to manage secrets securely.
- **Installation:** `openclaw skill enable 1password` (requires 1Password CLI configured)

### 3. **weather** (built-in)
- **What it does:** Checks weather forecast via wttr.in
- **Why it's essential:** Physical context matters. "Should I go out now?" "Will it rain at the outdoor meeting?"
- **Installation:** `openclaw skill enable weather`

### 4. **healthcheck** (built-in)
- **What it does:** Monitors HTTP/HTTPS services, notifies when they go down
- **Why it's essential:** Proactivity. Know if your site/API went down before customers complain.
- **Installation:** `openclaw skill enable healthcheck`

---

## 👔 Entrepreneur / Founder

Focus on operations, metrics, reports, decision-making.

### 1. **gog (Google Workspace)** (built-in)
- **What it does:** Accesses Gmail, Calendar, Drive, Sheets, Docs
- **Why it's useful:** Centralizes communication and data. Read emails, create events, generate reports directly from Sheets.
- **Installation:** `openclaw skill enable gog` (requires OAuth credentials)

### 2. **stripe-api** (clawhub.com/stripe)
- **What it does:** Queries revenue, customers, subscriptions, invoices in Stripe
- **Why it's useful:** Real-time revenue metrics. "How much did I earn today?" "How many new subscriptions?"
- **Installation:** `openclaw skill install clawhub/stripe`

### 3. **analytics-reports** (clawhub.com/analytics)
- **What it does:** Pulls data from Google Analytics and generates reports
- **Why it's useful:** Traffic, conversion, funnel — all accessible via chat.
- **Installation:** `openclaw skill install clawhub/analytics`

### 4. **postgres-query** (clawhub.com/postgres)
- **What it does:** Executes SQL queries on your production database (read-only recommended)
- **Why it's useful:** "How many active users?" "Which feature is used most?" Instant answers.
- **Installation:** `openclaw skill install clawhub/postgres`

### 5. **notion-db** (clawhub.com/notion)
- **What it does:** Reads/creates/updates databases in Notion
- **Why it's useful:** If you manage projects/CRM in Notion, the agent accesses and updates everything.
- **Installation:** `openclaw skill install clawhub/notion`

### 6. **slack-admin** (clawhub.com/slack)
- **What it does:** Sends messages, reads channels, creates threads in Slack
- **Why it's useful:** Delegate team notifications, summarize important conversations.
- **Installation:** `openclaw skill install clawhub/slack`

### 7. **financial-dashboard** (clawhub.com/finance)
- **What it does:** Connects multiple financial APIs (Stripe, QuickBooks, PagSeguro) and generates dashboards
- **Why it's useful:** Unified view of revenue, expenses, cash flow.
- **Installation:** `openclaw skill install clawhub/finance`

---

## 🎨 Content Creator

Focus on content production, social media, design, editing.

### 1. **openai-image-gen** (built-in)
- **What it does:** Generates images with DALL-E
- **Why it's useful:** Thumbnails, illustrations, visual assets on demand.
- **Installation:** `openclaw skill enable openai-image-gen`

### 2. **openai-whisper-api** (built-in)
- **What it does:** Transcribes audio to text (podcasts, interviews, videos)
- **Why it's useful:** Automatic transcriptions for captions, blog posts, show notes.
- **Installation:** `openclaw skill enable openai-whisper-api`

### 3. **video-frames** (built-in)
- **What it does:** Extracts frames from videos for analysis
- **Why it's useful:** Choose the best frame for thumbnails, analyze composition.
- **Installation:** `openclaw skill enable video-frames`

### 4. **ffmpeg-edit** (clawhub.com/ffmpeg)
- **What it does:** Cuts, concatenates, converts videos via ffmpeg
- **Why it's useful:** Quick edits without opening Premiere. "Cut the first 10s and export at 720p."
- **Installation:** `openclaw skill install clawhub/ffmpeg`

### 5. **youtube-metadata** (clawhub.com/youtube)
- **What it does:** Uploads, updates title/description/tags of videos on YouTube
- **Why it's useful:** Automate publishing. "Upload this video with this thumbnail and this description."
- **Installation:** `openclaw skill install clawhub/youtube`

### 6. **twitter-scheduler** (clawhub.com/twitter)
- **What it does:** Schedules tweets, threads, analyzes engagement
- **Why it's useful:** Create full threads in one conversation, the agent schedules and publishes.
- **Installation:** `openclaw skill install clawhub/twitter`

### 7. **canva-api** (clawhub.com/canva)
- **What it does:** Creates designs via Canva API (posts, stories, banners)
- **Why it's useful:** Visual asset generation at scale. "Create 5 variations of this post."
- **Installation:** `openclaw skill install clawhub/canva`

### 8. **subtitle-sync** (clawhub.com/subtitles)
- **What it does:** Generates and synchronizes SRT/VTT subtitles
- **Why it's useful:** Automatic accessibility. Transcription → synchronized subtitles.
- **Installation:** `openclaw skill install clawhub/subtitles`

---

## 💻 Developer

Focus on coding, CI/CD, debugging, deploy, monitoring.

### 1. **github** (built-in)
- **What it does:** Creates issues, PRs, searches code, manages repos
- **Why it's useful:** "Open an issue for this bug." "List PRs pending review."
- **Installation:** `openclaw skill enable github`

### 2. **tmux** (built-in)
- **What it does:** Manages tmux sessions (create, list, kill, send commands)
- **Why it's useful:** Run servers/builds in background, monitor processes.
- **Installation:** `openclaw skill enable tmux`

### 3. **docker-compose** (clawhub.com/docker)
- **What it does:** Starts/stops containers, reads logs, restarts services
- **Why it's useful:** "Restart the Redis container." "Backend logs for the last 5min."
- **Installation:** `openclaw skill install clawhub/docker`

### 4. **postgres-query** (clawhub.com/postgres)
- **What it does:** Executes SQL queries on dev/staging database
- **Why it's useful:** Quick debugging. "Show the last order from user X."
- **Installation:** `openclaw skill install clawhub/postgres`

### 5. **sentry-alerts** (clawhub.com/sentry)
- **What it does:** Queries errors in Sentry, automatically creates issues in GitHub
- **Why it's useful:** Proactivity. Critical errors become issues without manual intervention.
- **Installation:** `openclaw skill install clawhub/sentry`

### 6. **cloudflare-dns** (clawhub.com/cloudflare)
- **What it does:** Manages DNS, cache, firewall rules in Cloudflare
- **Why it's useful:** "Add an A record for staging." "Clear the cache."
- **Installation:** `openclaw skill install clawhub/cloudflare`

### 7. **aws-cli-wrapper** (clawhub.com/aws)
- **What it does:** Executes AWS commands (EC2, S3, Lambda, RDS)
- **Why it's useful:** "List active instances." "Deploy the Lambda." Infrastructure via chat.
- **Installation:** `openclaw skill install clawhub/aws`

### 8. **code-review-ai** (clawhub.com/code-review)
- **What it does:** Analyzes PRs, suggests improvements, detects bugs
- **Why it's useful:** Automatic review before requesting from the team. Instant feedback.
- **Installation:** `openclaw skill install clawhub/code-review`

---

## 📅 Personal Productivity

Focus on calendar, notes, tasks, routine automation.

### 1. **gog (Google Workspace)** (built-in)
- **What it does:** Accesses Gmail, Calendar, Drive, Docs
- **Why it's useful:** "What is my next meeting?" "Create a doc with my notes for today."
- **Installation:** `openclaw skill enable gog`

### 2. **todoist-sync** (clawhub.com/todoist)
- **What it does:** Reads/creates/completes tasks in Todoist
- **Why it's useful:** Task management via chat. "Add 'buy coffee' for tomorrow."
- **Installation:** `openclaw skill install clawhub/todoist`

### 3. **notion-db** (clawhub.com/notion)
- **What it does:** Reads/creates/updates databases in Notion
- **Why it's useful:** If you use Notion as your second brain, the agent accesses everything.
- **Installation:** `openclaw skill install clawhub/notion`

### 4. **obsidian-vault** (clawhub.com/obsidian)
- **What it does:** Reads/creates/searches notes in Obsidian (local vault)
- **Why it's useful:** Integrated PKM. "Search my notes on X." "Create a note with this content."
- **Installation:** `openclaw skill install clawhub/obsidian`

### 5. **calendar-assistant** (clawhub.com/calendar)
- **What it does:** Schedules meetings, detects conflicts, suggests time slots
- **Why it's useful:** "Schedule 30min with John next week, in the morning."
- **Installation:** `openclaw skill install clawhub/calendar`

### 6. **email-summarizer** (clawhub.com/email-summary)
- **What it does:** Summarizes unread inbox, highlights urgencies
- **Why it's useful:** "Summarize my emails for today." Assisted zero-inbox.
- **Installation:** `openclaw skill install clawhub/email-summary`

### 7. **habit-tracker** (clawhub.com/habits)
- **What it does:** Tracks daily habits, sends reminders
- **Why it's useful:** "Have I drunk 2L of water today?" "Remind me to meditate at 7pm."
- **Installation:** `openclaw skill install clawhub/habits`

---

## 🔍 How to Discover More Skills

- **Official ClawHub:** https://clawhub.com
- **GitHub topic:** search for `openclaw-skill` on GitHub
- **Discord community:** ask in #skills what people are using
- **Create your own:** if it doesn't exist, it's an opportunity! Skills are just bash + SKILL.md

---

## 📝 Anatomy of a Skill

An OpenClaw skill is simply:

```
skill-name/
├── SKILL.md          # Documentation + tool declarations
├── tool-one.sh       # Executable script
└── tool-two.sh       # Another script
```

The agent reads `SKILL.md`, discovers the available tools, and executes the scripts when needed.

**Tip:** Start simple. A 50-line skill that solves YOUR problem > a 500-line generic skill.

---

## ✅ Installation Checklist

Before installing a skill:

- [ ] I read the `SKILL.md` and understand what it does
- [ ] I reviewed the bash scripts (looking for `rm -rf`, suspicious `curl`, `eval`)
- [ ] I verified it does not duplicate functionality I already have
- [ ] I know which credentials/APIs it needs
- [ ] I tested it in an isolated environment first (if critical)

After installing:

- [ ] Configured credentials in `.env` or 1Password
- [ ] Tested each tool manually
- [ ] Documented specific usage in my `TOOLS.md`
- [ ] Updated `AGENTS.md` if the skill requires special rules

---

**Remember:** Skills amplify the agent. But an agent without a strong identity (SOUL.md, USER.md) remains generic, regardless of how many skills you install. Invest time in who the agent IS before multiplying what it DOES.
