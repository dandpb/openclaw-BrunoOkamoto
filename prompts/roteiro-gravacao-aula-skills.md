# Recording Script — "Skills: The Superpower System for Your Agent"
**Dedicated lesson | ~25 min | Reformulated Module 6**

---

## Setup before recording

- Terminal open with Amora's workspace visible
- VS Code showing `skills/` with real subfolders (content/, analytics/, operations/)
- ClawHub open in the browser: clawhub.com
- GitHub open with a third-party skill example
- Notifications disabled

---

## BLOCK 1 — Opening: Why 1 agent > multiple agents (2 min)

**[FRONT CAMERA]**

> "When people start really using OpenClaw, they inevitably fall into the same trap: they start creating an agent for everything.
>
> A content agent. A metrics agent. An email agent. A calendar agent.
>
> It seems to make sense. In practice, it's a nightmare.
>
> Why? Because each agent has its own context. You ask one to create a post, and another doesn't know the post was created. You make a decision with one, the other doesn't know. You become the manager of 8 dumb agents instead of having 1 smart assistant.
>
> The right way is different: **1 agent with multiple superpowers.** Each superpower is a skill.
>
> That's exactly what this lesson covers."

---

## BLOCK 2 — What is a skill (3 min)

**[SHARE SCREEN: VS Code, open skills/ in workspace]**

> "A skill is basically an instruction manual + tools you give your agent.
>
> Minimum structure:"

**[SHOW: tree of a real skill, e.g.: skills/content/carrossel-linkedin/]**

```
skills/
└── content/
    └── carrossel-linkedin/
        └── SKILL.md
```

> "It's just a SKILL.md file. The agent reads this file when it's about to execute the skill, understands what it can do, and executes.
>
> When I say 'create a LinkedIn carousel', the agent goes there, reads the skill, and follows the defined process. It doesn't improvise. It doesn't hallucinate the format. It follows what's written.
>
> This is the core point: **skill = documented process that the agent executes consistently.**"

**[SHOW: open a real SKILL.md — summarized content]**

> "The file has: a description of what the skill does, when to use it, what inputs it needs, and the step-by-step execution. It can have examples, quality rules, whatever is necessary."

---

## BLOCK 3 — How to organize skills in folders (3 min)

**[SHARE SCREEN: VS Code, full skills/ tree]**

> "Organization matters. My structure:"

**[SHOW: tree of real skills/]**

```
skills/
├── content/          ← everything that produces content
│   ├── carrossel-instagram/
│   ├── carrossel-linkedin/
│   └── yt-hype/
├── analytics/        ← metrics and data
│   ├── chartmogul/
│   └── ga4/
├── operations/       ← recurring operations
│   ├── notion-api/
│   ├── crisp-wrapup/
│   └── planner-adhd/
└── research/         ← research and intelligence
    ├── deep-research-protocol/
    └── blogwatcher/
```

> "Clear categories. When I'm going to create a new skill, I first ask myself: which category? If there's no category for it, it might be a new category — or I'd need to create that first.
>
> Why does this matter? Because when you have 20, 30 skills, without organization you waste time finding what's available. And more importantly: the agent also gets confused.
>
> The rule I use: **each skill solves one thing well.** Instagram carousel skill ≠ LinkedIn carousel skill — because the format, tone, and structure are completely different."

---

## BLOCK 4 — How to ask the agent to execute a skill (2 min)

**[FRONT CAMERA → SHARE SCREEN: terminal with agent]**

> "Two ways:"

**[LIVE DEMO: type both examples]**

> "Simple way — you just ask:"

```
"Create a LinkedIn carousel about Metricaas' growth"
```

> "The agent identifies that the LinkedIn carousel skill exists, reads the SKILL.md automatically, and executes.
>
> Explicit way — when you want to ensure which skill to use:"

```
"Use the carrossel-linkedin skill to create a carousel about..."
```

