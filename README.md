# Feelinsonice Plugin Marketplace

A collection of Claude Code plugins for enhanced development workflows.

## Available Plugins

| Plugin | Description |
|--------|-------------|
| [core-engineering](./plugins/core-engineering) | Systematic development methodology with 80% planning/review, 20% execution |

## Installation

Install plugins from this marketplace:

```bash
# Install a specific plugin
claude /plugin install feelinsonice/core-engineering

# Or install from local path during development
claude /plugin install ./plugins/core-engineering
```

## Repository Structure

```
feelinsonice-plugin/
├── .claude-plugin/
│   └── plugin.json      # Marketplace configuration
├── plugins/
│   └── core-engineering/  # Individual plugin
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── agents/
│       ├── commands/
│       ├── skills/
│       ├── CLAUDE.md
│       ├── README.md
│       └── CHANGELOG.md
└── README.md
```

## Adding New Plugins

1. Create a new directory under `plugins/`
2. Add `.claude-plugin/plugin.json` with plugin metadata
3. Add agents, commands, and skills as needed
4. Update this README to list the new plugin

## Contributing

See individual plugin READMEs for contribution guidelines.

## License

MIT
