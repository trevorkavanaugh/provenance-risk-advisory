# Provenance Risk Advisory — Website

Public website for Provenance Risk Advisory LLC, hosted on GitHub Pages.

**Live:** [provenanceriskadvisory.com](https://provenanceriskadvisory.com)

## Tech Stack

- Static HTML5 / CSS3 / Vanilla JavaScript
- GitHub Pages hosting (CNAME configured)
- Custom self-hosted analytics (sends to api.trevorkavanaugh.com)
- Google Fonts: Inter (body), Source Serif 4 (headings)

## Pages

| File | Route | Purpose |
|------|-------|---------|
| `index.html` | `/` | Homepage — hero, services overview, credentials, research |
| `about.html` | `/about` | Company overview, principal bio, research links |
| `services.html` | `/services` | 4 core service offerings + Fractional CTRO |
| `federal.html` | `/federal` | Federal contracting info, agency targets, NAICS codes |
| `contact.html` | `/contact` | Contact form, direct email/phone |

## Structure

```
provenance-risk-advisory/
├── index.html
├── about.html
├── services.html
├── federal.html
├── contact.html
├── CNAME                  # provenanceriskadvisory.com
├── css/
│   └── styles.css         # Full design system with CSS variables
└── js/
    ├── main.js            # Navigation, forms, scroll animations
    └── analytics.js       # Custom self-hosted analytics
```

## Design System

CSS custom properties define the palette:
- **Navy:** #1B2A4A (primary)
- **Gold:** #C5932A (accent)
- Responsive, mobile-first with breakpoints for tablet/desktop
- Spacing scale: 8px increments

## Development

No build step. Edit HTML/CSS/JS directly. Push to `main` for GitHub Pages deploy.

## Analytics

Custom tracking (not Google Analytics) in `js/analytics.js`:
- Page views, scroll depth, outbound clicks, CTA clicks
- Batched events (5-sec window, max 10 per batch)
- Sends to `https://api.trevorkavanaugh.com/api/analytics/collect`