> "The agent goes directly to that specific skill.
>
> **Important:** the agent only uses the skill if it's in the skills/ folder of the workspace. It doesn't make things up. If the skill doesn't exist, it either improvises — which is less consistent — or tells you it doesn't have that skill."

---

## BLOCK 5 — Every repetitive process becomes a skill (3 min)

**[FRONT CAMERA]**

> "This is the mindset that changes the game.
>
> Every time you do the same thing more than twice with your agent, you have a skill candidate.
>
> Concrete examples:"

**[SHOW ON SCREEN — simple list]**

> "- Every week you ask for a metrics report → weekly-metrics skill
> - Every time you record a video you ask for title, description, and tags → yt-hype skill
> - Every time you have a meeting you ask for a prep brief → meeting-prep skill
> - Every month you analyze churn → churn-analysis skill
>
> Why turn it into a skill instead of just repeating the prompt?
>
> Because when it's in the skill, the process is documented, tested, has defined quality criteria. You don't need to remember every detail. The agent doesn't improvise. And when you want to improve the process, you change the skill — and it changes forever.
>
> Think of it this way: **a prompt is a request. A skill is a process.**"

---

## BLOCK 6 — Sub-agents execute specific skills (2 min)

**[FRONT CAMERA]**

> "When you use sub-agents — which is when the main agent delegates a task to an isolated agent running in the background — the best practice is: the sub-agent has a clear scope and executes a specific skill.
>
> Wrong:"

**[SHOW ON SCREEN]**

> ❌ "Spawn an agent to 'take care of content'"

> "Right:"

> ✅ "Spawn an agent to execute the carrossel-linkedin skill with this input"

> "The difference: the loose agent will make random decisions. The agent with a skill has a defined process, clear inputs, and predictable output.
>
> Sub-agents are great for parallel and long-running tasks. But always with a closed scope. A sub-agent without a skill is a freelancer without a brief."

---

## BLOCK 7 — Backing up your skills (2 min)

**[SHARE SCREEN: terminal]**

> "Your skills are assets. If you lose your workspace, you lose all the processes you documented.
>
> Two backup options:"

**[SHOW: git command]**

> "The simplest: Git. Your workspace is already a repository. Commit and push:"

```bash
cd ~/your-workspace
git add skills/
git commit -m "backup skills $(date +%Y-%m-%d)"
git push
```

> "Private repository on GitHub, access for you only.
>
> Second option: automatic backup script. You set up a cron to run overnight and push automatically. There's an example script in the course reference workspace.
>
> The golden rule: **a skill that isn't in Git doesn't exist.** A disk crash, a corrupted workspace — and you lose months of documented processes. Don't let that happen."

---

## BLOCK 7b — Real demo: Meta Ads skill (2 min)

**[SHARE SCREEN: VS Code → skills/analytics/meta-ads/SKILL.md]**

> "Before talking about security, I want to show how a real analytics skill works in practice.
>
> This is the Meta Ads skill I run every day to track sales for Pixel Educação — the company behind the course. I'll open the SKILL.md:"

**[SHOW: SKILL.md open — credentials as XXXX]**

> "Look here: the Meta token and account ID are shown as `XXXX`. Never in the code — always via 1Password. The agent fetches them at runtime.
>
> What does it generate? A dashboard like this:"

**[SHOW: example-output-meta-ads.html file in the browser]**

> "Total revenue, split by product — OpenClaw Minicourse separate from Micro-SaaS PRO — refund rate, campaign ROAS. Generated automatically, sent to Telegram every day at 8am.
>
> That's what a well-built skill delivers. You describe the process once — and the agent executes it every time you ask, or at the time you configure."

---

## BLOCK 8 — Third-party skills: how to use them safely (4 min)

**[SHARE SCREEN: clawhub.com open in the browser]**

> "ClawHub is the OpenClaw community's skill marketplace. You'll find ready-made skills to install.
>
> But before installing anything, one inviolable rule:"

**[FRONT CAMERA — serious tone]**

