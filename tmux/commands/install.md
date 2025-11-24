---
name: tmux:install
description: Setup tmux-ctl for current session
---

Configures tmux-ctl access for the current Claude Code session.

## Steps

1. Find the plugin installation path:
```bash
find ~/.claude -name "tmux-ctl" -path "*/tmux/bin/tmux-ctl" 2>/dev/null | head -1
```

2. Inform user of the full path found

3. **IMPORTANT**: Update SKILL.md to use full path instead of just `tmux-ctl`:
   - Replace all `tmux-ctl` commands with the full path
   - Example: `tmux-ctl eval "echo test"` → `/full/path/to/tmux-ctl eval "echo test"`

4. Tell user:
   - `tmux-ctl` is now configured (using full path)
   - For cleaner commands, add to shell config: `export PATH="$PATH:/path/to/tmux/bin"`
   - Or create symlink: `ln -sf /path/to/tmux-ctl /usr/local/bin/tmux-ctl`
