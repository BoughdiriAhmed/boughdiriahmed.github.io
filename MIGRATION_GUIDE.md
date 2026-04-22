# Migration Guide: Academic Pages → Tufte-Jekyll

## Overview

You are migrating from the **Academic Pages** Jekyll theme to a custom
**Tufte-style** Jekyll site. The new site has:

- **Home page (`/`)** — bio + all publications + all talks
- **Blog page (`/blog/`)** — your portfolio items as blog posts
- **About & CV page (`/about/`)** — full CV (education, experience, projects)

---

## Step 1 — Back up your current repo

```bash
cd ~/path/to/boughdiriahmed.github.io
git checkout -b backup-academic-pages
git push origin backup-academic-pages
```

This preserves your old site on a branch. You can always go back.

---

## Step 2 — Delete old theme files from master

These are the old theme directories/files to DELETE (your content is safe — we've already ported it):

```bash
# Directories to delete entirely
rm -rf _includes _layouts _sass _portfolio _publications _talks _teaching _pages talkmap markdown_generator book

# Old config and dependency files
rm -f _config.dev.yml package.json talkmap.ipynb talkmap.py CHANGELOG.md CONTRIBUTING.md
```

Keep these:
- `_posts/` — we'll migrate those
- `_data/` — can keep, will be mostly unused
- `assets/`, `images/`, `files/` — keep all of these (profile photo, PDFs, etc.)
- `.gitignore`

---

## Step 3 — Copy in the new files from this package

Copy everything from this migration package into your repo root:

```
_config.yml           ← replaces old one
Gemfile               ← replaces old one
index.html            ← new home page
about/index.html      ← new About & CV page
blog/index.html       ← new Blog page
_layouts/             ← default.html, page.html, post.html
css/tufte.css         ← main stylesheet
fonts/                ← ET Book fonts (see Step 4)
_posts/               ← your migrated portfolio post (add more here)
.github/workflows/deploy.yml  ← GitHub Actions for deployment
```

---

## Step 4 — Download the ET Book fonts

The Tufte style uses the **ET Book** serif font. Download them from:

  https://github.com/edwardtufte/et-book/tree/gh-pages/et-book

You need these 3 `.woff` files placed in a `fonts/` folder at your repo root:

```
fonts/
  et-book-roman-line-figures.woff
  et-book-display-italic-old-style-figures.woff
  et-book-bold-line-figures.woff
```

Quick download via terminal:

```bash
mkdir -p fonts
curl -L "https://github.com/edwardtufte/et-book/raw/gh-pages/et-book/et-book-roman-line-figures/et-book-roman-line-figures.woff" -o fonts/et-book-roman-line-figures.woff
curl -L "https://github.com/edwardtufte/et-book/raw/gh-pages/et-book/et-book-display-italic-old-style-figures/et-book-display-italic-old-style-figures.woff" -o fonts/et-book-display-italic-old-style-figures.woff
curl -L "https://github.com/edwardtufte/et-book/raw/gh-pages/et-book/et-book-bold-line-figures/et-book-bold-line-figures.woff" -o fonts/et-book-bold-line-figures.woff
```

---

## Step 5 — Enable GitHub Actions deployment

Because this theme uses local Ruby plugins, GitHub Pages can no longer build
the site directly. You need to switch to **GitHub Actions** deployment.

1. Go to your repo on GitHub.com
2. Click **Settings** → **Pages**
3. Under "Build and deployment", change **Source** from `Deploy from a branch`
   to **GitHub Actions**
4. Save.

The `.github/workflows/deploy.yml` file in this package handles everything
automatically — every push to `master` will build and deploy your site.

---

## Step 6 — Test locally (optional but recommended)

```bash
# Install dependencies
gem install bundler
bundle install

# Serve locally
bundle exec jekyll serve

# Visit http://localhost:4000
```

---

## Step 7 — Migrate your existing `_posts/`

Your old `_posts/` markdown files will mostly work as-is. Just make sure
each post's front matter uses:

```yaml
---
layout: post
title: "Your Post Title"
date: 2024-01-01
---
```

Change `layout: single` (Academic Pages) → `layout: post` (new theme).

---

## Step 8 — Add new portfolio/blog posts

Any new project or portfolio item goes in `_posts/` as a regular markdown file:

```
_posts/2025-01-15-my-new-project.md
```

With front matter:
```yaml
---
layout: post
title: "My New Project"
date: 2025-01-15
---

Your content here. Supports full Markdown and MathJax, e.g. $Y = f(X) + \epsilon$.
```

---

## Step 9 — Push to GitHub

```bash
git add .
git commit -m "Migrate to Tufte-style theme"
git push origin master
```

GitHub Actions will build and deploy automatically. Your site will be live
at https://boughdiriahmed.github.io within ~1-2 minutes.

---

## Site Structure Summary

```
boughdiriahmed.github.io/
├── _config.yml               # Site config
├── Gemfile                   # Ruby dependencies
├── index.html                # Home: bio + publications + talks
├── about/index.html          # About & CV
├── blog/index.html           # Blog/portfolio index
├── _posts/                   # Blog posts (one per portfolio item or note)
├── _layouts/
│   ├── default.html          # Base HTML shell
│   ├── page.html             # Static pages
│   └── post.html             # Blog posts
├── css/tufte.css             # All styles
├── fonts/                    # ET Book font files
├── images/                   # Profile photo, etc.
├── files/                    # PDF slides, papers
└── .github/workflows/
    └── deploy.yml            # Auto-deploy on push
```

---

## Updating content in the future

| What you want to do | Where to edit |
|---|---|
| Update bio | `index.html` — the `.home-intro` section |
| Add a publication | `index.html` — add a new `.pub-item` block |
| Add a talk | `index.html` — add a new `.talk-item` block |
| Update CV | `about/index.html` |
| Add a blog/portfolio post | Create `_posts/YYYY-MM-DD-title.md` |
| Change styles | `css/tufte.css` |

---

## Troubleshooting

**Fonts not loading?**  Check that the `.woff` files are in `fonts/` and
that the paths in `css/tufte.css` match (`../fonts/...`).

**GitHub Actions failing?** Check the Actions tab in your repo for build logs.
Common cause: `Gemfile.lock` conflicts — delete it and let bundler regenerate.

**MathJax not rendering?** Make sure `mathjax: true` is in `_config.yml`.
Inline math uses `$...$`, display math uses `$$...$$`.
