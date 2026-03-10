# CI Security Gate — NanoClaw

Container-aware security gate for all Node.js/TypeScript PRs. Blocks merge on CRITICAL issues, validates container isolation boundaries.

## Trigger
- **Event**: GitHub PR opened or updated
- **Blocks**: merge if CRITICAL or HIGH security issues found
- **Special**: validates container isolation boundaries haven't been broken

## Pipeline

### Step 1: Dependency Audit
```bash
npm audit --audit-level=high
npx snyk test
```

### Step 2: Code Security (ESLint + Semgrep)
```bash
npx eslint --plugin security src/
npx semgrep --config=p/nodejs src/
```

### Step 3: Container Isolation Check (NanoClaw-Specific)
```javascript
// Checks that agent code doesn't leak state across containers
@Andy security-scanner --isolation-check --diff HEAD~1..HEAD
```

Flags:
- Shared `global` / `process.env` mutation across container boundaries
- Missing container cleanup on agent teardown
- Swarm nodes sharing mutable data structures

### Step 4: Secret Detection
```bash
npx detect-secrets scan --baseline .secrets.baseline
```

### Step 5: PR Report
```markdown
## NanoClaw Security Gate

✅ npm audit: no HIGH+ CVEs
✅ Container isolation: boundaries intact
⚠️ 1 MEDIUM: src/swarm/coding-team.ts:94 — missing error boundary
✅ No secrets detected

**Status: APPROVED**
```

## Thresholds
- **CRITICAL**: Blocks, Telegram alert
- **HIGH**: Blocks, PR comment
- **Container violation**: Always CRITICAL, blocks merge
- **MEDIUM / LOW**: Non-blocking, noted in comment
