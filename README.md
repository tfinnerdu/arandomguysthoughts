# A Random Guy's Thoughts

Personal blog built with [Hugo](https://gohugo.io/) and the [Blowfish](https://blowfish.page/) theme, hosted on GitHub Pages.

**Live site:** [arandomguysthoughts.com](https://arandomguysthoughts.com)

---

## Local Setup (Windows)

### 1. Install Hugo

Open PowerShell and install via winget (easiest on Windows):

```powershell
winget install Hugo.Hugo.Extended
```

Verify it installed:

```powershell
hugo version
```

You need **Hugo Extended** (not the standard version) — the Blowfish theme requires it for Tailwind CSS processing. The winget command above installs the extended version.

### 2. Clone This Repo

```powershell
git clone --recurse-submodules https://github.com/YOUR_USERNAME/arandomguysthoughts.git
cd arandomguysthoughts
```

If you already cloned without `--recurse-submodules`, pull the theme:

```powershell
git submodule update --init --recursive
```

### 3. Add the Blowfish Theme (First Time Only)

If setting up fresh (not cloning an existing repo):

```powershell
git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

### 4. Run the Dev Server

```powershell
hugo server -D
```

The `-D` flag includes draft posts. Open [http://localhost:1313](http://localhost:1313) in your browser.

Hugo watches for changes — edit a file, save it, and the browser refreshes automatically.

### 5. Create a New Post

```powershell
hugo new posts/things-we-dont-talk-about/my-new-post/index.md
```

This creates a new post with front matter. Edit it in VS Code or your preferred editor.

---

## Writing Posts

Posts live in `content/posts/` organized by category folder:

```
content/posts/
├── things-we-dont-talk-about/    # Mental health, grief, relationships
├── culinary-delights/            # Recipes, BBQ, cooking
├── video-games/                  # Gaming content
├── sports/                       # Sports takes
├── nerdy-stuff/                  # D&D, esports, tech
└── random/                       # Everything else
```

Each post is a folder with an `index.md` file inside. This lets you include images alongside the post:

```
content/posts/culinary-delights/smoked-ribs/
├── index.md          # Your post content
└── feature.png       # Hero image (auto-detected by Blowfish)
```

### Front Matter Template

```yaml
---
title: "Your Post Title"
date: 2026-04-17
draft: false
description: "A short description for SEO and social sharing."
summary: "What shows up on the post list/cards."
categories: ["Things We Don't Talk About"]
tags: ["mental health", "personal"]
---

Your content here in Markdown...
```

### Embedding YouTube Videos

```markdown
{{</* youtube VIDEO_ID */>}}
```

### Setting a Post Live

Change `draft: true` to `draft: false` in the front matter, commit, and push.

---

## Deploying

Deployment is automatic via GitHub Actions. Every push to `main` triggers a build and deploy to GitHub Pages.

### First-Time GitHub Pages Setup

1. Create a repo on GitHub (e.g., `arandomguysthoughts`)
2. Push your code to the `main` branch
3. Go to **Settings → Pages** in your GitHub repo
4. Under **Source**, select **GitHub Actions**
5. The workflow in `.github/workflows/hugo.yaml` handles the rest

### Custom Domain Setup

1. In your GitHub repo: **Settings → Pages → Custom domain** → enter `arandomguysthoughts.com`
2. At your domain registrar, add these DNS records:

**A Records** (point apex domain to GitHub Pages):
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**CNAME Record** (for www redirect):
```
www  →  YOUR_USERNAME.github.io
```

3. Wait for DNS propagation (5 min to 24 hours)
4. Back in GitHub Pages settings, check **Enforce HTTPS**

---

## Project Structure

```
arandomguysthoughts/
├── .github/workflows/hugo.yaml   # Auto-deploy workflow
├── assets/img/                   # Site logo and global images
├── config/_default/              # All site configuration
│   ├── hugo.toml                 # Core Hugo config
│   ├── params.toml               # Blowfish theme settings
│   ├── languages.en.toml         # Language & author info
│   ├── menus.en.toml             # Navigation menus
│   └── markup.toml               # Markdown rendering settings
├── content/
│   ├── _index.md                 # Homepage
│   ├── about/index.md            # About page
│   └── posts/                    # All blog posts by category
├── static/                       # Files served as-is (favicon, etc.)
└── themes/blowfish/              # Theme (git submodule)
```

---

## Daily Workflow

```powershell
# Start the dev server
hugo server -D

# Write a new post
hugo new posts/culinary-delights/smoked-brisket/index.md

# Preview at http://localhost:1313

# When ready to publish, set draft: false, then:
git add .
git commit -m "New post: Smoked Brisket"
git push origin main

# GitHub Actions auto-deploys in ~1-2 minutes
```
