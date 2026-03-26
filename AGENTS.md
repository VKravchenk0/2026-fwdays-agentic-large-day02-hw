# AGENTS.md

## Project Structure

Excalidraw is a **monorepo** with a clear separation between the core library and the application:

- **`packages/excalidraw/`** - Main React component library published to npm as `@excalidraw/excalidraw`
- **`excalidraw-app/`** - Full-featured web application (excalidraw.com) that uses the library
- **`packages/`** - Core packages: `@excalidraw/common`, `@excalidraw/element`, `@excalidraw/math`, `@excalidraw/utils`
- **`examples/`** - Integration examples (NextJS, browser script)

## Development Workflow

1. **Package Development**: Work in `packages/*` for editor features
2. **App Development**: Work in `excalidraw-app/` for app-specific features
3. **Testing**: Always run `yarn test:update` before committing
4. **Type Safety**: Use `yarn test:typecheck` to verify TypeScript

## Development Commands


```bash
yarn test:typecheck  # TypeScript type checking
yarn test:update     # Run all tests (with snapshot updates)
yarn fix             # Auto-fix formatting and linting issues
```

</CodeBlockWrapper>

## Architecture Notes

### Package System

- Uses Yarn workspaces for monorepo management
- Internal packages use path aliases (see `vitest.config.mts`)
- Build system uses esbuild for packages, Vite for the app
- TypeScript throughout with strict configuration

# Memory bank

## Pattern: Keep Memory Bank Updated After Project Changes

When working on Excalidraw, maintain a memory bank in `docs/memory/` to preserve knowledge across agent sessions:

**When to Update Memory:**
- After discovering new architecture patterns or constraints
- When fixing bugs that reveal unexpected behavior
- After learning project-specific conventions or gotchas
- When identifying integration points or dependencies between packages

**Memory Storage:**
- Store memories in `docs/memory/` directory
- Use descriptive filenames: `memory_<topic>.md`
- Include context about *why* the pattern matters, not just what it is
- Update memory references when code changes invalidate them

**Memory Categories:**
- **Architecture** - State management patterns, rendering pipeline, dependency rules
- **Debugging** - Common failure modes, test patterns, root causes
- **Workflow** - Build steps, testing requirements, package relationships
- **Gotchas** - Unexpected behaviors, version constraints, compatibility issues

**Before Coding:**
- Check `docs/memory/` for relevant context
- Verify memory is still accurate with current codebase
- Update stale memories immediately

