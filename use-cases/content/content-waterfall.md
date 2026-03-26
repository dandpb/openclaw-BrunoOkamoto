# 🎬 Use Case: Content Waterfall

> One video becomes 10+ pieces of content across multiple platforms.

## What it does

Takes a recorded video (YouTube, Tella, Loom) and automatically generates:
- LinkedIn post (long format, storytelling)
- X/Twitter thread (5-8 tweets)
- Instagram carousel (slides with design)
- Newsletter (editorial format)
- Reels/Shorts (60s script)
- Standalone tweets (isolated insights)

## How Amora does this

1. Transcribes the video (Whisper API or Apify)
2. Extracts the main insights
3. Adapts for each platform (tone, format, limitations)
4. Generates all pieces
5. Schedules publication (Late API or manual)

## Prompt

```
I just recorded a video about [TOPIC]. Here is the transcript:

[PASTE THE TRANSCRIPT OR VIDEO LINK]

I want you to apply the Content Waterfall:

1. Extract the 5-7 main insights from the video
2. Generate the following content pieces:
   - 1 LinkedIn post (storytelling format, 1200-1500 characters, strong hook on the first line)
   - 1 X/Twitter thread (5-8 tweets, first tweet is the hook)
   - 1 Reel/Short script (60 seconds, format: hook + content + CTA)
   - 1 newsletter block (editorial format, 300-500 words)
   - 3 standalone tweets (isolated insights, each one independent)

Rules:
- Use MY tone of voice (consult USER.md)
- Each platform has a different format — adapt accordingly
- LinkedIn: professional but human, no excessive hashtags
- Twitter: direct, provocative, strong opinion
- Reel: visual, dynamic, hook in the first 3 seconds
- Newsletter: deeper, with context and behind-the-scenes

Show me all the pieces and ask if I want to adjust anything before finalizing.
```

## Expected result

From 1 20-minute video → 7+ pieces ready to publish in ~10 minutes.

## Tip

Set up a cron to run the waterfall automatically every time a new video is detected on Tella/YouTube.
