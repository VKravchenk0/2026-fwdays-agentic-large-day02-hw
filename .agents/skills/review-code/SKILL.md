---
name: review-code
description: Review staged/unstaged changes or a specific file for security issues, convention violations, and type safety. Usage: /review-code [filepath]
argument-hint: "[filepath or leave empty for git diff]"
allowed-tools: Bash, Read, Grep
---

Review the following code carefully. If $ARGUMENTS is a file path, review that file. Otherwise, review all current git changes:

```
!`if [ -n "$ARGUMENTS" ]; then cat -n "$ARGUMENTS" 2>/dev/null || echo "File not found: $ARGUMENTS"; else git diff HEAD --unified=5 2>/dev/null || git diff --cached --unified=5; fi`
```

Perform a structured review across these dimensions:

## 1. Security
- XSS vectors: `dangerouslySetInnerHTML`, `eval()`, `new Function()`
- Untrusted input reaching the renderer or canvas without sanitization
- User-supplied IDs used as unique keys without `randomId()`
- Exposed stack traces or file paths

## 2. TypeScript Correctness
- Any use of `any` or `@ts-ignore` (strict mode violations)
- Missing or incorrect types on props and return values
- `interface` used where `type` is preferred (per conventions)

## 3. Code Conventions
- Default exports (should be named exports only)
- Class components (should be functional + hooks)
- Props interface not named `{ComponentName}Props`
- File naming: kebab-case for utils, PascalCase for components

## 4. Architecture
- State mutations bypassing `actionManager.dispatch()`
- Direct DOM manipulation instead of canvas render pipeline
- New npm packages introduced without explicit approval
- Modifications to protected files (`renderer.ts`, `restore.ts`, `manager.ts`, `types.ts`)

## 5. Testing
- New logic without a corresponding test file
- Mocked file-format layer (`restore.ts`)
- Floating promises in tests

---

Output format:

**[CRITICAL]** — must fix before merge  
**[WARNING]** — should fix, but not blocking  
**[SUGGESTION]** — optional improvement  

If no issues found in a category, write `✓ OK`. End with a one-line overall verdict.
