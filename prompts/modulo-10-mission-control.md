# Prompt — Module 10: Mission Control

> Paste this prompt in your OpenClaw chat after watching Module 10.

---

I just watched Module 10 on Mission Control — creating a visual interface to manage the agent. Even using Telegram for interaction, I need a panel to see the system state at a glance.

**What I need you to do:**

## 1. Explain why this matters

Before we start, explain:
- Why a visual panel helps (even when you have Telegram)?
- What kind of information should always be visible?
- How does this fit into the "proactivity" philosophy?
- Examples: what does a founder see vs. what a dev sees on the panel?

## 2. Help me choose the right tool

Present the options and help me decide based on **my technical level and needs**:

### Option A: NocoDB (recommended for beginners/intermediate)
- **What it is:** Notion-like, self-hosted, free, ready-made interface
- **Pros:** Quick setup, friendly GUI, REST API, table relationships
- **Cons:** Less customizable than custom code
- **Best for:** Those who want quick results without much coding
- **Setup:** Docker Compose + SQLite/Postgres

### Option B: Notion
- **What it is:** SaaS tool, relational databases
- **Pros:** Already use it daily, native mobile, easy sharing
- **Cons:** API with rate limits, data in the cloud (not self-hosted)
- **Best for:** Those who are already Notion power users
- **Setup:** Notion API + integration

### Option C: Google Sheets
- **What it is:** Spreadsheets with an API
- **Pros:** Maximum simplicity, everyone knows how to use it, native charts
- **Cons:** Not a real database, row limits
- **Best for:** Quick prototyping, simple dashboards
- **Setup:** Google Sheets API (via gog skill)

### Option D: Custom (Express + React + Supabase)
- **What it is:** Fully custom web app
- **Pros:** Full control, tailored UI, real-time, free hosting (Vercel/Supabase)
- **Cons:** Requires full-stack dev knowledge
- **Best for:** Devs who want something professional and scalable
- **Setup:** Next.js app + Supabase backend + API routes

**Ask me:**
- What is my technical level? (beginner/intermediate/advanced)
- Do I already use any of these tools?
- Do I prefer something fast or something perfect?
- Will I manage just my agent or a team of agents?

## 3. Setup for the chosen option

Once I choose, **guide me step by step**:

### If I chose NocoDB:
1. Create `docker-compose.yml` for NocoDB
2. Start the service (`docker-compose up -d`)
3. Access the web interface (localhost:8080)
4. Create the necessary tables (see structure below)
5. Generate API token
6. Create `nocodb-api` skill to connect the agent
7. Configure crons to update data automatically

### If I chose Notion:
1. Create a workspace in Notion
2. Create databases (Tasks, Memory, Crons, Health)
3. Create an integration (https://notion.so/my-integrations)
4. Grant permissions to the databases
5. Install/configure the `notion-db` skill (clawhub)
6. Test the connection and writing

### If I chose Google Sheets:
1. Create a "Mission Control" spreadsheet
2. Create tabs (Tasks, Memory, Crons, Health)
3. Configure the `gog` skill (if not already configured)
4. Create helper functions in the agent to write to sheets
5. Configure dashboard with charts

### If I chose Custom:
1. Scaffold Next.js project (`npx create-next-app@latest mission-control`)
2. Set up Supabase (free project)
3. Create tables in Supabase
4. Create API routes in Next.js
5. Connect the agent to the API routes
6. Deploy to Vercel (free)

## 4. Data structure (common base)

Regardless of the tool, these are the essential "tables":

### Tasks
- `id`, `title`, `status` (pending/done/blocked), `priority`, `created_at`, `due_date`, `assigned_to` (which agent/human)

### Memory Events
- `id`, `date`, `category` (decision/lesson/insight), `content`, `source` (main/heartbeat/cron)

### Cron Jobs
- `id`, `name`, `schedule`, `last_run`, `next_run`, `status` (active/paused), `last_result` (success/error)

### Health Checks
- `id`, `service` (gateway/telegram/skills), `status` (healthy/degraded/down), `last_check`, `uptime_%`

### Agent Stats (metrics)
- `id`, `date`, `messages_sent`, `skills_used`, `errors`, `model_tokens_used`, `uptime_hours`

Help me create these structures in the chosen tool.

## 5. Connect the agent to the panel

After setup, **create the necessary functions**:

### Functions the agent needs:
- `dashboard_log_task(title, priority)` — creates a task in the panel
- `dashboard_update_task(id, status)` — marks as done/blocked
- `dashboard_log_memory(content, category)` — saves important insight
- `dashboard_update_health(service, status)` — updates service status
- `dashboard_get_stats()` — returns daily summary

### Required crons (isolated + agentTurn):
- **stats-collector** (every 1h): Collects metrics (uptime, errors, skills used) and writes to the panel
- **health-monitor** (every 15min): Tests whether gateway/telegram/skills are responding
- **task-reminder** (every 4h): Checks tasks with upcoming due_date and notifies

Help me create these crons and functions.

## 6. Customize the panel for my profile

Based on my USER.md and my work (founder/dev/creator/productivity), **customize what is shown**:

**If I'm a Founder:**
- Business metrics (MRR, active users, churn)
- Sales pipeline
- Weekly OKRs

**If I'm a Dev:**
- Recent deploys
- Critical errors (via Sentry)
- Pending PRs for review
- Service uptime

**If I'm a Creator:**
- Content published this week
- Performance (views, engagement)
- Production pipeline (ideas → script → recording → editing → published)

**If I'm Productivity:**
- Today's meetings
- Completed vs. pending tasks
- Tracked habits
- Deep work time

Ask me what my profile is and suggest specific widgets.

## 7. Run the first test

After everything is configured:
1. Ask the agent to log a test task
2. Open the panel and confirm it appeared
3. Mark it as "done" via the agent
4. Refresh the panel and see the change
5. Verify that crons are running (check logs)

## 8. Document the setup

Create a file `docs/mission-control-setup.md` with:
- Chosen tool and why
- Required credentials (where they are stored)
- Data structure
- How to access the panel (URL, login)
- Useful commands (reset data, backup, etc.)
- Screenshots (if relevant)

**Important rules:**
- ❌ Don't hardcode credentials — everything in `.env` or 1Password
- ✅ Use `isolated` + `agentTurn` crons to update data (never systemEvent in main)
- ✅ Test in production slowly — start with read-only, then add write
- ✅ Make a backup before connecting a critical system to the panel

---

**Shall we build your Mission Control?** Tell me your technical level and preferences, and I'll guide you!
