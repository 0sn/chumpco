# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static website: `public/index.html`, `public/404.html`, and a shared `public/style.css`. No build step, no dependencies, no tests. Open files directly in a browser to preview. The two pages share structure and base CSS but have distinct color schemes and artwork.

## Working with these files

All files are short and can be read directly with the Read tool. No `sed` tricks needed.

The artwork is two external SVG files — `public/logo.svg` (eigengrau fill, for the light-background index page) and `public/antilogo.svg` (white fill, for the dark-background 404 page). Fills are baked into the SVG files; they are not controlled by CSS. The SVGs should not need to change.

Shared layout, typography, and spacing rules live in `style.css`. Each HTML file has a small inline `<style>` block for page-specific overrides only:

- `index.html`: `body` background (`#fff`) and color (`#16161D`)
- `404.html`: `body` background (`#16161D`) and color (`white`), `.art` rotation (`rotate(180deg)`), `strong` color (`gold`)

## Layout

`body` is a CSS grid with `place-items: center` and `min-height: 100dvh`. The single `<main>` child is a flex column. Responsive sizing uses `clamp()` and `min()` with `vmin` units via CSS custom properties (`--gap`, `--art-size`). The `.art` `<img>` uses explicit `width` and `height: var(--art-size)` (not `height: auto`) to prevent layout jump on load. The 404 page also applies `transform: rotate(180deg)` to `.art`.

## Color Scheme

| Role | Color |
|---|---|
| Body text & art fill | eigengrau `#16161D` |
| Highlights | gold `#FFD600` |
| Links | dark gold `#CCAA00` |
| Asides / secondary text | slate grey `#63768D` |
| Callout backgrounds | pale misty cyan `#E6FAFC` |
| Accent / fancy elements | fruit red `#950952` |
