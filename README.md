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
| `brands/paddle-pub/logo-horizontal-email-light.png` | 480×70 | 240×35 | `c.primary` `#0E4E64` | `Paddle Pub - Franchisee Forms`, `Paddle Pub - Newsletter Signups` |
| `brands/trolley-pub/logo-horizontal-email-light.png` | 480×60 | 240×30 | `c.primary` `#433E3B` | `Trolley Pub - Franchisee Forms`, `Trolley Pub - Newsletter Signups` |

The Paddle Pub light variant is the site's navy/teal wordmark with the navy recoloured white;
the site has no white wordmark of its own. The older `logo-horizontal-email.png` files
(flattened onto the light page colour) stay published because sent emails reference them.

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
