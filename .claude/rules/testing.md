---
description: Testing conventions — file structure, mocking policy, assertions, and coverage requirements
---

# Testing Rules

## Structure

- Unit tests live next to the file under test: `foo.ts` → `foo.test.ts`
- Component tests: `ComponentName.test.tsx` in the same directory as the component
- Integration / E2E tests: `packages/excalidraw/tests/` or `excalidraw-app/tests/`

## What to Test

- Test public API and observable behavior — NOT implementation details or private helpers
- Every new action registered in `actionManager` needs at least one unit test
- Snapshot tests are ONLY acceptable for stable SVG/canvas output; avoid for UI components

## Mocking

- Do NOT mock the file-format layer (`restore.ts`, `encode`/`decode`) — use real data fixtures
- Canvas API: use the `jest-canvas-mock` setup already in `setupTests.ts`
- Time-dependent tests: use `jest.useFakeTimers()` and restore with `afterEach`

## Assertions

- Prefer specific matchers (`toEqual`, `toHaveLength`) over `toBeTruthy` / `toBeDefined`
- For async code always `await` — never leave floating promises in tests

## Coverage

- New utility functions in `packages/utils/` require ≥ 80 % branch coverage
- Skipping a test (`test.skip`) requires a comment explaining why and a linked issue
