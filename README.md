# 🐚 AI-Agent-NanoClaw

<p align="center">
  <img src="assets/banner.png" alt="AI-Agent-NanoClaw" width="800">
</p>

<p align="center">
  <a href="https://github.com/qwibitai/NanoClaw"><img src="https://img.shields.io/github/stars/qwibitai/NanoClaw?style=for-the-badge&color=F97316" alt="Stars"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License"></a>
  <a href="https://ai-agent-nanoclaw.vercel.app"><img src="https://img.shields.io/badge/Website-Live-green?style=for-the-badge" alt="Website"></a>
  <img src="https://img.shields.io/badge/Claude_Agent_SDK-Native-orange?style=for-the-badge" alt="SDK">
  <img src="https://img.shields.io/badge/Agent_Swarms-Supported-purple?style=for-the-badge" alt="Swarms">
</p>

> **Agent Swarms. Container Isolation. Claude-Native Intelligence.**

🌐 **[Live Website](https://ai-agent-nanoclaw.vercel.app)** · 📖 **[Docs](https://nanoclaw.dev)** · 🚀 **[Quick Start](#quick-start)**

---

## 🐚 Overview
**NanoClaw** is the first personal AI assistant to support full **Agent Swarms**. Built on the Claude Agent SDK, it isolates every agent group in its own Linux container, providing OS-level security and a clean, self-modifying codebase.

### 🛡️ Core Principles
- **Isolation**: Containers ensure your personal data and agent workspace never bleed.
- **Self-Modification**: Use the assistant to add new features to itself via "/add" commands.
- **Swarm Support**: Orchestrate multiple specialized agents to solve complex problems.

---

## 🏗️ Architecture

```mermaid
graph TB
    subgraph Channels
        WA[WhatsApp]
        TG[Telegram]
        DC[Discord]
        SL[Slack]
        SI[Signal]
    end

    subgraph NanoClaw["NanoClaw (Single Node.js Process)"]
        OR[Message Orchestrator<br/>src/index.ts]
        RT[Router<br/>src/router.ts]
        SK[Scheduler<br/>src/task-scheduler.ts]
        DB[SQLite<br/>src/db.ts]
    end

    subgraph Groups["Isolated Groups"]
        direction LR
        EG["engineering/<br/>CLAUDE.md + filesystem"]
        JG["job-search/<br/>CLAUDE.md + filesystem"]
        PG["personal/<br/>CLAUDE.md + filesystem"]
    end

    subgraph Containers["Linux Containers (per group)"]
        C1[Container 1<br/>Apple Container / Docker]
        C2[Container 2<br/>Apple Container / Docker]
        C3[Container 3<br/>Apple Container / Docker]
    end

    subgraph Swarms["Agent Swarms"]
        CT["Coding Team<br/>Architect → Coder → Reviewer → Deployer"]
        RT2["Research Team<br/>Researcher → Writer → Editor"]
        DT["DevOps Team<br/>Monitor → Fixer → Reporter"]
    end

    Channels --> OR
    OR --> RT
    RT --> Groups
    Groups --> Containers
    Containers --> Swarms
    OR --> SK
```

---

## 🛠️ Skills-as-Transformations
NanoClaw doesn't just call tools; it **transforms itself**. Use these commands to inject features directly into the core.

| Skill | Command | Description |
|-------|---------|-------------|
| **`add-discord`** | `/add-discord` | Inject professional Discord support with threads and rich embeds. |
| **`add-github-actions`**| `/add-github-actions` | Auto-configure robust CI/CD pipelines for your workspace. |
| **`add-linear`** | `/add-linear` | Connect your agent to the Linear project management tool. |
| **`add-obsidian`** | `/add-obsidian` | Mount your Obsidian vault directly into the agent's container. |
| **`add-supabase`** | `/add-supabase` | Add persistent database storage for task tracking and analytics. |
| **`add-telegram`** | `/add-telegram` | Installs Telegram channel support: deps, adapter, bot token config |
| **`add-gmail`** | `/add-gmail` | Adds Gmail: IMAP monitoring, Claude composition, approval workflow |

---

## 👥 Agent Swarms
Orchestrate a team of agents that work together.

### Coding Team (4 agents)
- **Architect**: Designs system, writes ADRs, defines API contracts
- **Coder**: Implements features, writes tests
- **Reviewer**: Code quality, security audit, test coverage check
- **Deployer**: Ships to Vercel/Railway/Render

### DevOps Team (3 agents, 24/7)
- **Monitor**: Watches all 60 repos for CI failures and deployment health
- **Fixer**: Auto-patches issues (dependency bumps, broken links)
- **Reporter**: Generates status dashboards

---

## 📂 Repository Structure

```text
AI-Agent-NanoClaw/
├── .claude/
│   ├── skills/                # Skill-as-transformation source code
│   │   ├── add-discord/       # Discord adapter transformation
│   │   ├── add-github-actions/# CI/CD pipeline injection
│   │   ├── add-telegram/
│   │   ├── add-gmail/
│   │   └── add-supabase/
│   └── memory/                # Persistent context storage
├── assets/                    # Project branding & assets
├── groups/                    # Isolated group configs (engineering, personal)
│   ├── engineering/
│   ├── job-search/
│   └── personal/
├── scheduled-tasks/           # Recurring automation definitions
│   ├── daily-github-digest.md # Automated activity briefings
│   ├── monday-briefing.md
│   └── friday-review.md
├── swarms/                    # Agent swarm logic and team roles
│   ├── coding-team/
│   ├── research-team/
│   └── social-media-team/     # Content creation pipeline
├── use-cases/                 # Real-world deployment scenarios
│   ├── agent-swarm-coding/    # Multi-agent development
│   └── self-modifying-agent/  # Meta-programming guide
├── website/                   # Next.js Site
└── docs/                      # Technical Documentation
```

---

## ⚡ Quick Start

```bash
git clone https://github.com/qwibitai/NanoClaw.git
cd NanoClaw
claude
```

Then run `/setup`. Claude Code handles everything: dependencies, authentication, container setup, and service configuration.

```
/setup         → Full installation wizard
/customize     → Add Telegram, Gmail, Slack channels
/add-obsidian  → Mount your Obsidian vault
/add-supabase  → Connect persistent database
```

---

## 🗺️ Roadmap

- [x] Container isolation (Apple Container + Docker)
- [x] Agent Swarms (first personal assistant to support this)
- [x] WhatsApp + Telegram + Discord + Slack + Signal
- [x] Per-group isolated CLAUDE.md memory
- [x] Scheduled tasks
- [ ] Swarm UI visualizer
- [ ] Multi-device container sync
- [ ] NanoClaw ↔ OpenClaw migration bridge
- [ ] Public skill registry for transformations

---

## 🦞 Part of the Claw Ecosystem
| Repo | Focus |
|------|-------|
| [AI-Agent-OpenClaw](https://github.com/mk-knight23/AI-Agent-OpenClaw) | 🦞 Full-stack Hub |
| [AI-Agent-Nanobot](https://github.com/mk-knight23/AI-Agent-Nanobot) | 🐈 Lightweight Lab |
| [AI-Agent-ZeroClaw](https://github.com/mk-knight23/AI-Agent-ZeroClaw) | 🦀 Rust Runtime |
| [AI-Agent-PicoClaw](https://github.com/mk-knight23/AI-Agent-PicoClaw) | 🦐 Edge/IoT |
| [AI-Agent-NanoClaw](https://github.com/mk-knight23/AI-Agent-NanoClaw) | 🐚 Swarm Agent · **← You are here** |

*Part of the Claw Ecosystem by [mk-knight23](https://github.com/mk-knight23)*

---

## ⚖️ License
MIT © [mk-knight23](https://github.com/mk-knight23)
