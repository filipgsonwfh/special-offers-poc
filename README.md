# Special offers · clickable prototype

Stena Line special offers redesign: a clickable prototype that shows eight options for the special offers pages, plus the design brief behind them. Built in [Claude Design](https://claude.ai/design) and exported as static files. This repo serves that export on GitHub Pages.

- **Prototype:** https://filipgsonwfh.github.io/special-offers-poc/
- **Design brief:** https://filipgsonwfh.github.io/special-offers-poc/design-brief.html

## The options

The start page is "Pick a variant". Each variant opens as a working page: listing cards lead into the campaign pages, breadcrumbs lead back, and every "Search trip" or "Book" button lands on a booking stub that shows what would be handed to the booking flow.

| ID | Variant | Deep link | What it tries |
|----|---------|-----------|---------------|
| 1a | Listing with filters | [`#/listing`](https://filipgsonwfh.github.io/special-offers-poc/#/listing) | One list for all offers. Filter chips replace the separate Day trips page; a featured campaign slot sits on top. |
| 2c | Guided deal finder | [`#/finder`](https://filipgsonwfh.github.io/special-offers-poc/#/finder) | Three questions instead of a filter bar. Each answer rewrites the shortlist and promotes the best match. |
| 1b | Cruise hub | [`#/campaign/hub`](https://filipgsonwfh.github.io/special-offers-poc/#/campaign/hub) | Several products on one page. Product tiles in the booking panel; themed sailings as dated chips that deep-link into booking. |
| 2b | Sailing calendar | [`#/campaign/calendar`](https://filipgsonwfh.github.io/special-offers-poc/#/campaign/calendar) | The same cruises as a calendar. Filter by product, pick a date, book from the side panel. |
| 1c | Sale with deal selector | [`#/campaign/sale`](https://filipgsonwfh.github.io/special-offers-poc/#/campaign/sale) | A sale with four offer codes. The selected deal's code is applied automatically. |
| 3a | Editorial, booking first | [`#/campaign/editorial-booking`](https://filipgsonwfh.github.io/special-offers-poc/#/campaign/editorial-booking) | The sale as a long read with the booking panel in the hero and one chapter per deal. |
| 2a | Editorial with deal bar | [`#/campaign/editorial`](https://filipgsonwfh.github.io/special-offers-poc/#/campaign/editorial) | The long read with a sticky deal bar instead; booking panel at the end. |
| 1d | Mobile cruise hub | [`#/campaign/mobile`](https://filipgsonwfh.github.io/special-offers-poc/#/campaign/mobile) | The cruise hub at 375px, shown in a phone-width frame. |

Descriptions are the start-page card copy. Two fixtures carry the campaign pages: **Cruises to Sweden** (Gdynia – Karlskrona, 24h and 36h cruise products, Polish market) for 1b, 2b and 1d, and **Winter Sale** (Harwich – Hook of Holland, four offer codes, UK market) for 1c, 3a and 2a. The listing pages (1a, 2c) work on 21 offers across Holland and the Irish Sea.

## The brief, in short

- **Problem:** a special-offer page is bound to one product code and one Find-your-trip widget. Theme cruises need a page per product (24h, 36h); a sale with several products needs two or three landing pages. The listing is a flat list with Day trips as a separate page.
- **Proposal:** one **campaign page** holds any number of bookable products. The booking panel gets a product selector and the selected product's code goes to booking. Fixed-date sailings are **departures** that deep-link into booking with product and dates. Modules (what's included, prices, terms) vary per product. The listing merges Day trips as a filter.
- **Decisions:** radio tiles for up to four products, a dropdown beyond that. Both booking paths: the widget for open-date offers, deep links for fixed dates. Desktop first, one mobile view (1d). Codes marked * and the 36h prices are placeholders.

The full brief with annotated page renders is in `design-brief.html`.

## How it works

- `index.html` and `design-brief.html` are Claude Design documents: HTML templates with `{{ }}` bindings and a small logic script, rendered in the browser by `support.js` (the Claude Design runtime) on React 18. No build step.
- `vendor/` holds the React 18.3.1 UMD files the runtime would otherwise fetch from unpkg. They are loaded before the runtime, so the site has no CDN dependency for scripts. Their SHA-384 hashes match the ones pinned in `support.js`.
- `_ds/` is the Stena Line design system export the pages use: tokens (colours, type scale, spacing, radii) and the prebuilt component bundle (header, footer, buttons, tags, Find & Book fields, icons). Unmodified.
- Photos load from Stena Line's Scene7 CDN. Figtree from Google Fonts stands in for Stena Sans, which is not shipped.
- Routing is hash based, so deep links such as `/#/campaign/sale` work on GitHub Pages.

## Run locally

```sh
python3 -m http.server 8000
# open http://localhost:8000/
```

Serve it over HTTP rather than opening the file directly.

## Repo layout

```
index.html          the clickable prototype (start page + 8 variants + booking stub)
design-brief.html   the design brief with annotated renders of every variant
support.js          Claude Design runtime
vendor/             React 18.3.1 UMD
_ds/                Stena Line design system: tokens and the prebuilt component bundle
assets/             Stena Line logos used by the mobile variant
.nojekyll           keeps GitHub Pages from ignoring the _ds folder
```

## Notes and limitations

- This is a prototype, not production code. Styling is inline in the templates and components come from the prebuilt bundle.
- The booking stub books nothing. It shows the URL that would be handed to `book.stenaline.co.uk` or `book.stenaline.pl`.
- Offer codes, prices and dates are illustrative. The brief marks which ones are placeholders.
- The design system stylesheets reference a few card thumbnails that are not part of the export. They 404 in the console and nothing visible depends on them.
- Changes made to the Claude Design export for this repo: files renamed, `<title>` and favicon added, React vendored, embedded provenance metadata stripped from the two logo SVGs, a "Design brief" link added to the start page and a link back from the brief, and the bottom booking panel from the brief's 2a page ported into the prototype's 2a page (the start card describes it, the export lacked it).
- Source: export of the Claude Design project "Stena Line special offers redesign", 26 October 2026. Pasted reference screenshots and an unrelated "Stena Line BE" page from the same export are not included.
