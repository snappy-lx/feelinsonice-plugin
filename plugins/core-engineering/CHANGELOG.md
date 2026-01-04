# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-03

### Added

#### Agents
- **Review Agents (12)**
  - agent-native-reviewer
  - architecture-strategist
  - code-simplicity-reviewer
  - data-integrity-guardian
  - data-migration-expert
  - deployment-verification-agent
  - julik-frontend-races-reviewer
  - kieran-python-reviewer
  - kieran-typescript-reviewer
  - pattern-recognition-specialist
  - performance-oracle
  - security-sentinel

- **Research Agents (4)**
  - best-practices-researcher
  - framework-docs-researcher
  - git-history-analyzer
  - repo-research-analyst

- **Workflow Agents (3)**
  - bug-reproduction-validator
  - pr-comment-resolver
  - spec-flow-analyzer

- **Design Agents (3)**
  - design-implementation-reviewer
  - design-iterator
  - figma-design-sync

- **Docs Agents (1)**
  - ankane-readme-writer

#### Commands
- `/changelog` - Generate changelog from git merges
- `/create-agent-skill` - Create new skills with guidance
- `/deepen-plan` - Enhance plans with research
- `/plan_review` - Parallel plan review by agents
- `/playwright-test` - Run E2E tests on changed pages
- `/triage` - Categorize review findings into todos
- `/workflows:plan` - Transform ideas into structured plans
- `/workflows:work` - Execute plans efficiently
- `/workflows:review` - Comprehensive multi-agent code review
- `/workflows:compound` - Document solved problems for team knowledge

#### Skills
- agent-native-architecture
- create-agent-skills
- frontend-design
- git-worktree
- skill-creator
- file-todos
- gemini-imagegen

#### MCP Servers
- Playwright (browser automation)
- Context7 (library documentation)

### Notes

- Initial release based on compound-engineering-plugin structure
- Ruby/Rails specific components excluded
- Focus on language-agnostic engineering practices
