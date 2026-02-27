# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A personal elopement planning guide for a Colorado wedding weekend (August 6–9, 2026). The repo contains research notes and a rendered HTML presentation guide covering six candidate locations.

No build system, package manager, or test suite — this is static HTML and Markdown.

## File Structure

- `locations/*.md` — Source-of-truth research notes for each location (one file per location). More detailed than the HTML: includes couples massage, Thursday dinner, private car service, and Saturday brunch options not shown in the guide.
- `index.html` — The full rendered guide with all six locations (Aspen, Grand Lake, Boulder, Estes Park, Steamboat Springs, Palisade). This is the primary deliverable — the document shown to the couple.

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


## Instructions

### Researching Vendors
When researching vendors read and summarize google reviews for each vendor. Write a summary of the google reviews to the referenced location markdown file, underneath each vendor as a sub-bullet starting with "Google Review Summary:". Below that sub-bullet, state the star rating of the vendor from google reviews, starting with "Google rating:"  

### Populating the elopement_guide_template.html
When populating the template html page with a new location, read the corresponding markdown file in `locations/` to see each major component. Map each option under each component to the templated sections. Embed photos for each component based on the web links provided under each option. Also include the google review summary if available from the location file. For example:
```
# Aspen

## Lodging
- [The Little Nell](https://www.thelittlenell.com/) — Aspen's only Five-Star, Five-Diamond ski-in/ski-out hotel at the base of Aspen Mountain, fireplace rooms, heated pool, on-site spa, and Michelin-recommended restaurant — ~$400–$800/night (August low season), ~$1,200–$2,400 for 3 nights
    - Photo: <photo link 1>
    - Photo: <photo link 2>
    - Google review summary: <prefetched summary of google reviews>
    - Google rating: X/5 stars
```
Embed each photo link within the lodging section of the Aspen location to describe `The Little Nell` hotel

