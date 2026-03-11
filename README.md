# ccusage-skill

Claude Code skill for token usage statistics using [ccusage](https://github.com/ryoppippi/ccusage).

## Installation

```bash
npx skills add jeasonstudio/ccusage-skill --agent claude-code
```

## Prerequisites

No global installation needed. ccusage is called via npx:

```bash
npx ccusage@latest --help
```

## Usage

After installation, simply ask Claude about your token usage:

```
# Basic queries
"我今天用了多少 token？"
"How many tokens did I use today?"
"本月 API 成本是多少？"
"Show me my usage report"

# Time range queries
"上周的 token 消耗"
"3月份的使用统计"
"最近7天的使用量"

# Detailed analysis
"按模型细分成本"
"哪个项目用的最多"
"显示会话使用情况"
```

## Commands Reference

| Command | Description |
|---------|-------------|
| `npx ccusage@latest daily` | Usage by date (default) |
| `npx ccusage@latest monthly` | Usage by month |
| `npx ccusage@latest weekly` | Usage by week |
| `npx ccusage@latest session` | Usage by conversation session |
| `npx ccusage@latest blocks` | Usage by billing blocks |

## Common Options

```bash
# Date range
npx ccusage@latest daily --json --offline --since 20260301 --until 20260311

# Specific project
npx ccusage@latest daily --json --offline --project "my-project"

# Model breakdown
npx ccusage@latest daily --json --offline --breakdown

# Sort by newest first
npx ccusage@latest daily --json --offline --order desc
```

## License

MIT