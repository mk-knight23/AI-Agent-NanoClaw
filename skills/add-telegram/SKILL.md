---
name: add-telegram
description: "Transforms NanoClaw to add Telegram channel support. This skill modifies the NanoClaw codebase directly — installs the telegraf dependency, creates a Telegram channel adapter in src/channels/, registers it at startup in src/index.ts, and adds bot token configuration. Run /add-telegram when you want to receive and send messages via Telegram bot. Requires a Telegram bot token from @BotFather."
---

# add-telegram

A skill-as-transformation: adds Telegram to your NanoClaw fork by modifying the source code directly.

## Usage

```
/add-telegram
```

That's it. Claude Code handles everything.

## What This Skill Does To Your Codebase

### Files Created
```
src/channels/telegram.ts        # Telegraf-based channel adapter
```

### Files Modified
```
src/index.ts                    # Import + register TelegramChannel at startup
src/config.ts                   # Add TELEGRAM_BOT_TOKEN to config schema
package.json                    # Add 'telegraf' dependency
```

### Environment Variables Added
```
TELEGRAM_BOT_TOKEN=your_bot_token_here
```

## Step-by-Step What Happens

1. **Get bot token**: Instructions to create bot via @BotFather on Telegram
2. **Install dependency**: `npm install telegraf`
3. **Create adapter**: `src/channels/telegram.ts` — handles `bot.on('message')`, routes to orchestrator, sends replies
4. **Register at startup**: Adds `new TelegramChannel(config.telegram)` in `src/index.ts`
5. **Test**: Sends "Hello from NanoClaw" to your bot to verify

## The Resulting Telegram Adapter

```typescript
// src/channels/telegram.ts (generated)
import { Telegraf } from 'telegraf';

export class TelegramChannel {
  private bot: Telegraf;

  constructor(private config: { token: string }) {
    this.bot = new Telegraf(config.token);
  }

  async start(onMessage: (msg: string, reply: (r: string) => void) => void) {
    this.bot.on('text', ctx => {
      const trigger = /* your trigger word */;
      if (ctx.message.text.includes(trigger)) {
        onMessage(ctx.message.text, (r) => ctx.reply(r));
      }
    });
    await this.bot.launch();
  }
}
```

## Philosophy

This is NanoClaw's "skills over features" pattern. Instead of adding Telegram support to the core codebase (making it bigger), this skill modifies YOUR fork to add exactly what you need. You end up with clean code that does exactly what you want.
