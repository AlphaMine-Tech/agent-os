# AGENT-OS MANAGEMENT

Purpose: This directory is the **global, server-bound continuity system** for all agents working on your machine. It is designed so any AI agent — Claude, Codex, OpenClaw, or future tools — can pick up active work without depending on one tool's private transcript or memory store.

## Core Principles

1. **Canonical truth is global, not agent-local.**
   - Agent-local memory stores are allowed, but they are caches/fallbacks.
   - The durable source of truth for cross-agent continuity lives in `agent-os/`.

2. **Transcripts are fallback, not primary memory.**
   - Do not rely on chat history as the main continuity surface.
   - If a fact matters later, write it into the appropriate file here.

3. **Every durable fact gets one canonical home.**
   - Avoid duplicating the same truth across TODOs, memory, docs, and handoffs.
   - If something changes, update the canonical file rather than stacking contradictory notes.

4. **Long jobs must be resumable.**
   - Any long-running or multi-milestone task should use a build-state file under `build-state/`.
   - Progress should survive agent death, session resets, and chat compaction.

---

## Directory Layout

```text
agent-os/
  MANAGEMENT.md        # this file; how the system works
  TODO.md              # global active priorities across all agents
  MEMORY.md            # curated active durable truth
  memory/              # dated daily notes (append-only)
    YYYY-MM-DD.md
  docs/
    projects/          # stable per-project docs
    workflows/         # reusable operating procedures
    decisions/         # important decisions + rationale
  build-state/         # resumable state for long-running jobs
  handoffs/            # optional concise active handoff notes
  index/               # optional maps: repo map, host map, service map
```

---

## Startup Read Order for Any Agent

On entering a fresh session, an agent should read in this order:

1. `MANAGEMENT.md`
2. `TODO.md`
3. `memory/<today>.md` (if present)
4. `memory/<yesterday>.md` (if present)
5. `MEMORY.md`
6. relevant `docs/projects/*.md`
7. relevant `docs/workflows/*.md`
8. relevant `build-state/*.md` if continuing or resuming active work

Only read transcripts when the structured surfaces above are insufficient.

---

## Canonical Write Rules

### `TODO.md`
Use for:
- active priorities
- open tasks
- current blockers
- short status markers

Do NOT use for:
- detailed architecture
- raw notes
- historical logs

### `MEMORY.md`
Use for:
- active durable truth
- stable preferences
- operating rules
- current infrastructure truths that matter repeatedly
- high-value durable lessons

Do NOT use for:
- raw chronological logs
- temporary uncertainty
- stale/superseded facts left mixed in as truth

### `memory/YYYY-MM-DD.md`
Use for:
- daily residue
- recent events
- temporary context
- "remember this" items not yet curated
- notes from ongoing work

Rule:
- append during the day
- do not treat daily notes as canonical long-term truth until promoted

### `docs/projects/*.md`
Use for:
- stable project knowledge
- architecture
- paths/repos
- deploy notes
- key commands
- current project status
- known issues

### `docs/workflows/*.md`
Use for:
- repeatable operating procedures
- deployment flows
- shutdown/startup checklists
- agent operating patterns

### `docs/decisions/*.md`
Use for:
- important decisions that may need revisiting
- rationale, tradeoffs, alternatives considered, consequences

### `build-state/*.md`
Use for:
- long-running, multi-step, resumable jobs
- active worker/session IDs
- milestone tracking
- durable checkpoints
- blocker status

### `handoffs/*.md`
Use for:
- short active handoff notes when a task is mid-flight and another agent may need to take over quickly
- not a substitute for project docs or build-state

---

## Long Build Safe Mode

Use Long Build Safe Mode when any of the following are true:
- expected duration > 15 minutes
- multiple milestones
- heavy builds/tests/external waits
- unattended progress is expected
- losing session state would be expensive

### Required contract before work starts
Document in `build-state/<job-name>.md`:
- goal
- repo/workspace path
- definition of done
- milestone list
- current milestone
- completed milestones
- blocker rules
- recoverable failure rules
- last durable checkpoint
- last successful validation step
- active worker/session ID (if applicable)

### Execution model
- **Owner session:** human-facing chat
- **Detached worker:** executes implementation
- **Durable controller:** build-state file (or TaskFlow if available)
- **Durable evidence:** repo changes, test results, artifacts, updated notes, commits where appropriate

### Required behavior
- checkpoint after each milestone
- never let more than one milestone live only in transient session state
- if worker dies, resume from build-state + repo state
- only notify user on meaningful changes, blockers, completion, or risk boundary crossings

### Anti-patterns
Do not rely on:
- one giant silent foreground turn
- transcript memory as sole recovery path
- vague status without named milestones
- a running dev server as proof of durable progress

---

## Maintenance Rules

Periodic maintenance should:
- review recent daily notes
- promote durable items into `MEMORY.md`
- move project knowledge into `docs/projects/`
- record major decisions in `docs/decisions/`
- remove stale or contradicted items from `MEMORY.md`
- keep the retrieval corpus high-signal and bounded

---

## Safety / Operational Notes

- Do not make destructive or risky production changes without explicit direction from the operator.
- If a fact matters later, write it to the correct canonical file.
- Prefer clarity over cleverness. Future agents should be able to understand the system quickly.
- The goal is continuity that survives tool changes, session loss, and agent replacement.
