# Ari's Field Notes — Blog Workflow

## Where Everything Lives

| What | Location |
|------|----------|
| **Blog Repo** | `~/Dropbox/astropaperBlog2025/astropaper/` |
| **Posts (29)** | `~/Dropbox/astropaperBlog2025/astropaper/src/content/blog/` |
| **Images** | `~/Dropbox/astropaperBlog2025/astropaper/public/images/` |
| **CMS Config** | `~/Dropbox/astropaperBlog2025/astropaper/public/admin/config.yml` |
| **Site Config** | `~/Dropbox/astropaperBlog2025/astropaper/src/config.ts` |

---

## How the CMS Works

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Browser CMS    │────▶│  Decap Proxy     │────▶│  Local Files    │
│  localhost:4321 │     │  localhost:8081  │     │  src/content/   │
│  /admin/        │◀────│                  │◀────│  blog/*.md      │
└─────────────────┘     └──────────────────┘     └─────────────────┘
```

**Flow:**
1. You edit in the browser CMS
2. Decap proxy (`npx decap-server`) writes to local files
3. Files saved as markdown in `src/content/blog/`
4. Dropbox syncs files across devices automatically
5. Astro hot-reloads to show changes instantly

**No database** — posts are just `.md` files you own forever.

---

## Quick Start

```bash
cd ~/Dropbox/astropaperBlog2025/astropaper

# 1. Start the blog
npm run dev

# 2. Start CMS (in another terminal)
npx decap-server
```

| Service | URL |
|---------|-----|
| Blog | http://localhost:4321 |
| CMS Admin | http://localhost:4321/admin/ |

---

## Using the CMS

### Login
**No login required** — local mode writes directly to your files.

### Create a Post
1. Go to http://localhost:4321/admin/
2. Click **"New Blog Posts"**
3. Fill in:
   - **Title** — Your post title
   - **Publish Date** — When to publish
   - **Description** — Short summary (for SEO)
   - **Tags** — e.g., `essays`, `startup`, `health`
   - **Body** — Write in markdown
4. Click **"Publish"** (saves to `src/content/blog/`)

### Edit a Post
1. Go to http://localhost:4321/admin/
2. Click any post title
3. Make changes
4. Click **"Publish"**

---

## Manual Post Creation

Create a file in `src/content/blog/my-post.md`:

```markdown
---
title: "My Post Title"
pubDatetime: 2026-02-17T10:00:00Z
description: "A short description"
tags: ["essays", "life"]
featured: false
draft: false
---

Your content here in **markdown**...
```

---

## Publishing to Production

### Option 1: Vercel (Recommended)
```bash
npm install -g vercel
vercel
```

### Option 2: Netlify
```bash
npm run build
# Deploy the `dist/` folder
```

### Option 3: Manual
```bash
npm run build
# Upload `dist/` folder to any static host
```

---

## Folder Structure

```
astropaper/
├── src/content/blog/    ← Your posts (29 total)
├── public/admin/        ← CMS config
├── public/images/       ← Upload images here
└── dist/                ← Built site (after npm run build)
```

---

## Tips

- **Preview changes**: Blog auto-refreshes at localhost:4321
- **Images**: Drop in `public/images/`, reference as `/images/filename.jpg`
- **Drafts**: Set `draft: true` in frontmatter to hide from production
- **Featured**: Set `featured: true` to pin to top

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| CMS shows login | Make sure `npx decap-server` is running |
| Port in use | `lsof -ti:4321 | xargs kill -9` then restart |
| Posts not showing | Check frontmatter format, especially `pubDatetime` |

---

---

## Post Sources (Migrated)

| Source | Posts | Status |
|--------|-------|--------|
| AstroPaper (original) | 15 | ✅ In blog |
| BlotEssays | 14 | ✅ Migrated |
| Jekyll (2006-2018) | 108 | ⏳ Needs Dropbox sync |

**To migrate Jekyll posts:**
1. In Finder, go to `~/Dropbox/Projects/chemolog/arisamuel/_posts/`
2. Right-click → "Make Available Offline"
3. Once synced, run migration script

---

*Blog: AstroPaper v4 • CMS: Decap CMS (free, open source)*
*Created: 2026-02-17*
