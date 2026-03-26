# Recommended OpenClaw Settings

> Reference for configuring your openclaw.json

## Model by Use Case

| Use Case | Recommended Model | Why |
|----------|------------------|-----|
| Direct interaction | Claude Opus | Best reasoning, more creative |
| Crons / automation | Claude Sonnet | 90% cheaper, sufficient for tasks |
| Heartbeats | Claude Haiku | Minimum cost, just checks and reports |
| Images | Gemini Flash | Good and affordable |
| Advanced analysis / multimodal | Gemini 2.5 Pro | Huge context (1M tokens), native multimodal |
| Google alternative | Gemini 3.1 Pro (`google/gemini-3.1-pro-preview`) | Advanced reasoning, good fallback option |
| High volume / minimum cost | MiniMax (`minimax/minimax-01`) | 1M token context at extremely low cost |

### Model IDs (for openclaw.json)

```json
"anthropic/claude-opus-4-5"       // Claude Opus — main interaction
"anthropic/claude-sonnet-4-5"     // Claude Sonnet — crons and automation
"anthropic/claude-haiku-4-5"      // Claude Haiku — heartbeats
"google/gemini-2.5-pro-preview"   // Gemini 2.5 Pro — advanced analysis
"google/gemini-3.1-pro-preview"   // Gemini 3.1 Pro — reasoning / fallback
"google/gemini-flash-2.0"         // Gemini Flash — images and volume
"minimax/minimax-01"              // MiniMax — minimum cost, long context
```

## Compaction Config (IMPORTANT)

If not configured, your session will overflow tokens and the agent will freeze.

```json
{
  "compaction": {
    "mode": "default"
  },
  "contextTokens": 160000,
  "reserveTokensFloor": 30000
}
```

## Thinking Mode

| Level | When to use | Cost |
|-------|------------|------|
| off | Simple tasks, quick responses | $ |
| low | Day-to-day, most interactions | $$ |
| medium | Analysis, planning, content | $$$ |
| high | Coding, complex problems, strategy | $$$$ |

## Crons: Golden Rule

**ALWAYS:**
```json
{
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "Your task here"
  },
  "delivery": { "mode": "announce" }
}
```

**NEVER** use `sessionTarget: "main"` + `payload.kind: "systemEvent"` — it fires but doesn't execute.

## Cost-Saving Tips

1. Heartbeats with Haiku: ~$0.005 each (vs ~$0.10 with Opus)
2. Crons with Sonnet: ~90% savings vs Opus
3. Space crons: don't put multiple at the same minute (rate limit)
4. config.patch restarts gateway — do it at times with no crons running
