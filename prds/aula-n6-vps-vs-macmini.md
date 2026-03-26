# PRD — Lesson N-6: VPS vs Mac Mini — When to Use Each Infrastructure

**Module:** Core (N)  
**Lesson:** N-6  
**Estimated duration:** 15–20 minutes  
**Level:** Beginner / Setup  
**Instructor:** Bruno  

---

## 🎯 Lesson Objective

By the end of this lesson, the student should be able to confidently decide which infrastructure to use for running OpenClaw: cloud VPS or local Mac Mini.

## 📋 Prerequisites

- Watched N-1 through N-5 (OpenClaw introduction and basic configuration)
- Know what SSH is (no need to master it, just know it exists)

---

## 🎬 RECORDING SCRIPT

### [00:00 – 01:30] OPENING — The Question Everyone Has

**[Bruno on camera, casual tone, as if chatting]**

> "Hey everyone. If you've made it to this lesson, you've probably already tested OpenClaw and are thinking: *'But where am I going to run this for real?'* A laptop is fine for testing, but it freezes. You can't turn it off. And if you use the agent all day, you need something more robust.
>
> That's the question I get every week: *VPS or Mac Mini?*
>
> And the honest answer is: it depends on your case. But I'll give you a framework to decide in under 5 minutes. Let's go."

---

### [01:30 – 05:00] PART 1 — What Is VPS and When to Use It

**[Shared screen: slides or browser showing Hostinger/DigitalOcean]**

> "VPS stands for *Virtual Private Server* — basically it's a computer that stays on in a datacenter somewhere in the world. You pay a low monthly fee and have remote access via terminal.
>
> Think of it this way: you're renting someone else's computer, but you have full control over it."

**[Show list on screen]**

> "The advantages of VPS are clear:
>
> **First: low cost.** You can get a decent VPS for 20, 30 dollars a month. Sometimes less. Hostinger has plans starting at 10 dollars.
>
> **Second: always on.** You don't need to worry about power outages, computer crashes, none of that. The server runs 24/7.
>
> **Third: access from anywhere.** You're on your phone, at a café, traveling — you access your agent from anywhere with internet.
>
> **Fourth: no physical maintenance.** No hardware to care for. If something burns out, it's the datacenter's problem."

> "But VPS also has disadvantages. The main one: you'll be using some AI model's API, whether Claude, GPT, whatever. Your data *passes through* third-party servers. If you deal with very sensitive information, this can be an issue.
>
> Another thing: performance is limited by the plan you paid for. If you need to run heavy local models like Llama, a basic VPS won't handle it."

---

### [05:00 – 08:30] PART 2 — What Is Mac Mini and When to Use It

**[Cut to camera or slide with Mac Mini image]**

> "Mac Mini is an Apple computer. Small, quiet, very efficient. And in recent years, with the M1, M2, M3, and M4 chips, it's become absurdly powerful.
>
> The big deal about Mac Mini is that you can run AI models *locally*. No API. No token cost. Your data stays on your machine."

> "The advantages of Mac Mini for running OpenClaw:
>
> **Real local power.** A Mac Mini M4 Pro, for example, can run models with 30, 70 billion parameters at reasonable speed. That means the agent works even without internet.
>
> **Total privacy.** Nothing leaves your local network. If you deal with client data, contracts, confidential information, this changes everything.
>
> **Zero network latency.** The agent responds at the speed of the machine, doesn't depend on ping to a server.
>
> **Once purchased, no more payments.** No monthly fee. Buy once and use for years."

> "But there are clear disadvantages:
>
> **High initial cost.** A basic Mac Mini M4 starts at 600 dollars. The M4 Pro, which actually makes a difference for AI, is in the 1,400 to 2,000 dollar range.
>
> **You need to keep it on.** If the power goes out, it gets turned off accidentally, or needs a restart, the agent goes offline.
>
> **More complex setup.** You need to configure remote access, maintain the system, solve hardware problems if they arise."

---

### [08:30 – 11:00] PART 3 — Comparison Table

**[Shared screen: visual table]**

> "Let me put this side by side to make it clearer."

| Criterion | VPS | Mac Mini |
|---|---|---|
| **Monthly cost** | $10–$30/month | ~$0 (hardware paid for) |
| **Initial cost** | Zero | $600–$2,000+ |
| **Setup** | Medium (SSH + CLI) | More complex (local remote access) |
| **Maintenance** | Minimal | You handle hardware |
| **Performance** | Limited by plan | High (M4 is very powerful) |
| **Privacy** | Third-party API | Local data |
| **Local models** | No (usually) | Yes |
| **Remote access** | Native | Needs configuration |
| **Availability** | 99.9%+ guaranteed | Depends on you |
| **Ideal for** | Getting started, freelancer | Business, privacy |

> "Looking at it this way, it's easier to decide. But let me talk about user profiles."

---

