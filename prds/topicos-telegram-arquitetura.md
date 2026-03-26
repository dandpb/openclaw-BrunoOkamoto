# Complete Guide: Telegram Topics + Agent Architecture

**Objective:** Teach how to create and organize topics on Telegram, configure agents to respond without mention, and understand the architectural differences between **one shared MAIN agent** vs **isolated agents per topic**.

---

## 📱 Part 1: Creating Topics on Telegram

### What Are Topics?

Topics are **organized threads within a group**. Each topic works as a separate channel, but all are in the same group.

**When to use:**
- Separate different projects
- Organize conversations by subject (support, dev, ideas)
- Have specialized agents per context

### Step by Step: Creating a Group with Topics

#### 1. Create the Group

1. Open Telegram
2. Menu → **New Group**
3. Name: `Amora HQ` (or whatever you prefer)
4. Add at least 1 person (yourself can be enough)
5. Finish creation

#### 2. Convert to Supergroup

1. Open the **group settings** (click the name)
2. **Group Type** → **Public Group** (or keep private)
3. Set a `@username` for the group (e.g., `@amorahq_bruno`)
4. Telegram automatically converts to **Supergroup**

> ⚠️ **Important:** Only supergroups support topics!

#### 3. Enable Topics

1. Group settings → **Topics**
2. Toggle **"Enable Topics"**
3. Telegram automatically creates the **"General"** topic (id: `1`)

#### 4. Create Additional Topics

1. On the group screen, click the **topics icon** (top corner)
2. **"Create Topic"**
3. Give it a name: `OpenClaw Course`, `Support`, `Dev`, etc.
4. Choose an icon/emoji
5. Done! Each topic has a **unique ID** (e.g., `2638`, `2640`)

---

## 🤖 Part 2: Adding Agents to Topics

### Option A: Add the Bot to the Group

1. Go to **@BotFather**
2. `/mybots` → choose your bot
3. **Bot Settings → Group Privacy → Turn off "Privacy Mode"**
   - This allows the bot to see **all messages** in the group
4. Add the bot to the group: `@yourbothere`
5. Make it **admin** (necessary to act in topics)

### Option B: Use Existing Bot (without admin)

If the bot is NOT admin, it only responds when **mentioned** (`@bot message`).

---

## ⚙️ Part 3: Configuring Agents to Respond WITHOUT Mention

By default, Telegram bots only respond when mentioned. To enable **automatic response in specific topics**, you need to configure in `config.yaml`.

### Config Structure

```yaml
agents:
  - id: amora-main
    model: anthropic/claude-sonnet-4-6
    thinking: off
    workspaceDir: /root/.openclaw/workspace-amora
    
    activation:
      surfaces:
        - surface: telegram
          mode: mention  # Global default: only when mentioned
          
          overrides:
            # Topic "OpenClaw Course" — responds to EVERYTHING
            - chat: "telegram:-1003873964847:topic:2638"
              mode: all
            
            # Topic "Support" — responds to EVERYTHING
            - chat: "telegram:-1003873964847:topic:2640"
              mode: all
            
            # Topic "General" — only when mentioned
            - chat: "telegram:-1003873964847:topic:1"
              mode: mention
```

### How to Find the Chat ID

1. Send a message **in the topic** mentioning the bot
2. On the VPS terminal: `openclaw logs --tail 50`
3. Look for: `chat_id: "telegram:-1003873964847:topic:2638"`
4. Copy this ID and paste in the config

### Apply the Config

```bash
openclaw gateway restart
```

Now Amora responds **automatically** in topics configured with `mode: all`.

---

## 🏗️ Part 4: Agent Architecture — MAIN vs Isolated

Here is the **most important decision** of the course: how to organize your agents?

---

### 🔵 Architecture 1: **ONE Shared MAIN Agent**

**How it works:**
- **1 agent** (`amora-main`) responds in **multiple topics**
- All topics share:
  - Same **workspace**
  - Same **memory** (`MEMORY.md`, `memory/2026-02-25.md`)
  - Same **crons** (heartbeats, reminders)
  - Same **SOUL.md**, **USER.md**, **TOOLS.md**

**Example config:**

```yaml
agents:
  - id: amora-main
    workspaceDir: /root/.openclaw/workspace-amora
    activation:
      surfaces:
        - surface: telegram
          mode: mention
          overrides:
            - chat: "telegram:-1003873964847:topic:2638"  # Course
              mode: all
            - chat: "telegram:-1003873964847:topic:2640"  # Support
              mode: all
            - chat: "telegram:-1003873964847:topic:1"     # General
              mode: mention
```

