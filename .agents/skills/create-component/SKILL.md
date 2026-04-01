---
name: create-component
description: Scaffold a new React component following project conventions (functional, named export, Props type, kebab-case file, colocated test). Usage: /create-component ComponentName [target-directory]
argument-hint: "<ComponentName> [target-directory]"
allowed-tools: Bash, Read, Write, Glob
---

Scaffold a new React component from the arguments: $ARGUMENTS

Parse the arguments:
- First token = ComponentName (PascalCase)
- Second token (optional) = target directory; default to `packages/excalidraw/components/`

Then do the following steps in order:

## Step 1 — Verify target directory
Check that the target directory exists. If it doesn't, tell the user and stop.

## Step 2 — Create the component file
Filename: `{kebab-case-of-ComponentName}.tsx` inside the target directory.

Follow these rules exactly:
- Functional component only (no class components)
- Named export only (no `export default`)
- Props type named `{ComponentName}Props`
- Use `type` keyword, not `interface`
- No `any`, no `@ts-ignore`
- Import React only if JSX transform requires it (check `tsconfig.json` for `jsx` setting first)

Template:
```tsx
import type { ReactNode } from "react";

type {ComponentName}Props = {
  // TODO: define props
  children?: ReactNode;
};

export const {ComponentName} = ({ children }: {ComponentName}Props) => {
  return (
    <div>
      {children}
    </div>
  );
};
```

## Step 3 — Create the colocated test file
Filename: `{kebab-case-of-ComponentName}.test.tsx` in the same directory.

Template:
```tsx
import { render, screen } from "@testing-library/react";
import { {ComponentName} } from "./{kebab-case-of-ComponentName}";

describe("{ComponentName}", () => {
  it("renders without crashing", () => {
    render(<{ComponentName} />);
  });

  // TODO: add meaningful tests
});
```

## Step 4 — Report
List the created files with their full paths and remind the user to:
1. Define real props in `{ComponentName}Props`
2. Replace the placeholder `<div>` with actual markup
3. Add meaningful test cases
