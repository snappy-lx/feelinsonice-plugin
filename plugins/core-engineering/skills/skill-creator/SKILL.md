---
name: skill-creator
description: Create skills—modular packages that extend Claude's capabilities with specialized knowledge, workflows, and tool integrations. Use when building new skills from scratch or packaging existing knowledge into reusable format.
---

# Skill Creator

Create skills—modular, self-contained packages that extend Claude's capabilities with specialized knowledge, workflows, and tools.

## What Are Skills?

Skills consist of:
- **Required:** SKILL.md file with metadata and instructions
- **Optional:** Scripts, references, assets, templates

## Six-Step Creation Process

### 1. Understand with Examples

Before creating:
- Gather 3-5 concrete use cases
- Validate functionality requirements
- Identify what Claude needs to know/do

```markdown
## Use Cases

1. User wants to [action] when [context]
2. User needs to [action] for [purpose]
3. User asks to [action] with [constraints]
```

### 2. Plan Contents

Identify what the skill needs:

| Type | Purpose | Example |
|------|---------|---------|
| Scripts | Automation | `scripts/process.py` |
| References | Documentation | `references/api-docs.md` |
| Assets | Static files | `assets/template.json` |
| Templates | Starting points | `templates/config.yaml` |

### 3. Initialize Structure

Create the skill directory:

```
my-skill/
├── SKILL.md
├── scripts/
├── references/
└── assets/
```

### 4. Write SKILL.md

```yaml
---
name: my-skill
description: What it does. When to use it.
allowed-tools: Tool(specific-tool)
---

# Skill Name

Brief overview of what this skill enables.

## Quick Start

Immediate usage example.

## Instructions

Step-by-step guidance for Claude.

## Examples

### Example 1: [Scenario]

Input: [what user provides]
Output: [what Claude produces]

## Guidelines

- Best practice 1
- Best practice 2
```

### 5. Create Supporting Files

**Scripts** - Make executable and handle errors:

```python
#!/usr/bin/env python3
"""Script description."""

import sys

def main():
    try:
        # Do work
        pass
    except Exception as e:
        print(f"Error: {e}", file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**References** - Keep focused and under 5k words each.

### 6. Test and Iterate

Test with real tasks:
1. Use the skill for actual work
2. Note where instructions are unclear
3. Add examples for edge cases
4. Refine based on failures

## Context Management

Skills use progressive disclosure:

| Stage | Content | Size |
|-------|---------|------|
| Discovery | Metadata only | ~100 words |
| Triggered | SKILL.md loaded | <5k words |
| Deep Use | References loaded | As needed |

## Quality Checklist

Before publishing:

- [ ] Name follows conventions (lowercase, hyphens)
- [ ] Description has what AND when
- [ ] SKILL.md under 500 lines
- [ ] Examples are concrete and testable
- [ ] Scripts have error handling
- [ ] References are focused (<5k words each)
- [ ] Tested with real use cases

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Vague instructions | Add specific examples |
| Too much content | Split into references |
| No error handling | Add try/catch in scripts |
| Generic description | Include trigger phrases |
| Untested | Use for real work |
