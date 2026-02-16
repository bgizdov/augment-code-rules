---
type: "always_apply"
---

# Deployment Safety

Do not run deploy, publish, or similar scripts and commands that will update production environments.

This includes:
- Deployment scripts (e.g., `deploy.sh`, `publish.sh`)
- Package publishing commands (e.g., `npm publish`, `cargo publish`)
- Database migration scripts that affect production
- Infrastructure provisioning commands
- Any command that modifies production state

Always ask for explicit permission before executing any production-related commands.