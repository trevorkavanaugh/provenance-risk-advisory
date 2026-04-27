# Session Handoff - Provenance Risk Advisory Website - 2026-04-19

## Session Identity

You are the **Website session** (`provenance-website`). You own provenanceriskadvisory.com - a static HTML/CSS/JS site deployed via GitHub Pages. No frameworks, no build tools.

---

## What Was Accomplished This Session (April 7-19)

### 1. LinkedIn Branding Asset Kit (commits aec2bb6, 1d2a1d9)
Created a complete set of LinkedIn branding assets using Pillow with the actual brand fonts (Source Serif 4 + Inter downloaded from Google Fonts GitHub). All assets live in `assets/linkedin/`:

| File | Dimensions | Purpose |
|------|-----------|---------|
| `pra-logo-400x400.png` | 400x400 | Company page profile pic. Gold square with white "PR" in Source Serif 4 - matches the website header mark. |
| `pra-banner-1128x191.png` | 1128x191 | Company page cover/banner. Navy background, gold accent line at top, "Provenance Risk Advisory" in white serif, gold separator, tagline in gold. Note: LinkedIn company pages use 1128x191, NOT 4200x700. |
| `trevor-personal-banner-4200x700.png` | 4200x700 | Trevor's personal profile banner. Navy background, his name in large white serif, gold tagline, "Founder, Provenance Risk Advisory \| provenanceriskadvisory.com" in soft white. Personal profiles use 4200x700. |
| `pra-featured-card-1200x627.png` | 1200x627 | Featured posts highlight card. Navy background, Trevor's headshot (circular with gold ring) on right, PR mark + company name + taglines on left. Headshot source: `~/work/thought-leadership/assets/images/trevor_kavanaugh_headshot.jpg`. |

**Design decisions made via research:**
- Research agent studied LinkedIn pages of Prevalent, Venminder, Shared Assessments, Aravo, UpGuard, ProcessUnity, and boutique GRC consulting firms
- Finding: minimalist, logo-forward banners with simple color blocking dominate the TPRM/GRC space
- Mobile safe zone: center 60% of banner is all mobile users see - all content centered accordingly
- Company logo overlays bottom-left of banner on LinkedIn - kept that area clear

