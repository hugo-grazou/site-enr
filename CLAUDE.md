# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-page landing page for an "Agence ENR" (énergies renouvelables) lead-generation service targeting three French professional profiles: installateurs solaires, bureaux d'études thermique, installateurs de bornes de recharge (IRVE). All copy is in French.

## Structure

Single file: `index.html`. HTML, CSS, and JS are inline — there is no build step, no package manager, no test suite. Open `index.html` directly in a browser to preview.

## Architecture

The page is one fixed-viewport "stage" (`.stage`) — nothing scrolls. Layout, from top to bottom:

1. `.header` — logo + Contact button
2. `.hero` — Georgia-serif headline + subtitle
3. `.cards` — three `.card` elements with 3D flip on click
4. `.footer` — "Comment ça marche →" link

### Flip cards

Each `.card` has `transform-style: preserve-3d` with two `.face` children (`.front` / `.back`). Clicking toggles `.flipped`, which adds `rotateY(180deg)`. The JS enforces **one flipped card at a time** — clicking any card first removes `.flipped` from all, then flips the clicked one (unless it was already flipped, which closes it). Escape closes all.

The middle card has `.center` — `scale(1.08) translateY(-12px)` — so its flipped state must compose both transforms. When editing flip logic, preserve the separate rule for `.card.center.flipped` or the center card's scale/lift will be lost on flip.

## Design constraints (locked via iteration)

These reflect the validated design spec — don't substitute without asking:

- **Background**: `https://images.unsplash.com/photo-1497440001374-f26997328c1b?w=1920` with gradient overlay `rgba(0,0,0,0.5) → 0.3 → 0.7`.
- **Accent gold**: `#C9A84C` (play buttons, badges, card borders at 0.5 alpha).
- **Headline font**: Georgia serif, 72px, weight 800, normal casing (not uppercase). Earlier drafts using Bebas Neue / Inter were rejected.
- **Everything fits in the viewport** — no vertical scroll on desktop. When adding content, rework proportions rather than letting the page grow.
- **Card dimensions**: 240×340, border-radius 16, `2px solid rgba(201,168,76,0.5)`. Center card scaled 1.08.
- **Back face** uses `#0d1117`, gold pill badge, 3-column stats row, a round gold Play button, then an outline + filled button pair.
- Front photo area is an explicit placeholder (`📷 Votre photo ici`) — the client will supply real media later; don't swap in stock images without being asked.
