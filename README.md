# 📋 Task Tracker

An [OpenClaw](https://github.com/openclaw/openclaw) skill for proactive task state management that survives session resets.

## Problem

AI agents lose all context when conversations reset or compact. Background tasks, multi-step workflows, and pending results vanish from memory.

## Solution

Task Tracker teaches your agent to maintain a live `memory/tasks.md` file — a persistent state snapshot of everything in progress. When a new session starts, the agent reads this file and picks up exactly where it left off.

## What Gets Tracked

- 🔄 **In Progress** — active tasks, background processes (session IDs, PIDs, servers, commands)
- ✅ **Completed** — one-line summaries with references to daily notes
- ❌ **Failed** — errors, what went wrong
- ⏸️ **Paused** — waiting for user input or external dependency

## Install

```bash
clawhub install agent-task-tracker
```

Or manually copy `SKILL.md` into your OpenClaw workspace `skills/` directory.

## How It Works

The skill instructs the agent to:

1. **Write before reporting** — update `memory/tasks.md` before telling you results
2. **Record background processes** — session IDs, PIDs, servers, and commands
3. **Include enough detail to resume** — no prior conversation context needed
4. **Stay small** — 50 lines / 2KB limit, completed tasks compressed to one-line summaries
5. **Auto-prune** — completed tasks older than 3 days get cleaned up

## Example

```markdown
# Active Tasks

## [deploy-03] Deploy nginx config
- **Status**: 🔄 进行中
- **Requested**: 2026-02-19 02:38
- **Background**: warm-sage (PID 12345) on server-a — `sudo nginx -t && sudo systemctl reload nginx`
- **Notes**: config tested OK, reloading

# Completed (recent, auto-prune >3 days)

## [2026-02-19] Server benchmarks x3
itabashihome 1163/7150 | ali-tokyo 2942/3090 | oracle-arm 3362/13283
Details: memory/2026-02-19.md
```

## Design Principles

- **Write-first**: update file before reporting to user
- **Size-conscious**: read every session start, must stay lightweight (<2KB)
- **Self-maintaining**: auto-prune and compress keep it from growing unbounded

## License

MIT
