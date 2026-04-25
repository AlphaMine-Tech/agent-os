# SSH Safety Workflow

## Hard Rules
- Never guess SSH usernames.
- Always verify host, user, and port from canonical infra docs before connecting.
- Fail2ban or similar tools may be active; a single wrong login attempt can block future work.

## Before SSH
1. Check `index/hosts.md` and any relevant project docs.
2. Confirm correct username.
3. Check/load SSH key:
```bash
ssh-add -l || true
eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519
```

## If Banned
- Server-side unban may be required via fail2ban
- Jumping through another server may be needed for recovery

## Why This Exists
Wrong SSH guesses have already caused avoidable bans and wasted time. AI agents are especially prone to guessing usernames like `root`, `ubuntu`, or `admin` — which can trigger lockouts on hardened systems.
