---
name: workflows:plan
description: Transform feature descriptions into well-structured project plans following conventions
argument-hint: "[feature description, bug report, or improvement idea]"
---

# Create a Plan for a New Feature or Bug Fix

Transform feature descriptions, bug reports, or improvement ideas into well-structured markdown plans that follow project conventions and best practices.

## Feature Description

<feature_description> #$ARGUMENTS </feature_description>

**If the feature description above is empty, ask the user:** "What would you like to plan? Please describe the feature, bug fix, or improvement you have in mind."

Do not proceed until you have a clear feature description from the user.

## Main Tasks

### 1. Repository Research & Context Gathering

Run these three agents in parallel:

- Task repo-research-analyst(feature_description)
- Task best-practices-researcher(feature_description)
- Task framework-docs-researcher(feature_description)

**Reference Collection:**

- [ ] Document all research findings with specific file paths
- [ ] Include URLs to external documentation and best practices
- [ ] Create a reference list of similar issues or PRs
- [ ] Note any team conventions discovered in `CLAUDE.md`

### 2. Issue Planning & Structure

**Title & Categorization:**

- [ ] Draft clear, searchable title using conventional format (`feat:`, `fix:`, `docs:`)
- [ ] Determine issue type: enhancement, bug, refactor

**Content Planning:**

- [ ] Choose appropriate detail level based on complexity
- [ ] List all necessary sections
- [ ] Gather supporting materials

### 3. SpecFlow Analysis

Run SpecFlow Analyzer to validate and refine the feature specification:

- Task spec-flow-analyzer(feature_description, research_findings)

**Incorporate:**
- [ ] Identified gaps or edge cases
- [ ] Updated acceptance criteria based on findings

### 4. Choose Implementation Detail Level

#### MINIMAL (Quick Issue)

**Best for:** Simple bugs, small improvements, clear features

```markdown
[Brief problem/feature description]

## Acceptance Criteria
- [ ] Core requirement 1
- [ ] Core requirement 2

## Context
[Any critical information]
```

#### MORE (Standard Issue)

**Best for:** Most features, complex bugs, team collaboration

```markdown
## Overview
[Comprehensive description]

## Problem Statement / Motivation
[Why this matters]

## Proposed Solution
[High-level approach]

## Technical Considerations
- Architecture impacts
- Performance implications
- Security considerations

## Acceptance Criteria
- [ ] Detailed requirements
- [ ] Testing requirements

## Success Metrics
[How we measure success]

## Dependencies & Risks
[What could block or complicate this]

## References & Research
- Similar implementations: [file_path:line_number]
- Best practices: [documentation_url]
```

#### A LOT (Comprehensive Issue)

**Best for:** Major features, architectural changes, complex integrations

```markdown
## Overview
[Executive summary]

## Problem Statement
[Detailed problem analysis]

## Proposed Solution
[Comprehensive solution design]

## Technical Approach

### Architecture
[Detailed technical design]

### Implementation Phases

#### Phase 1: [Foundation]
- Tasks and deliverables
- Success criteria

#### Phase 2: [Core Implementation]
- Tasks and deliverables
- Success criteria

## Alternative Approaches Considered
[Other solutions evaluated]

## Acceptance Criteria

### Functional Requirements
- [ ] Detailed functional criteria

### Non-Functional Requirements
- [ ] Performance targets
- [ ] Security requirements

## Risk Analysis & Mitigation
[Comprehensive risk assessment]

## References & Research
### Internal References
- Architecture decisions: [file_path:line_number]

### External References
- Framework documentation: [url]
```

### 5. Issue Creation & Formatting

**Content Formatting:**

- [ ] Use clear headings with proper hierarchy
- [ ] Include code examples with syntax highlighting
- [ ] Use task lists for trackable items
- [ ] Add collapsible sections for lengthy content

### 6. Final Review

**Pre-submission Checklist:**

- [ ] Title is searchable and descriptive
- [ ] All template sections are complete
- [ ] Links and references are working
- [ ] Acceptance criteria are measurable
- [ ] Add ERD mermaid diagram if applicable for model changes

## Output Format

Write the plan to `plans/<issue_title>.md`

## Post-Generation Options

After writing the plan file, present options:

1. **Open plan in editor** - Open for review
2. **Run `/deepen-plan`** - Enhance with parallel research agents
3. **Run `/plan_review`** - Get feedback from reviewers
4. **Start `/workflows:work`** - Begin implementing
5. **Create Issue** - Create in project tracker (GitHub/Linear)
6. **Simplify** - Reduce detail level

## Issue Creation

When user selects "Create Issue":

**GitHub:**
```bash
gh issue create --title "feat: [Plan Title]" --body-file plans/<issue_title>.md
```

**Linear:**
```bash
linear issue create --title "[Plan Title]" --description "$(cat plans/<issue_title>.md)"
```

NEVER CODE! Just research and write the plan.
