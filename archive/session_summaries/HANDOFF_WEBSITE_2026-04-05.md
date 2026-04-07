Session Handoff — Provenance Risk Advisory — 2026-04-05

  What Was Accomplished This Session

  1. Homepage Rebalancing (commit 92bf823)
  - Changed primary positioning from federal-agency-first to audience-neutral
  - New headline: "Governance-first third-party risk advisory for regulated institutions and federal agencies"
  - New subheadline speaks to "organizations" broadly, references both regulated financial services and federal frameworks
  - Problem statement section: "Third-party risk governance is no longer optional" — leads with financial regulators, then federal mandates
  - Added "OCC / FFIEC" framework tag alongside existing federal ones
  - Contact CTA updated to mention "regulatory exams"
  - Meta/OG tags updated for audience-neutral positioning
  - Footer brand tagline reordered: "regulated institutions and federal agencies"

  2. Research Nav Link (commit 48b4092)
  - Added "Research" link to all 5 pages (desktop nav, mobile nav, footer nav)
  - Points to https://trevorkavanaugh.com/research/collective-fragility-paradox.html
  - Opens in new tab (target="_blank")
  - No content hosted on provenanceriskadvisory.com — purely external pointer

  3. Nav Reorder (same commit)
  - New order across all 5 pages: Home → Services → Federal → Research → About → Contact
  - Applied to: desktop nav, mobile menu, footer nav

  4. Analytics Integration (commit 8ea7a05)
  - Copied analytics.js from ~/scripts/consulting_business/frontend/js/analytics.js to provenance-risk-advisory/js/analytics.js
  - Added <script src="js/analytics.js" defer></script> to all 5 HTML pages (after main.js)
  - Tracks: page views, scroll depth, time on page, outbound clicks, CTA clicks, PDF downloads
  - Sends data to https://api.trevorkavanaugh.com/api/analytics/collect

  5. API Server Update (deployed to droplet)
  - File: ~/scripts/consulting_business/api/index.js
  - Added to allowedOrigins: https://provenanceriskadvisory.com, https://www.provenanceriskadvisory.com
  - Updated checkSuspicious() referer check to accept provenanceriskadvisory.com
  - SCP'd to naughtymoddy@64.23.250.139:/home/naughtymoddy/trevorkavanaugh-api/index.js
  - PM2 restarted: pm2 restart trevorkavanaugh-api — confirmed online

  6. Services Page (external change, not by us)
  - services.html was modified outside this session — new content includes:
    - Updated page header subtitle for audience-neutral positioning
    - New Service 02 (Third-Party Risk Architecture) copy targeting community banks
    - New Service 05: Fractional Chief Third-Party Risk Officer
    - New "Targeted Engagements" section (TPRM Policy Suite, Regulatory Exam Prep, SOC Report Review)
    - Framework tags include FFIEC, OCC 2013-29

  Architecture & Key Details

  Two-Site Structure (intentional):
  - provenanceriskadvisory.com — the business (GitHub Pages, static HTML)
  - trevorkavanaugh.com — personal brand/research (GitHub Pages, static HTML)
  - Both share the same analytics backend on Digital Ocean

  Analytics Infrastructure:
  - Custom self-hosted platform (Express.js + SQLite)
  - Droplet: 64.23.250.139, SSH user: naughtymoddy
  - API: https://api.trevorkavanaugh.com
  - Dashboard: https://api.trevorkavanaugh.com/analytics/login.html
  - PM2 process: trevorkavanaugh-api
  - Both sites' traffic visible in same dashboard, distinguished by page paths

  Site Structure:
  provenance-risk-advisory/
  ├── index.html      (homepage)
  ├── services.html   (advisory services)
  ├── about.html      (about/bio)
  ├── federal.html    (federal clients)
  ├── contact.html    (contact form)
  ├── css/styles.css  (all styling)
  ├── js/main.js      (UI interactions)
  ├── js/analytics.js (tracking)
  └── CNAME           (domain config)

  Git State:
  - Branch: master, tracking origin/master
  - Latest commit: 8ea7a05 — analytics integration
  - Remote: github.com:trevorkavanaugh/provenance-risk-advisory.git
  - All changes pushed, nothing uncommitted

  What Needs Attention Next Session

  - Verify analytics is collecting — visit provenanceriskadvisory.com and check the analytics dashboard for incoming pageview data
  - Services page updates were made externally — the new Fractional CTRO and Targeted Engagements content should be reviewed for consistency with homepage messaging
  - Homepage service cards (index.html lines 119-144) still show the original 4 services — may need updating to reflect the new Service 05 (Fractional CTRO) and Targeted Engagements added to services.html