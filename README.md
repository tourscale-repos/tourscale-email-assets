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
| `training/` | training material, excluded from robots |

## Logos for email need their own file

Email clients are not browsers, so a brand's website logo is usually the wrong file:

- **Flatten the alpha.** Outlook renders neither `.webp` nor reliable PNG transparency — an
  alpha PNG can come out on a black or white box. Export onto the exact background the
  masthead sits on rather than relying on transparency.
- **Size it at 2× the rendered dimensions**, and no larger. Templates set explicit `width`/
  `height` on the `<img>`; a multi-megapixel source just costs the recipient bandwidth.

Name the file for its shape and variant so the two don't get confused —
`logo-horizontal-email.png` next to `logo-stacked-yellow.png`.

Current email mastheads:

| File | Size | Rendered | Flattened onto | Used by |
|---|---|---|---|---|
| `brands/paddle-pub/logo-horizontal-email.png` | 480×98 | 240×49 | `#F2F7F9` | `Paddle Pub - Franchisee Forms` (n8n) |
| `brands/trolley-pub/logo-horizontal-email.png` | 480×100 | 240×50 | `#F5F5F5` | `Trolley Pub - Franchisee Forms` (n8n) |

The "flattened onto" colour is that brand's `c.paper` token in the workflow's "Format Email"
node — the masthead cell's background. Read it from the node rather than guessing, or the
logo sits in a visible box of the wrong colour.

Pedal Pub and Tiki Pub still serve their mastheads from their own live sites
(`pedalpub.com/favicon.png`, `tikipub.com/images/logo.png`). Those work because those
domains already point at the rebuilt sites; move them here if that ever changes.
