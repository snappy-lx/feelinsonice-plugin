---
name: workflows:work
description: Execute work plans efficiently while maintaining quality and finishing features
argument-hint: "[plan file, specification, or todo file path]"
---

# Work Plan Execution Command

Execute a work plan efficiently while maintaining quality and finishing features.

## Input Document

<input_document> #$ARGUMENTS </input_document>

**If empty:** Ask user for the plan file path or what they want to work on.

## Execution Workflow

### Phase 1: Quick Start

#### 1. Read Plan and Clarify
- Read the work document completely
- Review all references mentioned
- Ask clarifying questions if needed
- Get user approval before proceeding

#### 2. Setup Environment
Choose between:
- **Live work** - Current branch
- **Parallel work** - Git worktree (recommended for multiple features)

#### 3. Create Todo List
Using TodoWrite:
- Break plan into actionable tasks
- Include dependencies between tasks
- Prioritize by implementation order
- Keep tasks specific and completable

### Phase 2: Execute

#### 1. Task Execution Loop

For each task:
1. Mark as `in_progress` in TodoWrite
2. Read referenced files from plan
3. Look for similar code patterns in codebase
4. Implement following conventions
5. Write tests for new functionality
6. Run tests to verify
7. Mark as `completed` in TodoWrite

#### 2. Follow Existing Patterns

- Read plan references first
- Match naming conventions
- Reuse existing components
- Follow coding standards from CLAUDE.md
- Grep for similar implementations

#### 3. Test Continuously

- Run relevant tests after significant changes
- Don't wait until the end
- Fix failures immediately

#### 4. Figma Design Sync (For UI Work)

- Implement components following design specs
- Use figma-design-sync agent iteratively
- Capture screenshots for comparison

#### 5. Track Progress

- Keep TodoWrite updated
- Note blockers in task notes
- Create new tasks if scope expands
- Keep user informed of progress

### Phase 3: Quality Check

#### 1. Run Core Quality Checks

```bash
# Run tests
npm test  # or pytest, etc.

# Run linting
npm run lint  # or equivalent
```

#### 2. Consider Reviewer Agents

Use for complex, risky, or large changes:
- code-simplicity-reviewer
- performance-oracle
- security-sentinel
- kieran-typescript-reviewer (for TS)
- kieran-python-reviewer (for Python)

#### 3. Final Validation

- [ ] All TodoWrite tasks completed
- [ ] Tests pass
- [ ] Linting passes
- [ ] Code follows existing patterns
- [ ] Designs match (if UI work)
- [ ] No console errors

### Phase 4: Ship It

#### 1. Create Commit

```bash
git add .
git commit -m "feat: [descriptive message]

- Implementation details
- Key changes made

Co-Authored-By: Claude <noreply@anthropic.com>"
```

#### 2. Capture Screenshots (For UI Changes)

Use Playwright MCP to capture before/after screenshots.

#### 3. Create Pull Request

```bash
gh pr create --title "feat: [title]" --body "$(cat <<'EOF'
## Summary
[Brief description of changes]

## Changes
- [Change 1]
- [Change 2]

## Testing
- [ ] Tests pass
- [ ] Manual testing done

## Screenshots
[Before/after if applicable]

EOF
)"
```

#### 4. Notify User

- Summarize what was completed
- Link to PR
- Note any follow-up work needed
- Suggest next steps

## Key Principles

| Principle | Meaning |
|-----------|---------|
| Start fast, execute faster | Don't over-analyze, begin implementing |
| The plan is your guide | Refer back to plan frequently |
| Test as you go | Don't leave testing for the end |
| Quality is built in | Follow patterns, run checks continuously |
| Ship complete features | Don't leave things 80% done |

## Quality Checklist

- [ ] All clarifying questions asked and answered
- [ ] All TodoWrite tasks marked completed
- [ ] Tests pass
- [ ] Linting passes
- [ ] Code follows existing patterns
- [ ] Figma designs match (if applicable)
- [ ] Screenshots captured (for UI changes)
- [ ] Commit messages follow conventional format
- [ ] PR description is complete

## When to Use Reviewer Agents

Use only when:
- Large refactors (10+ files)
- Security-sensitive changes
- Performance-critical code
- Complex algorithms
- Explicit user request

## Common Pitfalls to Avoid

| Pitfall | Why It's Bad |
|---------|--------------|
| Analysis paralysis | Blocks progress |
| Skipping clarifying questions | Leads to rework |
| Ignoring plan references | Misses context |
| Testing at the end | Late failures |
| Forgetting TodoWrite | Loses progress tracking |
| 80% done syndrome | Features never ship |
| Over-reviewing simple changes | Wastes time |
