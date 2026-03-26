# Student Prompt — Bonus Lesson: Community Report

> Copy, adapt the parts in brackets, and send to your OpenClaw agent.

---

## Main Prompt

```
I want to create an automatic weekly report of my community's messages.

**My data source:**
[Describe where the messages are stored. Examples:
- "I have a Supabase with a 'messages' table. Fields: created_at, content, user_name, chat_id"
- "I use MyGroupMetrics — my user_owner is [your ID]"
- "I have access to the Crisp API with workspace_id [your ID]"
- "I have a CSV exported from the group — I can upload it"]

**Groups/channels to analyze:**
[List the groups or channels. Examples:
- "WhatsApp Students Group — chat_id: 120363xxxxxxxx"
- "Telegram Clients Channel — @mychannel"
- "Crisp Workspace — all tickets"]

**Credentials:**
[Are the credentials in 1Password? If so, provide the item name and vault.
If not, let me know and I'll guide you to store them before continuing.]

**What I want in the report:**
- Overall sentiment for the week (positive / negative / neutral)
- Most frequent questions and topics
- Peak activity times
- Who helps others the most (potential ambassadors)
- Comparison with previous weeks

**Delivery format:**
- Dark theme HTML with visual charts
- Converted to PDF
- Sent here on Telegram every Monday at 9am

**What I need you to do:**
1. Create a Skill in skills/research/report-[community-name]/ with the entire process documented
2. Test the connection to my data source
3. Generate the first report now so I can see how it looks
4. Create the cron to run automatically every Monday at 9am

GUARDRAIL: read-only access to data. No writing, updating, or deletion without my explicit authorization.
```

---

## Variations by Data Source

### If you use MyGroupMetrics (Supabase MGM)

```
My data source is the MyGroupMetrics Supabase.
Credentials are in 1Password under the name "Supabase MGM", vault "Amora Vault".
Relevant fields from the interactions table: created_at, message, user_name, chat_id, response_to.

My groups:
- [Group name 1] — chat_id: [WhatsApp group ID]
- [Group name 2] — chat_id: [WhatsApp group ID]

My group_owner in the database is: [your user ID in MGM]
```

### If you use Crisp

```
My data source is Crisp.
Credentials (website_id and token) are in 1Password as "Crisp API", vault "Amora Vault".
I want to analyze all conversations from the last 30 days in the workspace.
```

### If you have your own Supabase

```
I have my own Supabase.
URL and service_key are in 1Password as "[Item Name]", vault "[Vault Name]".
Table: [table name]
Fields: [created_at or equivalent], [text field], [user field], [group/channel field if available]
```

### If you only have a CSV

```
I have a CSV file with the group's history.
I'll upload it now. After analyzing it, I want you to create a process so I can update the CSV every week and generate the new report.
Fields in the CSV: [list the columns]
```

---

## What to Expect After Sending the Prompt

The agent will:

1. **Confirm the connection** — it will test access to your data source and tell you how many messages it found
2. **Create the Skill** — it will document the entire process in `skills/research/report-[name]/SKILL.md`
3. **Generate the first report** — HTML + PDF directly in the chat for you to view and approve
4. **Create the cron** — it will check if Monday at 9am is free and configure the schedule

If something doesn't work (wrong credential, different table structure), the agent will ask for the missing information before continuing.

---

## Tips

**Calibrate sentiment for your niche**

After the first report, if the percentages don't seem right, ask:
```
The positive sentiment is too high / too low.
Show me which messages were classified as positive and negative.
I want to adjust the word dictionary.
```

**Add topics specific to your area**

```
I want the report to also identify messages about [your specific topic].
Keywords: [list of words]
```

**Change the frequency**

```
Instead of weekly, I want a monthly report — on the 1st of every month at 8am.
Adjust the cron to: 0 8 1 * *
```
