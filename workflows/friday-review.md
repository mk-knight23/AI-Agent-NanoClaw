# Friday Review — NanoClaw

Every Friday afternoon, NanoClaw summarizes the week and surfaces what needs attention before the weekend.

## Trigger
- **Schedule**: Every Friday at 4:00 PM
- **Manual**: `@NanoClaw run friday-review`

## Prerequisites
- `GITHUB_TOKEN` for PR/issue stats (optional but recommended)
- At least one channel installed

## What NanoClaw Covers

### Week in Code
- PRs merged this week (yours + team)
- Issues closed vs opened ratio
- Open PRs waiting >3 days

### Open Threads
- Slack/Telegram conversations without resolution
- GitHub issues you commented on but didn't close
- Emails awaiting reply (if Gmail installed)

### What's Blocked
- PRs with failing CI
- Issues assigned to you with no activity

### Next Week Preview
- Issues labeled `next-week` or `sprint-planned`
- PRs close to mergeable

## Example Output

```
📅 Friday Review — Week of Mar 3–7

Code this week:
  ✓ 3 PRs merged  |  5 issues closed  |  12 commits
  ⚠ PR #45 "Refactor auth" open 5 days — needs your review

Open threads:
  • GitHub issue #92: You asked a question Tuesday, no response yet

Next week:
  • v2.3.0 release tagged for Monday
  • Issue #103 "Add rate limiting" labeled next-week
```

## Customization

```
@NanoClaw friday-review include-emails
@NanoClaw friday-review set-time 15:00
```
