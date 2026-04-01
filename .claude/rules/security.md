---
description: Security rules for XSS prevention, file handling, canvas safety, and dependency hygiene
---

# Security Rules

## XSS Prevention

- NEVER use `dangerouslySetInnerHTML` — all user content must be rendered as text nodes
- NEVER use `eval()`, `new Function()`, or dynamic `import()` with user-supplied strings
- Sanitize any data coming from external URLs or file imports before passing to the renderer

## File Handling

- Validate file type and size before parsing (check MIME type, not just extension)
- Use `JSON.parse` inside a try/catch for all external JSON — never trust file content
- Do NOT expose internal file paths or stack traces to the user

## Canvas & Rendering

- Element IDs must be generated via `randomId()` from `packages/excalidraw/random.ts` — never trust user-supplied IDs as unique
- Do NOT embed raw user text in canvas `drawText` calls without length/encoding checks

## Dependencies

- Do NOT add packages with known CVEs — run `npm audit` before proposing any new dependency
- Prefer built-in browser APIs over third-party crypto/hash libraries
