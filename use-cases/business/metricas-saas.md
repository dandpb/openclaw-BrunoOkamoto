# 📊 Use Case: Automatic SaaS Metrics

> MRR, churn, LTV and conversion dashboard delivered directly to Telegram.

## What it does

Connects to your billing API (ChartMogul, Stripe, Paddle) and generates automatic reports:
- Current MRR and month-over-month variation
- Churn rate and cancellation reasons
- Average LTV and per plan
- Trial → paid conversion
- Failed payments and recovery
- Top customers and churn risks

## Prompt

```
I want you to automatically monitor my SaaS metrics.

Configuration:
- My billing is [CHARTMOGUL/STRIPE/PADDLE]
- API key is in 1Password in the [VAULT NAME] vault

Create the following automatic reports:

1. **Daily quick** (every day at 9am, via cron):
   - Current MRR
   - New customers yesterday
   - Cancellations yesterday
   - Pending failed payments

2. **Weekly digest** (Monday at 10am):
   - MRR weekly variation
   - Top 5 churn reasons
   - Trial→paid conversion
   - Comparison with previous week

3. **Monthly deep dive** (1st of each month):
   - Full report with charts
   - Trend analysis
   - Next month MRR forecast
   - Recommended actions

Deliver to the [TOPIC NAME] topic on Telegram.
Notify me IMMEDIATELY if churn rises >5% or MRR drops >3% in a single day.
```

## Real example

Amora monitors MyGroupMetrics via ChartMogul:
- MRR: R$8,000 (+11.2% month)
- Churn: 8% (dropped from 23% → 8% with the new version)
- Alert: R$3,347 in failed payments (mainly insufficient balance)
