# Nasriflix — Notion Ambassador Portfolio

A Netflix-style static site showcasing Nasri Nasir's talks, workshops, topics, and services. Built as a single `index.html` with local image assets — no build step, no dependencies.

Data sourced from the **Nasri Nasir — Notion Ambassador Portfolio** (Workshops & Talks database).

## Structure

```
.
├── index.html            # the whole site (HTML + CSS + JS inline)
├── assets/
│   └── images/           # event photos (web-optimised, 800x450)
├── netlify.toml          # Netlify static-hosting config
├── .gitignore
└── README.md
```

## Run locally

Just open `index.html` in a browser. Or serve it:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy: GitHub → Netlify

### 1. Push to GitHub

```bash
cd nasriflix-site
git init
git add .
git commit -m "Initial commit: Nasriflix portfolio site"
git branch -M main
git remote add origin https://github.com/<your-username>/nasriflix-site.git
git push -u origin main
```

### 2. Deploy on Netlify

**Option A — Connect the repo (auto-deploys on every push):**
1. Go to https://app.netlify.com → **Add new site** → **Import an existing project**.
2. Choose **GitHub** and select your `nasriflix-site` repo.
3. Leave the build command **empty** and set the **publish directory** to `.` (root). The included `netlify.toml` already sets this.
4. Click **Deploy**. Your site goes live at a `*.netlify.app` URL.

**Option B — Drag & drop (fastest, no GitHub needed):**
1. Go to https://app.netlify.com/drop
2. Drag the entire `nasriflix-site` folder onto the page. Done.

### 3. (Optional) Custom domain
In Netlify: **Domain settings** → **Add a domain** → point your DNS (e.g. nasrinasir.com) per the instructions.

## Editing content

All content lives in the `<script>` block in `index.html`:
- `talks` — events (name, slug, role, date, location, description, optional link)
- `topics` — the themes row
- `offers` — the services row

To change an event photo, replace the matching file in `assets/images/` (keep the same filename / slug).
