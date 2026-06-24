# Narges Nourish — Website

A fast, responsive single-page website for **nargesnourish.com**, built as static files
(HTML/CSS/JS) so it hosts for free on **GitHub Pages**. No build step, no framework.

```
index.html        → the website (all CSS + JS inline, easy to edit)
404.html          → branded "page not found"
CNAME             → your custom domain (nargesnourish.com) — required by GitHub Pages
robots.txt        → search-engine crawl rules
sitemap.xml       → single-page sitemap
assets/
  favicon.svg         → browser tab icon
  apple-touch-icon.png → home-screen icon (iOS)
  og-image.png        → preview image for WhatsApp / social shares
```

---

## 1 · Put the files on GitHub

**Option A — website (no Git needed)**
1. Create a free account at github.com.
2. New repository → name it `nargesnourish` (public) → Create.
3. On the repo page: **Add file → Upload files** → drag in *everything in this folder*
   (keep the `assets/` folder structure) → **Commit changes**.

**Option B — command line**
```bash
git init
git add .
git commit -m "Launch Narges Nourish website"
git branch -M main
git remote add origin https://github.com/<your-username>/nargesnourish.git
git push -u origin main
```

## 2 · Turn on GitHub Pages
1. Repo → **Settings → Pages**.
2. **Source:** Deploy from a branch → **Branch: main** → **/ (root)** → **Save**.
3. Wait ~1 minute. Your site is live at `https://<your-username>.github.io/nargesnourish/`.
4. Under **Custom domain**, type `nargesnourish.com` → **Save**.
   (The included `CNAME` file already sets this — confirm it shows the domain.)

## 3 · Point Cloudflare DNS to GitHub
In the Cloudflare dashboard → your domain → **DNS → Records**, add these.

**Apex domain (nargesnourish.com)** — add all four A records, name `@`:
| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

*(Optional IPv6 — add as AAAA, name `@`:)*
`2606:50c0:8000::153` · `2606:50c0:8001::153` · `2606:50c0:8002::153` · `2606:50c0:8003::153`

**www subdomain** — add one CNAME:
| Type | Name | Value |
|------|------|-------|
| CNAME | www | `<your-username>.github.io` |

> **Cloudflare-specific tips**
> - Set each new record's proxy status to **DNS only (grey cloud)** first. GitHub needs this
>   to issue your free HTTPS certificate. Leave it grey until the padlock works.
> - Go to **SSL/TLS → Overview** and set the mode to **Full** (not *Flexible* — Flexible causes
>   a redirect loop with GitHub Pages).
> - You can later switch records to **Proxied (orange cloud)** for Cloudflare's CDN/caching,
>   but only after HTTPS is confirmed working, and keep SSL mode on **Full**.
> - If Cloudflare auto-added a placeholder A/AAAA or "parked" record, delete it first.

## 4 · Enable HTTPS
Back in **GitHub → Settings → Pages**, wait until the certificate is provisioned
(can take 15 min – a few hours), then tick **Enforce HTTPS**.
DNS changes can take up to 24 hours to fully propagate.

---

## Editing the site
Everything lives in `index.html`. Common edits:
- **Menu items / prices** — search for `class="bowls"` and edit the four `<article class="bowl">` blocks.
- **WhatsApp ordering** — replace `97400000000` (in the "Order on WhatsApp" links) with your real
  number in international format, e.g. `974XXXXXXXX`.
- **Email** — replace `hello@nargesnourish.com` if you use a different address.
- **Email sign-up form** — replace `https://formspree.io/f/your-form-id` with a free form endpoint
  from formspree.io (or your provider) so submissions reach your inbox.
- **Social links** — update the footer URLs (Instagram / Facebook / X / LinkedIn).
- **Colours & fonts** — the brand tokens are defined at the top of the `<style>` block under `:root`.

Brand assets, logos, and the full brand book are in the separate **Narges Nourish Brand Kit**.
