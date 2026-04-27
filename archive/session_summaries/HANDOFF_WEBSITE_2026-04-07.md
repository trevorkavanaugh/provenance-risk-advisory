# Session Handoff - Provenance Risk Advisory Website - 2026-04-07

## Session Identity

You are the **Website session** (`provenance-website`). You own provenanceriskadvisory.com - a static HTML/CSS/JS site deployed via GitHub Pages. No frameworks, no build tools.

---

## What Was Accomplished This Session

### 1. Inline Style Cleanup (deployed)
- Replaced all inline `style` attributes in the Targeted Engagements section of `services.html` (lines 242-283) with proper CSS classes
- New classes added to `css/styles.css`:
  - `.service-detail--alt-bg` - background color for the section
  - `.quick-win-grid` - responsive grid layout (auto-fit, minmax 280px)
  - `.quick-win-card` - card styling (padding, border, radius, background)
  - `.quick-win-card h3` / `.quick-win-card p` / `.quick-win-timeline` - typography
- All classes use design system tokens instead of hardcoded hex values

### 2. Handoff Archival
- Moved `HANDOFF_WEBSITE_2026-04-05.md` and `HANDOFF_WEBSITE_2026-04-06.md` to `archive/session_summaries/`

### 3. Screenshot Removal (commit f6a3e67)
- Removed `Screenshot 2026-03-21 095825.png` from repo root - it was a stale March 21 homepage screenshot from before the positioning rebalance

### 4. Live Site Verification
- **Homepage**: All 5 service cards present (C-SCRM, Third-Party Risk Architecture, CMMC Readiness, Risk Governance Training, Fractional CTRO). Targeted Engagements callout visible below cards.
- **Services page**: All 6 quick-win cards rendering in 2-column grid. Fractional CTRO section present.
- **Nav order**: Home - Services - Federal - Research - About - Contact (correct across all pages)
- **Analytics script**: Loaded on all 5 HTML pages (`js/analytics.js` with `defer`)
- **Analytics dashboard**: api.trevorkavanaugh.com/analytics/login.html is up and rendering

### 5. Analytics Separation Spec
- Discovered that both sites (trevorkavanaugh.com and provenanceriskadvisory.com) dump into one shared SQLite database with NO domain column
- Trevor wants separate tabs in the dashboard (same login, isolated data per site)
- Wrote detailed implementation spec at `~/work/thought-leadership/SPEC_ANALYTICS_SITE_SEPARATION.md`
- Sent a comms message to the `thought-leadership` session via the inter-session comms system requesting they implement it
- Spec covers: schema migration, PRA data scrub, collect endpoint changes, dashboard query filters, tab UI, deployment steps

### 6. Analytics Verification - Still Pending
- Could not log into the analytics dashboard to confirm pageview data is actually being recorded
- Trevor needs to check this himself at api.trevorkavanaugh.com/analytics/login.html
- The collect endpoint returned 404 on GET (expected - it only accepts POST from the client-side analytics.js)

---

## Git State

- **Branch:** master, tracking origin/master
- **Latest commit:** f6a3e67 - removed stale screenshot
- **Remote:** github.com:trevorkavanaugh/provenance-risk-advisory.git
- **All changes pushed, working tree clean**

Recent commits:
```
f6a3e67 chore: remove stale homepage screenshot from repo root
7be0942 checkpoint: pre-CLAUDE.md-refactor
b97f4bb feat: add Fractional CTRO card and targeted engagements link to homepage
8ea7a05 feat: add self-hosted analytics tracking
48b4092 fix: point Research nav link to specific research page
```

---

## Site Structure

```
provenance-risk-advisory/
├── index.html          # Homepage - hero, 5 service cards, credentials, research
├── services.html       # 5 core services + 6 targeted engagement cards
├── about.html          # Company overview, principal bio
├── federal.html        # Federal contracting info, NAICS codes
├── contact.html        # Contact form, direct email/phone
├── CNAME               # provenanceriskadvisory.com
├── css/styles.css      # Full design system with CSS custom properties
├── js/main.js          # Navigation, forms, scroll animations
├── js/analytics.js     # Custom self-hosted analytics (sends to api.trevorkavanaugh.com)
├── archive/
│   └── session_summaries/
│       ├── HANDOFF_WEBSITE_2026-04-05.md
│       └── HANDOFF_WEBSITE_2026-04-06.md
├── CLAUDE.md           # Repo-specific Claude Code instructions
└── README.md           # Repo overview
```

---

## Architecture

- **Two-site structure**: provenanceriskadvisory.com (business) + trevorkavanaugh.com (personal/research)
- **Hosting**: GitHub Pages, auto-deploys on push to master
- **Analytics**: Custom self-hosted Express.js + SQLite on Digital Ocean droplet 64.23.250.139 (SSH user: naughtymoddy)
- **API**: api.trevorkavanaugh.com
- **Dashboard**: api.trevorkavanaugh.com/analytics/login.html
- **PM2 process**: trevorkavanaugh-api
- **Design system**: CSS custom properties in styles.css - navy (#1B2A4A), gold (#C5932A), Inter body font, Source Serif 4 headings, 8px spacing scale

---

## Inter-Session Comms System

A file-based messaging system exists at `~/work/.comms/`. You are `provenance-website`. Messages are checked automatically via a PostToolUse hook.

Key commands:
```bash
~/work/.comms/bin/send --to <session> --type <update|request|blocker|handoff> --subject "..." --body "..."
~/work/.comms/bin/list              # check unread
~/work/.comms/bin/read-msg --all    # mark all read
```

Sessions: master, research, career, thought-leadership, provenance-bd, provenance-website, provenance-engine, provenance-govcon

I already sent an urgent request to `thought-leadership` about the analytics separation spec. That message is in their inbox.

---

## Key Context About Trevor

- Engineer first, not a salesman. Builds tools in parallel with revenue-seeking - this is deliberate, not procrastination. Do NOT nag about revenue unless he's genuinely falling behind on time-sensitive BD tasks.
- Revenue nudging is the BD session's job, not ours. Stay in your lane.
- Active pipeline as of today: Nexbank call with Ryan (consulting, exploratory), Caterpillar VP Third-Party Cyber Risk Management (employment, interview requested via warm lead).
- Baby girl due late May 2026. Runway is tight.
- Voice: conversational, confident, direct, no-BS. Not corporate boilerplate.
- No em dashes anywhere. Use hyphens with spaces.

---

## What Needs Attention Next

1. **Analytics verification** - Trevor still needs to confirm pageview data is actually recording. Ask him if he's checked the dashboard.
2. **Mobile QA** - The CSS cleanup should render identically but worth confirming on mobile at provenanceriskadvisory.com/services.html#quick-wins
3. **No other open items** - site is clean and deployed. Wait for Trevor's direction on next website work.
