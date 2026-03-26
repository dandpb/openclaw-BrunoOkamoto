# Prompt — Extra Lesson A: Integrating Your Tools

> Paste this prompt in your agent chat after watching Extra Lesson A.

---

I just watched the lesson on tool integration. Now I want to connect my agent to the tools I use daily.

**What I need to do:**

## 1. Map my tools

Help me list the tools/platforms I use most:
- Project management? (Notion, Trello, Asana, Monday...)
- Payments? (Stripe, PayPal, Mercado Pago...)
- Analytics? (Google Analytics, Mixpanel, Amplitude...)
- CRM/Sales? (HubSpot, Pipedrive, RD Station...)
- Email marketing? (ConvertKit, Mailchimp...)
- Social media? (Buffer, Later, Hootsuite...)
- Other critical tools?

For each one, tell me:
- ✅ Is there a ready-made skill on ClawHub? (`clawhub search name`)
- ❌ Needs direct API integration?

## 2. Install ready-made skills

For tools that **have a ready-made skill**, guide me to:
1. Install the skill (`clawhub install name`)
2. Configure credentials (if necessary)
3. Test if it works
4. Document in TOOLS.md

## 3. Integrate direct APIs

For tools **without a ready-made skill**, guide me to:
1. Find where the API key is in the tool
2. Store it in 1Password (or teach me how to set up 1Password if I don't have it)
3. Test the API with you
4. Document in TOOLS.md with:
   - Integration name
   - Item in 1Password
   - Permissions (read/write)
   - Limitations or guardrails

## 4. Document everything in TOOLS.md

Create or update my `TOOLS.md` with:
- List of all active integrations
- How to access each one
- Security guardrails (what you can/cannot do)

## 5. Practical use cases

After everything is configured, suggest **3 practical use cases** to test the integrations. Examples:
- "Show me my current MRR from Stripe"
- "List Notion tasks with status 'In Progress'"
- "How many site visits did we get yesterday?"

**Important rules:**

🔴 **NEVER** put API keys directly in code or config — always 1Password
🔴 **ALWAYS** ask me before performing write operations (create, update, delete)
🔴 **ALWAYS** document in TOOLS.md when adding a new integration

**If I don't have 1Password installed:**
Explain how to install and configure it (or suggest alternatives like Bitwarden).

---

Let's start by mapping my tools. Ask me the questions and we'll integrate them one by one.
