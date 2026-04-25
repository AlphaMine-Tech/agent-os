# Build State: Example Long Build

<!-- Copy this template for multi-step or long-running jobs -->

## Goal
What we're building and why.

## Definition of Done
How we know it's complete.

## Repo/Workspace
`/path/to/workspace`

## Milestones
- [x] Step 1: Clone and configure
- [x] Step 2: Build image
- [ ] Step 3: Deploy and validate    ← current
- [ ] Step 4: Cutover traffic
- [ ] Step 5: Verify end-to-end

## Current Milestone
Step 3: Deploy and validate

## Last Checkpoint
Step 2 completed at YYYY-MM-DD HH:MM UTC.
Image: `my-image:v1.0` (sha256:abc123...)

## Blockers
None currently.

## Blocker Rules
- If build fails: check logs, fix, retry
- If dependency unavailable: document and pause
- If disk full: alert operator before proceeding

## Active Worker
- PID: N/A
- Log: `/path/to/build.log`
- Session: tmux session `my-build`
