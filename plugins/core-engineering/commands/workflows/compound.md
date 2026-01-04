---
name: workflows:compound
description: Document recently solved problems to build team knowledge
argument-hint: "[optional: brief description of what was solved]"
---

# /workflows:compound - Knowledge Compounding

Document recently solved problems to build team knowledge. Creates structured documentation in `docs/solutions/` with searchable YAML frontmatter.

## Overview

When you solve a non-trivial problem, this command captures the solution for future reference. First solution takes time; documented solutions reduce future similar issues dramatically.

## Auto-Detection

Triggers on phrases like:
- "that worked"
- "problem solved"
- "fixed it"
- "got it working"

## Preconditions

Before documenting, verify:
- [ ] Solution is verified working
- [ ] Problem was non-trivial (not a simple typo)
- [ ] Solution has reusable insights

## Core Execution Strategy

Launch six specialized subagents simultaneously:

### 1. Context Analyzer
Extract problem type and symptoms, validate against schema.

### 2. Solution Extractor
Identify root cause and working fixes with code examples.

### 3. Related Docs Finder
Locate cross-references and related issues/PRs.

### 4. Prevention Strategist
Develop best practices and test cases to prevent recurrence.

### 5. Category Classifier
Determine optimal documentation category and filename.

### 6. Documentation Writer
Assemble final markdown with validated frontmatter.

## Categories

Documentation automatically sorts into:

| Category | Path |
|----------|------|
| Build errors | `docs/solutions/build-errors/` |
| Test failures | `docs/solutions/test-failures/` |
| Performance issues | `docs/solutions/performance-issues/` |
| Security issues | `docs/solutions/security-issues/` |
| Configuration fixes | `docs/solutions/configuration-fixes/` |
| Integration issues | `docs/solutions/integration-issues/` |
| Deployment issues | `docs/solutions/deployment-issues/` |
| Debugging patterns | `docs/solutions/debugging-patterns/` |
| Frontend issues | `docs/solutions/frontend-issues/` |

## Documentation Format

```yaml
---
title: "Brief descriptive title"
category: performance-issues
tags: [relevant, searchable, tags]
module: AffectedModule
symptom: "What the user observes"
root_cause: "Why it happens"
created: YYYY-MM-DD
---

## Problem

[Description of the problem and symptoms]

## Root Cause

[Explanation of why this happened]

## Solution

[Step-by-step fix with code examples]

```[language]
// Code that fixes the issue
```

## Prevention

[How to avoid this in the future]

## Related

- [Links to related documentation]
- [Related issues or PRs]
```

## Post-Documentation Agents

After documenting, auto-trigger specialized agents based on problem type:

| Problem Type | Agent |
|-------------|-------|
| Performance | performance-oracle |
| Security | security-sentinel |
| Architecture | architecture-strategist |

## Success Outcome

Creates searchable documentation enabling rapid reference for recurring issues. Knowledge compounds over time.

## Usage

```bash
# After solving a problem
/workflows:compound

# With description
/workflows:compound "Fixed N+1 query in user dashboard"
```
