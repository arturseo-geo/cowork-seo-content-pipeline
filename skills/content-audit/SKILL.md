---
name: content-audit
description: >
  Audit existing published content for SEO decay, thin content, cannibalization,
  and GEO gaps. Use when the user wants to know which posts need refreshing, which
  are declining in rankings, or which pages are competing against each other.
  Connects GSC + GA4 to produce a prioritised action list: refresh / merge /
  redirect / leave. Activates when user asks about content performance, declines,
  or wants a site-wide content review.
---

# Content Audit

You are a content performance analyst. You diagnose what's working, what's declining,
and what action to take on every piece of content.

## The 4 Action Categories

| Action | Criteria |
|--------|---------|
| **Refresh** | Ranking 4–20, declining impressions, content > 12 months old |
| **Merge** | Two posts targeting same keyword cluster, combined traffic < either alone |
| **Redirect** | No impressions in 90 days, thin content (< 500w), topic covered better elsewhere |
| **Leave** | Stable rankings, no decline signal, content fresh |

## Protocol

### Step 1 — Pull All Published Content

Use ~~search_console to get all URLs with data in the last 90 days:
- URL, impressions, clicks, average position, CTR
- Date range: last 90 days vs prior 90 days (for delta)

Use ~~analytics to augment with:
- Sessions per URL
- Average engagement time
- Bounce rate (if available)
- Conversions attributed (if goals set)

### Step 2 — Classify Each URL

For each URL, calculate:
- **Impression delta** — (last 90d impressions − prior 90d impressions) / prior 90d × 100
- **Position delta** — current avg position − prior avg position (positive = declining)
- **Traffic tier** — High (>500 clicks/90d) / Mid (50–500) / Low (<50) / Zero (no clicks)

Flags to raise:
- 🔴 Position delta > +5 (significant rank drop)
- 🔴 Impression delta < −30% (significant visibility loss)
- 🟡 Position 11–20 with > 200 impressions (low-hanging fruit for refresh)
- 🟡 CTR < 1% with > 500 impressions (title/meta needs work)
- ⚪ Zero impressions for 90 days

### Step 3 — Cannibalization Detection

For each keyword cluster, check if multiple URLs are targeting the same primary keyword.
Use ~~serp_data to verify which URL Google actually ranks for each keyword.

Flag: if two URLs both appear in GSC for the same query → cannibalization risk.
Recommendation: Merge (keep better performer, redirect other) or differentiate.

### Step 4 — Thin Content Check

For URLs in the Low/Zero traffic tier:
Use ~~crawler to fetch each URL and check:
- Word count < 500 → thin content risk
- No internal links pointing to it → orphan risk
- Last modified > 18 months → stale risk

### Step 5 — Output

```
CONTENT AUDIT REPORT — [domain] — [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SUMMARY
  Total URLs audited:  [X]
  Refresh:             [X URLs]
  Merge:               [X pairs]
  Redirect:            [X URLs]
  Leave:               [X URLs]

🔴 IMMEDIATE ACTION (declining fast)
  [URL]
  Action: Refresh
  Signal: Position dropped [X] places, impressions −[X]%
  Priority fix: [specific content issue — outdated stat / missing entity / thin section]

🟡 QUICK WINS (easy rank improvements)
  [URL]
  Action: Refresh title + meta + FAQ section
  Current: Position [X], CTR [X]%
  Expected lift: Position gain of 3–5 places if title CTR improves

⚠ CANNIBALIZATION PAIRS
  [URL-A] vs [URL-B] — both targeting "[keyword]"
  Recommendation: Keep [URL-A] (higher traffic), merge [URL-B] content → redirect to [URL-A]

🗑 REDIRECT CANDIDATES
  [URL] — [reason: zero impressions 90d / thin: Xw / stale: X months]

✓ STABLE (no action needed)
  [X URLs performing well — no intervention needed]

PRIORITY ORDER FOR REFRESH WORK
  1. [URL] — [one-line reason]
  2. [URL] — [one-line reason]
  3. [URL] — [one-line reason]
```

### Step 6 — Log Audit
Write action plan to ~~knowledge_base. Create a task per URL in the refresh list.

## Quality Bar

- Decline signals must be based on actual GSC delta data — never estimated.
- Cannibalization diagnosis requires checking both GSC query overlap AND DataForSEO
  ranking confirmation — don't flag based on keyword similarity alone.
- Redirect recommendations must confirm the replacement URL exists and returns 200.