> "Read the code. Always.
>
> A skill has access to your workspace, can run commands, can read files. A malicious skill can exfiltrate credentials, delete data, execute anything.
>
> The basic manual protocol:"

**[SHARE SCREEN: terminal]**

```bash
git clone https://github.com/user/skill-name /tmp/review-skill
cat /tmp/review-skill/SKILL.md
grep -r "curl" /tmp/review-skill/
grep -r "rm -rf" /tmp/review-skill/
grep -r "eval" /tmp/review-skill/
```

> "It works. But there's a better way.
>
> Adrylan — one of the most advanced students in the course — created a skill that audits other skills. It's based on the OWASP ASI Top 10 of 2026, the Snyk scanner, and Aguara. Nine verification categories: prompt injection, data exfiltration, malicious code, hardcoded credentials, social engineering...
>
> You install it once — and from then on, every time you find a new skill, you paste the content and ask: 'audit this skill'. The agent runs the full checklist and gives you a report: clean, attention, or critical.
>
> The complete SKILL.md is in the bonus material on Drive. **It's the first skill you should install — before any other.**"

---

## BLOCK 9 — Do Claude Code skills work in OpenClaw? (2 min)

**[FRONT CAMERA]**

> "Frequent question: I have Claude Code skills, do they work in OpenClaw?
>
> Short answer: it depends.
>
> Claude Code skills — the CLAUDE.md files — have a different format. They are instructions for the agent on how to behave in a specific code project. They are not the same concept as OpenClaw skills.
>
> To adapt:
> 1. The instruction content is generally usable — you take the context and rules and put them in an OpenClaw SKILL.md
> 2. Bash scripts that Claude Code uses generally run in OpenClaw without modification — the execution environment is compatible
> 3. What doesn't work directly are Claude Code-specific integrations (MCP servers, for example) — those need to be adapted to the OpenClaw equivalent
>
> In practice: if you have an elaborate prompt you use in Claude Code, turn it into a SKILL.md in OpenClaw. The behavior will be equivalent."

---

## BLOCK 10 — Closing (1 min)

**[FRONT CAMERA]**

> "To summarize:
>
> One agent with skills > multiple agents. Unified context, consistent process.
>
> Every repetitive process becomes a skill. A prompt is a request, a skill is a process.
>
> Sub-agent without a skill = freelancer without a brief. Always give a clear scope.
>
> Back up to Git. Skills are assets, treat them like code.
>
> Third-party skill: read the code first. Always.
>
> The full material — skills list by profile, security checklist, and the installation prompt — is on Drive, link in the description."

---

## Pre-recording checklist

- [ ] VS Code with `skills/` open showing real categories
- [ ] `skills/analytics/meta-ads/SKILL.md` open (credentials as XXXX)
- [ ] `reports/misc/exemplo-output-meta-ads.html` open in browser (sales dashboard)
- [ ] Terminal ready for clone + security grep demo
- [ ] clawhub.com open in the browser
- [ ] skill-audit SKILL.md ready to show (bonus material)
- [ ] Git backup script ready in the terminal
- [ ] Notifications disabled

## Approximate timings

| Block | Content | Time |
|-------|---------|------|
| 1 | Opening: 1 agent > multiple | 2:00 |
| 2 | What is a skill | 3:00 |
| 3 | Organization in folders | 3:00 |
| 4 | How to ask to execute | 2:00 |
| 5 | Every process becomes a skill | 3:00 |
| 6 | Sub-agents + skills | 2:00 |
| 7 | Git backup | 2:00 |
| 7b | Real demo: Meta Ads skill | 2:00 |
| 8 | Third-party skills + bonus skill-audit | 4:00 |
| 9 | Claude Code → OpenClaw | 2:00 |
| 10 | Closing | 1:00 |
| **Total** | | **~26 min** |

## Links to put in the description

- ClawHub: https://clawhub.com
- Skills by profile (PDF): Drive → OpenClaw Course → aula-06-skills → skills-by-profile.pdf
- Installation prompt: Drive → aula-06-skills → prompts → modulo-06-skills.md
