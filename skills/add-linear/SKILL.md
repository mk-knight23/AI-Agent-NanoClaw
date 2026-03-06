---
name: add-linear
description: "Transformation skill to add Linear integration. Installs linear-sdk, configures OAuth/API keys, and adds handlers for issue tracking and project management. Mounts Linear team context into agent containers."
---

# add-linear

Add Linear project management to your NanoClaw.

## Transformation Steps
1. **Dependencies**: Installs `@linear/sdk`.
2. **Adapter**: Adds `src/adapters/linear.ts`.
3. **Config**: Appends Linear settings to `config.json`.
4. **Skills**: Injects `create-issue`, `list-projects`, and `update-status` commands.

## Usage
Run `/add-linear` in the chat. Claude will execute the transformation.

## Benefits
- **Sync**: Keep agent tasks in sync with your team's Linear board.
- **Automation**: Auto-create issues from chat discussions.
- **Context**: Agents can read project docs directly from Linear.
