# AI-Agent-NanoClaw

Single Node.js process. Agents run in isolated containers. Claude Agent SDK.

## Quick Context  
- Container isolation: Apple Container (macOS) or Docker
- 3 active groups: engineering, job-search, personal
- 3 agent swarms: coding-team, research-team, devops-team
- Skills are code transformations, not config files

## Groups
- engineering/ — full stack, all 60 repos in memory
- job-search/ — resume, target companies, interview prep
- personal/ — schedule, preferences, family

## Key- **Skills (Transformations)**:
  - `skills/add-web-ui`: Injects Next.js frontend.
  - `skills/add-linear`: Linear PM integration.
  - `skills/add-discord`: Professional Discord support.
  - `skills/add-github-actions`: robust CI/CD pipelines.
- **Swarms**:
  - `swarms/social-media-team`: 3-agent content loop.
- /setup, /customize, /debug, /update

## Trigger Word
Default: @Andy
