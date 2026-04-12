# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ARRI Frameline Visualizer — a static, single-page web tool for previewing ARRI camera frameline XML files. Cinematographers and DITs use it to verify framing guides before loading them on camera. Live at https://www.jenssage.com/arri-frameline-visualizer/.

## Architecture

This is a zero-build, no-dependencies project. Everything lives in a single `index.html` file (HTML + CSS + inline JS). There is no build step, no bundler, no framework.

- **`index.html`** — the entire application: UI markup, styles (`<style>` block), and all JavaScript (`<script>` block at the bottom)
- **`arri_camera_formats.json`** — camera format database (sensor resolutions, physical dimensions, codecs) sourced from ARRI's formats overview PDF v6.0. Loaded at runtime via `fetch()`
- **`xmls/`** — example frameline XML files selectable from the in-app library popup
- **`sample-image-jens-sage-2880-2160.jpg`** — built-in 4:3 sample background image

## Development

Open `index.html` in a browser. No server required for basic testing, though fetching `arri_camera_formats.json` and XML files needs a local server (e.g., `python3 -m http.server`).

## Key Concepts

- **Frameline XML format**: Based on ARRI FLT-5.3.1 spec. Contains `<camera>` metadata, `<rect>` elements (blackouts/shading with normalized 0.0–1.0 coordinates), and `<line>` elements (framelines with color, width, and normalized positions)
- **Normalized coordinates**: All frameline positions use 0.0–1.0 values, making them resolution-independent
- **Canvas rendering**: Uses HTML5 Canvas API. Background (image/grey grid) is drawn first, then rect overlays (black at varying opacity), then colored frame lines
- **Aspect ratio validation**: Uploaded images are validated against the selected camera format with 5% tolerance
- **XML library**: The `xmlFiles` array in the script hardcodes the list of available XML files from `xmls/`; adding a new XML file requires updating this array

## XML Library File Naming Convention

Files in `xmls/` follow this pattern:

```
FL_{Camera}_{Format}_{Framelines}.xml
```

- **FL** — prefix, stands for "Frameline"
- **Camera** — short camera code: `AMini` (ALEXA Mini), `AMiniLF` (ALEXA Mini LF), `A35` (ALEXA 35), `AXT` (ALEXA XT), `ASXT` (ALEXA SXT), `ALF` (ALEXA LF), `A65` (ALEXA 65)
- **Format** — recording format shorthand matching the camera's sensor mode, e.g. `4x3-2.8K`, `LF-OG-4.5K`, `16x9-3.2K`
- **Framelines** — describes the frameline content: aspect ratios joined by `-` (e.g. `16x9-9x16`), followed by style (`fullbox`/`corner`) and shading (`shade25`/`shade50`/`blackout`/`noshade`)

Examples:
- `FL_AMini_4x3-2.8K_16x9-9x16-corner-shade25.xml`
- `FL_AMiniLF_LF-OG-4.5K_16x9-9x16-fullbox-blackout.xml`
