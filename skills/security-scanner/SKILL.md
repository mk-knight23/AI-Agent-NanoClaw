---
name: security-scanner
description: "Node.js security audit: npm audit for known CVEs, Snyk for supply chain vulnerabilities, eslint-plugin-security for code patterns (eval, prototype pollution, path traversal), and AI-driven analysis of container isolation boundaries. Generates SECURITY_REPORT.md with CRITICAL/HIGH/MEDIUM severity ratings. Adapted from ZeroClaw's Rust security-scanner for Node.js/npm ecosystem. Run before any release or dependency update."
---

# security-scanner

Full-spectrum Node.js security audit — CVEs, supply chain, code patterns, container isolation.

## Usage
```
@Andy security-scanner --full
@Andy security-scanner --deps-only         # npm audit + Snyk only
@Andy security-scanner --code-only         # ESLint security rules only
@Andy security-scanner --fail-on high      # Exit non-zero if HIGH+ issues found (CI mode)
```

## What It Checks

### 1. Known CVEs — `npm audit`
- All direct + transitive dependencies checked against npm security advisories
- Each finding includes: CVE ID, severity, affected package, fix version

### 2. Supply Chain — Snyk
- License compliance (blocks AGPL, GPL-3.0 by default — configurable)
- Typosquatting detection: flags packages with names similar to popular ones
- Deprecated package warnings

### 3. Code Security Patterns — ESLint Security Plugin
- `eval()` and `new Function()` usage
- Prototype pollution via `__proto__`, `constructor.prototype`
- Path traversal in `fs.readFile`, `path.join` with user input
- Hardcoded secrets (API keys, tokens in source)
- `child_process.exec` with unsanitized input

### 4. Container Isolation Audit (NanoClaw-Specific)
- Shared state leaking between agent containers
- Unauthenticated inter-container communication
- Swarm nodes exposing internal ports without firewall rules

## Files Created
```
SECURITY_REPORT.md          # Full report with severity ratings
security_audit.json         # Machine-readable JSON for CI
```

## CI Integration
```yaml
# .github/workflows/security.yml
- name: NanoClaw Security Scan
  run: |
    npm audit --audit-level=high
    andy security-scanner --full --fail-on high
```

## Philosophy
Container isolation is NanoClaw's core security model. Every issue that could allow one agent to affect another is treated as CRITICAL, regardless of what npm audit says.
