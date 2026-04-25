<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=28&duration=3000&pause=1000&color=00F0FF&center=true&vCenter=true&multiline=true&repeat=true&width=700&height=100&lines=%F0%9F%A7%A0+agent-os;Cross-Agent+Continuity+System" alt="agent-os" />
</p>

<p align="center">
  <a href="#-quick-start"><img src="https://img.shields.io/badge/get_started-00F0FF?style=for-the-badge&logo=rocket&logoColor=black" alt="Get Started" /></a>
  <a href="#-how-it-works"><img src="https://img.shields.io/badge/how_it_works-7B61FF?style=for-the-badge&logo=bookopen&logoColor=white" alt="How It Works" /></a>
  <a href="#-tip-jar"><img src="https://img.shields.io/badge/tip_jar-FFD700?style=for-the-badge&logo=ethereum&logoColor=black" alt="Tip Jar" /></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/agents-Claude%20%7C%20Codex%20%7C%20OpenClaw%20%7C%20Any-blueviolet?style=flat-square" />
  <img src="https://img.shields.io/badge/memory-durable%20%26%20structured-00F0FF?style=flat-square" />
  <img src="https://img.shields.io/badge/sessions-WebUI%20%E2%86%94%20Discord%20%E2%86%94%20CLI-green?style=flat-square" />
  <img src="https://img.shields.io/badge/license-MIT-yellow?style=flat-square" />
</p>

---

## 🧬 What is agent-os?

**agent-os** is a filesystem-based continuity system that lets multiple AI agents share memory, context, and active work — across sessions, across tools, and across time.

It solves the #1 problem with AI-assisted development: **when you close the chat, the agent forgets everything.**

```
                    ┌─────────────┐
                    │  WebUI Chat │
                    └──────┬──────┘
                           │
    ┌──────────┐    ┌──────▼──────┐    ┌───────────┐
    │ Discord  │◄──►│  agent-os/  │◄──►│   Codex   │
    │   Bot    │    │             │    │   Agent   │
    └──────────┘    │  📁 Shared  │    └───────────┘
                    │  Continuity │
    ┌──────────┐    │    Layer    │    ┌───────────┐
    │  Claude  │◄──►│             │◄──►│  Future   │
    │   Code   │    └─────────────┘    │  Agents   │
    └──────────┘                       └───────────┘
```

### ✨ Key Features

- 🔁 **Session-proof memory** — Agents pick up exactly where the last one left off
- 🤝 **Multi-agent handoffs** — WebUI → Discord → CLI → back again, seamlessly
- 📋 **Structured knowledge** — Not chat logs. Real, organized, queryable docs
- 🏗️ **Long build tracking** — Multi-hour jobs survive session death with build-state files
- 🧩 **Tool-agnostic** — Works with Claude, Codex, OpenClaw, or any agent that can read files
- 🛡️ **Safety rails** — Built-in workflows to prevent SSH bans, production accidents, and data loss

---

## 🚀 Quick Start

```bash
# Clone the repo
git clone https://github.com/AlphaMine-Tech/agent-os.git ~/agent-os
cd ~/agent-os

# That's it. Point your agents at ~/agent-os/ and go.
```

Then tell your agent:

> *"Read ~/agent-os/MANAGEMENT.md and follow the startup read order."*

The agent will bootstrap itself into your continuity system automatically.

---

## 📂 Directory Structure

```
agent-os/
│
├── 📜 MANAGEMENT.md            # How the system works (start here)
├── 📋 TODO.md                  # Active priorities across all agents
├── 🧠 MEMORY.md                # Curated active durable truth
├── 🤖 AGENT-BOOTSTRAP-PROMPT.md # Copy-paste prompt to onboard any new agent
│
├── 📅 memory/                  # Daily notes (append-only raw context)
│   └── YYYY-MM-DD.md
│
├── 📚 docs/
│   ├── projects/               # Stable per-project knowledge
│   ├── workflows/              # Reusable operating procedures
│   └── decisions/              # Important decisions + rationale
│
├── 🔧 build-state/             # Resumable state for long-running jobs
│
├── 🔀 handoffs/                # Active task handoff notes between agents
│
└── 🗺️ index/                   # Infrastructure maps (hosts, repos, services)
```

---

## 🧠 How It Works

### The Memory Hierarchy

agent-os uses a **5-layer memory system** — from hot session context to cold archival docs:

```
Layer 1: Live Session Context     ← immediate reasoning (volatile)
Layer 2: Daily Notes              ← raw residue from today's work
Layer 3: MEMORY.md                ← curated active truths
Layer 4: Decision Records         ← rationale and tradeoffs
Layer 5: Project & Workflow Docs  ← stable long-term knowledge
```

### Core Principles

| Principle | What It Means |
|-----------|--------------|
| 🎯 **Canonical truth is global** | Agent-local memory is a cache. `agent-os/` is the source of truth |
| 📝 **Transcripts are fallback** | If a fact matters later, write it to a file. Don't rely on chat history |
| 🏠 **Every fact gets one home** | No duplicating truth across TODO, memory, and docs |
| 🔄 **Long jobs must be resumable** | Multi-step work uses `build-state/` files to survive session death |

### Agent Startup Read Order

When any agent joins a fresh session, it reads in this order:

```
1. MANAGEMENT.md        → understand the system
2. TODO.md              → know what's active
3. memory/today.md      → recent context
4. memory/yesterday.md  → recent context
5. MEMORY.md            → durable truths
6. docs/projects/       → relevant project knowledge
7. docs/workflows/      → relevant operating procedures
8. build-state/         → any resumable active work
```

---

## 🔀 WebUI ↔ Discord Handoffs

