---
name: codebase-explore
description: Understand an unfamiliar area of the codebase by mapping structure, data flow, and dependencies
---

# Skill: Codebase Explorer

## When to use

When you need to understand an unfamiliar area of the codebase.
Triggered by: "explore", "investigate", "how does X work?"

## Inputs

- Area of interest (module, feature, file pattern)

## Steps

1. Identify relevant directory/files using @folder or @codebase
2. Read README or top-level comments in the area
3. Map the key files and their responsibilities
4. Trace data flow: entry point → processing → output
5. Identify dependencies (imports from other packages)
6. Document findings in a summary

## Outputs

- Summary: purpose, key files, data flow, dependencies
- List of related files for deeper investigation

## Safety

- READ-ONLY — do not modify any files during exploration
- Verify findings against actual code, not assumptions

## How to verify

- All key files listed in the summary actually exist (`Glob` or `ls` to confirm)
- Data flow description can be traced step-by-step through the actual source (no invented intermediaries)
- Dependencies listed match actual `import` statements in the files (grep to confirm)
- No files were modified: `git status` should show a clean working tree after the skill runs