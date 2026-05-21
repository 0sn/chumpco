# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Two-file static website (`index.html` and `404.html`, nearly identical). No build step, no dependencies, no tests. Open files directly in a browser to preview.

## Working with these files

Both files are ~40 KB and 58 lines, but each contains a minified inline SVG on a single line that pushes the token count over the context window limit. **Always use `sed` to skip that line.**

| File | Style block | SVG line | Rest |
|---|---|---|---|
| `index.html` | lines 7–48 | line 52 | lines 1–51, 53–58 |
| `404.html` | lines 7–49 | line 53 | lines 1–52, 54–58 |

```bash
# Read everything except the SVG line (index.html)
sed -n '1,51p' index.html && sed -n '53,58p' index.html

# Read everything except the SVG line (404.html)
sed -n '1,52p' 404.html && sed -n '54,58p' 404.html

# Read just the <style> block
sed -n '7,48p' index.html   # or 7,49p for 404.html
```

The SVG content itself (the artwork) should not need to change. All layout, typography, and spacing work happens in the `<style>` block.

## Layout

`body` is a CSS grid with `place-items: center` and `min-height: 100dvh`. The single `<main>` child is a flex column. Responsive sizing uses `clamp()` and `min()` with `vmin` units via CSS custom properties (`--gap`, `--art-size`).

## Color Scheme

Text is in eigengrau, #16161D. Highlights are gold, #FFD600, and links are a darker version #CCAA00. Asides and notes are in slate grey, #63768D. Callout backgrounds are pale misty cyan, #E6FAFC, and anything else fancy can be a lipsticky sort of fruit red #950952.
