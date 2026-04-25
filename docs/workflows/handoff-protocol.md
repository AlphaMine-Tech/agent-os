# Handoff Protocol: WebUI ↔ Discord ↔ CLI

## Purpose
Enable seamless work transfer between different agent interfaces (WebUI chat, Discord bot, CLI sessions) without losing context.

## When to Write a Handoff
- Pausing work mid-task in one session
- Switching from WebUI to Discord (or vice versa)
- Ending a session with incomplete work
- Before a long background job that may outlive the session

## Handoff File Format

Create `handoffs/<task-name>-<date>.md`:

```markdown
# Handoff: <Task Name>

**Project:** <Project name>
**Task:** <What's being done>
**Date:** <ISO timestamp>
**Author:** <Agent/session that wrote this>

---

## Current Status
<What's done, what's running, what's blocked>

## Blocker (if any)
<The specific issue preventing completion>

## Exact Next Steps
1. <First thing to try>
2. <If that fails, try this>
3. <Validation command>

## Files/Paths
| Path | Description |
|------|-------------|
| /path/to/thing | What it is |

## Risks
<Anything the next agent should be careful about>
```

## Picking Up a Handoff
In the receiving session, tell the agent:

> "Check the latest handoff and continue from the recorded next steps."

The agent reads `handoffs/`, finds the most recent relevant file, and resumes work with full context.

## Rules
- Handoffs are disposable once their contents are absorbed into canonical files
- Do not use handoffs as a substitute for build-state, project docs, or MEMORY.md
- Keep handoffs short and actionable — the next agent should be able to act immediately
- Include exact commands when possible — don't make the next agent figure out syntax
