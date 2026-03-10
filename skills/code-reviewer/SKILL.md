---
name: code-reviewer
description: "Runs ESLint, TypeScript type checking (tsc --noEmit), and AI-driven review on any JavaScript/TypeScript Node.js codebase or diff. Identifies bugs, type issues, security vulnerabilities (via eslint-plugin-security), async pitfalls, and style violations. Outputs a CODE_REVIEW.md report with CRITICAL/HIGH/MEDIUM/LOW severity ratings. Use before committing or merging Node.js code. Adapted from Nanobot's Python code-reviewer for Node.js/TypeScript runtimes."
---

# code-reviewer

Static analysis + AI review for Node.js and TypeScript. Catches bugs, types, and security in one pass.

## Usage
```
@Andy code-reviewer --path src/
@Andy code-reviewer --diff HEAD~1..HEAD
@Andy code-reviewer --file src/agent/gateway.ts
@Andy code-reviewer --strict               # Fail on MEDIUM+ issues
```

## What It Runs

| Tool | Purpose |
|------|---------|
| `eslint` | Style, imports, common bugs, async patterns |
| `tsc --noEmit` | TypeScript type checking, missing types |
| `eslint-plugin-security` | Hardcoded secrets, injection, unsafe eval |
| `depcheck` | Unused dependencies |
| AI review | Logic bugs, container isolation issues, SDK misuse |

## Files Created
```
CODE_REVIEW.md                  # Full report with severity-rated findings
```

## CODE_REVIEW.md Structure
```
## Summary
- CRITICAL: 0 | HIGH: 1 | MEDIUM: 4 | LOW: 7

## HIGH Issues
### src/agent/gateway.ts:82 — Unhandled promise rejection
**Issue**: `asyncFunc()` called without await in event handler.
**Fix**: Wrap in `try/catch` or add `.catch(err => logger.error(err))`.

## MEDIUM Issues
...
```

## Node.js / NanoClaw-Specific Checks
- Container isolation violations: agent code referencing shared state outside its container
- Claude Agent SDK misuse: incorrect tool_use format, missing content types
- Swarm concurrency issues: shared mutable state across swarm nodes
- Memory leaks: EventEmitter listeners not removed, timers not cleared

## Exit Codes (for CI)
```bash
andy code-reviewer --path src/ --strict
# Exit 0: no MEDIUM+ issues
# Exit 1: issues found above threshold
```

## Philosophy
NanoClaw's container isolation means bugs can be subtle — a memory leak in one swarm node won't crash others, but it will silently degrade performance. The AI review pass specifically looks for cross-container coupling that static analysis misses.
