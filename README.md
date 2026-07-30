# Mom's Backlog

Hugo site. Custom hand-built theme (no external theme dependency) — layout and CSS live in `layouts/` and `static/css/style.css`.

## Local preview

```
hugo server --buildDrafts
```
`--buildDrafts` shows MB-002 (Routine Boards), which is `draft: true` until it's ready to publish.

## Push to GitHub and go live

```
git init
git add .
git commit -m "Initial scaffold: Mom's Backlog"
git branch -M main
git remote add origin git@github.com:<your-username>/moms-backlog.git
git push -u origin main
```

Then on GitHub: **Settings → Pages → Build and deployment → Source: GitHub Actions**. The workflow in `.github/workflows/deploy.yml` builds and deploys on every push to `main` — no manual build step after this.

## Custom domain (momsbacklog.com)

1. Buy the domain (Namecheap, Google Domains successor, etc.) — this step is yours, not automatable.
2. Add a `static/CNAME` file containing just `momsbacklog.com`.
3. At your DNS provider, add:
   - `A` records pointing `@` to GitHub Pages IPs (185.199.108.153, .109.153, .110.153, .111.153)
   - `CNAME` record pointing `www` to `<your-username>.github.io`
4. In GitHub Settings → Pages, set the custom domain and enable "Enforce HTTPS".
5. Update `baseURL` in `hugo.toml` to `https://momsbacklog.com/`.

## Adding a new case study

Create `content/case-studies/<slug>.md` with this front matter:

```yaml
---
title: "Ticket title"
ticket_id: "MB-00X"
status: "Shipped" # or "In Progress"
weight: 3         # controls ordering, lower = higher on the backlog
date: 2026-01-01
tags: ["tag1", "tag2"]
summary: "One-line teaser shown on the card."
download_url: ""  # link to a PDF/board if there's a toolkit to sell/share
draft: false       # true hides it from the live site until ready
---

## Problem
## Why the standard approaches failed
## Discovery
## Solution design
## The product
## Results
## Retro
```

Section headings are a convention, not enforced by code — keep them for consistency across case studies.

## Ongoing maintenance

Recommended: use **Claude Code** against this repo for layout tweaks, new sections, or design iteration — it can run `hugo server` locally, edit templates, and commit/push directly. This scaffold was hand-built (no external theme), so changes are template edits, not fighting an upstream theme's conventions.
