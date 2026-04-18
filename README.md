# Lab Website

Hugo-based static site, auto-deployed to GitHub Pages.

## Quick Start

### 1. Prerequisites

Install Hugo (extended version):

```bash
# macOS
brew install hugo

# or download from https://gohugo.io/installation/
```

### 2. Local Preview

```bash
git clone <your-repo-url>
cd lab-website
hugo server -D
# Open http://localhost:1313
```

### 3. Deploy to GitHub Pages

1. Push this repo to GitHub (public repo)
2. Go to repo **Settings → Pages**
3. Under **Source**, select **GitHub Actions**
4. Push to `main` branch — the site auto-builds and deploys

### 4. Custom Domain Setup

#### In this repo:
Edit `static/CNAME` — replace `YOUR-DOMAIN.com` with your actual domain.

#### In Namecheap:
1. Log in → **Domain List** → click your domain → **Advanced DNS**
2. Delete any existing records, then add:

| Type   | Host  | Value                    | TTL       |
|--------|-------|--------------------------|-----------|
| CNAME  | www   | `<your-github-user>.github.io` | Automatic |
| A      | @     | 185.199.108.153          | Automatic |
| A      | @     | 185.199.109.153          | Automatic |
| A      | @     | 185.199.110.153          | Automatic |
| A      | @     | 185.199.111.153          | Automatic |

#### In GitHub:
1. Repo **Settings → Pages → Custom domain** — enter your domain (e.g. `yourdomain.com`)
2. Check **Enforce HTTPS** (may take a few minutes to provision the certificate)

DNS propagation takes 5–30 minutes.

---

## Content Guide

### Add a team member
Create `content/team/firstname-lastname.md`:
```yaml
---
title: "Name"
role: "PhD Student"
email: "name@meduniwien.ac.at"  # use `emails` instead if there are multiple addresses
# emails:
#   - "name@meduniwien.ac.at"
#   - "name@students.meduniwien.ac.at"
photo: "/img/name.jpg"   # optional, put image in static/img/
weight: 3                 # controls display order
---
```

### Add a publication
Create `content/publications/short-name.md`:
```yaml
---
title: "Paper Title"
date: 2026-01-15
authors: "Author A, Author B, et al."
venue: "Journal Name"
doi: "10.xxxx/xxxxx"
pdf: "/uploads/paper.pdf"
code: "https://github.com/..."
---
```

### Add a tool / application
Create `content/tools/tool-name.md`:
```yaml
---
title: "Tool Name"
summary: "One-line description."
icon: "🤖"
status: "live"       # live | beta | coming
external_url: "https://..."   # optional external link; omit for internal page
---

Optional longer description here (Markdown).
```

For tools with multiple possible access points, omit `external_url` and add an `external_urls` list instead:
```yaml
external_urls:
  - label: "Access Route 1"
    url: "http://100.100.87.79:8000/login"
  - label: "Access Route 2"
    url: "http://100.116.163.47/login"
```

### Add a news post
Create `content/posts/post-slug.md`:
```yaml
---
title: "Post Title"
date: 2026-04-15
tags: ["conference", "publication"]
---

Post content in Markdown.
```

### Edit homepage research cards
Edit `data/research.yaml`.

### Add images
Put images in `static/img/` or `static/uploads/`, reference as `/img/filename.jpg`.

---

## Project Structure

```
├── hugo.yaml                  # Site config (title, menu, params)
├── data/research.yaml         # Homepage research cards
├── content/
│   ├── posts/                 # News / blog
│   ├── team/                  # Team members
│   ├── publications/          # Paper entries
│   └── tools/                 # Applications & tools
├── layouts/                   # HTML templates
├── static/
│   ├── css/style.css          # Stylesheet
│   ├── img/                   # Images
│   └── CNAME                  # Custom domain
└── .github/workflows/deploy.yml
```
