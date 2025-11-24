---
name: tmux:install
description: Add tmux-ctl to PATH for current session
---

Adds `tmux-ctl` to PATH for the current Claude Code session.

## Steps

1. Add plugin bin directory to PATH:
```bash
export PATH="$PATH:$HOME/.claude/plugins/tmux@deevs-agent-system/bin"
```

2. Verify installation:
```bash
which tmux-ctl
```

3. Inform user:
   - `tmux-ctl` is now available for this session
   - Run `/tmux:install` again in new sessions if needed
   - Or add to shell config (~/.zshrc) for permanent availability
