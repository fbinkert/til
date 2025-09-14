---
title: 'Editing Wrapped Text with Vim'
description: 'Navigate wrapped lines with Vim g-motions'
pubDate: 2025-09-14
author: 'Fabian Binkert'
tags: ['Vim']
---
Vim distinguishes between buffer (logical) lines and screen (display) lines
when text wraps. Use g-prefixed motions to move within wrapped segments
precisely. This keeps navigation predictable in prose or long code comments.

## Example

- `gj`: Down one display line
- `gk`: Up one display line
- `g0`: To first character of display line
- `g^`: To first nonblank character of real line
- `g$`: To end of display line

## Notes:
- Default motions (j, k, 0, ^, $) operate on file lines. Prefix with g to
  target display lines.
- Use when a single long line wraps into multiple on screen (e.g., Markdown,
  commit messages, long comments).

## Caveats:
Only matters when content actually wraps (Context‑dependent): long lines or
when `:set wrap` is enabled.
Wrap boundaries depend on window width and options like linebreak (where wraps occur).
