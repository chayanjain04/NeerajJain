# STATUS.md

_Last regenerated: 2026-08-29_

## Current state
Repo contains a single working artifact: **`neeraj.html`**, a self-contained "Standard Work CAD Layout Editor" (~1860 lines: HTML + CSS + vanilla JS). No backend, no build, no tests. Git history: 2 commits ("Initial commit", "first commit"), working tree clean on `main`.

## Feature inventory (as observed in code)
- Canvas-based shape drawing with multiple tool modes (`setMode`)
- Shape selection, move, resize/rotate via handles (`getHandles`, `getHandleAtPoint`, `transformPoint`)
- Copy/paste of shapes (`copySelected`, `pasteClipboard`)
- Undo/redo history (`saveState`, `undo`, `redo`)
- Inline text editing on shapes (`openInlineTextInput`, `commitInlineText`)
- Grid with snapping, unit scale conversion (`snap`, `pxToUnit`, `unitToPx`, `updateScaleDisplay`)
- Image insertion onto the canvas (`handleImageUpload`)
- Project persistence as JSON (`saveProjectJson`, `handleJsonImport`) — "Save Project" / "Open Project" buttons
- PDF export via jsPDF CDN library (`exportToPDF`, `renderPdfLabel`)
- Process-symbol / scale row in the UI ("second-bar") and a right-hand inspector panel (`updateEditPanel`)

## Known gaps / open items
- No automated tests exist for any of the above flows.
- No documented list of specific shape/process-symbol types — would need a closer read of `drawShape`/`getShapeDisplayType` to enumerate exactly which standard-work symbols are supported.
- No CI, linting, or formatting config in the repo.

## Tracking files in this repo
- `AGENTS.md` — architecture and file/function map, for any agent picking up this repo.
- `CLAUDE.md` — Claude Code specific working conventions (verify-in-browser, no-build-step rule, regenerate-each-session rule).
- `STATUS.md` (this file) — snapshot of app state; regenerate at the start of each session rather than trusting the previous snapshot, since the user wants a from-scratch review each time.
