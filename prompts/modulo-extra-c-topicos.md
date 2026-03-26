# Student Prompt: Telegram Topics + Agent Architecture

**Paste this prompt in your chat with your Amora:**

---

Amora, I need your help to set up topics in Telegram and understand the difference between having a shared MAIN agent vs. isolated agents.

**Tasks:**

1. **Guide me through creating topics in Telegram:**
   - How to convert my group into a supergroup
   - How to enable and create topics
   - How to find the chat ID of each topic

2. **Configure you to respond without a mention in specific topics:**
   - Show how to edit `config.yaml` so you respond automatically
   - Explain `mode: mention` vs `mode: all`
   - Test if it worked

3. **Explain the two architectures:**
   - **Shared MAIN** — one agent responding across multiple topics
   - **Isolated agents** — one agent per topic
   - Pros and cons of each
   - When to use each one

4. **Impact on:**
   - Workspace (where are the files?)
   - Memory (shared or isolated MEMORY.md?)
   - Crons (shared or isolated heartbeats?)
   - SOUL.md, USER.md, TOOLS.md (global or per agent?)

5. **Help me decide which architecture to use:**
   - Ask me questions about my use case
   - Recommend the best option
   - Show a complete config example

**Context about me:**
- [Describe here: do you work alone? do you have multiple clients? do you need privacy between topics? related or isolated projects?]

**Example:**
> "I'm a freelancer with 3 clients. Each client has a topic in my Telegram group. I need data from one client to NEVER appear to another."

---

**Read the complete guide at:**
`/root/.openclaw/workspace-curso-openclaw/prds/topicos-telegram-arquitetura.md`

**After configuring:**
- Test by sending messages to the topics
- Verify that you respond automatically (when `mode: all`)
- Confirm that each isolated agent **does not see** the other agents' workspaces
- Adjust the SOUL.md of each agent (if isolated)

**If something goes wrong:**
- `openclaw logs --tail 100` to see errors
- `openclaw gateway restart` to apply config changes
- Message me in private and I'll help you

Ready to start?
