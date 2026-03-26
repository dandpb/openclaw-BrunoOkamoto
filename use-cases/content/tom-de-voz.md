# 🎤 Use Case: Tone of Voice Analysis

> Teach your agent to write LIKE YOU.

## What it does

Analyzes your existing content and creates a tone of voice guide:
- Technical vocabulary you use
- Expressions and catchphrases
- Style by platform (LinkedIn vs Twitter vs YouTube)
- What you would NEVER say
- Level of formality, humor, opinion

## Prompt

```
I want you to learn my tone of voice by analyzing my existing content.

Analyze:
- [NUMBER] posts from my LinkedIn: [LINK OR PASTE THE POSTS]
- [NUMBER] videos from my YouTube: [LINKS OR TRANSCRIPTS]
- [NUMBER] reels/posts from Instagram: [LINKS OR TEXTS]

For each platform, deliver:

1. **Frequent vocabulary** — words and expressions I use repeatedly
2. **Typical structure** — how I open, develop, and close posts
3. **Tone** — formal/informal, humorous/serious, opinionated/neutral
4. **Hooks that work** — the first lines of my posts with the most engagement
5. **Anti-patterns** — things I NEVER do (e.g.: too many hashtags, emojis, etc.)
6. **Style guide** — summarized document for me to paste into SOUL.md

After analyzing, write 3 test posts in my style and ask me:
"Does this sound like you?"

If it doesn't, tell me what to adjust.
```

## Real example

Amora analyzed 129 LinkedIn posts + 106 YouTube videos + 97 Instagram reels from Bruno and created a complete tone of voice guide that went into USER.md (400+ lines).
