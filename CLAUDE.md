# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-file static website (`index.html`). No build step, no dependencies, no tests. Open the file directly in a browser to preview.

## Working with index.html

The file is ~94 KB but only 167 lines. Nearly all of that bulk is an inline SVG containing base64-encoded raster image data and ~100 `<path>` elements. Reading the file directly will exceed the context window token limit.

**Always use `sed` or `grep` to work around this:**

```bash
# Read only the HTML/CSS skeleton (strips SVG paths and base64 blobs)
sed -n '49,167p' index.html | grep -v 'data:image\|base64\|<path\|<polygon\|<polyline\|<rect\|<circle\|<ellipse\|<line'

# Read just the <style> block (lines 6–48)
sed -n '6,48p' index.html

# Find a specific line number first, then read a small window around it
grep -n 'keyword' index.html
```

The SVG content itself (the artwork) should not need to change. All layout, typography, and spacing work happens in the `<style>` block in the `<head>`.

## Layout

`body` is a CSS grid with `place-items: center` and `min-height: 100dvh`. The single `<main>` child is a flex column. Responsive sizing uses `clamp()` and `min()` with `vmin` units via CSS custom properties (`--gap`, `--art-size`).
