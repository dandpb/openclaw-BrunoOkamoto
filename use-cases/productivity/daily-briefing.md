# ☀️ Use Case: Daily Briefing

> Wake up every day with a summary of what needs attention.

## What it does

Automatic cron that runs every morning and consolidates:
- Today's schedule (events in the next 24h)
- Urgent unread emails
- Business metrics (if configured)
- Social media (performance of recent posts)
- Projects with approaching deadlines
- Pending reminders

## Setup prompt

```
I want you to create an automatic Daily Briefing that runs every day at [TIME] in the morning.

The briefing should include:
1. 📅 **Schedule** — today's and tomorrow's events (Google Calendar)
2. 📧 **Emails** — urgent unread messages (if Gmail integrated)
3. 📊 **Metrics** — quick business summary (if integrated)
4. 📱 **Social media** — performance of recent posts
5. 📋 **Projects** — status of active projects, alert upcoming deadlines
6. ⏰ **Reminders** — pending items I asked to be reminded of

Format:
- Maximum 10 lines — I'm busy, I want to be quick
- If there's nothing urgent, say "Quiet day 😎" and that's it
- If there's something urgent, highlight with ⚠️
- Deliver on [TELEGRAM/WHATSAPP]

Set up as a cron with:
- sessionTarget: isolated
- payload: agentTurn
- delivery: announce
- model: Sonnet (no need for Opus for this)
```

## Output example

```
☀️ Briefing — Tuesday 02/18

📅 2pm: Call with investor (Zoom)
📅 5pm: Reminder to record YouTube video

📊 MRR: R$8.2k (+1.5% week) ✅
⚠️ 3 pending failed payments (R$347)

📱 Yesterday's LinkedIn post: 2.3k views, 89 likes — above average

📋 Content Waterfall project: 3 pieces pending approval

Productive day ahead! 🚀
```