#### ✅ Advantages

1. **Total continuity** — Amora remembers EVERYTHING that happened in all topics
2. **Resource savings** — 1 process, 1 workspace, 1 memory
3. **Single crons** — Heartbeats, reminders, backups run only once
4. **Cross-context** — "That file you created in topic X" works
5. **Easy setup** — Only one agent to configure

#### ❌ Disadvantages

1. **Polluted context** — Conversations from different topics mix in history
2. **No isolation** — If someone messes up in one topic, it affects the whole workspace
3. **Context explodes fast** — Multiple active topics = 100k tokens in days
4. **Zero privacy** — Amora can mention things from a private topic in a public one
5. **Single behavior** — Can't have "Technical Amora" vs "Creative Amora"

#### 🎯 When to use

- **You're the only human** using the topics
- You want **total continuity** between conversations
- Topics are **variations of the same context** (related projects)
- You don't care about **memory bleed** between topics

---

### 🟢 Architecture 2: **Isolated Agents per Topic**

**How it works:**
- **Each topic has its own agent** (`amora-course`, `amora-support`, `amora-dev`)
- Each agent has:
  - **Separate workspace** (`/workspace-course`, `/workspace-support`)
  - **Isolated memory** (each has its own `MEMORY.md`)
  - **Independent crons** (each can have different heartbeats)
  - **Custom SOUL.md** (specialized behavior)

**Example config:**

```yaml
agents:
  # Agent for topic "OpenClaw Course"
  - id: amora-course
    model: anthropic/claude-sonnet-4-6
    workspaceDir: /root/.openclaw/workspace-course
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2638"
              mode: all
  
  # Agent for topic "Support"
  - id: amora-support
    model: anthropic/claude-haiku-4-5  # Cheaper
    workspaceDir: /root/.openclaw/workspace-support
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2640"
              mode: all
  
  # Agent for topic "Dev"
  - id: amora-dev
    model: anthropic/claude-opus-4-6  # More powerful
    thinking: on
    workspaceDir: /root/.openclaw/workspace-dev
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2641"
              mode: all
```

#### ✅ Advantages

1. **Total isolation** — Each topic has its own sandbox
2. **Specialization** — Support agent uses Haiku (cheap), Dev uses Opus (powerful)
3. **Custom SOUL.md** — "Teacher Amora" in course, "DevOps Amora" in support
4. **Privacy** — Data from one topic **never leaks** to another
5. **Clean context** — Each agent only sees messages from its topic
6. **Granular control** — Different crons per agent (e.g., heartbeat only in support)
7. **Scalability** — Adding a new topic = new agent, without polluting existing ones

#### ❌ Disadvantages

1. **Zero continuity** — Agents don't know what happened in other topics
2. **Higher cost** — Multiple processes running (more RAM, more API calls)
3. **Duplicated crons** — If 3 agents have heartbeat, they run 3x
4. **Complex setup** — Need to create workspace + config for each agent
5. **No sharing** — File created in topic X doesn't exist in Y

#### 🎯 When to use

- **Multiple humans** using different topics
- You need **privacy between topics** (client A vs client B)
- You want **specialized behaviors** (support vs development)
- Topics have **completely different contexts**
- You want **different models per topic** (Haiku for support, Opus for dev)

---

## 📊 Direct Comparison

| Aspect | Shared MAIN | Isolated Agents |
|---------|------------|-----------------|
| **Memory** | Shared between topics | Isolated per topic |
| **Workspace** | 1 single workspace | 1 workspace per agent |
| **SOUL.md** | Global behavior | Customized per topic |
| **USER.md** | 1 human, unified context | Can have different USER.md |
| **TOOLS.md** | Global tools | Tools per agent |
| **Crons** | Run 1x (shared) | Run N times (per agent) |
| **Heartbeats** | 1 global heartbeat | 1 heartbeat per agent |
| **Context** | Crosses between topics | Never crosses |
| **Privacy** | Zero — everything leaks | Total — complete isolation |
| **Cost (API)** | Cheaper | More expensive |
| **Cost (RAM)** | 1 process | N processes |
| **Setup** | Simple (1 agent) | Complex (N agents) |
| **Ideal use** | Related projects | Isolated contexts |

---

## 🛠️ Part 5: Advanced Configuration

