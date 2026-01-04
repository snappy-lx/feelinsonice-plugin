# Core Engineering Plugin - Development Standards

## Overview

This plugin implements a systematic development methodology emphasizing an **80% planning/review to 20% execution ratio**. Each unit of engineering work should make subsequent units easier.

## Version Management

### Required Updates for All Changes

For any change to this plugin, update these three files:

1. `.claude-plugin/plugin.json` - Update version
2. `CHANGELOG.md` - Document changes
3. `README.md` - Verify component documentation is accurate

### Semantic Versioning

| Change Type | Version Bump | Examples |
|-------------|--------------|----------|
| Major | X.0.0 | Breaking changes, substantial reorganization |
| Minor | 0.X.0 | New agents, commands, or skills |
| Patch | 0.0.X | Bug fixes, documentation, minor enhancements |

## Documentation Standards

### Skills

All skills must include:
- YAML frontmatter with `name` and `description`
- Description in third person ("Guides creation of..." not "Guide creation of...")
- Markdown-formatted links (not backticks)
- Clear trigger phrases in description

### Agents

All agents must include:
- YAML frontmatter with `name` and `description`
- Example usage scenarios
- Clear output format specification

### Commands

All commands must include:
- YAML frontmatter with `name`, `description`, and `argument-hint`
- Clear workflow steps
- Error handling guidance

## Code Style

### General Principles

- **Explicit > Implicit**: Always prefer explicit code over implicit behavior
- **Duplication > Complexity**: Simple duplicated code beats complex abstractions
- **Adding modules is never bad; making modules complex is bad**

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Skills | lowercase-hyphenated | `git-worktree` |
| Agents | lowercase-hyphenated | `security-sentinel` |
| Commands | lowercase, underscores OK | `plan_review` |
| Workflow commands | `workflows:name` | `workflows:plan` |

## Workflow Philosophy

### The 80/20 Rule

- 80% of time on planning and review
- 20% of time on execution
- Well-planned work compounds over time

### Core Workflows

1. `/workflows:plan` - Transform ideas into structured plans
2. `/workflows:work` - Execute plans efficiently
3. `/workflows:review` - Comprehensive code review
4. `/workflows:compound` - Document solutions for future reference

## Quality Standards

### Before Merging Any Change

- [ ] All referenced agents/skills exist
- [ ] Version updated in plugin.json
- [ ] CHANGELOG updated
- [ ] README accurate
- [ ] No broken links
- [ ] Examples are correct

### Testing

Test changes by:
1. Installing the plugin locally
2. Running affected commands
3. Verifying agents work as documented
4. Checking skill triggers correctly

## Contributing

1. Follow the version management rules
2. Document changes in CHANGELOG.md
3. Update README.md if adding/removing components
4. Test before committing