### [11:00 – 13:30] PART 4 — Use Scenarios: Which Is Yours?

**[Camera, direct tone]**

> "I'm going to talk about three profiles that appear a lot among course students."

**Scenario 1: Solo Freelancer**
> "You work alone. You use the agent to organize tasks, respond to clients, generate reports. No ultra-sensitive data. Want to start fast and spend little.
>
> **Recommendation: VPS.** Costs 15–20 dollars a month, always on, you access from anywhere. Perfect."

**Scenario 2: Small Business**
> "You have a team of 2 to 10 people. You deal with client data, contracts, financial information. Privacy is important. You already have minimal IT infrastructure.
>
> **Recommendation: Mac Mini.** The initial investment pays off in privacy and processing power. You can run local models for sensitive data."

**Scenario 3: Personal Use / Hobby**
> "You want to experiment, learn, see what OpenClaw can do. No critical uptime need.
>
> **Recommendation: Basic VPS or even your own computer.** No need to spend much yet. Test, learn, then decide."

---

### [13:30 – 16:00] PART 5 — Basic Configuration of Each Option

**[Shared screen: terminal]**

> "Now I'll show you how you *start* in each case. This isn't a full setup lesson — that has its own lesson — but I want to give you an idea of what to expect."

**VPS — The Basic Flow:**
> "With a VPS, you'll:
>
> 1. Rent the server (Hostinger, DigitalOcean, Contabo)
> 2. Connect via SSH: `ssh root@your-ip`
> 3. Install OpenClaw with the install command
> 4. Configure your agent
>
> That's it. In 30 to 60 minutes you're up and running. No hardware headaches."

```bash
# Connect to VPS
ssh root@123.456.789.0

# Install OpenClaw (example)
curl -fsSL https://openclaw.com/install.sh | bash

# Start the agent
openclaw start
```

**Mac Mini — The Basic Flow:**
> "With a Mac Mini, you'll:
>
> 1. Turn on the Mac Mini and connect to the network
> 2. Enable Remote Sharing in System Preferences
> 3. Install OpenClaw normally
> 4. Configure remote access (SSH or VNC)
> 5. Optionally install Ollama for local models
>
> It's a bit longer, but you do it once."

---

### [16:00 – 17:30] PART 6 — When to Migrate and the Hybrid Setup

**[Camera, consultative tone]**

> "A question that comes up a lot: *when should I migrate from VPS to Mac Mini (or vice versa)?*"

**Migrate from VPS to Mac Mini when:**
> "You started with VPS, the business grew, and now you deal with client data that can't go to the cloud. Or you start wanting to run heavy local models. Or the VPS monthly cost starts to seem high compared to investing once in hardware."

**Migrate from Mac Mini to VPS when:**
> "The Mac Mini is causing availability problems — power outages, someone accidentally turns it off. Or you need guaranteed access from anywhere in the world. In that case, either you solve the Mac Mini's infrastructure problem, or you use a VPS as an extra layer."

**The Hybrid Setup:**
> "My favorite setup for those who already have a Mac Mini: use the Mac Mini as the main server — for sensitive data, local models — and keep a small VPS as backup and external access point. If the Mac Mini goes down, the VPS still works for basic tasks.
>
> It's the best of both worlds. But it costs a bit more and adds complexity."

---

### [17:30 – 18:30] CLOSING — Bruno's Recommendation

**[Camera, straight to the point]**

> "So, my final recommendation:
>
> **If you're starting now: VPS.** Simple as that. It's cheaper to start, easier to configure, and you'll learn without worrying about hardware.
>
> **If you've been using OpenClaw for a while, have sensitive data, or want maximum performance: Mac Mini M4 Pro.**
>
> **If you want the best possible setup and can invest: Mac Mini + VPS as backup.**
>
> There's no wrong answer. There's the right answer for your moment.
>
> In the next lesson, we'll set up a VPS from scratch — from signing up to the agent running. See you there!"

---

## 📊 Topic Structure

1. Introduction — the common question (1.5 min)
2. What is VPS — pros and cons (3.5 min)
3. What is Mac Mini — pros and cons (3.5 min)
4. Comparison table (2.5 min)
5. Use scenarios (2.5 min)
6. Basic configuration of each (2.5 min)
7. When to migrate + hybrid (1.5 min)
8. Final recommendation (1 min)

**Total:** ~19 minutes

---

## 🎨 Required Assets

- [ ] Slide with comparison table (HTML/Notion or Figma)
- [ ] Terminal showing SSH and installation commands
- [ ] Hostinger/DigitalOcean panel screenshot
- [ ] Mac Mini M4 image (Apple website or own photo)

## 📦 Related Deliverables

- `docs/aula-n6-vps-vs-macmini.html` — Visual support material
- `docs/aula-n6-vps-vs-macmini.pdf` — Download version
- `prompts/aula-n6-vps-vs-macmini-prompt-aluno.md` — Post-lesson prompt
