---
name: deepen-plan
description: Enhance an existing plan with parallel research agents for best practices, performance, and implementation details
argument-hint: "[plan file path]"
---

# Deepen Plan - Power Enhancement Mode

Take an existing plan (from `/workflows:plan`) and enhance each section with parallel research agents.

## Plan File

<plan_path> #$ARGUMENTS </plan_path>

**If the plan path above is empty:**
1. Check for recent plans: `ls -la plans/`
2. Ask the user: "Which plan would you like to deepen? Please provide the path (e.g., `plans/my-feature.md`)."

Do not proceed until you have a valid plan file path.

## Main Tasks

### 1. Parse and Analyze Plan Structure

Read the plan file and extract:
- [ ] Overview/Problem Statement
- [ ] Proposed Solution sections
- [ ] Technical Approach/Architecture
- [ ] Implementation phases/steps
- [ ] Code examples and file references
- [ ] Acceptance criteria
- [ ] Any UI/UX components mentioned
- [ ] Technologies/frameworks mentioned
- [ ] Domain areas (data models, APIs, UI, security, performance, etc.)

### 2. Discover and Apply Available Skills

**Step 1: Discover ALL available skills**

```bash
# Project-local skills
ls .claude/skills/

# User's global skills
ls ~/.claude/skills/

# Plugin skills
find ~/.claude/plugins/cache -type d -name "skills" 2>/dev/null
```

**Step 2: For each skill, read its SKILL.md to understand what it does**

**Step 3: Match skills to plan content**

**Step 4: Spawn a sub-agent for EVERY matched skill**

### 3. Launch Per-Section Research Agents

For each major section, launch parallel research:

```
Task Explore: "Research best practices, patterns, and real-world examples for: [section topic].
Find:
- Industry standards and conventions
- Performance considerations
- Common pitfalls and how to avoid them
- Documentation and tutorials
Return concrete, actionable recommendations."
```

### 4. Discover and Run ALL Review Agents

**Step 1: Discover ALL available agents**

```bash
# Project-local agents
find .claude/agents -name "*.md" 2>/dev/null

# User's global agents
find ~/.claude/agents -name "*.md" 2>/dev/null

# Plugin agents (all subdirectories)
find ~/.claude/plugins/cache -path "*/agents/*.md" 2>/dev/null
```

**Step 2: Launch ALL agents in parallel**

For EVERY agent discovered, launch a Task in parallel to review the plan.

### 5. Synthesize Everything

Collect outputs from ALL sources:
- Skill-based sub-agents
- Research agents
- Review agents
- Web searches

For each agent's findings, extract:
- [ ] Concrete recommendations (actionable items)
- [ ] Code patterns and examples (copy-paste ready)
- [ ] Anti-patterns to avoid (warnings)
- [ ] Performance considerations
- [ ] Security considerations
- [ ] Edge cases discovered
- [ ] Documentation links

### 6. Enhance Plan Sections

**Enhancement format for each section:**

```markdown
## [Original Section Title]

[Original content preserved]

### Research Insights

**Best Practices:**
- [Concrete recommendation 1]
- [Concrete recommendation 2]

**Performance Considerations:**
- [Optimization opportunity]
- [Benchmark or metric to target]

**Implementation Details:**
```[language]
// Concrete code example from research
```

**Edge Cases:**
- [Edge case 1 and how to handle]
- [Edge case 2 and how to handle]

**References:**
- [Documentation URL 1]
- [Documentation URL 2]
```

### 7. Add Enhancement Summary

At the top of the plan:

```markdown
## Enhancement Summary

**Deepened on:** [Date]
**Sections enhanced:** [Count]
**Research agents used:** [List]

### Key Improvements
1. [Major improvement 1]
2. [Major improvement 2]
3. [Major improvement 3]

### New Considerations Discovered
- [Important finding 1]
- [Important finding 2]
```

## Output Format

Update the plan file in place (or create `plans/<original-name>-deepened.md` if requested).

## Quality Checks

Before finalizing:
- [ ] All original content preserved
- [ ] Research insights clearly marked and attributed
- [ ] Code examples are syntactically correct
- [ ] Links are valid and relevant
- [ ] No contradictions between sections
- [ ] Enhancement summary accurately reflects changes

## Post-Enhancement Options

After writing the enhanced plan, use the **AskUserQuestion tool** to present options:

**Question:** "Plan deepened at `[plan_path]`. What would you like to do next?"

**Options:**
1. **View diff** - Show what was added/changed
2. **Run `/plan_review`** - Get feedback from reviewers
3. **Start `/workflows:work`** - Begin implementing this enhanced plan
4. **Deepen further** - Run another round of research on specific sections
5. **Revert** - Restore original plan

NEVER CODE! Just research and enhance the plan.
