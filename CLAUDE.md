# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Two-file static website (`public/index.html` and `public/404.html`, nearly identical). No build step, no dependencies, no tests. Open files directly in a browser to preview.

## Working with these files

Both files are ~40 KB but each contains a minified inline SVG on a single line that pushes the token count over the context window limit. **Always use `sed` to skip that line.**

| File | Style block | SVG line | Rest |
|---|---|---|---|
| `public/index.html` | lines 7–61 | line 65 | lines 1–64, 66–72 |
| `public/404.html` | lines 7–64 | line 68 | lines 1–67, 69–74 |

```bash
# Read everything except the SVG line (index.html)
sed -n '1,64p' public/index.html && sed -n '66,72p' public/index.html

# Read everything except the SVG line (404.html)
sed -n '1,67p' public/404.html && sed -n '69,74p' public/404.html

# Read just the <style> block
sed -n '7,61p' public/index.html   # or 7,64p for 404.html
```

The SVG artwork itself should not need to change. All layout, typography, and spacing work happens in the `<style>` block. Note that the SVG paths have no fill of their own — color is applied via `.art path { fill: … }` in CSS, so path color is part of the theme.

## Layout

`body` is a CSS grid with `place-items: center` and `min-height: 100dvh`. The single `<main>` child is a flex column. Responsive sizing uses `clamp()` and `min()` with `vmin` units via CSS custom properties (`--gap`, `--art-size`). The `.art` SVG uses explicit `width` and `height: var(--art-size)` (not `height: auto`) to prevent layout jump on load.

## Color Scheme

| Role | Color |
|---|---|
| Body text & art fill | eigengrau `#16161D` |
| Highlights | gold `#FFD600` |
| Links | dark gold `#CCAA00` |
| Asides / secondary text | slate grey `#63768D` |
| Callout backgrounds | pale misty cyan `#E6FAFC` |
| Accent / fancy elements | fruit red `#950952` |
