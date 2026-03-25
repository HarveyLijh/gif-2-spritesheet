# GIF to Spritesheet for AI Agents

**Convert GIFs into single-image spritesheets — built for sharing AI agent demos with Claude Code, Cursor, and beyond.**

**[Try it now](https://harveylijh.github.io/gif-2-spritesheet/)**

---

## Demo

**Input:** An animated GIF recording

![Demo GIF](./demo-assets/demo.gif)

**Output:** A single spritesheet PNG with numbered frames

![Demo Spritesheet](./demo-assets/demo-spritesheet.png)

**Interface:**

![Interface](./demo-assets/interface.png)

---

## Why?

Screen recordings of AI coding agents (Claude Code, Cursor, Windsurf, etc.) often produce GIFs or videos with hundreds of frames. Sharing these in conversations, docs, or issues hits size limits fast — and animated GIFs can't be annotated or scanned at a glance.

**A spritesheet solves this.** One static PNG. Every frame visible. Numbered, bordered, and sized exactly how you need it.

## Features

| Feature | Details |
|---|---|
| **Frame sampling** | Keep every Nth frame to reduce noise from long recordings |
| **Frame picker** | Click to include/exclude individual frames; shift-click for range selection |
| **Customizable columns** | Control grid layout (2-20 columns) |
| **Scale** | 1x to 4x scaling for readability |
| **Frame numbers** | Sequential or source-index numbering, any corner, auto-contrast colors |
| **Borders** | Adjustable thickness and color (auto, black, white, grey, red, green) |
| **Max frames cap** | Limit output to a set number of frames |
| **Live preview** | Zoomable preview with fit-to-window |
| **One-click export** | Download as PNG or copy stats to clipboard |

## How to Use

1. Open the [tool](https://harveylijh.github.io/gif-2-spritesheet/)
2. Drag & drop a `.gif` (or click to browse)
3. Adjust sampling, columns, borders, and numbering
4. Pick or exclude specific frames
5. Download the spritesheet as a single PNG

## Use Cases

- **Sharing Claude Code sessions** — turn a terminal recording into a scannable image for PRs, docs, or bug reports
- **AI agent demo reels** — compress long automation GIFs into a single annotated image
- **Bug reproduction** — show exact frames where an issue occurs with numbered references
- **Documentation** — embed step-by-step visuals without requiring GIF playback support
- **Code review** — attach before/after spritesheets to pull requests

## Technical Notes

- Runs entirely in your browser — no uploads, no server, no dependencies
- Uses the [ImageDecoder API](https://developer.mozilla.org/en-US/docs/Web/API/ImageDecoder) (Chrome/Edge required)
- Zero install — just open the page

## Roadmap

- [x] GIF → spritesheet PNG, fully in-browser — no uploads, no server
- [x] Frame sampling — keep every Nth frame to reduce noise
- [x] Interactive frame picker — click to include/exclude, shift-click for range selection
- [x] Max frames cap — limit total output frames
- [x] Configurable columns (2–20) and scale (1x–4x)
- [x] Frame number overlay — sequential or source index, any corner, auto-contrast color
- [x] Border controls — adjustable thickness and color presets
- [x] Live zoomable preview with fit-to-window
- [x] One-click PNG download
- [ ] Video input (`.mp4`, `.webm`, `.mov`) — no GIF conversion step
- [ ] Animated WebP & APNG input
- [ ] Auto-dedup — skip visually identical frames automatically
- [ ] Diff highlight mode — color-code pixels that changed between frames
- [ ] Per-frame captions and callout arrows (rendered into the PNG)
- [ ] URL-encoded config sharing + named presets (Claude Code, Cursor, …)
- [ ] `npx gif2spritesheet` CLI with watch mode
- [ ] GitHub Action for CI spritesheet generation
- [ ] `gif2spritesheet` npm library (ESM, browser + Node.js)

See [ROADMAP.md](./ROADMAP.md) for details and motivation behind each item.

## Contributing

Feature requests are welcome — [open an issue](https://github.com/HarveyLijh/gif-2-spritesheet/issues). Feel free to fork and build on it however you like.

## License

MIT
