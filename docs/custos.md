# 💰 Costs — Real Breakdown of Running an AI Agent

> What it actually costs in practice, with optimizations applied.

---

## Infrastructure

| Item | Cost/month | Notes |
|------|-----------|-------|
| VPS Hostinger KVM 1 | ~R$25-50 | 2 vCPU, 4GB RAM, Ubuntu 24.04 |
| VPS Hostinger KVM 2 | ~R$39-60 | 2 vCPU, 8GB RAM (recommended for multi-agent) |
| Domain (optional) | ~R$5-10 | For Mission Control |
| Cloudflare Tunnel | Free | Secure remote access |
| **Infra subtotal** | **R$25-60** | |

## Model API (Anthropic)

### Without optimization (everything on Opus)
| Usage | Cost/day | Cost/month |
|-------|-----------|-----------|
| Daily interaction | ~$2-3 | ~$70-90 |
| 17 crons | ~$1-2 | ~$30-60 |
| Heartbeats | ~$0.50 | ~$15 |
| **Total** | **~$3-5** | **~$100-150** |

### With optimization (smart split) ✅
| Usage | Model | Cost/day | Cost/month |
|-------|--------|-----------|-----------|
| Interaction (chat) | Opus | ~$0.50-1.00 | ~$15-30 |
| Execution crons | Sonnet | ~$0.10-0.20 | ~$3-6 |
| Heartbeats | Haiku | ~$0.01-0.02 | ~$0.30-0.60 |
| Heartbeats | Ollama local | $0 | $0 |
| **Optimized total** | | **~$0.60-1.20** | **~$18-36** |

### Savings
| Metric | Before | After |
|--------|-------|--------|
| Daily cost | $3-5 | $0.60-1.20 |
| Monthly cost | $100-150 | $18-36 |
| **Savings** | | **~75-80%** |

### Tip: Anthropic Subscription
- Pro plan ($20/month) includes generous Claude usage
- If using via subscription instead of API, cost drops dramatically
- Bruno uses the subscription and has never hit the limit

## External APIs and Tools

| Tool | Cost/month | What for |
|------|-----------|---------|
| 1Password | Free (personal) or $3 | Manage credentials |
| RapidAPI | Free (free tier) | Proxy for YouTube, Instagram, X |
| Apify | Free ($5 credit/month) | YouTube transcripts (~714 videos) |
| Brave Search API | Free (2k searches/month) | Web search |
| Google APIs | Free | Calendar, Drive, YouTube Data |
| OpenAI (Whisper) | ~$1-3 | Audio transcription |
| **APIs subtotal** | **$0-10** | Most have free tiers |

## Estimated Total Cost

### Beginner (1 agent, moderate use)
| Item | Cost/month |
|------|-----------|
| VPS KVM 1 | R$25-50 |
| Anthropic API (optimized) | R$90-180 (~$18-36) |
| External APIs | R$0-25 |
| **Total** | **R$115-255/month** |
| **Per day** | **~R$4-8** |

> "Less than a coffee per day to have a 24/7 AI assistant"

### Advanced (6 agents, 22 crons, full stack)
| Item | Cost/month |
|------|-----------|
| VPS KVM 2 | R$39-60 |
| Anthropic API (optimized) | R$180-360 (~$36-72) |
| External APIs | R$25-50 |
| Supabase (MC) | Free (free tier) |
| **Total** | **R$244-470/month** |
| **Per day** | **~R$8-16** |

> "The equivalent of 1/10 of a full-time employee, working 24/7"

## Comparison with Alternatives

| Solution | Cost/month | Availability | Customization |
|---------|-----------|-----------------|----------------|
| **Optimized OpenClaw** | R$115-255 | 24/7 | Total |
| Freelance assistant | R$2,000-5,000 | Business hours | Medium |
| Full-time employee | R$3,000-8,000 | Business hours | High |
| ChatGPT Pro | R$100 | On demand | Low |
| N8N + Zapier | R$200-500 | 24/7 (limited) | Medium |

## Cost-Saving Tips

1. **Sonnet for crons** — 90% savings vs Opus
2. **Haiku for heartbeats** — or local Ollama (free)
3. **Session initialization** — 8KB vs 50KB = 80% fewer tokens
4. **Rate limits** — prevents automation runaway
5. **Free tiers** — RapidAPI, Apify, Brave, Google APIs are generous
6. **Subscription vs API** — Anthropic subscription can be cheaper for personal use

---

*Values based on real production — Feb/2026*
*Approximate exchange rate: $1 = R$5*
