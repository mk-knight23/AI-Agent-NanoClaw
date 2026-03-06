---
name: add-slack
description: "Transforms NanoClaw to add Slack workspace integration. Installs the @slack/bolt dependency, creates a Slack channel adapter, sets up OAuth app permissions, and registers it at startup. Run /add-slack when you want NanoClaw to listen and respond in Slack channels or DMs. Requires a Slack app with Bot Token and Signing Secret."
---

# add-slack

Adds Slack to your NanoClaw fork: workspace connection, channel listening, DM support, and thread-aware reply routing.

## Usage

```
/add-slack
```

## What This Skill Does To Your Codebase

### Files Created
```
src/channels/slack.ts           # Slack Bolt-based channel adapter
```

### Files Modified
```
src/index.ts                    # Import + register SlackChannel at startup
src/config.ts                   # Add SLACK_BOT_TOKEN, SLACK_SIGNING_SECRET, SLACK_APP_TOKEN
package.json                    # Add '@slack/bolt' dependency
```

### Environment Variables Added
```
SLACK_BOT_TOKEN=xoxb-your-bot-token
SLACK_SIGNING_SECRET=your_signing_secret
SLACK_APP_TOKEN=xapp-your-app-token   # Required for Socket Mode
```

## Step-by-Step What Happens

1. **Create Slack app**: Instructions to create app on api.slack.com with required OAuth scopes
2. **Enable Socket Mode**: Avoids need for public webhook URL
3. **Install dependency**: `npm install @slack/bolt`
4. **Create adapter**: `src/channels/slack.ts` — handles `app.message()`, routes to orchestrator, sends replies
5. **Scoped permissions**: Only requests `chat:write`, `app_mentions:read`, `im:history`
6. **Register at startup**: Adds `new SlackChannel(config.slack)` in `src/index.ts`

## The Resulting Slack Adapter

```typescript
// src/channels/slack.ts (generated)
import { App } from '@slack/bolt';

export class SlackChannel {
  private app: App;

  constructor(private config: { botToken: string; signingSecret: string; appToken: string }) {
    this.app = new App({
      token: config.botToken,
      signingSecret: config.signingSecret,
      socketMode: true,
      appToken: config.appToken,
    });
  }

  async start(onMessage: (msg: string, reply: (r: string) => void) => void) {
    const trigger = process.env.NANOCLAW_TRIGGER ?? '@Andy';
    this.app.message(new RegExp(trigger), async ({ message, say }) => {
      const text = (message as { text?: string }).text ?? '';
      onMessage(text, (r) => say(r));
    });
    await this.app.start();
  }
}
```

## Philosophy

Slack as a power-user channel. Thread-aware routing means NanoClaw can follow multi-turn conversations in channels and respond with full context — without losing track of what question is being answered.
