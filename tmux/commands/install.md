---
name: tmux:install
description: Add tmux-ctl to PATH for current session
---

Adds `tmux-ctl` to PATH for the current Claude Code session.

## Steps

1. Find the plugin installation path:
```bash
TMUX_BIN=$(find ~/.claude -name "tmux-ctl" -path "*/tmux/bin/tmux-ctl" 2>/dev/null | head -1)
TMUX_BIN_DIR=$(dirname "$TMUX_BIN")
```

2. Add to PATH and verify:
```bash
export PATH="$PATH:$TMUX_BIN_DIR" && which tmux-ctl
```

3. Inform user:
   - `tmux-ctl` is now available for this session
   - Run `/tmux:install` again in new sessions if needed
   - For permanent setup, add to shell config: `export PATH="$PATH:$TMUX_BIN_DIR"`
