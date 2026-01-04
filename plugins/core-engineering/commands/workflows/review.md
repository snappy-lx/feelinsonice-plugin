---
name: workflows:review
description: Perform exhaustive code reviews using multi-agent analysis
argument-hint: "[PR number, GitHub URL, branch name, or empty for current]"
---

# Code Review Workflow

Perform exhaustive code reviews using multi-agent analysis and deep local inspection.

## Usage

```bash
/workflows:review              # Current branch vs main
/workflows:review 847          # PR number
/workflows:review feature/auth # Branch name
```

## Key Process Phases

### Phase 1: Setup & Target Determination

1. Identify review target (PR, URL, branch, or current state)
2. Prepare codebase for analysis
3. Get the diff to review

```bash
# For PR
gh pr diff [number]

# For branch
git diff main...[branch]

# For current
git diff
```

### Phase 2: Parallel Agent Analysis

Launch all review agents simultaneously:

**Core Reviewers:**
- architecture-strategist
- code-simplicity-reviewer
- security-sentinel
- performance-oracle
- pattern-recognition-specialist

**Language-Specific:**
- kieran-typescript-reviewer (for TS/JS)
- kieran-python-reviewer (for Python)
- julik-frontend-races-reviewer (for frontend)

**Conditional Agents:**
- data-integrity-guardian (for migrations)
- data-migration-expert (for data transforms)
- deployment-verification-agent (for deployment changes)

### Phase 3: Stakeholder Perspective Analysis

Consider review from multiple perspectives:

| Stakeholder | Concerns |
|-------------|----------|
| Developers | Maintainability, clarity, patterns |
| Operations | Deployment, monitoring, reliability |
| End Users | Performance, UX, accessibility |
| Security Team | Vulnerabilities, data protection |
| Business | Risk, compliance, value delivery |

### Phase 4: Comprehensive Synthesis

Consolidate findings by severity:

**P1 (Critical):**
- Security vulnerabilities
- Data corruption risks
- Breaking changes

**P2 (Important):**
- Performance issues
- Architectural concerns
- Reliability problems

**P3 (Nice-to-Have):**
- Code cleanup
- Minor optimizations
- Documentation improvements

## Deliverables

### Todo Files

Create in `todos/` directory:

```yaml
---
id: "001"
status: pending
priority: p1
category: security
title: "Fix SQL injection in user query"
location: "src/db/users.ts:42"
---

## Problem Statement
[Clear description of the issue]

## Findings
[Evidence from the review]

## Proposed Solutions

### Option 1: [Parameterized Query]
- Effort: Low
- Risk: Low
- Code: [Example fix]

### Option 2: [ORM Method]
- Effort: Medium
- Risk: Low
- Code: [Example fix]

## Acceptance Criteria
- [ ] Query uses parameterized inputs
- [ ] Tests cover injection attempts
```

### Review Summary

```markdown
## Code Review Summary

**Target:** [PR/Branch/Commit]
**Reviewers:** [List of agents used]

### Critical Issues (P1)
| Issue | Location | Agent | Status |
|-------|----------|-------|--------|
| [issue] | [file:line] | [agent] | [open] |

### Important Issues (P2)
[Similar table]

### Suggestions (P3)
[Similar table]

### Positive Observations
- [What's working well]
- [Good patterns observed]

### Next Steps
1. Address P1 issues before merge
2. Consider P2 improvements
3. Optional P3 enhancements
```

## Final Steps

### End-to-End Testing (Optional)

For web projects:
```bash
/playwright-test [target]
```

### Merge Gate

**DO NOT merge until P1 findings are resolved.**

### Post-Review Options

1. Run `/triage` to organize findings
2. Run `/workflows:work` to fix issues
3. Create follow-up issues for P3 items
