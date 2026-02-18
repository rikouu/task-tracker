# 📋 Task Tracker

An [OpenClaw](https://github.com/openclaw/openclaw) skill for proactive task state management that survives session resets.

## Problem

AI agents lose all context when conversations reset or compact. Background tasks, multi-step workflows, and pending results vanish from memory.

## Solution

Task Tracker teaches your agent to maintain a live `memory/tasks.md` file — a persistent state snapshot of everything in progress. When a new session starts, the agent reads this file and picks up exactly where it left off.

## What Gets Tracked

- 🔄 **In Progress** — active tasks, background processes (session IDs, PIDs, servers, commands)
- ✅ **Completed** — results, output links, summaries
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
4. **Auto-prune** — completed tasks older than 3 days get cleaned up

## Example

```markdown
# Active Tasks

## [bench-01] ECS Benchmark - server-a
- **Status**: 🔄 进行中
- **Requested**: 2026-02-19 02:38
- **Background**: warm-sage (PID 12345) on server-a — `bash ecs.sh`
- **Notes**: CPU test done, running disk fio

## [deploy-03] Deploy nginx config
- **Status**: ✅ 完成
- **Result**: nginx reloaded, SSL cert verified
```

## License

MIT
