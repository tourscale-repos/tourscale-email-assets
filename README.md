# tourscale-email-assets

Publicly-reachable images and files referenced by email templates and n8n notification
workflows. Every file on `main` is published to GitHub Pages by
`.github/workflows/pages.yml`, so the repo layout *is* the URL:

```
https://tourscale-repos.github.io/tourscale-email-assets/<path-in-repo>
```

e.g. `logos/tourscale-logo-white.png` →
<https://tourscale-repos.github.io/tourscale-email-assets/logos/tourscale-logo-white.png>

A file is live only once it is merged to `main` and the Pages deploy finishes. Reference a new
asset from a template **after** that, or the recipient sees a broken image.

`robots.txt` keeps `/training/` out of search results. Nothing here is access-controlled —
never commit anything that shouldn't be public.

## Layout

| Path | Holds |
|---|---|
| `brands/<brand>/` | per-brand logo variants |
| `logos/` | TourScale corporate logos |
| `<campaign>/` | photos for one campaign or announcement (`the-port-2026/`, `conference-2026/`, …) |
| `drips/<brand>/` | hero photo per email in that brand's CRM drip, `<n>-<slot>.jpg` |
| `training/` | training material, excluded from robots |

## Logos for email need their own file

Email clients are not browsers, so a brand's website logo is usually the wrong file:

- **PNG, never `.webp`.** Outlook's Word engine does not render WebP.
- **Put the logo on a dark brand cell, not on the page colour.** A logo flattened onto a light
  page colour shows up as a pale box as soon as the client paints a different background —
  dark mode in Gmail, Apple Mail and Outlook does exactly that, and leaves images alone. A dark
  cell is left dark, so a light wordmark on a transparent PNG reads the same in both modes.
- **Size it at 2× the rendered dimensions**, and no larger. Templates set explicit `width`/
  `height` on the `<img>`; a multi-megapixel source just costs the recipient bandwidth.

Name the file for its shape and variant so they don't get confused —
`logo-horizontal-email-light.png` next to `logo-stacked-yellow.png`.

Current n8n notification mastheads, each inside the hero cell of the "Format Email" /
"Format Franchisee Email" node:

| File | Size | Rendered | Sits on | Used by |
|---|---|---|---|---|
| `brands/paddle-pub/logo-long-email-light.png` | 480×71 | 240×35 | `c.primary` `#0E4E64` | `Paddle Pub - Franchisee Forms`, `Paddle Pub - Newsletter Signups` |
| `brands/trolley-pub/logo-long-email-light.png` | 480×58 | 240×29 | `c.primary` `#433E3B` | `Trolley Pub - Franchisee Forms`, `Trolley Pub - Newsletter Signups` |
The Paddle Pub and Trolley Pub files are the franchise kit's `*-mark-long.svg` wordmarks with
the dark letters recoloured white and the wheel kept in its brand colour. The older
`logo-horizontal-email*.png` files stay published because sent emails reference them.

### Cruisin' Tikis notification emails

`brands/cruisin-tikis/email/` holds every image the `Cruisin Tikis - Franchisee Forms` and
`Cruisin Tikis - Newsletter Signups` emails draw. The design is the cruisintikis.com site's, and
its type (Signmaker, Costa Brisa) and art cannot load in a mail client, so each piece set in them
was rendered from the site's own built CSS and fonts in headless Chrome at 2×. Only what varies
per submission — the dock, the date, the field values — is live text.

| File | Rendered | What |
|---|---|---|
| `logo-horizontal-email.png` | 200×31 | the site's header wordmark, on the cream header cell |
| `hero-<form_type>.jpg` | 600×220 | sunrise gradient, palms, script eyebrow and Signmaker title; one per form type (`contact`, `private_charter`, `group_booking`, `newsletter_signup`) plus `hero-default.jpg` for any other |
| `heading-*.png` | 552×40 | "Contact details", "Subscriber details", "Message" |
| `stamp-*.png` | 56×56 | the "Find the dock" postage-stamp icons, one per field kind |
| `wavy-rule.png` | 552×8 | the rule between rows |
| `button-reply.png` | 220×48 | the primary button, "Reply by email" |
| `bamboo-rule.png` | 600×42 | the bamboo cane, half cream and half sunset, joining the body to the footer |
| `footer-crew.jpg` | 600×150 | the site footer's crew and wordmark, on sunset `#FF7733` |

A new form type needs its own `hero-<form_type>.jpg` and an entry in the node's `HEROES`;
until then it gets the default hero. Changing a word on any image means re-rendering it — the
words are not in the HTML.

Pedal Pub and Tiki Pub still serve their mastheads from their own live sites
(`pedalpub.com/favicon.png`, `tikipub.com/images/logo.png`). Those work because those
domains already point at the rebuilt sites; move them here if that ever changes.

## CRM drip assets

Moved here from the retired `email-assets` repo, which stays published only because sent
emails reference it. `zoho-mcp/scripts/email_brands.py` builds every URL from these paths.

| File | Use on |
|---|---|
| `brands/pedal-pub/logo-stacked-white.png` | dark grounds (white wordmark, gold sprocket) |
| `brands/trolley-pub/logo-stacked-white.png` | dark grounds (white/gold) |
| `brands/tiki-pub/logo-horizontal-white.png` | dark grounds (white wordmark) |
| `brands/tourcraft/logo-horizontal-white.png` | dark grounds (white/teal) |
| `brands/paddle-pub/logo-horizontal.png` | light grounds only (navy/teal wordmark) |
| `logos/tourscale-logo-color.png` | light grounds (black/blue wordmark) |

Logos are 480px wide for a ~220px display width, transparent PNG32. Drip photos are 1072px
wide (2× a 536px column), cropped 3:2, JPEG q78 progressive, metadata stripped — around
100–140KB each, taken from each brand site's own franchise photography.
