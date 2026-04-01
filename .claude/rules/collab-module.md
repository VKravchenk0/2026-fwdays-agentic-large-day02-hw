---
description: Rules for the real-time collaboration module — WebSocket protocol, state reconciliation, and user identity
globs: excalidraw-app/collab/**
---

# Collab Module Rules

## WebSocket & Real-time

- All outgoing messages MUST be serialized with `getSyncableElements()` — never send raw `AppState`
- Reconcile remote state via `reconcileElements()` only — do NOT merge arrays manually
- Handle disconnect/reconnect gracefully: buffer local changes, replay on reconnect

## Room & User Identity

- Room IDs are user-facing — generate with `generateCollaborationLinkData()`, never expose internal UUIDs directly
- User pointer/cursor data is ephemeral — do NOT persist it to the scene or history

## Error Handling

- WebSocket errors must be caught and surfaced via `app.setState({ errorMessage })`, not `console.error` alone
- Do NOT silently swallow `socket.on("error")` events

## Testing

- Mock `socket.io-client` in unit tests — do NOT open real WebSocket connections in CI
- Integration tests for collab live in `excalidraw-app/collab/` next to the module
