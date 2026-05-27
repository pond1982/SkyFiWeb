# SkyFi — Marketing & Support Site

Static site for the App Store submission. Designed to be hosted on GitHub Pages from this `docs/` directory.

| File | Purpose | App Store role |
|---|---|---|
| `index.html` | Marketing landing page | Optional; link as **Marketing URL** in App Store Connect |
| `privacy.html` | Privacy policy | **Required** — link as **Privacy Policy URL** in App Store Connect |
| `support.html` | FAQ + troubleshooting + contact | **Required** — link as **Support URL** in App Store Connect |
| `style.css` | Shared dark-navy theme | — |
| `.nojekyll` | Tells GitHub Pages to skip Jekyll processing | — |

## Deploy to GitHub Pages (free + HTTPS)

1. Create a new public GitHub repo, e.g. `skyfi`.
2. Push this whole project. The `docs/` folder is what we'll serve.
3. In the repo's GitHub web UI: **Settings → Pages**.
4. Under **Source**, pick **Deploy from a branch**.
5. Choose branch `main` (or whatever your default is) and folder `/docs`.
6. Save. Within ~30 seconds GitHub builds and publishes.
7. Your URLs become:
   - Home: `https://<your-github-username>.github.io/<repo-name>/`
   - Privacy: `https://<your-github-username>.github.io/<repo-name>/privacy.html`
   - Support: `https://<your-github-username>.github.io/<repo-name>/support.html`

Paste the **privacy** and **support** URLs into App Store Connect.

## Custom domain (optional)

If you own `skyfi.app` or similar, add it in **Settings → Pages → Custom domain**, then create a `CNAME` file in `docs/` containing just the domain. Add the corresponding DNS records at your registrar (`A` records → `185.199.108.153–111`, or a `CNAME` → `<username>.github.io`).

## Before submitting to the App Store

Search and replace these placeholders across `index.html`, `privacy.html`, `support.html`:

| Placeholder | Replace with |
|---|---|
| `support@skyfi.example` | Your real support email |
| `Last updated: 27 May 2026` (in `privacy.html`) | Today's date if you edit the policy |
| `27 May 2026` (anywhere else) | Today's date |
| The App Store download link in `index.html` (currently a `#download` anchor) | Your real App Store URL once approved |

You can do this with one command:

```bash
cd docs
sed -i '' 's/support@skyfi\.example/your-real@email.com/g' *.html
```

## Local preview

Any of these work:

```bash
# Python (already installed on macOS)
cd docs && python3 -m http.server 8000
# Open http://localhost:8000

# Or just open the files directly
open index.html
```

## Validate before publishing

- Open `privacy.html` and `support.html` in mobile Safari (or the iOS simulator) — confirm they're readable at iPhone widths.
- Run them through [PageSpeed Insights](https://pagespeed.web.dev/) — should score 95+ since they're static HTML/CSS with no scripts.
- Verify HTTPS works (GitHub Pages enables HTTPS automatically; Apple requires it for the Privacy Policy URL).

## App Store Connect mapping

In App Store Connect → App Information:

| App Store Connect field | Value |
|---|---|
| **Privacy Policy URL** | `https://<your-pages-url>/privacy.html` |
| **Support URL** | `https://<your-pages-url>/support.html` |
| **Marketing URL** (optional) | `https://<your-pages-url>/` |

All three sit on the same site, so editing them is just `git push`.
