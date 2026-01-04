---
name: playwright-test
description: Run end-to-end browser tests on pages affected by PR or branch changes using Playwright MCP
argument-hint: "[PR number, branch name, or empty for current]"
---

# Playwright Test Command

Run end-to-end browser tests on pages affected by PR or branch changes using Playwright MCP.

## Usage

```bash
/playwright-test              # Current branch
/playwright-test 847          # Specific PR
/playwright-test feature/name # Named branch
```

## Prerequisites

- Local development server running (localhost:3000)
- Playwright MCP server connected

## Workflow

### 1. Determine Test Scope

Identify changed files from:
- PR number (if provided)
- Branch name (if provided)
- Current HEAD changes

```bash
# For PR
gh pr diff [number] --name-only

# For branch
git diff main...[branch] --name-only

# For current
git diff --name-only
```

### 2. Map Files to Routes

Convert file changes to testable URLs:

| File Pattern | Route Pattern |
|-------------|---------------|
| `app/controllers/*_controller` | Corresponding view routes |
| `app/views/**/*.erb` | Parent route |
| `components/**/*` | Pages using component |
| `app/helpers/*` | Pages using helper |
| `stylesheets/**/*` | Visual regression on affected pages |

### 3. Verify Server Running

```bash
curl -s -o /dev/null -w "%{http_code}" http://localhost:3000
```

If not running, prompt user to start server.

### 4. Test Each Page

For each identified route:

```javascript
// Using Playwright MCP
await page.goto(route);
await page.screenshot({ path: `screenshots/${routeName}.png` });

// Check for console errors
const errors = await page.evaluate(() => window.consoleErrors || []);

// Verify key elements
await expect(page.locator('[data-testid="main-content"]')).toBeVisible();
```

### 5. Human Verification Points

Pause for manual testing when routes involve:
- OAuth flows
- Payment processing
- SMS/Phone verification
- External API integrations

### 6. Handle Failures

When a test fails:

```markdown
## Test Failure: [Route]

**Error:** [Error message]
**Screenshot:** [Path to failure screenshot]

**Options:**
1. Fix the issue now
2. Create a todo for later
3. Skip (known issue)
```

### 7. Test Summary

```markdown
## Playwright Test Results

| Route | Status | Notes |
|-------|--------|-------|
| /users | ✅ Pass | |
| /dashboard | ✅ Pass | |
| /settings | ❌ Fail | Console error: [message] |

### Screenshots
- [Link to screenshot directory]

### Console Errors
- [Any captured errors]

### Manual Verification Needed
- [ ] OAuth flow on /login
- [ ] Payment form on /checkout
```

## Error Handling

- **Server not running**: Prompt to start server
- **Route not found**: Skip with warning
- **Timeout**: Retry once, then fail
- **Screenshot failure**: Continue without screenshot

## Tips

- Run on feature branches before PR
- Compare screenshots to main branch for visual regression
- Check mobile viewports for responsive issues
