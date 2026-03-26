# PRD — Bonus Lesson: Community Report with AI

> **Level:** Intermediate
> **Estimated Duration:** 15–18 minutes
> **Prerequisites:** OpenClaw installed, at least one group connected to MyGroupMetrics (or any message data source)

---

## 🎯 Lesson Objective

By the end of this lesson, the student will understand that OpenClaw can:

1. Connect to any database with messages (Supabase, REST API)
2. Automatically analyze the community's mood, questions, and patterns
3. Generate a complete visual report — HTML + PDF — without writing a single line of code manually
4. Deliver that report right to your inbox, every week, without any interaction

**Lesson angle:** The result first. The code is just proof that it's simple.

---

## 📋 Recording Script — Section by Section

---

### 🎬 OPENING (0:00 – 1:30)

**[Bruno on screen with the report PDF open on the side]**

> "Hey everyone. Look at this PDF right here."

> "This report arrived for me yesterday morning, without me asking for anything. It shows me: community mood this week, which questions came up most often, what times the group is most active, who are the students helping others the most."

> "14,725 messages analyzed. Four WhatsApp groups. Four weeks of data. And I did absolutely nothing."

> "In this lesson I'm going to show you how I did this — and more importantly: how you'll do the same for your community."

---

### 📊 SECTION 1: The problem this solves (1:30 – 4:00)

**[Bruno on camera, conversational tone]**

> "Let me ask you a quick question."

> "Do you have a WhatsApp group for students, clients, community? How many messages per week? 200? 500? 2,000?"

> "Now tell me: can you answer these questions without opening the group right now?"

**[Show on screen — slide with the 4 questions]**

> "What was the community's mood this week — are people excited or frustrated?"
> "Which question came up more than three times in the last 7 days?"
> "What time of day does the group engage most — when should I pin announcements?"
> "Who are the members that help others the most — my potential moderators?"

> "Most creators can't answer any of the four. Because those answers are buried in thousands of messages."

> "OpenClaw reads all of that, analyzes it, and delivers the answers every Monday morning."

---

### 🔁 SECTION 2: How it works in 3 steps (4:00 – 7:00)

**[Screen: simple diagram with 3 blocks]**

> "The entire process has three parts. And each part the agent does on its own."

**Step 1 — Fetch the data**

> "The agent connects to your database — in my case it's the MyGroupMetrics Supabase. It fetches all messages from the last 30 days. With pagination, because large databases return data in chunks."

> "Result: 14,725 messages in a JSON file in the agent's memory."

**Step 2 — Analyze**

> "With the data in hand, the agent applies analyses. Sentiment: which messages are positive, which are negative, with real examples so you understand why. Topics: what comes up most — installation, errors, success stories, costs. Patterns: times, days of the week, who responds most, who goes quiet."

> "All of this without a machine learning library. Pure Python, a word dictionary calibrated for your context."

**Step 3 — Deliver**

> "The agent generates a complete HTML — dark theme, CSS charts, 14 sections — converts it to PDF via Chrome and sends it directly on Telegram. I receive the file here, and I can forward it to students if I want."

---

### 🧠 SECTION 3: The Skill — the process memory (7:00 – 10:00)

**[Screen: the SKILL.md file open in the editor]**

> "Now I'm going to show you the most important part. It's not the code — it's the Skill."

> "Every time the agent wakes up to generate the report, it reads this file here. The Skill is the process memory — it documents where to fetch the data, how to analyze it, what format to generate, where to save it, how to deliver it."

> "If I didn't have this, the agent would forget everything between one session and the next. With the Skill, it always does it the same way. Every week. Without variation."

**[Show the SKILL.md structure]**

> "Look at the structure: what the skill does, when to use it, the groups it analyzes with their IDs, how to fetch credentials from 1Password — never a hardcoded password —, the step-by-step process, and at the end: guardrail. Read-only. Zero writes to the database without authorization."

> "This is what transforms a task I did once into a process that runs forever."

---

### ⏰ SECTION 4: The Cron — set and forget (10:00 – 12:30)

**[Screen: cron list in the terminal or in the interface]**

> "With the Skill ready, creating the cron is the fastest part."

> "I asked the agent: 'Create a cron to run this skill every Monday at 9am.' It checked if the time slot was free, configured it, and that was it."

**[Show the cron config]**

> "Notice the detail: sessionTarget isolated. The task runs in a separate session — it doesn't pollute my main chat history. And the delivery: announce to the Telegram topic. The result arrives here, in the right group."

> "Since I set it up, I haven't had to think about it anymore. It arrives every Monday. I read it in two minutes. I have a complete overview of the week."

---

### 🌍 SECTION 5: Adapt to your context (12:30 – 15:30)

**[Bruno on camera]**

> "Now the question you're asking: 'Bruno, but I don't have MyGroupMetrics. Does this work for me?'"

> "Yes. You need three things:"

**[Show on screen — simple list]**

> "First: a data source with messages accessible via API — can be Supabase, Crisp, Zendesk, anything that has a REST endpoint."

> "Second: know which fields that table has — created_at, message, user. Three fields are already enough."

> "Third: ask the agent to create the Skill adapted to your context."

**[Show the student prompt on screen]**

> "There's a prompt in the lesson material. You copy it, adapt it with your data, send it to the agent. It will create the Skill, test the connection, generate the first report, and set up the cron. In less than an hour you have the process running."

> "Customer community, student group, support channel — anything that generates messages becomes actionable intelligence."

---

### 🎯 CLOSING (15:30 – 17:00)

**[Bruno on camera, closing tone]**

> "Let me summarize what happened here."

> "I had 14,725 messages I was never going to read. Now every Monday morning I know exactly what's happening in the community: what's blocking students, who's progressing, when the group pulses, what needs attention."

> "This isn't analysis — it's operational intelligence. It's the difference between managing a community in the dark and managing with data."

> "The entire process — connection, analysis, report, delivery — is documented in a one-page Skill. Runs automatically. Doesn't depend on me."

> "In the next lesson we'll see how to create Skills from scratch for any recurring process you want to automate. See you then."

---

## 🖥️ What to show on screen (screen guide)

| Moment | What to show |
|---------|--------------|
| Opening | Report PDF open — camera sees Bruno and the PDF side by side |
| Section 1 | Slide with the 4 questions most creators can't answer |
| Section 2 | Diagram: 3 blocks (Fetch → Analyze → Deliver) |
| Section 2 (detail) | Briefly: terminal showing "Total: 14,725 messages" |
| Section 3 | SKILL.md open in the editor — slow scroll |
| Section 4 | `cron list` in terminal + cron config |
| Section 5 | Student prompt (lesson material) on screen |
| Closing | Bruno on camera, direct wrap-up |

---

## ⚠️ Recording notes

- **Don't go into Python code details** — mention it exists, briefly show it if you want, but don't explain line by line
- **Show the real PDF** at the opening — the visual impact is the hook
- **Pronounce "MyGroupMetrics"** as the case study context, but make it clear it works with other sources
- **Mention pagination** only as "the agent knows how to fetch data in chunks" — no technical details
- **Guardrail** — briefly mention that the Skill has a read-only rule. Builds student confidence

---

## 📁 Lesson Files

| File | Drive Destination |
|---------|--------------|
| HTML material | Extra Lessons / Extra Lesson Materials / html/ |
| PDF material | Extra Lessons / Extra Lesson Materials / pdf/ |
| Student prompt | Extra Lessons / Extra Lesson Materials / |
| Sample report (PDF) | Extra Lessons / use-cases/ |
