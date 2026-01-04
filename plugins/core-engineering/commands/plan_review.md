---
name: plan_review
description: Have multiple specialized agents review a plan in parallel
argument-hint: "[plan file path or plan content]"
---

# Plan Review

Have multiple specialized agents review a plan in parallel.

## Usage

```bash
/plan_review plans/my-feature.md
```

## Agents to Invoke

Run these review agents in parallel:

1. **@agent-architecture-strategist** - Review architectural implications
2. **@agent-code-simplicity-reviewer** - Ensure plan isn't over-engineered
3. **@agent-security-sentinel** - Check for security considerations
4. **@agent-performance-oracle** - Identify performance implications

For TypeScript/JavaScript plans:
- **@agent-kieran-typescript-reviewer** - TypeScript-specific review

For Python plans:
- **@agent-kieran-python-reviewer** - Python-specific review

## Review Process

1. Read the plan file at the specified path
2. Launch all applicable review agents in parallel
3. Collect feedback from each agent
4. Synthesize into a consolidated review

## Output Format

```markdown
## Plan Review Summary

### Architecture Review
[Findings from architecture-strategist]

### Simplicity Review
[Findings from code-simplicity-reviewer]

### Security Review
[Findings from security-sentinel]

### Performance Review
[Findings from performance-oracle]

### Language-Specific Review
[Findings from language-specific reviewer]

---

## Consolidated Recommendations

### Must Address (Before Implementation)
1. [Critical finding]
2. [Critical finding]

### Should Consider
1. [Important finding]
2. [Important finding]

### Nice to Have
1. [Minor improvement]
2. [Minor improvement]
```

## Next Steps

After review, offer options:
1. Update plan based on feedback
2. Proceed to `/workflows:work`
3. Request more specific review on a section
