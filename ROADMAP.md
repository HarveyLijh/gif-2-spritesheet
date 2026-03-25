# Roadmap

This tool started as a way to share AI coding agent sessions (Claude Code, Cursor, Windsurf) without hitting file size limits or requiring GIF playback. The goal is to make it the best-in-class converter for exactly that use case — turning time-based recordings into scannable, shareable, referenceable images.

Pull requests and discussion are welcome — [open an issue](https://github.com/HarveyLijh/gif-2-spritesheet/issues).

---

## v1.0 — Shipped ✅

Core tool live at [harveylijh.github.io/gif-2-spritesheet](https://harveylijh.github.io/gif-2-spritesheet/).

- [x] GIF → spritesheet PNG, fully in-browser, no uploads
- [x] Frame sampling (every Nth frame)
- [x] Interactive frame picker with shift-click range selection
- [x] Configurable columns, scale, frame numbers, borders
- [x] Live zoomable preview + one-click PNG download

---

## v1.1 — Remove Input Friction 🎬

> **Pain point:** Most people record as `.mp4` or `.webm` (OBS, Screen Studio, Kap). Converting to GIF first is lossy and annoying. The tool should accept what you already have.

- [ ] **Video input (`.mp4`, `.webm`, `.mov`)** — extract frames directly from video files in the browser using the WebCodecs API; no conversion step needed
- [ ] **Animated WebP input** — increasingly common from screen capture tools and design apps
- [ ] **APNG input** — covers macOS screen capture edge cases
- [ ] **Drag-to-trim** — set in/out points on the frame strip before generating the spritesheet, so you don't have to export a trimmed clip first

---

## v1.2 — Smarter Frame Selection 🧠

> **Pain point:** Long AI sessions produce hundreds of near-identical frames (waiting for a compile, scrolling through output). Manual sampling is a blunt instrument — you either keep too many frames or cut something important.

- [ ] **Auto-deduplicate** — detect and skip frames that are visually identical (pixel diff below a threshold), keeping only frames where something meaningfully changed
- [ ] **Motion heatmap** — show a sparkline of "how much changed per frame" so you can see where the action was before picking
- [ ] **Smart sample** — instead of "every Nth frame", pick N frames distributed proportionally to how much changed in each region of the recording
- [ ] **Scene detection** — automatically identify "chapters" in the recording (e.g., editing a file → running tests → fixing errors) and label them

---

## v1.3 — Annotation & Communication 🖊️

> **Pain point:** The spritesheet is a static image. When attaching it to a PR or issue, you often want to say "look at frame 12" or "the error appears here." That context is lost once you leave the tool.

- [ ] **Frame captions** — add a short text label to any frame ("build failed", "after fix", "line 42") that renders directly into the PNG
- [ ] **Callout arrows** — draw arrows and boxes on the spritesheet before exporting (rendered into the output, not a separate layer)
- [ ] **Highlight frame** — mark one or more frames with a colored border ring to draw attention ("this is the frame that matters")
- [ ] **Diff highlight mode** — automatically color-code pixels that changed between consecutive frames, making code edits visible at a glance without reading the text

---

## v1.4 — Shareable Configurations 🔗

> **Pain point:** Every new recording means redoing the same settings. Teams standardize on particular layouts but there's no way to encode that.

- [ ] **URL-encoded config** — settings serialize into the URL hash so you can share a pre-configured link (e.g., "use these settings for all our Claude Code recordings")
- [ ] **Named presets** — save and load configs locally; ship built-in presets for common tools:
  - `Claude Code` — terminal dark theme, 4 cols, sequential numbering
  - `Cursor` — editor recordings, higher frame density
  - `Screen Studio` — handles variable frame rate output
- [ ] **Export config as JSON** — for teams that want to check a config into their repo

---

## v2.0 — CLI & Automation 🖥️

> **Pain point:** Developers don't want to open a browser tab manually. They want spritesheet generation to happen as part of their workflow — on save, on commit, or in CI.

- [ ] **`npx gif2spritesheet` CLI** — same engine, same options, zero install

  ```bash
  npx gif2spritesheet session.mp4 --cols 4 --scale 2 --sample auto --out session-spritesheet.png
  ```

- [ ] **Watch mode** — regenerate the spritesheet whenever the source file changes

  ```bash
  npx gif2spritesheet --watch ./recordings/ --out-dir ./docs/
  ```

- [ ] **Config file** — `.gif2spritesheet.json` in the project root so settings are committed with the repo

  ```json
  { "cols": 4, "scale": 2, "sample": "auto", "captions": true }
  ```

---

## v2.1 — GitHub Action 🤖

> **Pain point:** AI coding workflows often involve session recordings as artifacts. Teams want these automatically attached to PRs — without a manual "open the tool, upload the GIF, download the PNG" step.

- [ ] **`HarveyLijh/gif-2-spritesheet-action`** — official GitHub Action

  ```yaml
  - uses: HarveyLijh/gif-2-spritesheet-action@v1
    with:
      input: ./recordings/*.gif
      output-dir: ./docs/spritesheets
      cols: 4
      sample: auto
  ```

- [ ] **Auto-comment on PR** — optionally post the generated spritesheet as a PR comment with a summary table (frames kept, duration, file size)
- [ ] **Artifact upload** — attach the spritesheet as a downloadable GitHub Actions artifact

---

## v2.2 — JavaScript / TypeScript Library 📦

> **Pain point:** Some tools (documentation generators, CI scripts, VS Code extensions) want to embed this capability without shelling out to a CLI.

- [ ] **`gif2spritesheet` npm package** — the core engine as a pure ESM library, no DOM dependencies

  ```ts
  import { toSpritesheet } from 'gif2spritesheet'

  const png = await toSpritesheet(inputBuffer, {
    cols: 4,
    scale: 2,
    sample: 'auto',
    diffHighlight: true,
  })
  ```

- [ ] **Type-safe options** — full TypeScript types for all config options
- [ ] **Node.js + browser** — same package works in both environments (browser uses WebCodecs/ImageDecoder, Node.js uses canvas/ffmpeg binding)

---

## Considering 💬

Not scheduled. Open an issue to discuss.

- **Copy to clipboard** — paste directly into Slack, Notion, or a GitHub comment
- **WebP output** — smaller files for embedding
- **Export frames as ZIP** — individual PNGs from selected frames
- **Firefox / Safari support** — currently requires Chrome/Edge due to the `ImageDecoder` API; a canvas-based fallback would unlock all browsers
- **Dark/light UI theme**

---

## Won't Do

- **Server-side processing** — no-upload, zero-dependency is a core guarantee
- **Account system / cloud storage** — out of scope
- **Video editing** — trimming and annotation are scoped to what's useful for sharing; this is not a video editor

---

_Last updated: March 2026_
