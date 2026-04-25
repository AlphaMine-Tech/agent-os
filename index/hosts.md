# Host Inventory

<!-- List your servers/machines here so agents know how to connect -->
<!-- IMPORTANT: Do NOT commit real credentials, passwords, or private keys -->

| Alias | IP/Hostname | SSH User | Port | Role | Notes |
|-------|-------------|----------|------|------|-------|
| build-server | 192.168.1.x | myuser | 22 | Build host | GPU builds |
| web-server | 10.0.0.x | ubuntu | 22 | Web/API | Nginx + apps |

## SSH Keys
- Default key: `~/.ssh/id_ed25519`
- Always verify user and host from this file before connecting
- See `docs/workflows/ssh-safety.md` for the full protocol
