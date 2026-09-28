# Palindromic — developer website

Static site for **www.palindromic.ca** (plain HTML + CSS, no build step), hosted on GitHub Pages.

## Preview locally

Open `index.html` in a browser. Or run a local server from the repo root:

```
python -m http.server 8000
```

Then visit http://localhost:8000.

## GitHub Pages setup

1. Push this repo to GitHub (`main` branch).
2. Repo **Settings → Pages**.
3. Source: **Deploy from a branch**, Branch: `main`, folder: `/ (root)`, then **Save**.
4. Under **Custom domain**, enter `www.palindromic.ca` and save (the `CNAME` file already contains it).
5. After DNS works and the certificate is issued, tick **Enforce HTTPS**.

## DNS (Cloudflare)

In Cloudflare → your domain → **DNS → Records**. Set each record to **DNS only** (grey cloud) so GitHub can issue the HTTPS certificate.

| Type  | Name  | Content                |
|-------|-------|------------------------|
| A     | `@`   | 185.199.108.153        |
| A     | `@`   | 185.199.109.153        |
| A     | `@`   | 185.199.110.153        |
| A     | `@`   | 185.199.111.153        |
| AAAA  | `@`   | 2606:50c0:8000::153 *(optional)* |
| AAAA  | `@`   | 2606:50c0:8001::153 *(optional)* |
| AAAA  | `@`   | 2606:50c0:8002::153 *(optional)* |
| AAAA  | `@`   | 2606:50c0:8003::153 *(optional)* |
| CNAME | `www` | `sbulbul.github.io`    |

DNS can take from a few minutes up to 24 hours. Then enable **Enforce HTTPS** in Settings → Pages.

### Verify the domain (prevents takeover)

1. GitHub → your avatar → **Settings → Pages** (account settings, not the repo).
2. **Add a domain** → `palindromic.ca`.
3. GitHub shows a `TXT` record (name like `_github-pages-challenge-sbulbul`). Add it in Cloudflare DNS.
4. Back in GitHub, click **Verify**. Keep the TXT record in place.

## Adding an app later

1. Copy `apps/_template/` to `apps/<app-slug>/` (e.g. `apps/my-notes/`).
2. Replace every `{{PLACEHOLDER}}` (`{{APP_NAME}}`, `{{APP_SLUG}}`, `{{PACKAGE_NAME}}`, …) in all three files.
3. Remove the `<meta name="robots" content="noindex">` line from each copied page.
4. On `index.html`, replace the "Coming soon" card in the Apps section with a card linking to `apps/<app-slug>/index.html`.
5. Add the three pages to `sitemap.xml`.
6. In Play Console, use `https://www.palindromic.ca/apps/<app-slug>/privacy.html` as the privacy policy URL.
