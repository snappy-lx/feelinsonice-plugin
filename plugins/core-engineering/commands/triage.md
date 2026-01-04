---
name: triage
description: Categorize findings from code reviews, security audits, and performance analyses
argument-hint: "[path to pending todos or review output]"
---

# Triage Command

Categorize findings from code reviews, security audits, and performance analyses into actionable todos.

## Workflow Phases

### Step 1: Present Findings

For each finding, display:
- **Severity**: P1 (Critical), P2 (Important), P3 (Nice-to-Have)
- **Category**: Security, Performance, Architecture, Code Quality, etc.
- **Location**: File path and line numbers
- **Problem**: Description of the issue
- **Scenario**: How it could cause problems
- **Proposed Solution**: Recommended fix

### Step 2: User Decision

For each finding, ask:

**Options:**
- `yes` - Create/update todo for this finding
- `next` - Skip this finding (won't create todo)
- `custom` - Modify the finding before deciding

### Step 3: File Management

Based on decision:

**Yes:**
- Create todo file: `todos/{id}-ready-{priority}-{description}.md`
- Update YAML frontmatter: `status: ready`

**Next:**
- Skip without creating file
- (If file exists, delete it)

**Custom:**
- Gather modifications
- Re-present finding
- Ask again

### Step 4: Summary

After all findings processed:

```markdown
## Triage Summary

**Total Items:** [count]
**Approved Todos:** [count]
**Skipped:** [count]

### Created Todos
- `todos/001-ready-p1-fix-sql-injection.md`
- `todos/002-ready-p2-optimize-query.md`

### Next Steps
1. Run `/resolve_todo_parallel` to implement approved todos
2. Commit the todos
3. End session
```

## Critical Constraints

**DO NOT CODE** - Triage only categorizes; implementation happens in `/resolve_todo_parallel`

**File Naming**: `{id}-ready-{priority}-{description}.md`
- Priorities: p1, p2, p3

**Progress Tracking**: Display X/Y completed with time estimates

## Todo File Format

```yaml
---
id: "001"
status: ready
priority: p1
category: security
title: "Fix SQL injection vulnerability"
location: "src/db/queries.ts:42"
---

## Problem
[Description of the issue]

## Evidence
[Code snippet or log showing the problem]

## Proposed Solutions

### Option 1: [Name]
- Effort: [Low/Medium/High]
- Risk: [Low/Medium/High]
- Description: [How to fix]

### Option 2: [Name]
- Effort: [Low/Medium/High]
- Risk: [Low/Medium/High]
- Description: [Alternative approach]

## Acceptance Criteria
- [ ] [Criteria 1]
- [ ] [Criteria 2]

## References
- [Related documentation or issues]
```

## Priority Guidelines

**P1 (Critical):**
- Security vulnerabilities
- Data corruption risks
- Breaking changes in production
- Blocking issues

**P2 (Important):**
- Performance issues affecting users
- Architectural concerns
- Reliability problems
- Technical debt with growing cost

**P3 (Nice-to-Have):**
- Code cleanup
- Minor optimizations
- Documentation improvements
- Style consistency

## Final Options

After triage completion, offer:

1. **Run `/resolve_todo_parallel`** - Implement approved todos
2. **Commit the todos** - Save for later
3. **End session** - Exit without further action
