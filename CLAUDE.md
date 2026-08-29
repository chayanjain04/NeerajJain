# CLAUDE.md

Project-specific instructions for Claude Code in this repo (`NeerajJain`).

## Session start behavior
Per user instruction: at the start of each session, re-derive understanding of the codebase from scratch (don't rely on stale memory of prior sessions) and refresh `AGENTS.md` and `STATUS.md` to reflect the current state of `neeraj.html`.

## Project shape
- Single-file browser app: `neeraj.html` (CAD-style "Standard Work" layout editor, canvas-based). No package.json, no build system, no server code.
- `README.md` is minimal (just the repo name/author) — not a source of project context.
- See `AGENTS.md` for the functional breakdown of `neeraj.html`.

## How to verify changes
- This is a pure front-end HTML file — the standard "start a dev server and test in browser" workflow means literally opening `neeraj.html` in a browser.
- For any UI/canvas/tool behavior change, manually exercise: drawing a shape, undo/redo, save/open project JSON, and PDF export, since these are the core flows and easy to regress.
- No automated test suite exists; do not claim "tests pass" — state explicitly that verification was manual/visual or not yet done.

## Conventions
- Keep everything in the one file unless the user asks to split it up.
- Match existing code style: vanilla JS, inline `onclick=` handlers, global functions (no modules/classes-heavy architecture currently).
- Don't introduce frameworks (React, Vue, etc.) or a build pipeline without explicit request.
