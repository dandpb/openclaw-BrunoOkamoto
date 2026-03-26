# Useful Cron Examples

> Copy and adapt. All use isolated + agentTurn (the approach that works).

## 📅 Schedule Check (daily, 8am)

```json
{
  "name": "Check Agenda",
  "schedule": { "kind": "cron", "expr": "0 8 * * *", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Check Google Calendar for today and tomorrow. If there are appointments, notify on Telegram with times and context.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## 🔍 Cron Watchdog (daily, 8:30am)

```json
{
  "name": "Watchdog - Cron Monitor",
  "schedule": { "kind": "cron", "expr": "30 8 * * *", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "List all crons. Check the last run of each one. If any failed in the last 24h, try to re-execute. If it fails again, alert on Telegram.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## 📊 Weekly Review (Friday, 4pm)

```json
{
  "name": "Weekly Review",
  "schedule": { "kind": "cron", "expr": "0 16 * * 5", "tz": "America/Sao_Paulo" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Do weekly review: 1) Read daily notes from the week 2) Consolidate into topic files 3) Update MEMORY.md 4) List pending items 5) Report summary on Telegram.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## ⏰ One-shot Reminder (example)

```json
{
  "name": "Reminder: Meeting with Someone",
  "schedule": { "kind": "at", "at": "2026-02-15T09:00:00-03:00" },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Reminder: Meeting with Someone in 30 minutes. Send message on Telegram.",
    "model": "anthropic/claude-sonnet-4-5"
  },
  "delivery": { "mode": "announce" }
}
```

## 🔴 Important Tips

1. **Always** use `model: "anthropic/claude-sonnet-4-5"` (full name, not alias)
2. **Space** crons by 15-30 min (avoids rate limit)
3. **Never** use `sessionTarget: "main"` with `systemEvent` (doesn't work properly)
4. **Test** with `cron run <id>` before trusting it will work
