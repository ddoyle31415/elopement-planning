# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A personal elopement planning guide for a Colorado wedding weekend (August 6–9, 2026). The repo contains research notes and a rendered HTML presentation guide covering six candidate locations.

No build system, package manager, or test suite — this is static HTML and Markdown.

## File Structure

- `locations/*.md` — Source-of-truth research notes for each location (one file per location). More detailed than the HTML: includes couples massage, Thursday dinner, private car service, and Saturday brunch options not shown in the guide.
- `elopement_guide_full.html` — The full rendered guide with all six locations (Aspen, Grand Lake, Boulder, Estes Park, Steamboat Springs, Palisade). This is the primary deliverable — the document shown to the couple.
- `elopement_guide_template.html` — Blank template for adding new locations. Copy the `<section class="location">` block for each new location. All placeholders use `[CAPS_IN_BRACKETS]` format.

## HTML Architecture

The guide is a single self-contained HTML file with no external JS and no build step. All styling uses CSS custom properties defined in `:root`:

```
--ink, --cream, --gold, --gold-light, --gold-pale, --muted, --white, --card-bg, --divider
```

**Per-location section structure** (in order):
1. `.loc-header` — cinematic full-bleed background image with location name, tagline, and meta tags
2. `.components` — contains four `.component` blocks:
   - **Lodging** — hotel/B&B with photo, details list, review panel, price bar
   - **Friday Dinner** — restaurant with same structure
   - **Ceremony** — site with permit details; may include `.permit-alert` for time-sensitive bookings
   - **Saturday Adventure** — activity/company
3. `.budget-summary` — weekend total estimate with notes

**Component anatomy:**
- `.component-label` (category name) + `.component-name` (h3) + `.component-website` (link)
- `.component-photo` — single full-width image, 420px tall
- `.component-body` — two-column grid: left = `.details-list` (bullet points with `→`), right = `.review-panel`
- `.review-panel` — contains `.review-stars` (use `.star` / `.star-empty`), `.review-score`, `.review-summary`, `.review-quote`
- `.price-bar` — estimated cost footer

## Key Discrepancies to Be Aware Of

The `locations/` markdown files are the research source; the HTML was written separately and may differ:
- **Palisade**: `.md` lists Colorado National Monument as ceremony site; HTML uses a generic vineyard ceremony instead
- **Aspen**: `.md` lists two Friday dinner options (Bosq, The Monarch); HTML omits the Friday dinner component entirely
- Some locations in the markdown have more components (couples massage, private car, Thursday dinner) that are not in the HTML guide

When updating the HTML, cross-reference the corresponding `.md` file for accurate vendor names, URLs, phone numbers, and pricing.
