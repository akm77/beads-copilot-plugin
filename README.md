# beads-copilot-plugin

GitHub Copilot CLI plugin for [beads](https://github.com/gastownhall/beads) — a distributed graph issue tracker for AI agents, powered by Dolt.

This is a full-featured adaptation of the [original Claude Code plugin](https://github.com/gastownhall/beads/tree/main/claude-plugin) for GitHub Copilot CLI, providing the same quality of integration.

## Features

- **25+ slash commands** — `/beads:ready`, `/beads:create`, `/beads:show`, `/beads:close`, and more
- **Autonomous task agent** — finds and completes ready work
- **Deep skill integration** — persistent memory, dependency tracking, compaction survival
- **MCP server** — full beads-mcp integration for natural language interaction
- **Session hooks** — auto-loads context on session start and before compaction
- **15 resource guides** — workflows, patterns, troubleshooting, advanced features

## Prerequisites

- [GitHub Copilot CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli) installed
- [beads CLI](https://github.com/gastownhall/beads) (`bd`) installed and in PATH (v0.60.0+)
- [uv](https://github.com/astral-sh/uv) package manager (for MCP server)

## Installation

### From GitHub

```bash
copilot plugin install gastownhall/beads-copilot-plugin
```

### From local clone

```bash
git clone https://github.com/gastownhall/beads-copilot-plugin.git
copilot plugin install ./beads-copilot-plugin
```

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
├── commands/                # 25+ slash commands
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

## How It Compares

| Feature | This Plugin | Author's Copilot Integration |
|---------|-------------|------------------------------|
| Slash commands | 25+ commands | None |
| Agent | Autonomous task agent | None |
| Skill with resources | Full skill + 15 guides | Instructions file only |
| Hooks | SessionStart + PreCompact | None |
| MCP server | Included | Manual setup required |
| Installation | `copilot plugin install` | Manual file editing |

## Updating

```bash
copilot plugin update beads
```

## Uninstalling

```bash
copilot plugin uninstall beads
```

## License

MIT — same as [beads](https://github.com/gastownhall/beads).

## Credits

- [Steve Yegge](https://github.com/steveyegge) — beads creator
- Original [Claude Code plugin](https://github.com/gastownhall/beads/tree/main/claude-plugin)
