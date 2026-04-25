# Long Build Safe Mode

Use this workflow for any task that is long-running, multi-step, or expensive to lose.

## Use When
- expected duration > 15 minutes
- multiple milestones
- heavy builds/tests/external waits
- unattended progress expected
- session loss would be expensive

## Required File
Create `build-state/<job-name>.md` with:
- goal
- repo path
- definition of done
- milestone list
- current milestone
- completed milestones
- blockers
- last checkpoint
- last successful validation
- active worker/session ID

## Execution Model
- owner session = human-facing chat
- detached worker = implementation agent/session
- durable controller = build-state file
- durable evidence = repo changes, tests, artifacts, docs updates, commits when appropriate

## Rules
- checkpoint after each milestone
- never leave more than one milestone only in transient state
- resume from build-state + repo if worker dies
- notify only on meaningful progress, blockers, completion, or risk boundary crossings
