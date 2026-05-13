# SciComm Collective — Quarto Website

A fully featured Quarto website for a science communication group. Write content in Markdown (`.qmd` files), preview locally, and deploy automatically to GitHub Pages via a GitHub Actions workflow.

---

## Project structure

```
scicomm-quarto/
├── _quarto.yml              # Site config: nav, footer, theme, plugins
├── index.qmd                # Homepage
│
├── posts/                   # Blog (Quarto listing — auto-generates index)
│   ├── index.qmd            # Blog listing page
│   └── YYYY-MM-DD-slug/
│       └── index.qmd        # Each post in its own folder
│
├── podcast/                 # Podcast pages
│   ├── index.qmd
│   └── ep42.qmd, ep41.qmd …
│
├── workshops/               # Workshop pages
│   ├── index.qmd
│   └── writing-beginners.qmd …
│
├── cafe/
│   └── index.qmd            # Science Café page
│
├── about/
│   └── index.qmd            # About & contact page
│
├── assets/
│   └── css/
│       ├── custom.scss      # Quarto SCSS theme overrides
│       └── main.css         # Component styles
│
└── .github/
    └── workflows/
        └── deploy.yml       # GitHub Actions: auto-build & deploy
```

---

## Preview locally

### 1. Install Quarto

Download the installer for your OS from **[quarto.org/docs/get-started](https://quarto.org/docs/get-started/)** and run it.

Verify the install:
```bash
quarto --version
```

### 2. Preview the site

```bash
cd scicomm-quarto
quarto preview
```

Quarto starts a local server and opens your browser automatically at `http://localhost:4321`. The site live-reloads on every file save — no refresh needed.

### 3. Build (optional — produces the `_site/` folder)

```bash
quarto render
```

---

## Deploy to GitHub Pages

This repo includes a GitHub Actions workflow (`.github/workflows/deploy.yml`) that builds and deploys the site automatically on every push to `main`. No local Quarto install needed on the server.

### One-time setup

**Step 1 — Update `_quarto.yml`**

Edit the `website:` block:
```yaml
website:
  site-url: "https://YOUR-USERNAME.github.io/scicomm-collective"
```

**Step 2 — Push to GitHub**

```bash
git init
git add .
git commit -m "Initial Quarto site"
git remote add origin https://github.com/YOUR-USERNAME/scicomm-collective.git
git push -u origin main
```

**Step 3 — Enable GitHub Pages with GitHub Actions**

- Go to your repo → **Settings → Pages**
- Under **Source**, select **GitHub Actions** (not "Deploy from branch")
- Click **Save**

The workflow runs automatically. Watch progress under the **Actions** tab. Your site will be live at `https://YOUR-USERNAME.github.io/scicomm-collective/` within a couple of minutes.

---

## Adding content

### New blog post

Create a folder in `posts/` and add an `index.qmd`:

```
posts/
└── 2025-06-15-my-post-title/
    └── index.qmd
```

Minimal front matter:
```yaml
---
title: "Your Post Title"
description: "One sentence summary shown in the listing."
author: "Your Name"
date: "2025-06-15"
categories: [Neuroscience]
reading-time: true
---

Your post content in Markdown...
```

The post appears automatically in the blog listing — no other files to edit.

### New podcast episode

Add a `.qmd` file to `podcast/` and link it from `podcast/index.qmd`.

### New workshop

Add a `.qmd` to `workshops/` and add a card to `workshops/index.qmd`.

### Update Science Café

Edit `cafe/index.qmd` — update the date, topic, and past discussions list directly.

---

## Connecting real forms

The RSVP and contact forms currently show a confirmation message on click. To receive real submissions, use [Formspree](https://formspree.io) (free for 50 submissions/month):

Replace each button with a proper form tag:
```html
<form action="https://formspree.io/f/YOUR-FORM-ID" method="POST">
  <input type="text" name="name" class="sc-input" placeholder="Your name">
  <input type="email" name="email" class="sc-input" placeholder="you@example.com">
  <button type="submit" class="btn btn-teal">Submit →</button>
</form>
```

---

## Customising the look

- **Colours** — edit the `:root` CSS variables in `assets/css/main.css`
- **Fonts** — change the `@import` in `assets/css/custom.scss` and update `$font-family-sans-serif` / `$headings-font-family`
- **Navbar & footer** — edit the `website:` section of `_quarto.yml`
- **Theme base** — change `cosmo` in `_quarto.yml` to any [Bootswatch theme](https://bootswatch.com/)
