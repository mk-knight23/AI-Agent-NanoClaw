# Daily GitHub Digest — NanoClaw

Runs every morning. NanoClaw scans your watched repos for overnight activity and delivers a structured summary.

## Trigger
- **Schedule**: Daily at 8:00 AM (configurable)
- **Manual**: `@NanoClaw run daily-github-digest`

## Prerequisites
- `GITHUB_TOKEN` in environment
- Repos configured in `config/repos.json`
- At least one channel installed (Telegram, Slack, or email)

## What NanoClaw Does

1. Fetches all events since yesterday 8:00 AM for each watched repo
2. Groups by repo, then by type (Issues / PRs / CI / Releases)
3. Highlights items requiring your attention: mentions, assigned issues, failing CI on your PRs
4. Sends via configured channel

## Example Output

```
📋 GitHub Digest — 2026-03-05

anthropics/anthropic-sdk-typescript
  • PR #842 merged: "Add streaming response types" (your PR ✓)
  • Issue #901 opened: "Rate limit handling broken in v2.1"

your-org/api-service
  • CI failed on main (3 flaky tests)
  • 2 PRs awaiting your review

your-org/frontend
  • No activity
```

## Configuration

```json
{
  "repos": ["your-org/api-service", "your-org/frontend"],
  "digest_time": "08:00",
  "highlight_mentions": true,
  "skip_bots": true
}
```

## Customizing

```
@NanoClaw daily-github-digest add-repo your-org/new-service
@NanoClaw daily-github-digest set-time 07:30
```