**Tagline iterations on featured card:**
- Original had "14 Years | 600+ Vendor Relationships | FDIC-Regulated" - BD session flagged "FDIC-Regulated" as inaccurate (Trevor isn't regulated, his former employer was)
- BD session provided alternatives. Trevor chose: "TPRM and C-SCRM Consulting for Regulated Institutions" as the credentials line
- Upper tagline stayed: "THIRD-PARTY RISK MANAGEMENT & CYBER SUPPLY CHAIN ADVISORY"

**Font generation approach:** Fonts downloaded to `/tmp/pra-fonts/` (SourceSerif4-Variable.ttf, Inter-Variable.ttf). Python scripts are also there but ephemeral. If you need to regenerate images, download the variable fonts from `https://raw.githubusercontent.com/google/fonts/main/ofl/sourceserif4/SourceSerif4%5Bopsz%2Cwght%5D.ttf` and the Inter equivalent.

### 2. AP-TPRM Vendor Reconciliation - New Targeted Engagement (commit aec2bb6)
Added a new targeted engagement card to `services.html` based on a request from the `provenance-bd` session via comms. The service is about cross-referencing AP payment data against the TPRM vendor inventory to find shadow vendors. Key backstory: Trevor discovered 150+ untracked vendors at First Foundation Bank using this approach, FDIC issued an MRBA, he remediated by deadline.

Card positioned between "Vendor Inventory Reconciliation" and "Vendor Exit Planning" in the quick-win grid. Timeline: 2-4 weeks.

### 3. Custom Scoping Callout (commit 73afdb8)
Added a paragraph below the targeted engagement cards grid inviting prospects to discuss custom-scoped engagements: "Don't see exactly what you need? Every organization's risk landscape is different. Let's talk and we'll scope an engagement that fits your situation." Links to contact page.

### 4. Comms Processed
- **From thought-leadership**: Analytics site separation fully implemented and deployed (schema migrated, PRA data scrubbed, site tabs live, API filtering in place)
- **From provenance-bd**: AP-TPRM service addition request (implemented)
- **From provenance-bd**: Tagline suggestions for featured card (implemented)
- **Replied to BD**: Confirmed AP-TPRM service added and tagline updated

---

## Git State

- **Branch:** master, tracking origin/master
- **Latest commit:** 73afdb8 - custom scoping callout
- **Remote:** github.com:trevorkavanaugh/provenance-risk-advisory.git
- **All changes pushed, working tree clean** (only untracked: .comms-session and this handoff's predecessor)

Recent commits (this session):
```
73afdb8 feat: add custom scoping callout to targeted engagements section
1d2a1d9 feat: add LinkedIn featured card with headshot and tagline
aec2bb6 feat: add LinkedIn branding assets and AP-TPRM targeted engagement
```

Prior commits for context:
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
├── services.html       # 5 core services + 7 targeted engagement cards + custom scoping CTA
├── about.html          # Company overview, principal bio
├── federal.html        # Federal contracting info, NAICS codes
├── contact.html        # Contact form, direct email/phone
├── CNAME               # provenanceriskadvisory.com
├── css/styles.css      # Full design system with CSS custom properties
├── js/main.js          # Navigation, forms, scroll animations
├── js/analytics.js     # Custom self-hosted analytics (sends to api.trevorkavanaugh.com)
├── assets/
│   └── linkedin/
│       ├── pra-logo-400x400.png
│       ├── pra-banner-1128x191.png
│       ├── trevor-personal-banner-4200x700.png
│       └── pra-featured-card-1200x627.png
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
- **Dashboard**: api.trevorkavanaugh.com/analytics/login.html (now has separate tabs per site - separation was implemented by thought-leadership session)
- **PM2 process**: trevorkavanaugh-api
- **Design system**: CSS custom properties in styles.css
  - Colors: navy (#1B2A4A), navy-dark (#141F38), navy-light (#2A3D62), gold (#C5932A), gold-light (#D4A94A), gold-dark (#A67B1F)
  - Typography: Inter (body), Source Serif 4 (headings) via Google Fonts
  - Spacing: 8px base scale
  - Shadows, radii, transitions all tokenized

---

## Services Page Current State (services.html)

**5 Core Services:**
1. C-SCRM Program Design (Service 01)
2. Third-Party Risk Architecture (Service 02)
3. CMMC Readiness Advisory (Service 03)
4. Risk Governance Training (Service 04)
5. Fractional Chief Third-Party Risk Officer (Service 05)

**7 Targeted Engagements (quick-win cards):**
1. TPRM Policy Suite (2-3 weeks)
2. Regulatory Exam Preparation (2-4 weeks)
3. SOC Report Review Program (2-3 weeks)
4. Vendor Inventory Reconciliation (3-4 weeks)
5. AP-TPRM Vendor Reconciliation (2-4 weeks) - NEW this session
6. Vendor Exit Planning (1-2 weeks)
7. TPRM Policy Review & Redline (1-2 weeks)

**Custom scoping callout** below the cards grid with link to contact page.

---

## Inter-Session Comms System

File-based messaging at `~/work/.comms/`. You are `provenance-website`. A PostToolUse hook checks inbox automatically (60-second throttle). If expecting a message, check actively with `~/work/.comms/bin/list`.

```bash
~/work/.comms/bin/send --to <session> --type <update|request|blocker|handoff> --subject "..." --body "..."
~/work/.comms/bin/list
~/work/.comms/bin/read-msg --all
~/work/.comms/bin/reply <msg-id> --body "..."
```

Sessions: master, research, career, thought-leadership, provenance-bd, provenance-website, provenance-engine, provenance-govcon

**No pending messages or outstanding requests.**

---

## Key Context About Trevor

- Engineer first, not a salesman. Builds tools in parallel with revenue-seeking - this is deliberate, not procrastination. Do NOT characterize tool-building as avoidance.
- Revenue nudging is the BD session's job, not ours. Stay in your lane.
- Baby girl due late May 2026. Runway is tight (~$11,300/mo burn).
- Voice: conversational, confident, direct, no-BS. Not corporate boilerplate.
- No em dashes anywhere. Use hyphens with spaces ( - ).
- Don't tell him to rest, sleep, eat, or log off. His energy management is his decision.
- Active pipeline as of April 7: Nexbank call with Ryan (consulting, exploratory), Caterpillar VP Third-Party Cyber Risk Management (employment, interview via warm lead). Status may have changed - check with Trevor.

---

## What Needs Attention

1. **Analytics verification** - Still unconfirmed whether pageview data is actually recording for provenanceriskadvisory.com. The site separation was implemented, but Trevor hasn't confirmed data is flowing. Ask if he's checked the dashboard.
2. **Mobile QA** - The CSS cleanup from April 5-6 and the new AP-TPRM card haven't been verified on mobile.
3. **Inline style remaining** - There's at least one inline style in the footer (`style="font-family: var(--font-heading);"` on line 301 and `style="color: rgba(255,255,255,0.5);"` on line 322). Minor cleanup opportunity.
4. **Old handoff** - `HANDOFF_WEBSITE_2026-04-07.md` is in the repo root (untracked). Should be archived to `archive/session_summaries/`.
5. **LinkedIn assets delivered** - All 4 images are ready to upload. Trevor may or may not have uploaded them yet.
6. **No other open items** - site is clean and deployed. Wait for Trevor's direction.