### Hybrid: MAIN + Specialized Agents

You can **mix** both architectures:

```yaml
agents:
  # MAIN Agent — responds in private and "General"
  - id: amora-main
    workspaceDir: /root/.openclaw/workspace-amora
    activation:
      surfaces:
        - surface: telegram
          mode: mention  # Default: only when mentioned
          overrides:
            - chat: "telegram:1983085858"  # Private with Bruno
              mode: all
  
  # Specialized agent — only in "Course" topic
  - id: amora-course
    model: anthropic/claude-sonnet-4-6
    workspaceDir: /root/.openclaw/workspace-course
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2638"
              mode: all
  
  # Specialized agent — only in "Support" topic
  - id: amora-support
    model: anthropic/claude-haiku-4-5
    workspaceDir: /root/.openclaw/workspace-support
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2640"
              mode: all
```

**Advantages:**
- MAIN maintains personal context (private with you)
- Specialized agents stay isolated
- Best of both worlds

---

## 🧠 Part 6: Impact on Memory and Context

### Scenario 1: Shared MAIN

**Memory structure:**

```
/root/.openclaw/workspace-amora/
├── MEMORY.md               ← Global context (read in ALL sessions)
├── memory/
│   ├── 2026-02-25.md       ← Daily log (mixes ALL topics)
│   ├── 2026-02-26.md
```

**When Amora responds in the "Course" topic:**
1. Reads `MEMORY.md` (global context)
2. Reads `memory/2026-02-25.md` (conversations from ALL topics)
3. Responds with **complete context**

**Problem:**
- If you talked about "secret project X" in the "Dev" topic in the morning
- And someone asks in the "Course" topic in the afternoon
- Amora **might mention the secret project** (memory bleed)

---

### Scenario 2: Isolated Agents

**Memory structure:**

```
/root/.openclaw/workspace-course/
├── MEMORY.md               ← Course context ONLY
├── memory/
│   ├── 2026-02-25.md       ← Course topic log ONLY

/root/.openclaw/workspace-support/
├── MEMORY.md               ← Support context ONLY
├── memory/
│   ├── 2026-02-25.md       ← Support topic log ONLY
```

**When amora-course responds:**
1. Reads `MEMORY.md` from workspace-course
2. Reads `memory/2026-02-25.md` from workspace-course
3. **Does NOT have access** to workspace-support

**Benefit:**
- Zero context leakage
- Each agent only knows what happened in its topic

---

## 🔄 Part 7: Impact on Crons

### Shared MAIN

```yaml
# /root/.openclaw/config.yaml
cron:
  jobs:
    - name: "Global Heartbeat"
      schedule:
        kind: every
        everyMs: 1800000  # 30 min
      payload:
        kind: systemEvent
        text: "Read HEARTBEAT.md if it exists..."
      sessionTarget: main
      delivery:
        mode: announce
        channel: telegram
        to: "1983085858"  # Private with Bruno
```

**How it works:**
- Runs **once every 30 min**
- Uses the **global workspace** (`/workspace-amora`)
- Can check things from **all topics** (emails, calendar, etc.)
- Saves API calls (1 heartbeat vs 3)

---

### Isolated Agents

```yaml
cron:
  jobs:
    # "Course" agent heartbeat
    - name: "Course Heartbeat"
      schedule:
        kind: every
        everyMs: 3600000  # 60 min
      payload:
        kind: agentTurn
        message: "Check for new questions in the course"
        agentId: amora-course
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "-1003873964847:topic:2638"
    
    # "Support" agent heartbeat
    - name: "Support Heartbeat"
      schedule:
        kind: every
        everyMs: 1800000  # 30 min
      payload:
        kind: agentTurn
        message: "Check pending tickets"
        agentId: amora-support
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "-1003873964847:topic:2640"
```

**How it works:**
- Each agent has **its own heartbeat**
- They run on **separate workspaces**
- **More API calls**, but **focused context**

---

## 🧪 Part 8: Real Use Cases

### Case 1: Freelancer with Multiple Clients

**Problem:** Need to separate context for each client (privacy).

**Solution:** Isolated agents

```yaml
agents:
  - id: amora-client-a
    workspaceDir: /workspace-client-a
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2638"
              mode: all
  
  - id: amora-client-b
    workspaceDir: /workspace-client-b
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2640"
              mode: all
```

**Benefits:**
- Client A **never sees** Client B's data
- Custom SOUL.md per client (e.g., "Speak formally with Client A")
- Different models (Haiku for support, Opus for dev)

