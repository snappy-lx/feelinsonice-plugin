---
name: agent-native-architecture
description: Guides building AI agents using prompt-native architecture where features live in prompts and agents figure out how to achieve outcomes. Use when designing agent systems, creating MCP tools, writing system prompts, or refactoring code toward prompt-native patterns.
---

# Agent-Native Architecture Skill

Build AI agents using **prompt-native architecture** where features live in prompts, not code, and agents figure out *how* to achieve outcomes you describe.

## Core Philosophy

**The foundational principle:** Whatever users can do, agents should be able to do. Don't artificially limit agent capabilities.

### Key Inversion

| Traditional Software | Prompt-Native |
|---------------------|---------------|
| Code defines workflows → agent executes | Prompts define outcomes → agent figures out HOW |

Features become "prompt + primitive tools" rather than pre-written functions.

## What This Skill Covers

1. **Design architecture** - Plan prompt-native agent systems
2. **Create MCP tools** - Build primitives following the philosophy
3. **Write system prompts** - Define agent behavior in natural language
4. **Self-modification** - Enable safe agent evolution
5. **Refactor existing code** - Migrate toward prompt-native patterns
6. **Context injection** - Inject runtime app state into prompts
7. **Action parity** - Ensure agents can do everything users can
8. **Shared workspace** - Agents and users operate on same data
9. **Testing** - Validate capability and parity
10. **Mobile patterns** - Handle background execution, permissions, costs
11. **API integration** - Connect to external APIs dynamically

## Core Principles

### Action Parity
Every UI action should have an equivalent agent tool.

### Context Parity
Agents should see the same data users see.

### Shared Workspace
Agents and users work in the same data space.

### Primitives over Workflows
Tools should be primitives, not encoded business logic.

```typescript
// BAD: Tool encodes business logic
tool("process_feedback", async ({ message }) => {
  const category = categorize(message);
  const priority = calculatePriority(message);
  if (priority > 3) await notify();
});

// GOOD: Tool is a primitive
tool("store_item", async ({ key, value }) => {
  await db.set(key, value);
  return { text: `Stored ${key}` };
});
```

### Dynamic Context Injection
System prompts should include runtime app state.

## Cardinal Anti-Pattern

**The most common mistake:** "You fall back into writing workflow code and having the agent call it" instead of defining outcomes and letting intelligence emerge.

This defeats the entire purpose.

## Tool Design Guidelines

### Do
- Make tools primitives (read, write, store)
- Accept data as inputs, not decisions
- Return rich output for verification
- Document in system prompt

### Don't
- Encode business logic in tools
- Make decisions inside tool implementations
- Hide capabilities from the agent
- Create separate agent sandboxes

## System Prompt Template

```markdown
# [App Name] Agent

## Available Resources
- [Resource 1]: [Description of what it is]
- [Resource 2]: [Description of what it is]

## Capabilities
- [Action 1]: Use [tool_name] to [achieve outcome]
- [Action 2]: Use [tool_name] to [achieve outcome]

## Domain Vocabulary
- [Term 1]: [Definition in app context]
- [Term 2]: [Definition in app context]

## Current State
- User: [Current user info]
- Recent activity: [What user has done]
- Available data: [What user can see]
```

## Success Indicators

You've succeeded when:
- The agent can surprise you with clever approaches you didn't anticipate
- Changing behavior means editing prose, not refactoring code
- Adding features means adding to prompts, not writing new endpoints
- Users and agents work in the same space seamlessly
