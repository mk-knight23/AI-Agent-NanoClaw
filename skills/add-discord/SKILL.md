---
name: add-discord
description: "Transformation skill to add high-fidelity Discord support. Installs discord.js, creates a multi-channel adapter with thread support, and configures bot intents/tokens. Enables rich embeds and slash command registration."
---

# add-discord

Add professional-grade Discord integration to your NanoClaw.

## Transformation Steps
1. **Dependencies**: Installs `discord.js`.
2. **Adapter**: Creates `src/channels/discord.ts` with full event handling.
3. **Tests**: Adds `src/channels/discord.test.ts` for verification.
4. **Wiring**: Modifies `src/index.ts` to register the new channel.

## Usage
Run `/add-discord` in the chat.

## Advanced Features
- **Thread Management**: Automatically creates and manages threads for complex discussions.
- **Rich Embeds**: Uses beautiful Discord embeds for reporting status and logs.
- **Intents**: Configured with minimal necessary intents for security.
