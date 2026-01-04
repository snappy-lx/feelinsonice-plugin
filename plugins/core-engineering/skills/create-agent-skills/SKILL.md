---
name: create-agent-skills
description: Expert guidance for authoring Claude Code Skills—reusable prompts that extend Claude's capabilities through the SKILL.md format. Use when creating new skills, improving existing skills, or learning skill best practices.
---

# Creating Agent Skills

Author Claude Code Skills—reusable prompts that extend Claude's capabilities through the SKILL.md format.

## Core Principles

**Skills as Prompts:** Apply standard prompting best practices. Be clear and direct, assuming Claude's intelligence.

**Format Standard:** Use YAML frontmatter with markdown body. No XML tags—use standard markdown headings.

**Progressive Disclosure:** Keep primary SKILL.md under 500 lines. Split detailed content into separate reference files loaded as needed.

**Strong Descriptions:** Include both functionality AND usage triggers.

```yaml
description: Extracts text and tables from PDF files, fills forms, merges documents. Use when working with PDF files...
```

## Required Structure

### Frontmatter Fields

```yaml
---
name: skill-name              # Required: lowercase, hyphens, max 64 chars
description: What + when      # Required: max 1024 chars
allowed-tools: Tool(name)     # Optional: pre-approved tools
model: sonnet                 # Optional: specific model requirement
---
```

### Body Sections

1. **Quick Start** - Immediate usage
2. **Instructions** - Core guidance
3. **Examples** - Concrete usage
4. **Advanced Features** - Extended capabilities
5. **Guidelines** - Best practices

## Naming Convention

Use gerund form (verb + -ing):
- `processing-pdfs`
- `analyzing-spreadsheets`
- `generating-reports`

**Avoid:** Generic terms like `helper`, `utils`, or `claude-*` prefixes.

## File Organization

```
skill-folder/
├── SKILL.md          # Entry point (required)
├── reference.md      # Detailed documentation
├── examples.md       # Usage samples
└── scripts/          # Utility scripts
    └── helper.py
```

## Writing Guidelines

### Be Direct
```markdown
# Good
Generate a report using [format].

# Bad
You might want to consider generating a report...
```

### Provide Examples

```markdown
## Example: Processing a CSV

Input: `data.csv` with columns [name, email, status]

Output:
```json
{
  "total": 150,
  "active": 120,
  "inactive": 30
}
```
```

### Handle Errors

```markdown
## Error Handling

If the file doesn't exist:
1. Check the path is correct
2. Verify file permissions
3. Report: "File not found: [path]"
```

## Quality Checklist

Before publishing:

- [ ] Name is lowercase with hyphens
- [ ] Description includes what AND when
- [ ] SKILL.md under 500 lines
- [ ] Examples are concrete and testable
- [ ] Reference files one level deep max
- [ ] No vague or time-sensitive content
- [ ] Errors handled explicitly

## Testing

Test with real tasks, not test scenarios:
1. Use the skill for actual work
2. Note friction points
3. Iterate on instructions
4. Verify examples work
