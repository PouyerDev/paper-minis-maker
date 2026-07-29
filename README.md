# Paper Minis — Offline D&D Miniature Maker

A **single-file, offline-first** web app for creating printable paper miniatures for tabletop RPGs like D&D, Pathfinder, etc. No installation, no account, no internet required — just open the HTML file in any modern browser.

> **🌐 Try it online:** [https://papermini.netlify.app](https://papermini.netlify.app) — no download needed, works instantly in your browser.

---

##  Features

### Image Handling
- **Multiple input methods**: Upload files, drag & drop, or paste from clipboard
- **Batch processing**: Add multiple images at once
- **Auto-packing**: Arranges copies side-by-side on print sheets efficiently

### Miniature Generation
- **Double-sided**: Creates front + mirrored back for foldable minis
- **Auto-fit bases**: Base size adapts to artwork proportions automatically
- **Per-mini controls**: Adjust figure height, art zoom, base size, and copy count individually
- **Fold guides**: Dotted separator lines + two glue tabs on each base

### Print Layout
- **True multi-page preview** — see exactly what prints
- **Smart packing**: Larger minis placed first for optimal space usage
- **Page-aware**: Starts new sheet before a mini would be cut off
- **Actual-size rendering**: On-screen preview matches paper proportions (scrolls instead of shrinking)
- **Oversize protection**: Automatically scales down only minis that would exceed page bounds

### Print Settings
- Paper size: **A4** or **US Letter**
- Adjustable margins
- Optional cut guides & silhouette outlines
- **Print at 100% / "Actual Size"** — never "Fit to Page"

### Background Removal
- Click any background area to make it transparent (flood-fill)
- Adjustable tolerance slider
- **Undo (Ctrl+Z)** support for mistakes

### Privacy & Persistence
- **100% client-side** — images never leave your browser
- **Optional local storage** — saves your minis between sessions (IndexedDB)
- Clears on browser data clear or manual reset

---

## 🚀 Quick Start

1. **Download** `dnd-miniature-maker.html` (or clone this repo)
2. **Open** it in Chrome, Firefox, Edge, or Safari
3. **Add images** via:
   - Click the upload zone
   - Drag & drop files
   - `Ctrl+V` / `Cmd+V` to paste from clipboard
4. **Tune each mini** using the per-image controls
5. **Adjust global settings** (paper, margins, guides) in the sidebar
6. **Print** → Choose **100% / Actual Size** → Print on cardstock

---

## 🖨️ Assembly Instructions

1. **Print** on heavy cardstock (200–300 gsm) at **actual size**
2. **Cut** along the solid outer outline of each piece
3. **Fold** on the dashed center line (front-to-back)
4. **Fold** the two bottom tabs outward
5. **Glue** tabs together to form a triangular base

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl/Cmd + V` | Paste image from clipboard |
| `Ctrl/Cmd + Z` | Undo last Magic Wand click (in modal) |
| `Delete` / `Backspace` | Remove selected mini (in list) |

---

## Technical Details

- **Single HTML file** — HTML + CSS + vanilla JS (ES6 modules not needed)
- **No build step** — runs directly in browser
- **Canvas 2D API** for rendering & flood-fill
- **IndexedDB** for optional local persistence
- **CSS Grid/Flexbox** for responsive layout
- **Print CSS** (`@media print`) for clean output

### Browser Support
| Browser | Minimum Version |
|---------|-----------------|
| Chrome  | 80+ |
| Firefox | 75+ |
| Edge    | 80+ |
| Safari  | 14+ |

---

## Contributing

1. Fork the repo
2. Make changes to `dnd-miniature-maker.html`
3. Test thoroughly in browser (print preview, multiple images, edge cases)
4. Submit a PR with a clear description

---

## License

MIT License — free for personal use.

---

## Credits
- PouyerDev

- Built for the tabletop RPG community. Inspired by the need for quick, custom minis without a 3D printer.