---

### Case 2: Related Personal Projects

**Problem:** You work on 3 projects, but they're all yours (e.g., blog, app, course).

**Solution:** Shared MAIN

```yaml
agents:
  - id: amora-main
    workspaceDir: /workspace-amora
    activation:
      surfaces:
        - surface: telegram
          mode: mention
          overrides:
            - chat: "telegram:-1003873964847:topic:1"    # Blog
              mode: all
            - chat: "telegram:-1003873964847:topic:2"    # App
              mode: all
            - chat: "telegram:-1003873964847:topic:3"    # Course
              mode: all
```

**Benefits:**
- Amora remembers EVERYTHING (useful cross-context)
- "That idea for the app we discussed yesterday" works in the blog topic
- Saves resources (1 process)

---

### Case 3: Hybrid — Personal + Professional

**Problem:** You want **privacy** between work and personal life.

**Solution:** Hybrid

```yaml
agents:
  # Personal agent — private + "Life" topic
  - id: amora-personal
    workspaceDir: /workspace-personal
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:1983085858"                # Private
              mode: all
            - chat: "telegram:-1003873964847:topic:1"    # "Life" topic
              mode: all
  
  # Professional agent — "Work" topic
  - id: amora-work
    model: anthropic/claude-opus-4-6
    workspaceDir: /workspace-work
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2"    # "Work" topic
              mode: all
```

**Benefits:**
- Zero leakage between personal life and work
- Different models (Haiku personal, Opus professional)
- Specialized behavior (different SOUL.md)

---

## 🚨 Part 9: Common Pitfalls

### Pitfall 1: Mixing Chat IDs

**Error:**
```yaml
- chat: "telegram:-1003873964847"  # Group ID (without :topic:)
  mode: all
```

**Result:** Amora responds in **ALL topics** of the group (chaos).

**Fix:**
```yaml
- chat: "telegram:-1003873964847:topic:2638"  # Specific topic ID
  mode: all
```

---

### Pitfall 2: Forgetting to Make Bot Admin

**Error:** Adding bot to the group but **not giving admin permissions**.

**Result:** Bot can't read messages in topics (only in "General").

**Fix:**
1. Group settings → **Administrators**
2. Add the bot
3. Enable permission: **"Manage Topics"**

---

### Pitfall 3: Isolated Agents Sharing Workspace

**Error:**
```yaml
agents:
  - id: amora-course
    workspaceDir: /workspace-amora  # ❌ Same workspace
  - id: amora-support
    workspaceDir: /workspace-amora  # ❌ Same workspace
```

**Result:** Agents step on each other (overwritten files, shared memory).

**Fix:**
```yaml
agents:
  - id: amora-course
    workspaceDir: /workspace-course  # ✅ Isolated workspace
  - id: amora-support
    workspaceDir: /workspace-support  # ✅ Isolated workspace
```

---

### Pitfall 4: Crons on the Wrong Agent

**Error:** Creating a cron for `amora-course` but trying to access data from `amora-support`.

**Result:** Cron can't find the files (different workspaces).

**Fix:** Make sure the cron **uses the correct agentId**:

```yaml
cron:
  jobs:
    - name: "Check course"
      payload:
        kind: agentTurn
        message: "Check new questions"
        agentId: amora-course  # ✅ Uses the correct workspace
```

---

## 📝 Part 10: Decision Checklist

### Questions to ask yourself:

1. **Is privacy critical?**
   - ❌ No → Shared MAIN
   - ✅ Yes → Isolated agents

2. **Do the topics have related contexts?**
   - ✅ Yes (e.g., personal projects) → Shared MAIN
   - ❌ No (e.g., different clients) → Isolated agents

3. **Do you need specialized behaviors?**
   - ❌ No → Shared MAIN
   - ✅ Yes (e.g., Teacher Amora vs DevOps) → Isolated agents

4. **Do you want to save resources (RAM/API)?**
   - ✅ Yes → Shared MAIN
   - ❌ No → Isolated agents

5. **Is cross-context useful or dangerous?**
   - Useful (e.g., "remember that idea?") → Shared MAIN
   - Dangerous (e.g., data leakage) → Isolated agents

---

## 🎯 Final Recommendation

**For beginners:**
- Start with **Shared MAIN**
- It's simpler, more economical, and "just works"
- Migrate to isolated when you feel the pain (context pollution, privacy)

