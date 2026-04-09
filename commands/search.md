---
description: Search issues by text query
argument-hint: "<query> [--status] [--label] [--assignee]"
---

Search issues across title, description, and ID with a simple text query.

**Note:** The `search` command is optimized for quick text searches and uses less context than `list` when accessed via MCP. For advanced filtering options, use `bd list`.

## Basic Usage

```bash
bd search "authentication bug"
bd search login --status open
bd search database --label backend
bd search "bd-5q"  # Search by partial issue ID
```

## Filters

- **--status, -s**: Filter by status (open, in_progress, blocked, closed)
- **--assignee, -a**: Filter by assignee
- **--type, -t**: Filter by type (bug, feature, task, epic, chore, decision)
- **--label, -l**: Filter by labels (must have ALL specified labels)
- **--label-any**: Filter by labels (must have AT LEAST ONE)
- **--limit, -n**: Limit number of results (default: 50)
- **--sort**: Sort by field: priority, created, updated, closed, status, id, title, type, assignee
- **--reverse, -r**: Reverse sort order
- **--long**: Show detailed multi-line output for each issue
- **--json**: Output results in JSON format

## Comparison with bd list

| Command | Best For | Default Limit | Context Usage |
|---------|----------|---------------|---------------|
| `bd search` | Quick text searches, exploratory queries | 50 | Low (efficient for LLMs) |
| `bd list` | Advanced filtering, precise queries | None | High (all results) |
