# Domain shop restyle (domains.aspireconsultingpartners.com)

Aspire's domain shop is ResellerClub's hosted storefront ("SuperSite") under the
direct reseller account (WebPro 1321813), shown at **https://domains.aspireconsultingpartners.com**.
This folder is the source of truth for the customizations made in RC's web editor.
The leading underscore keeps GitHub Pages (Jekyll) from publishing it.

Installed 2026-10-13.

## How it's built

- **CSS and text only.** Page templates stay on RC's defaults (no "Advanced Editing
  mode"), so RC's template upgrades keep applying.
- **DNS:** Cloudflare A record `domains` -> `72.22.93.2`, **proxied**. Zone SSL mode is
  Full, which accepts RC's `*.myorderbox.com` origin cert, so no SSL upload to RC.

## Files

| File | Where it goes in RC |
|---|---|
| `aspire-overrides.css` | Appended to the END of `css/themepluginlogos/themepluginlogos.css` in theme **ResponsiveTheme** (the last file RC merges into `production.css`). |
| `logo.gif` | Theme **ResponsiveTheme** > Edit Theme Logo (slot is `images/logo.gif`, 920x128, on navy `#0f172a`). |
| `logo.svg`, `logo.png`, `logo@2x.png` | Sources for the GIF. Rebuild: `magick logo@2x.png -background '#0f172a' -flatten -colors 128 logo.gif` |

## Where to edit

SuperSite admin: RC panel > Pro-Suite > SuperSite > **Customize your Supersite**
(opens https://domains.aspireconsultingpartners.com/admin/).

- **CSS:** My Themes > ResponsiveTheme > Customize Theme (Images, CSS) > Edit CSS >
  Themepluginlogos > Themepluginlogos.css. The editor has two code panels; the
  **right** one is editable and is what gets saved.
- **Text:** English > Manage Site > Edit Content > (section) > file > basic editor.
  Changed so far, in `homepage/domain-focused-indexv1.html`:
  - "Book your Domain" -> "Find your domain"
  - "Create your Online Identity in Minutes" -> "Domain registration for Aspire Consulting Partners clients" (the template wraps it in quote marks)
  - "Lowest Price Guaranteed!" -> "Popular extensions"
  - "Free Add-Ons with every Domain Name!" -> "Included with every domain"

## Gotchas

- **Font:** an `@import` is ignored mid-`production.css`, so Manrope is declared
  with `@font-face` pointing at Google's woff2.
- **Logo cache:** RC's image CDN (cdnassets.com) caches `logo.gif` for ~8 days. The
  CSS hides the `<img>` and loads the logo from this site's own path as a background.
  A `?v=` query string on that path makes RC return 404, so don't add one.
- **Dark body is home page only** (`body:has(.domain-focused-homepage)`). RC's other
  pages hard-code dark text, so they keep RC's light content area.
- **Copyright line** ("Copyright © Richard Asp") comes from the RC account profile's
  Company/Brand Name, not from a template. Change it there.

## Undo

- CSS: delete the appended block in the right panel, Save (or "Reset to Default").
- Text: revert each changed string in the basic editor.
- Logo: upload another image to the same slot.
