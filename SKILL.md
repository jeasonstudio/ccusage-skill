---
name: ccusage
description: "Token usage statistics for Claude Code CLI. Use when users ask about token consumption, API costs, usage reports, or billing data. Triggers include 'token usage', 'how many tokens', 'API costs', 'usage report', 'spending', 'claude code usage', 'token consumption', 'cost breakdown', 'usage statistics', 'daily/weekly/monthly usage'."
---

# CCUsage - Claude Code Token Usage Statistics

Analyze token consumption and costs from Claude Code CLI usage.

## Quick Start

```bash
ccusage --json --offline
```

Default command shows daily breakdown. Always use `--json` for structured output and `--offline` to avoid API calls.

## Commands

| Command | Description |
|---------|-------------|
| `ccusage daily` | Usage by date (default) |
| `ccusage monthly` | Usage by month |
| `ccusage weekly` | Usage by week |
| `ccusage session` | Usage by conversation session |
| `ccusage blocks` | Usage by billing blocks (5-hour windows) |
| `ccusage statusline` | Compact status for hooks |

## Common Filters

```bash
# Date range
ccusage daily --json --offline --since 20260301 --until 20260311

# Specific project
ccusage daily --json --offline --project "my-project"

# Model breakdown
ccusage daily --json --offline --breakdown

# Instance breakdown
ccusage daily --json --offline --instances
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
ccusage daily --json --offline --since $(date +%Y%m%d)
```

**This month:**
```bash
ccusage monthly --json --offline --since $(date +%Y%m01)
```

**Cost by model:**
```bash
ccusage daily --json --offline --breakdown
```

**Most active sessions:**
```bash
ccusage session --json --offline --order desc
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