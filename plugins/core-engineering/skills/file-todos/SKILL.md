---
name: file-todos
description: Markdown-based todo system for tracking code review feedback, technical debt, and work items in the todos/ directory. Use when creating persistent todos that survive sessions, tracking multi-step work items, or managing technical debt.
---

# File-Based Todo Tracking

Manage a markdown-based todo system in the `todos/` directory for tracking code review feedback, technical debt, and work items.

## Directory Structure

```
todos/
├── 001-ready-p1-fix-sql-injection.md
├── 002-pending-p2-optimize-query.md
├── 003-complete-p3-add-docs.md
└── README.md
```

## Naming Convention

```
{issue_id}-{status}-{priority}-{description}.md
```

| Component | Values | Example |
|-----------|--------|---------|
| issue_id | Sequential 3-digit | 001, 002, 003 |
| status | pending, ready, complete | ready |
| priority | p1, p2, p3 | p1 |
| description | kebab-case summary | fix-sql-injection |

## Priority Levels

| Priority | Meaning | Response Time |
|----------|---------|---------------|
| p1 | Critical - Security, data loss, breaking | Immediate |
| p2 | Important - Performance, UX, maintainability | This sprint |
| p3 | Nice-to-have - Cleanup, optimization, docs | When convenient |

## File Template

```markdown
---
id: "001"
status: pending
priority: p1
category: security
title: "Fix SQL injection vulnerability"
location: "src/db/queries.ts:42"
created: 2024-01-15
dependencies: []
---

## Problem Statement

Clear description of what needs to be done and why.

## Findings

Evidence discovered during review:
- [Finding 1]
- [Finding 2]

## Proposed Solutions

### Option 1: [Name]
- **Effort:** Low/Medium/High
- **Risk:** Low/Medium/High
- **Description:** How to implement

### Option 2: [Name]
- **Effort:** Low/Medium/High
- **Risk:** Low/Medium/High
- **Description:** Alternative approach

## Acceptance Criteria

- [ ] Criteria 1
- [ ] Criteria 2
- [ ] Tests pass
- [ ] No regressions

## Work Log

### [Date] - Session 1
- **Actions:** What was done
- **Learnings:** What was discovered
- **Files:** Files modified
- **Next:** What's left
```

## Core Workflows

### Creating a Todo

1. Determine next ID: `ls todos/ | sort | tail -1`
2. Create file with template
3. Fill required sections
4. Set status: `pending` (needs triage) or `ready` (can start)

```bash
# Example
touch todos/004-pending-p2-refactor-auth.md
```

### Triaging Todos

Review pending items and decide:
- **Approve** → Change status to `ready`
- **Defer** → Keep as `pending`, add note
- **Reject** → Delete file

```bash
# Rename to ready
mv todos/004-pending-p2-refactor-auth.md todos/004-ready-p2-refactor-auth.md
```

### Working a Todo

1. Change status to `ready` if not already
2. Add work log entry
3. Do the work
4. Update acceptance criteria
5. Change status to `complete` when done

### Managing Dependencies

Track blockers in frontmatter:

```yaml
dependencies: ["001", "003"]
```

Only start work when dependencies are complete.

## When to Create a Todo

**Create a todo when:**
- Work requires 15+ minutes
- Research is needed
- Has dependencies on other work
- Needs approval or triage
- Is technical debt to track

**Don't create a todo when:**
- Fix is trivial (<5 minutes)
- Solution is obvious
- No tracking needed

## Integration

This file-based system is for **persistent tracking** across sessions. It differs from:
- **TodoWrite tool** - Session-only task tracking
- **GitHub Issues** - External issue tracking
- **Project boards** - Sprint planning

Use file todos for work items that need detailed tracking and work logs.
