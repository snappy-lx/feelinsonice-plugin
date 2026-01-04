# Core Engineering Plugin

A systematic development methodology plugin for Claude Code emphasizing **80% planning/review to 20% execution**. Each unit of engineering work makes subsequent units easier.

## Installation

```bash
claude /plugin install core-engineering
```

## Components

### Agents (19 total)

#### Review Agents (12)
| Agent | Purpose |
|-------|---------|
| agent-native-reviewer | Reviews code for agent-native architecture compliance |
| architecture-strategist | Analyzes architectural decisions and patterns |
| code-simplicity-reviewer | Ensures code simplicity and YAGNI adherence |
| data-integrity-guardian | Reviews database migrations and data models |
| data-migration-expert | Validates data migrations against production |
| deployment-verification-agent | Generates deployment checklists |
| julik-frontend-races-reviewer | Reviews frontend code for race conditions |
| kieran-python-reviewer | High-quality Python code review |
| kieran-typescript-reviewer | High-quality TypeScript code review |
| pattern-recognition-specialist | Analyzes code patterns and anti-patterns |
| performance-oracle | Reviews code for performance issues |
| security-sentinel | Comprehensive security audits |

#### Research Agents (4)
| Agent | Purpose |
|-------|---------|
| best-practices-researcher | Researches external best practices |
| framework-docs-researcher | Gathers framework documentation |
| git-history-analyzer | Analyzes git history for context |
| repo-research-analyst | Systematic repository research |

#### Workflow Agents (3)
| Agent | Purpose |
|-------|---------|
| bug-reproduction-validator | Validates bug reports through reproduction |
| pr-comment-resolver | Addresses PR review comments |
| spec-flow-analyzer | Analyzes specs for user flows and gaps |

#### Design Agents (3)
| Agent | Purpose |
|-------|---------|
| design-implementation-reviewer | Compares implementations to Figma designs |
| design-iterator | Iterative design refinement |
| figma-design-sync | Synchronizes code with Figma designs |

#### Docs Agents (1)
| Agent | Purpose |
|-------|---------|
| ankane-readme-writer | Creates Ankane-style README files |

### Commands (10 total)

#### Utility Commands (6)
| Command | Purpose |
|---------|---------|
| `/changelog` | Generate changelog from git merges |
| `/create-agent-skill` | Create new skills with guidance |
| `/deepen-plan` | Enhance plans with research |
| `/plan_review` | Parallel plan review by agents |
| `/playwright-test` | Run E2E tests on changed pages |
| `/triage` | Categorize review findings into todos |

#### Workflow Commands (4)
| Command | Purpose |
|---------|---------|
| `/workflows:plan` | Transform ideas into structured plans |
| `/workflows:work` | Execute plans efficiently |
| `/workflows:review` | Comprehensive multi-agent code review |
| `/workflows:compound` | Document solved problems for team knowledge |

### Skills (7 total)

| Skill | Purpose |
|-------|---------|
| agent-native-architecture | Build prompt-native agent systems |
| create-agent-skills | Author Claude Code skills |
| frontend-design | Create distinctive UI designs |
| git-worktree | Manage git worktrees for parallel work |
| skill-creator | Create skill packages |
| file-todos | Markdown-based todo tracking |
| gemini-imagegen | Generate images with Gemini API |

### MCP Servers (2)

| Server | Purpose |
|--------|---------|
| Playwright | Browser automation for testing |
| Context7 | Library documentation context |

## Quick Start

### Plan a Feature
```bash
/workflows:plan Add user authentication with OAuth
```

### Review Code
```bash
/workflows:review 847  # Review PR #847
```

### Execute a Plan
```bash
/workflows:work plans/add-oauth.md
```

### Document a Solution
```bash
/workflows:compound  # After solving a problem
```

## Philosophy

This plugin implements a systematic approach where:

1. **Planning compounds** - Well-structured plans make implementation faster
2. **Reviews compound** - Thorough reviews prevent future bugs
3. **Documentation compounds** - Solved problems become team knowledge
4. **Patterns compound** - Following conventions reduces cognitive load

## License

MIT
