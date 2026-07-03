# HotChili Analytics — Static Site

Plain HTML/CSS replacement for the Webflow-hosted [hotchilianalytics.com](https://www.hotchilianalytics.com). No build step — edit files and push.

## Structure

```
index.html      # Single-page site
style.css       # Stylesheet
404.html        # GitHub Pages 404
CNAME           # www.hotchilianalytics.com
sitemap.xml
robots.txt
assets/         # Logo + product screenshots
```

## Local preview

```bash
cd hotchilianalytics-site
python3 -m http.server 8080
# open http://localhost:8080
```

## Deploy to GitHub Pages

### 1. Create repo and push

```bash
cd hotchilianalytics-site
git init
git add .
git commit -m "Initial static site — replace Webflow"
git branch -M main
git remote add origin git@github.com:hotchilianalytics/hotchilianalytics-site.git
git push -u origin main
```

Create the repo `hotchilianalytics/hotchilianalytics-site` on GitHub first (empty, no README).

### 2. Enable GitHub Pages

1. Repo **Settings → Pages**
2. **Source:** Deploy from branch
3. **Branch:** `main` / `/ (root)`
4. Save — site will be at `https://hotchilianalytics.github.io/hotchilianalytics-site/` until DNS cutover

### 3. DNS cutover (registrar: ultranameservers.com)

| Record | Type | Value |
|--------|------|-------|
| `www` | CNAME | `hotchilianalytics.github.io` |
| `@` (apex) | A | `185.199.108.153` |
| `@` (apex) | A | `185.199.109.153` |
| `@` (apex) | A | `185.199.110.153` |
| `@` (apex) | A | `185.199.111.153` |

Remove old Webflow records (`www` → `cdn.webflow.com`, etc.).

### 4. Finalize

1. In GitHub Pages settings, wait for DNS check on `www.hotchilianalytics.com`
2. Enable **Enforce HTTPS** once the certificate issues (can take up to 24h)
3. Unpublish/cancel the Webflow site after verifying the new site

## Editing

1. Edit `index.html` or `style.css`
2. `git add -A && git commit -m "Update copy" && git push`
3. GitHub Pages redeploys in ~1 minute

## Content sections

- **Hero** — HotChili positioning (video verification + applied AI)
- **VerityNgn OSS** — pip install, GitHub, Streamlit demo
- **VerityIndex** — legal dossiers, agency sponsor-readiness, Deep Research
- **InvestItNow** — algo investing (separate product)
- **Footer** — YouTube/Google editorial disclaimer, Apache 2.0 note

## License

Site content © HotChili Analytics, LLC. VerityNgn OSS is Apache 2.0.
