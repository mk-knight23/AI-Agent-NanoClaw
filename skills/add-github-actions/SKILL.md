---
name: add-github-actions
description: "Transformation skill to add robust CI/CD via GitHub Actions. Configures workflows for linting, testing, and auto-deployment. Adds secrets management and PR automation hooks."
---

# add-github-actions

Automate your development lifecycle with GitHub Actions.

## Transformation Steps
1. **Directory**: Creates `.github/workflows/`.
2. **CI Pipeline**: Adds `ci.yml` for linting and testing.
3. **CD Pipeline**: Adds `cd.yml` for auto-deployment to Vercel/Railway.
4. **Secrets**: Provides instructions for setting up `GITHUB_TOKEN` and other API keys.

## Usage
Run `/add-github-actions` in the chat.

## Benefits
- **Quality Control**: Ensures every PR passes tests before merging.
- **Hands-free Deployment**: Push to `main` and your agent's website/gateway updates automatically.
- **Security**: Automated dependency auditing on a weekly schedule.
