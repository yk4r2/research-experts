# Chain System

Multi-session workflow chains for maintaining linked context across conversations.

## Overview

Manage conversation "chains" - structured context across multiple sessions. Each chain link captures detailed technical state, making it easy to pause and resume complex projects without losing context.

**vs `/compact`**: `/compact` reduces context in single sessions; chains preserve detailed history across sessions for multi-session projects.

## Commands

### `/chain-link [chain-name]`
Saves current conversation chunk as a chain link.

**Captures**: User requests, code changes (files/lines), unresolved bugs with solutions attempted, pending tasks, next step.

**Saves to**: `.claude/chains/[chain-name]/[timestamp]-[slug].md`

### `/chain-load [chain-name]`
Loads most recent chain link to continue work.

**Shows**: Summary, next step, list of 5 most recent links, option to load additional links.

### `/chain-list`
Lists all available chains with link count and most recent work.

## Workflow

1. Work on feature → `/chain-link my-feature` when done
2. New session → `/chain-load my-feature` to continue
3. Multiple chains → `/chain-list` to see all ongoing work

## Installation

```bash
/plugin marketplace add https://github.com/Deevs/agent-system
/plugin install chain-system@deevs-agent-system
```

## File Structure

```
.claude/chains/
├── my-feature/
│   └── 2025-11-24-0145-implement-auth.md
└── bug-fixes/
    └── 2025-11-20-1000-investigate-timeout.md
```
