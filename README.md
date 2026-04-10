# beads-copilot-plugin

**English** | [Русский](README.ru.md)

GitHub Copilot CLI plugin for [beads](https://github.com/gastownhall/beads) — a distributed graph issue tracker for AI agents, powered by Dolt.

This is a full-featured adaptation of the [original Claude Code plugin](https://github.com/gastownhall/beads/tree/main/claude-plugin) for GitHub Copilot CLI, providing the same quality of integration.

## Features

- **25 slash commands** — `/beads:ready`, `/beads:create`, `/beads:show`, `/beads:close`, and more
- **Autonomous task agent** — finds and completes ready work
- **Deep skill integration** — persistent memory, dependency tracking, compaction survival
- **MCP server** — full beads-mcp integration for natural language interaction
- **Session hooks** — auto-loads context on session start and before compaction
- **15 resource guides** — workflows, patterns, troubleshooting, advanced features

## Prerequisites

- [GitHub Copilot CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli) installed
  <!-- TODO: Update link when stable Copilot CLI plugin system docs are published -->
- [beads CLI](https://github.com/gastownhall/beads) (`bd`) installed and in PATH (v0.60.0+)
- [uv](https://github.com/astral-sh/uv) package manager (for MCP server)

## Installation

### From GitHub

```bash
copilot plugin install akm77/beads-copilot-plugin
```

### From local clone

```bash
git clone https://github.com/akm77/beads-copilot-plugin.git
copilot plugin install ./beads-copilot-plugin
```

### From marketplace

```bash
copilot plugin marketplace add akm77/copilot-marketplace
copilot plugin install beads@akm77-marketplace
```

> **Note:** The Copilot CLI plugin ecosystem is still evolving. The installation commands above
> reflect the current documentation. If something doesn't work, try the local clone method
> or check `copilot plugin --help` for the latest syntax.

### Verify installation

```bash
copilot plugin list
```

In an interactive session:
```
/plugin list
/beads:version
```

## Quick Start

1. **Initialize beads** in your project:
   ```bash
   bd init
   ```

2. **Start a Copilot CLI session** and use beads commands:
   ```
   /beads:ready          # Find unblocked work
   /beads:create         # Create a new issue
   /beads:workflow       # See the full workflow guide
   ```

3. **Or use natural language** (via MCP):
   ```
   "What issues are ready to work on?"
   "Create a bug for the login timeout issue"
   "Show me the dependency tree for bd-42"
   ```

## Available Commands

| Command | Description |
|---------|-------------|
| `/beads:ready` | Find ready-to-work tasks |
| `/beads:create` | Create a new issue |
| `/beads:show` | Show issue details |
| `/beads:update` | Update issue fields |
| `/beads:close` | Close a completed issue |
| `/beads:list` | List issues with filters |
| `/beads:search` | Search issues by text |
| `/beads:dep` | Manage dependencies |
| `/beads:blocked` | Show blocked issues |
| `/beads:comments` | View/add comments |
| `/beads:stats` | Project statistics |
| `/beads:workflow` | Workflow guide |
| `/beads:epic` | Epic management |
| `/beads:label` | Manage labels |
| `/beads:decision` | Record decisions |
| `/beads:template` | Issue templates |
| `/beads:audit` | Audit logging |
| `/beads:init` | Initialize beads |
| `/beads:prime` | Load AI context |
| `/beads:version` | Version info |
| `/beads:export` | Export to JSONL |
| `/beads:compact` | Compact old issues |
| `/beads:reopen` | Reopen closed issues |
| `/beads:restore` | Restore compacted issues |
| `/beads:rename-prefix` | Rename issue prefix |
| `/beads:delete` | Delete issues |

## Architecture

```
beads-copilot-plugin/
├── plugin.json              # Plugin manifest
├── hooks.json               # Session & compaction hooks
├── mcp.json                 # MCP server configuration
├── agents/
│   └── task-agent.agent.md  # Autonomous task completion agent
├── commands/                # 25 slash commands
│   ├── ready.md
│   ├── create.md
│   ├── show.md
│   └── ...
└── skills/
    └── beads/
        ├── SKILL.md         # Main skill definition
        ├── CLAUDE.md        # Maintenance guide
        ├── README.md        # Human documentation
        ├── adr/             # Architecture Decision Records
        └── resources/       # 15 deep-dive guides
```

## Relationship to the Original

This plugin builds on the excellent work by [Steve Yegge](https://github.com/steveyegge) and the [beads](https://github.com/gastownhall/beads) project. The original repository provides a [Copilot integration guide](https://github.com/gastownhall/beads/blob/main/docs/COPILOT_INTEGRATION.md) based on MCP server setup and instruction files — a solid foundation that works well.

This plugin takes that further by packaging the full feature set of the [Claude Code plugin](https://github.com/gastownhall/beads/tree/main/claude-plugin) into the Copilot CLI plugin format, making it installable with a single command. We hope this stays true to the author's original vision while making beads more accessible to Copilot CLI users.

| Feature | This Plugin | Original Copilot Integration |
|---------|-------------|------------------------------|
| Slash commands | 25 commands | Via MCP tools |
| Agent | Autonomous task agent | — |
| Skill with resources | Full skill + 15 guides | Instruction file |
| Hooks | SessionStart + PreCompact | — |
| MCP server | Bundled | Manual setup |
| Installation | `copilot plugin install` | Manual configuration |

## Updating

```bash
copilot plugin update beads
```

> For local installs, re-run `copilot plugin install ./beads-copilot-plugin` after pulling new changes.

## Uninstalling

```bash
copilot plugin uninstall beads
```

> The name `beads` comes from the `name` field in `plugin.json`.

## Tested

Integration-tested with Copilot CLI v1.0.21-1.0.22 building a complete mini CRM application (Python + SQLAlchemy + SQLite). The plugin successfully handled epic creation, 13 task tracking issues with dependencies, claim/close lifecycle, and `bd prime` hooks across a full development workflow.

Demo project: [copilot-mini-crm](https://github.com/akm77/copilot-mini-crm)

## Known Limitations (Copilot CLI)

- **Permission fatigue**: Each distinct beads MCP tool name (`context`, `create`, `stats`, `list`, `claim`, `close`, etc.) requires a separate user approval prompt, even after selecting "approve all tools from server beads". This is a Copilot CLI behavior, not a beads plugin issue.
- **Parallel writes**: Embedded Dolt supports only one writer at a time. If Copilot dispatches multiple `create` calls in parallel, some will fail with a lock error. Copilot typically recovers by retrying sequentially.
- **Worktree permissions**: When using git worktrees, beads may warn about `.beads` directory permissions. Run `chmod 700 <worktree>/.beads` to resolve.

## License

MIT — same as [beads](https://github.com/gastownhall/beads).

## Credits

- [Steve Yegge](https://github.com/steveyegge) — beads creator
- Original [Claude Code plugin](https://github.com/gastownhall/beads/tree/main/claude-plugin)
