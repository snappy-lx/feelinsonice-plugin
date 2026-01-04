---
name: git-worktree
description: Unified management for Git worktrees enabling isolated parallel development workflows. Use when working on multiple features simultaneously, reviewing PRs in isolation, or needing separate working directories for different branches.
---

# Git Worktree Manager

Manage Git worktrees for isolated parallel development workflows.

## Why Worktrees?

Worktrees let you have multiple branches checked out simultaneously in separate directories. This enables:

- Working on feature A while testing feature B
- Reviewing PRs without switching branches
- Running different versions side-by-side
- Isolating experimental work

## Directory Structure

```
project/
├── main/              # Main working directory
└── worktrees/         # All worktrees live here
    ├── feature-auth/  # Worktree for auth feature
    ├── fix-bug-123/   # Worktree for bug fix
    └── pr-review-456/ # Worktree for PR review
```

## Core Operations

### Create a Worktree

```bash
# Create worktree for new branch
git worktree add worktrees/feature-name -b feature-name

# Create worktree for existing branch
git worktree add worktrees/feature-name feature-name

# Create worktree for PR review
git worktree add worktrees/pr-123 origin/pr-branch
```

### List Worktrees

```bash
git worktree list
```

### Switch Between Worktrees

```bash
# Just cd to the worktree directory
cd worktrees/feature-name
```

### Clean Up Worktrees

```bash
# Remove a worktree
git worktree remove worktrees/feature-name

# Or force remove if there are changes
git worktree remove --force worktrees/feature-name

# Prune stale worktree references
git worktree prune
```

## Setup Script

Create `scripts/worktree-manager.sh`:

```bash
#!/bin/bash

WORKTREES_DIR="worktrees"

create_worktree() {
    local name=$1
    local branch=${2:-$name}

    mkdir -p "$WORKTREES_DIR"

    # Add to .gitignore if not present
    if ! grep -q "^$WORKTREES_DIR/" .gitignore 2>/dev/null; then
        echo "$WORKTREES_DIR/" >> .gitignore
    fi

    # Create worktree
    git worktree add "$WORKTREES_DIR/$name" -b "$branch" 2>/dev/null || \
    git worktree add "$WORKTREES_DIR/$name" "$branch"

    # Copy environment files
    for env_file in .env .env.local .env.development; do
        [ -f "$env_file" ] && cp "$env_file" "$WORKTREES_DIR/$name/"
    done

    echo "Worktree created at $WORKTREES_DIR/$name"
}

list_worktrees() {
    git worktree list
}

cleanup_worktree() {
    local name=$1
    read -p "Remove worktree '$name'? (y/N) " confirm
    if [[ $confirm == [yY] ]]; then
        git worktree remove "$WORKTREES_DIR/$name"
        echo "Removed worktree: $name"
    fi
}

case "$1" in
    create) create_worktree "$2" "$3" ;;
    list) list_worktrees ;;
    cleanup) cleanup_worktree "$2" ;;
    *) echo "Usage: $0 {create|list|cleanup} [name] [branch]" ;;
esac
```

## Integration with Workflows

### Code Review

```bash
# Create isolated review environment
./scripts/worktree-manager.sh create pr-123 origin/feature-branch

# Navigate and review
cd worktrees/pr-123

# Clean up after review
cd ../..
./scripts/worktree-manager.sh cleanup pr-123
```

### Parallel Development

```bash
# Create worktree for second feature
./scripts/worktree-manager.sh create feature-b

# Work on feature-b in new terminal
cd worktrees/feature-b
# ... make changes ...

# Switch back to main feature
cd ../../
# ... continue main work ...
```

## Best Practices

1. **Keep worktrees directory in .gitignore** - Prevents accidental commits
2. **Copy env files** - Each worktree needs its own environment
3. **Clean up regularly** - Remove worktrees when done
4. **Use descriptive names** - `pr-123`, `feature-auth`, `hotfix-login`
5. **Don't nest worktrees** - Keep them at the same level

## Common Issues

### "fatal: is already checked out"
The branch is checked out elsewhere. Use a different branch name or remove the other worktree.

### Missing dependencies
Run `npm install` or equivalent in each worktree—they have separate node_modules.

### Stale worktree references
Run `git worktree prune` to clean up references to deleted worktrees.
