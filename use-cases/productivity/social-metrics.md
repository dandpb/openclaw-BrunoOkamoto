# 📱 Use Case: Social Media Metrics Sync

> All social media metrics in a single report.

## What it does

Pulls data from all platforms and consolidates:
- YouTube: subscribers, views, best-performing videos
- Instagram: followers, engagement rate, text vs reels
- LinkedIn: impressions, avg likes/post, growth
- X/Twitter: followers, tweets, engagement
- Week-over-week comparison

## Setup prompt

```
I want you to automatically monitor my social media.

My profiles:
- YouTube: [CHANNEL]
- Instagram: [PROFILE]
- LinkedIn: [PROFILE]
- X/Twitter: [PROFILE]

Configure:
1. **Daily sync** (cron at 10pm, Sonnet):
   - Pulls updated metrics from all platforms
   - Saves snapshot to database/file

2. **Weekly report** (Monday at 9am):
   - Current week vs previous week comparison
   - Top 3 best-performing posts (with link)
   - Platform that grew the most
   - Recommendation: where to focus this week

3. **Alerts** (immediate):
   - Post going viral (>5x average engagement)
   - Sharp drop in followers
   - Negative comment with high reach

Use RapidAPI as a proxy for Instagram and X (cloud IPs are blocked).

Deliver to the Metrics topic on Telegram.
```

## Real example

Amora's metrics:
- YouTube: 69.8k subs, 1.4M views, 276 videos
- Instagram: 52.7k followers, 0.87% ER
- Twitter: 2.3k followers, 338 tweets
- LinkedIn: 247 avg likes/post
- Insight discovered: Instagram text > reels (21x more ER!)
