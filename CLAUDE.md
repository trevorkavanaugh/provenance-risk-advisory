# Provenance Risk Advisory Website — Claude Code Instructions

> **Single-session repo.** The **Website** session owns this repo.
> Handoffs: `HANDOFF_WEBSITE_*.md` in this directory.
> See `../SESSION_GUIDE.md` for the full multi-session structure.

## Overview

Static website for Provenance Risk Advisory LLC. No build tools, no frameworks — pure HTML/CSS/JS served via GitHub Pages.

## Development

- Edit files directly. No build step, no bundler.
- Push to `main` deploys to GitHub Pages automatically.
- Test locally by opening HTML files in a browser or using `python -m http.server`.

## Design System

All visual tokens are CSS custom properties in `css/styles.css`:
- Colors: `--navy`, `--gold`, `--light-grey`, etc.
- Typography: Inter (body), Source Serif 4 (headings) via Google Fonts
- Spacing: 8px base scale

## Key Rules

1. **No frameworks.** Vanilla HTML/CSS/JS only. No React, no Tailwind, no build tools.
2. **No client data.** This is a public marketing site.
3. **Accessibility first.** Semantic HTML, ARIA labels, skip links, keyboard navigation.
4. **Mobile-first responsive.** Flexbox/grid layouts with media queries.
5. **Performance matters.** No heavy JS libraries. Fonts load via Google Fonts CDN.
6. **Analytics is custom.** `js/analytics.js` sends to our own endpoint, not Google. Do not add third-party tracking.

## Content Alignment

Service descriptions and credentials must match:
- `pra-consulting/LLC/docs/BUSINESS_PLAN.md` (source of truth for business details)
- `government_contract_bot/generator/capability_profile.py` (source of truth for capabilities)

## File Responsibilities

- `css/styles.css` — Complete design system. All styling lives here.
- `js/main.js` — Mobile nav, header scroll effects, contact form handling, scroll animations.
- `js/analytics.js` — Event tracking. Self-contained. Do not merge with main.js.
