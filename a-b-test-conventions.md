## A/B Test: conventions.md

- **Prompt**: "Create a new component for displaying element coordinates"
- **Result A (rule ON)**: uses props interface, colocated test, prefers `type` over `interface` for simple types. Uses kebab-case for files.
- **Result B (rule OFF)**: does not use props interface, doesn't have colocated test, uses `interface` for simple types, uses PascalCase for files
- **Conclusion**: Rule enforces the use of the project code conventions