# Theme Editor Tool - Implementation Plan

## Overview
A bookmarklet-based theme editor that injects a floating Mantine UI panel into any webpage, allowing live CSS variable manipulation and theme export/import.

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│  Theme Editor (New Repo)                                │
├─────────────────────────────────────────────────────────┤
│  /                    Landing page with bookmarklet     │
│  /editor.js           Bundled editor (injected by       │
│                       bookmarklet into target pages)    │
│  /palettes.json       Pre-built palette suggestions     │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼ Bookmarklet click
┌─────────────────────────────────────────────────────────┐
│  Any Webpage (e.g., localhost:3000)                     │
├─────────────────────────────────────────────────────────┤
│  [Your App Content]                                     │
│                                                         │
│  ┌─────────────────┐  ← Injected floating panel         │
│  │ Theme Editor    │                                    │
│  │ ─────────────── │                                    │
│  │ Primary: [____] │                                    │
│  │ Secondary:[___] │                                    │
│  │ ...             │                                    │
│  │ [Palettes ▼]    │                                    │
│  │ [Export JSON]   │                                    │
│  └─────────────────┘                                    │
└─────────────────────────────────────────────────────────┘
```

## Tech Stack
- **React 18** + **Mantine v7** - UI components
- **Vite** - Build tool (outputs single bundled JS for bookmarklet)
- **TypeScript** - Type safety
- **LocalStorage** - Session persistence
- **JSON files** - Export/import themes

## Features

### Core
1. **Live CSS Variable Editor**
   - Color pickers for: bg, surface, primary, secondary, accent, text, muted, border
   - Changes apply instantly via `document.documentElement.style.setProperty()`

2. **Palette Suggestions**
   - Pre-built palettes (import from your THEMES.md - all 30 themes)
   - Color harmony generators (complementary, analogous, triadic)

3. **Theme Management**
   - Export current theme as JSON
   - Import JSON theme file
   - Copy theme as CSS variables
   - Copy theme as Mantine config

### UI Components
- Draggable floating panel (position persists)
- Collapsible sections for each color role
- Palette browser with preview swatches
- Dark/light mode toggle for the editor itself

## File Structure
```
theme-editor/
├── src/
│   ├── main.tsx              # Entry point
│   ├── App.tsx               # Landing page
│   ├── editor/
│   │   ├── Editor.tsx        # Main editor panel
│   │   ├── ColorPicker.tsx   # Individual color control
│   │   ├── PaletteBrowser.tsx
│   │   ├── ExportPanel.tsx
│   │   └── inject.ts         # Injection logic
│   ├── palettes/
│   │   └── presets.ts        # 30 themes from THEMES.md
│   └── utils/
│       ├── css-vars.ts       # CSS variable manipulation
│       └── color-harmony.ts  # Generate harmonious colors
├── public/
│   └── bookmarklet.js        # Minified loader
├── package.json
├── vite.config.ts
└── index.html
```

## Bookmarklet Flow

1. **User Setup (once)**
   - Visit theme-editor landing page
   - Drag bookmarklet to bookmarks bar

2. **Usage**
   - Open any webpage (e.g., localhost:3000)
   - Click bookmarklet
   - Bookmarklet injects `<script src="https://[hosted]/editor.js">`
   - Editor panel appears, reads existing CSS variables
   - User edits colors, sees live changes
   - User exports JSON when satisfied

## Implementation Steps

### Phase 1: Project Setup
1. ~~Create new repo `theme-editor`~~ ✅
2. Initialize Vite + React + TypeScript
3. Add Mantine v7 dependencies
4. Configure Vite to output single bundle for injection

### Phase 2: Core Editor
1. Build draggable floating panel component
2. Implement color pickers for 8 CSS variable roles
3. Add live CSS variable manipulation
4. Add localStorage persistence for panel position/state

### Phase 3: Palettes
1. Import 30 themes from THEMES.md as presets
2. Build palette browser UI with swatches
3. Add "Apply Palette" functionality
4. Add color harmony generation (complementary, etc.)

### Phase 4: Export/Import
1. Export as JSON button
2. Import JSON file input
3. Copy as CSS variables
4. Copy as Mantine theme config

### Phase 5: Landing Page & Bookmarklet
1. Build landing page with instructions
2. Generate bookmarklet code
3. Add drag-to-bookmark-bar UI

## Verification
1. Build the project: `npm run build`
2. Serve locally: `npm run dev`
3. Open landing page, get bookmarklet
4. Open a test page (e.g., dmv-monitor dashboard on localhost)
5. Click bookmarklet, verify panel injects
6. Change colors, verify live updates
7. Export JSON, verify file downloads
8. Import JSON, verify colors apply

## Decisions Made
- ✅ Location: New standalone repo
- ✅ Architecture: Bookmarklet injection
- ✅ Storage: Local JSON file export/import
