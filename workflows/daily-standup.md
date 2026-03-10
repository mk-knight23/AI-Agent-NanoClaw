# Daily Standup — NanoClaw

Automated morning briefing: what happened yesterday, what's planned today, blockers from all 3 groups.

## Schedule
- **Trigger**: Every day at 9:00 AM
- **Duration**: ~5 minutes
- **Output**: Telegram + Slack

## Pipeline

### Phase 1: Yesterday's Summary (parallel across groups)
```javascript
const [engineering, jobSearch, personal] = await Promise.all([
  summarizeGroup('engineering'),
  summarizeGroup('job-search'),
  summarizeGroup('personal')
]);
```

Each group summary includes:
- GitHub PRs merged / opened
- Linear issues resolved
- Emails sent/received (job-search group)
- Calendar events completed

### Phase 2: Today's Plan
- Pull today's Linear issues (assigned to me)
- Pull today's calendar events
- Pull open PRs needing review
- Rank by priority using Claude Sonnet

### Phase 3: Blocker Detection
- PRs open > 3 days without review → flag as blocker
- Linear issues with no activity > 2 days → flag
- Job applications with no response > 7 days → flag

### Phase 4: Standup Message
```
🌅 DAILY STANDUP — March 10, 2026

📦 ENGINEERING
✅ Yesterday: Merged PR #42 (NanoClaw swarm isolation fix)
📋 Today: Code review for batch-processor skill
⚠️ Blocker: PR #38 needs 2nd reviewer

💼 JOB SEARCH
📧 Yesterday: 3 emails sent (Cohere, Replit, OpenAI)
📋 Today: Follow up with Anthropic (7 days since send)

📅 PERSONAL
- Team lunch at 12:30 PM
- Weekly review at 5:00 PM
```

## Configuration
```json
{
  "trigger": "0 9 * * *",
  "groups": ["engineering", "job-search", "personal"],
  "channels": ["telegram", "slack"],
  "blocker_threshold_days": 3
}
```
