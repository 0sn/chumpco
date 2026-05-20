# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-file static website (`index.html`). No build step, no dependencies, no tests. Open the file directly in a browser to preview.

## Working with index.html

The file is ~40 KB and 58 lines, but the inline SVG on line 52 is a single minified line containing base64-encoded image data — it will still exceed the context window token limit if read directly.

**Always use `sed` to work around this:**

```bash
# Read everything except the SVG line
sed -n '1,51p' index.html && sed -n '53,58p' index.html

# Read just the <style> block (lines 7–48)
sed -n '7,48p' index.html
```

The SVG content itself (the artwork) should not need to change. All layout, typography, and spacing work happens in the `<style>` block (lines 7–48).

## Layout

`body` is a CSS grid with `place-items: center` and `min-height: 100dvh`. The single `<main>` child is a flex column. Responsive sizing uses `clamp()` and `min()` with `vmin` units via CSS custom properties (`--gap`, `--art-size`).