One of agent-os's most powerful patterns: **seamlessly hand off work between different agent interfaces**.

### Writing a Handoff

When pausing work in one session (e.g., WebUI), write a handoff:

```markdown
# handoffs/my-task-2026-04-25.md

## Current Status
What's done, what's running, what's blocked.

## Blocker
The specific issue preventing completion.

## Exact Next Steps
1. Try this first
2. If that fails, try this
3. Validation command: `some-command --check`

## Files/Paths
| Path | Description |
|------|-------------|
| /path/to/thing | What it is |
```

### Picking Up a Handoff

In the next session (e.g., Discord bot), the agent reads the handoff and continues:

> *"Check the latest handoff and continue from the recorded next steps."*

The new agent has full context without needing the old chat transcript.

---

## 🏗️ Long Build Safe Mode

For multi-hour builds, deployments, or migrations that must survive agent restarts:

```markdown
# build-state/my-build.md

## Goal
What we're building and why.

## Definition of Done
How we know it's complete.

## Milestones
- [x] Step 1: Clone and configure
- [x] Step 2: Build image
- [ ] Step 3: Deploy and validate    ← current
- [ ] Step 4: Cutover and verify

## Last Checkpoint
Step 2 completed at 2026-04-25 20:30 UTC.
Image: my-image:v1.0 (sha256:abc123...)

## Blockers
None currently.
```

If the session dies mid-build, the next agent reads `build-state/` and picks up from the last checkpoint.

---

## 🛡️ Safety Workflows

agent-os includes built-in safety patterns to prevent common AI-agent accidents:

### SSH Safety
```markdown
# Never guess SSH usernames — wrong guesses trigger fail2ban lockouts
# Always verify host, user, and port from index/hosts.md first
```

### Production Safety
```markdown
# Never make destructive changes without explicit human approval
# Always check for active jobs before shutting down services
# Never assume resource usage alone proves active work
```

### Infrastructure Safety
```markdown
# Always checkpoint before multi-step operations
# Never leave more than one milestone only in transient state
# If worker dies, resume from build-state + repo, not memory
```

---

## 🤖 Bootstrap a New Agent

Copy-paste this into any AI agent to onboard it into your agent-os:

```
You are joining an active multi-agent operating environment.

Read these files in order:
1. ~/agent-os/MANAGEMENT.md
2. ~/agent-os/TODO.md
3. ~/agent-os/memory/<today>.md
4. ~/agent-os/MEMORY.md

Then read relevant docs/projects/ and docs/workflows/ files.

Rules:
- agent-os/ is the canonical source of truth
- Transcripts are fallback, not primary memory
- Write durable facts to the appropriate canonical file
- Use build-state/ for any work lasting > 15 minutes
- Never make destructive changes without human approval

Report what you found and what's currently active.
```

---

## 📋 Example: Template Files

### MEMORY.md (Template)
```markdown
# Active Durable Truth

## Infrastructure
- Primary server: <hostname> at <role>
- Services: <list of running services>

## Operating Rules
- Rule 1: Never do X without approval
- Rule 2: Always verify Y before Z

## Lessons Learned
- <Date>: <What happened and what we learned>
```

### TODO.md (Template)
```markdown
# Active Priorities

## High Priority
- [ ] Task description — context and blockers

## Medium Priority
- [ ] Task description

## Completed Recently
- [x] Task — completed YYYY-MM-DD
```

---

## 🏛️ Philosophy

agent-os was born from real production pain:

> *We were running AI agents across WebUI, Discord, and CLI to manage infrastructure, deploy services, and coordinate multi-hour builds. Every time a session ended, the next agent started from scratch. We lost context, repeated mistakes, and wasted hours re-learning what the last agent already knew.*

agent-os fixes this by making **the filesystem the memory** — not the chat window.

It's intentionally simple: just markdown files in a directory. No database, no API, no lock-in. Any agent that can read files can participate in the continuity system.

---

## 👥 Authors

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/alphaminedefi">
        <img src="https://github.com/alphaminedefi.png" width="80px;" alt="AlphaMine"/><br />
        <sub><b>AlphaMine</b></sub>
      </a><br />
      <sub>🏗️ Creator & Architect</sub>
    </td>
    <td align="center">
      <a href="https://claude.ai">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/78/Anthropic_logo.svg/1200px-Anthropic_logo.svg.png" width="80px;" alt="Lord Beerus"/><br />
        <sub><b>Lord Beerus</b></sub>
      </a><br />
      <sub>🤖 AI Co-Author (Claude Opus)</sub>
    </td>
  </tr>
</table>

---

## 💰 Tip Jar

If agent-os saved you time or inspired your setup, consider leaving a tip:

| Network | Address |
|---------|---------|
| ₿ **Bitcoin** | `bc1q52ceav67rp8mxa3ptany2l59kfdat6q7ne86ck` |
| ⟠ **Ethereum** | `0x8A69d2C99b8a537acC7Da124E00cf38d876815D4` |
| 🟣 **Quai Network** | `0x003078b752c0cabF8bbf2b956711DfA44864BA6C` |
| 💎 **Kaspa** | `kaspa:qypcrq3zu0ufvvg8ch5spclu2nwpjywl5rsmcjrxs1u34dwyuh7yhyg5268s8d4` |

---

## 📄 License

MIT License — use it, fork it, make it yours.

---

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&duration=4000&pause=2000&color=7B61FF&center=true&vCenter=true&repeat=true&width=500&lines=Built+by+humans+and+AI%2C+working+together.;Memory+that+survives+the+session.;Your+agents+deserve+continuity." alt="Footer" />
</p>
