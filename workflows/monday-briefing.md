# Monday Briefing — NanoClaw

Every Monday morning, NanoClaw scans the weekend's activity and sets up your week.

## Trigger
- **Schedule**: Every Monday at 8:00 AM
- **Manual**: `@NanoClaw run monday-briefing`

## Prerequisites
- `GITHUB_TOKEN` for repo activity (optional)
- Channel installed for delivery

## What NanoClaw Covers

### Weekend Activity
- GitHub: PRs merged, issues opened/closed, CI results
- Slack/Telegram: messages you missed
- Email: unread emails awaiting reply (if Gmail installed)

### Week Priorities
- Issues assigned to you, sorted by label priority
- PRs that need your review
- Deadlines from README or project board

### Dependency Updates
- New versions of your direct dependencies
- Security advisories released over the weekend

## Example Output

```
☕ Monday Briefing — March 10

Weekend summary:
  • 2 PRs merged by teammates
  • 3 new issues opened (1 high priority: "Login broken in Safari")

Your week:
  🔴 Issue #201 [CRITICAL]: Login broken in Safari — assigned to you
  🟡 PR #189: Awaiting your review
  🟢 Issue #195: Implement dark mode — next planned task

Dependency updates:
  • @anthropic-ai/sdk: 0.24.0 → 0.25.1 (streaming improvements)
```
