---
name: changelog
description: Generate an engaging changelog from recent Git merges for development teams
argument-hint: "[daily|weekly|days:N]"
---

# Changelog Generator

Generate an engaging summary of recent Git merges to the main branch for development teams.

## Time Period Options

- `daily` - Last 24 hours (default)
- `weekly` - Last 7 days
- `days:N` - Custom number of days (e.g., `days:14`)

## Usage

```bash
/changelog           # Last 24 hours
/changelog weekly    # Last 7 days
/changelog days:14   # Last 14 days
```

## Analysis Process

### 1. Gather Merged PRs

```bash
# Get merged PRs in timeframe
git log --merges --since="[timeframe]" --pretty=format:"%h %s" main
```

### 2. For Each PR, Analyze

Extract from commits and PR metadata:
- New features added
- Bug fixes
- Significant changes
- Issue references
- Contributor names
- Labels/categories
- Breaking changes
- Linked issues

### 3. Content Prioritization

Organize by impact:

1. **Breaking Changes** (highest priority)
2. **User-Facing Features**
3. **Critical Bug Fixes**
4. **Performance Improvements**
5. **Developer Experience Enhancements**
6. **Documentation Updates**

### 4. Deployment Considerations

Note when applicable:
- Database migrations required
- Environment variable changes
- Manual steps needed
- Dependency updates

## Format Requirements

- **Length**: Under 2,000 characters (Discord compatible)
- **Structure**: Organized sections with consistent emojis
- **Technical Terms**: Use backticks for code/commands
- **Traceability**: Include PR numbers
- **Credit**: Recognize contributors

## Output Format

```markdown
# Changelog: [Date Range]

## Breaking Changes
- [Change description] (#PR)

## New Features
- [Feature description] by @contributor (#PR)

## Bug Fixes
- [Fix description] (#PR)

## Improvements
- [Improvement description] (#PR)

## Deployment Notes
- [Any migration or manual steps required]

---
Contributors: @name1, @name2, @name3
```

## Optional Features

### Discord Webhook Integration

If configured, post directly to Discord:
```bash
curl -X POST -H "Content-Type: application/json" \
  -d '{"content": "[changelog]"}' \
  $DISCORD_WEBHOOK_URL
```

### Audience-Specific Tone

Adjust style for:
- **Dev Teams**: Technical details, breaking changes emphasis
- **Product**: User-facing features, impact descriptions
- **Leadership**: High-level summary, metrics

## Error Handling

- If no merges in period: "No changes to report for [timeframe]"
- If git command fails: Provide manual instructions

## Quality Standards

- Clarity and engagement
- Give credit to contributors
- Maintain technical accuracy
- Keep within character limits
