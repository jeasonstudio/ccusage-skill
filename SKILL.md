---
name: ccusage
description: "Token usage statistics for Claude Code CLI. Use when users ask about token consumption, API costs, usage reports, or billing data. Triggers include 'token usage', 'how many tokens', 'API costs', 'usage report', 'spending', 'claude code usage', 'token consumption', 'cost breakdown', 'usage statistics', 'daily/weekly/monthly usage'."
---

# CCUsage - Claude Code Token Usage Statistics

Analyze token consumption and costs from Claude Code CLI usage.

## Quick Start

```bash
npx ccusage@latest --json --offline
```

Default command shows daily breakdown. Always use `--json` for structured output and `--offline` to avoid API calls.

## Commands

| Command | Description |
|---------|-------------|
| `npx ccusage@latest daily` | Usage by date (default) |
| `npx ccusage@latest monthly` | Usage by month |
| `npx ccusage@latest weekly` | Usage by week |
| `npx ccusage@latest session` | Usage by conversation session |
| `npx ccusage@latest blocks` | Usage by billing blocks (5-hour windows) |
| `npx ccusage@latest statusline` | Compact status for hooks |

## Common Filters

```bash
# Date range
npx ccusage@latest daily --json --offline --since 20260301 --until 20260311

# Specific project
npx ccusage@latest daily --json --offline --project "my-project"

# Model breakdown
npx ccusage@latest daily --json --offline --breakdown

# Instance breakdown
npx ccusage@latest daily --json --offline --instances
```

## JSON Output Structure

### Daily/Monthly/Weekly
```json
{
  "daily": [{
    "date": "2026-03-11",
    "inputTokens": 1000,
    "outputTokens": 500,
    "cacheCreationTokens": 2000,
    "cacheReadTokens": 5000,
    "totalTokens": 8500,
    "totalCost": 0.05,
    "modelsUsed": ["claude-sonnet-4-6"],
    "modelBreakdowns": [...]
  }]
}
```

### Session
```json
{
  "sessions": [{
    "sessionId": "-path-to-project",
    "inputTokens": 1000,
    "outputTokens": 500,
    "totalCost": 0.05,
    "lastActivity": "2026-03-11",
    "modelsUsed": [...],
    "projectPath": "project-name"
  }]
}
```

### Blocks
```json
{
  "blocks": [{
    "id": "2026-03-11T08:00:00.000Z",
    "startTime": "...",
    "endTime": "...",
    "isActive": false,
    "totalTokens": 8500,
    "costUSD": 0.05,
    "models": [...]
  }]
}
```

## Common Queries

**Today's usage:**
```bash
npx ccusage@latest daily --json --offline --since $(date +%Y%m%d)
```

**This month:**
```bash
npx ccusage@latest monthly --json --offline --since $(date +%Y%m01)
```

**Cost by model:**
```bash
npx ccusage@latest daily --json --offline --breakdown
```

**Most active sessions:**
```bash
npx ccusage@latest session --json --offline --order desc
```

## Key Options

| Option | Description |
|--------|-------------|
| `-s, --since` | Start date (YYYYMMDD) |
| `-u, --until` | End date (YYYYMMDD) |
| `-p, --project` | Filter by project name |
| `-b, --breakdown` | Show per-model costs |
| `-i, --instances` | Show project breakdown |
| `-o, --order` | Sort: `asc` or `desc` |
| `-z, --timezone` | Timezone for grouping |
| `-O, --offline` | Use cached pricing |
| `-j, --json` | JSON output |