---
name: add-obsidian
description: "Transforms NanoClaw to mount and query your Obsidian vault. Mounts the vault directory read-only into the container context, adds a VaultSearch tool that Claude can call, and enables weekly digest generation from your notes. Run /add-obsidian when you want NanoClaw to reference your personal knowledge base. Requires your vault path."
---

# add-obsidian

Gives NanoClaw read access to your Obsidian vault. Enables note search, daily note summarization, and weekly digest delivery.

## Usage

```
/add-obsidian
```

## What This Skill Does To Your Codebase

### Files Created
```
src/tools/vault-search.ts       # VaultSearch tool for Claude to call
src/tools/vault-digest.ts       # Weekly digest generator from vault notes
```

### Files Modified
```
src/index.ts                    # Register VaultSearch tool with orchestrator
src/config.ts                   # Add OBSIDIAN_VAULT_PATH to config schema
```

### Environment Variables Added
```
OBSIDIAN_VAULT_PATH=/Users/you/Documents/Obsidian/MyVault
```

## Step-by-Step What Happens

1. **Set vault path**: You provide local path to your Obsidian vault
2. **Create VaultSearch tool**: Recursively indexes markdown files, enables Claude to search by keyword or tag
3. **Create digest tool**: Reads daily notes from the past 7 days, generates structured summary
4. **Register tools**: Both tools become available to Claude in all group contexts
5. **Mount read-only**: Container config updated to mount vault at runtime (read-only, no writes)

## The Resulting Vault Search Tool

```typescript
// src/tools/vault-search.ts (generated)
import { readFileSync, readdirSync } from 'fs';
import { join } from 'path';

export const vaultSearch = {
  name: 'vault_search',
  description: 'Search the Obsidian vault for notes matching a query',
  parameters: { query: 'string', tag?: 'string' },
  execute: async ({ query, tag }: { query: string; tag?: string }) => {
    const vaultPath = process.env.OBSIDIAN_VAULT_PATH!;
    // Recursively find markdown files, search content, return matches
  }
};
```

## Philosophy

Your vault is personal memory. This skill makes it available to NanoClaw as a read-only context source — enabling briefings, summaries, and intelligent responses grounded in your own notes.