**For advanced users:**
- Use **isolated agents** from the start
- Costs more, but scales better
- Especially if you work with multiple clients/projects

**For most people:**
- **Hybrid** is the sweet spot
- MAIN for personal context
- Isolated for professional/private contexts

---

## 🛠️ Part 11: Complete Setup Example

### Group Structure

```
Amora HQ (Telegram Group)
├── 📌 General (id: 1) — only when mentioned
├── 📚 OpenClaw Course (id: 2638) — isolated agent, responds to everything
├── 🛠️ Support (id: 2640) — isolated agent, responds to everything
└── 💬 Bruno Private (chat: 1983085858) — MAIN, responds to everything
```

### Complete Config

```yaml
# /root/.openclaw/config.yaml

agents:
  # MAIN Agent — private with Bruno
  - id: amora-main
    model: anthropic/claude-sonnet-4-6
    thinking: off
    workspaceDir: /root/.openclaw/workspace-amora
    activation:
      surfaces:
        - surface: telegram
          mode: mention
          overrides:
            - chat: "telegram:1983085858"  # Private
              mode: all

  # Course Agent — isolated
  - id: amora-course
    model: anthropic/claude-sonnet-4-6
    thinking: off
    workspaceDir: /root/.openclaw/workspace-course
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2638"
              mode: all

  # Support Agent — isolated, cheaper model
  - id: amora-support
    model: anthropic/claude-haiku-4-5
    thinking: off
    workspaceDir: /root/.openclaw/workspace-support
    activation:
      surfaces:
        - surface: telegram
          overrides:
            - chat: "telegram:-1003873964847:topic:2640"
              mode: all

cron:
  jobs:
    # MAIN Heartbeat — only for Bruno
    - name: "Personal Heartbeat"
      schedule:
        kind: every
        everyMs: 1800000  # 30 min
      payload:
        kind: systemEvent
        text: "Read HEARTBEAT.md..."
      sessionTarget: main
      delivery:
        mode: announce
        channel: telegram
        to: "1983085858"
    
    # Course Heartbeat — checks every 1h
    - name: "Course Heartbeat"
      schedule:
        kind: every
        everyMs: 3600000
      payload:
        kind: agentTurn
        message: "Check for new questions in the course"
        agentId: amora-course
      sessionTarget: isolated
      delivery:
        mode: announce
        channel: telegram
        to: "-1003873964847:topic:2638"
```

### Workspace Structure

```
/root/.openclaw/
├── workspace-amora/           # MAIN (personal)
│   ├── SOUL.md                # "Be intimate, casual, use slang"
│   ├── USER.md                # Bruno's context
│   ├── MEMORY.md              # Personal memory
│   ├── memory/
│   │   └── 2026-02-25.md
│   └── HEARTBEAT.md           # Personal checks
│
├── workspace-course/           # Isolated agent
│   ├── SOUL.md                # "Be a teacher, didactic, patient"
│   ├── USER.md                # Student profiles
│   ├── MEMORY.md              # Common questions, course decisions
│   ├── memory/
│   │   └── 2026-02-25.md
│   └── HEARTBEAT.md           # Check for new questions
│
└── workspace-support/         # Isolated agent
    ├── SOUL.md                # "Be technical, objective, fast"
    ├── USER.md                # Client profiles
    ├── MEMORY.md              # Resolved tickets, known bugs
    ├── memory/
    │   └── 2026-02-25.md
    └── HEARTBEAT.md           # Check pending tickets
```

---

## 🎓 Conclusion

### Summary of the Summary

**Shared MAIN = Total Memory, Zero Privacy**
- Use when cross-context is desirable
- Saves resources
- Ideal for related personal projects

**Isolated Agents = Total Privacy, Zero Cross-Memory**
- Use when cross-context is dangerous
- Costs more resources
- Ideal for multiple clients/contexts

**Hybrid = Best of Both Worlds**
- MAIN for personal use
- Isolated for professional contexts
- Recommended for most cases

---

**Next Steps:**
1. Decide which architecture to use
2. Create the topics on Telegram
3. Configure the `config.yaml`
4. Test each topic
5. Adjust each agent's SOUL.md
6. Configure crons (if necessary)

**Questions?**
- Review the **Decision Checklist** section
- Test with 1-2 topics first
- Migrate gradually if you need to change architecture

---

**Last tip:** There's no "wrong architecture" — there's the one that works **for you**. Test, learn, adjust. That's how you build a custom system.
