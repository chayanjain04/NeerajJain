# AGENTS.md

## What this repo is
A single-page, single-file HTML/CSS/JS application: **`neeraj.html`** — a "Standard Work CAD Layout Editor". It's a browser-based 2D CAD-style drawing tool for creating factory/process floor layouts (standard work diagrams), all client-side, no build step, no backend.

There is no framework, no package.json, no bundler. Everything (markup, styles, logic) lives in `neeraj.html` (~1860 lines). The only external dependency is loaded from a CDN:
- `jspdf` (2.5.1, from cdnjs) — used for PDF export.

## Running it
Just open `neeraj.html` directly in a browser (double-click, or `start neeraj.html` on Windows). No install, no server required. A local static server (e.g. `npx serve .`) can be used if the browser blocks `file://` access to anything, but currently the app doesn't fetch external files itself.

## Structure inside neeraj.html
- `<style>` block: dark-theme UI (VS Code-like) — top bar, second bar (process symbols/scale), left toolbar (drawing tools), right toolbar (inspector), canvas viewport, HUD overlays.
- `<body>`: toolbar buttons wired via inline `onclick` handlers, a `<canvas>` for the drawing surface, hidden `<input type="file">` elements for image/JSON import.
- `<script>` (bottom of file): all application logic, notably:
  - State/history: `saveState`, `undo`, `redo`, `restoreShapes`, `updateUndoRedoUI`
  - Project persistence: `saveProjectJson`, `triggerJsonImport`, `handleJsonImport`, `createNewPage`
  - Image handling: `triggerImageUpload`, `handleImageUpload`
  - Export: `exportToPDF`, `renderPdfLabel`
  - Canvas/view: `resizeCanvas`, `toWorldCoords`, `toScreenCoords`, `drawGrid`, `draw`
  - Shape drawing/editing: `setMode`, `finishDrawing`, `clearCanvas`, `getShapeCenter`, `getShapeBoundingBox`, `getHandles`, `getHandleAtPoint`, `transformPoint`, `getRotateHandlePos`, `drawShape`, `isPointInShape`, `getShapeArea`, `deleteSelected`, `copySelected`, `pasteClipboard`
  - Scale/units: `snap`, `pxToUnit`, `unitToPx`, `updateScaleDisplay`
  - Inline text editing: `openInlineTextInput`, `commitInlineText`, `handleTextKey`
  - Inspector panel: `updateEditPanel`

## Working conventions for agents
- This is a single-file app — always read the relevant section of `neeraj.html` before editing; there's no separate module to open.
- Preserve the no-build, no-dependency-manager nature of the project unless the user explicitly asks to introduce tooling.
- When adding third-party libraries, only load them via `<script src="https://cdnjs.cloudflare.com/...">` (or another CDN already in use) — do not introduce npm/build steps without asking first.
- There are currently no automated tests. Verify changes by opening the file in a browser and manually exercising the affected tool/feature (see CLAUDE.md workflow note on browser verification for UI changes).
- Keep the dark VS Code-like visual style consistent with existing CSS variables/colors when adding UI elements.

## Tracking files
- `AGENTS.md` (this file) — architecture/orientation, regenerate from scratch each session start per user request.
- `CLAUDE.md` — Claude-specific working notes for this repo.
- `STATUS.md` — snapshot of current app state/features and open items, regenerated each session.
