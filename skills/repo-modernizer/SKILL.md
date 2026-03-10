---
name: repo-modernizer
description: "Automated portfolio hygiene for Node.js repositories. Updates package.json dependencies to latest stable, migrates CommonJS to ESM, upgrades TypeScript config to strict mode, adds missing .gitignore patterns, adds GitHub Actions CI, generates missing README sections, and standardizes the project structure. Cross-ported from OpenClaw's repo-modernizer. Use when a repository is stale or missing modern Node.js conventions."
---

# repo-modernizer

Modernize any Node.js/TypeScript repository in one pass.

## Usage
```
@Andy repo-modernizer --repo ./my-project
@Andy repo-modernizer --repo ./my-project --dry-run     # Preview changes
@Andy repo-modernizer --repo ./my-project --skip deps   # Skip dependency updates
@Andy repo-modernizer --scan-all                        # Run on all 3 groups
```

## What It Modernizes

### 1. Dependencies (`package.json`)
- Updates all deps to latest stable versions (non-breaking)
- Separates `devDependencies` correctly
- Removes unused dependencies (via `depcheck`)
- Adds missing tooling: `eslint`, `prettier`, `typescript` if absent

### 2. Module System
- Migrates `require()` / `module.exports` to `import` / `export`
- Updates `package.json` with `"type": "module"`
- Fixes `.js` extension in imports (required for ESM)

### 3. TypeScript Configuration
```json
// Upgrades tsconfig.json to strict mode
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true
  }
}
```

### 4. GitHub Actions CI
- Adds `.github/workflows/ci.yml` if missing
- Node.js matrix: 20, 22 LTS
- Steps: install → lint → type-check → test

### 5. README Hygiene
- Adds missing sections: Installation, Usage, Contributing, License
- Adds badges: CI status, npm version, license
- Generates API reference from JSDoc comments

### 6. Code Quality
- Adds `.eslintrc` with recommended + security rules
- Adds `.prettierrc` with consistent formatting
- Adds `lint-staged` + `husky` pre-commit hooks

## Output
```
MODERNIZATION_REPORT.md     # What was changed and why
```

## Philosophy
Running repo-modernizer on all 3 NanoClaw groups keeps the engineering, job-search, and personal repos healthy without manual effort. Schedule it monthly.
