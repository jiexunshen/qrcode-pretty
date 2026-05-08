# QR Code Pretty

[中文](./README-Zh.md)

This fork keeps the original `qrcode-pretty` command-line tool and adds a browser-based visual designer on top of it.

## What Changed

### Visual Designer

Added [`docs/qrcode-designer.html`](./docs/qrcode-designer.html), a local browser page for building QR codes visually.

It supports the same style controls as the original CLI:

- module style
- inner finder style
- outer finder style
- base color
- inner finder color
- outer finder color
- center image
- transparent background
- QR version
- box size
- border
- error correction level

The designer can export both SVG and PNG.

### Presets

Added built-in presets:

- Classic high contrast
- GitHub repository
- arXiv preprint
- Soft round accent

Presets tune the QR module colors and finder colors to match the selected logo while keeping enough contrast for scanning.

The page also supports browser-local saved presets. Saved presets are stored in `localStorage`.

### Logo Handling

Added bundled logo assets:

- [`assets/github-logo.svg`](./assets/github-logo.svg)
- [`assets/arxiv-logo.svg`](./assets/arxiv-logo.svg)

The designer clears QR modules behind the logo using the QR module grid instead of raw pixels.
This keeps the logo backplate aligned when changing logo size, logo padding, box size or border.

Exported SVG and PNG files embed logo images as data URLs, so the logo does not disappear after export.

### URL Validation

The visual designer only generates QR codes for valid `http` or `https` website addresses.
Invalid input shows a warning and leaves the preview empty.

### Language Switcher

Added an `EN` / `ZH` segmented language switcher.

### Assets

Moved logo files into `assets/` and renamed them to stable project asset names:

- `GitHub_Invertocat_Black.svg` -> `assets/github-logo.svg`
- `arxiv-logo.svg` -> `assets/arxiv-logo.svg`

## Run the Designer

From the project root:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:8000/docs/qrcode-designer.html
```

## Notes

The original Python package and CLI remain available.
This README only describes the changes made on top of the original project.
