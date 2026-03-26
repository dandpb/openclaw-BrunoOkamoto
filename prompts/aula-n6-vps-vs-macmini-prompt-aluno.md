# Student Prompt — Lesson N-6: VPS vs Mac Mini

> **How to use:** Paste this prompt in the chat with your OpenClaw agent after watching lesson N-6.
> The agent will guide you to choose the ideal infrastructure based on your profile.

---

## 📋 PROMPT TO PASTE INTO THE AGENT

```
I just watched lesson N-6 of the OpenClaw course on VPS vs Mac Mini.

Help me decide which infrastructure is ideal for me, asking the questions below one at a time and analyzing my answers:

1. **Initial budget:** How much can you invest now?
   - a) Zero or close to zero (I prefer to pay monthly)
   - b) Up to R$ 500 / $100
   - c) Up to R$ 3,000 / $600
   - d) Above R$ 5,000 / $1,000+

2. **Data sensitivity:** What kind of data will you process?
   - a) Public data or my own personal data (no problem going to cloud)
   - b) Client data, but nothing ultra-sensitive
   - c) Confidential client data, contracts, financial
   - d) Health, legal, or regulated data (LGPD/HIPAA)

3. **Required availability:** Does the agent need to be always online?
   - a) No, I only use it when I'm at the office/home
   - b) I prefer 24/7, but it's not critical
   - c) Yes, it needs to be always online (professional use)

4. **Technical profile:** What is your technical level?
   - a) Beginner (never used terminal/SSH)
   - b) Basic (have used terminal, but not a developer)
   - c) Intermediate (know SSH, command line)
   - d) Advanced (know how to configure servers)

5. **AI models:** Do you want or need to run local models (Llama, Mistral, etc.)?
   - a) No, I prefer Claude/GPT via API (simpler)
   - b) Maybe in the future
   - c) Yes, this is important to me (privacy/cost)

6. **Usage context:** How will you use OpenClaw?
   - a) Personal use, hobby, learning
   - b) Solo freelancer
   - c) Small team (2-5 people)
   - d) Company with sensitive data

---

Based on my answers:
- Give a clear recommendation (VPS, Mac Mini, or Hybrid)
- Explain why in 2-3 sentences
- Tell me which specific VPS or Mac Mini you recommend (model/provider)
- List the next 3 steps for me to get started
- If the answer is hybrid, explain what the ideal setup would be

Be direct and practical, like Bruno is in the lesson.
```

---

## 💡 Usage Tip

After receiving the agent's recommendation:

1. **Save the decision** by asking: *"Save this infrastructure decision in the file memory/infra-decision.md"*
2. **Move on to the next lesson** — N-7 covers complete VPS configuration, and N-8 covers Mac Mini
3. **If still in doubt**, ask the agent: *"Give me a real cost example for my case per month"*

---

## 🔗 Related Lessons

- **N-5:** Installing OpenClaw (the basics before choosing infrastructure)
- **N-7:** Configuring your VPS from scratch *(next lesson)*
- **N-8:** Configuring Mac Mini as a server *(if you choose that path)*
- **N-9:** Hybrid setup: Mac Mini + VPS backup
