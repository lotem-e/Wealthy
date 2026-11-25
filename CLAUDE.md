# Wealthy - Claude Instructions

## What this is

A Hebrew PWA ( an app that runs in the browser and can be added to the phone's
home screen ) for tracking personal expenses and budget. Full product details
are in `wealthy-PRD.md` ( written in Hebrew ). Known bugs are in `BUGS.md`.

## This repository is PUBLIC

Everything committed here is visible to anyone. Before every commit, check that
no personal financial data is included.

- `import-data/` and every `*.csv` file are ignored by git on purpose. They
  hold real financial data and one-off import scripts. Never remove them from
  `.gitignore`, and never copy their contents into a tracked file.
- The Supabase URL and publishable key inside `index.html` are meant to be
  public. The data is protected by row level security in the database, not by
  hiding the key.

## Stack and structure

The whole app is one file, `index.html`: React 18 and Babel loaded from a CDN,
with no build step, no Node and no `package.json`. Supabase handles sign-in
( Google ) and cloud storage; `localStorage` is the local cache.

This is different from my other projects, which use Vite. Do not add a build
step or split the file without asking.

- Backend: the shared Supabase hub described in `../CLAUDE.md`. Wealthy's data
  lives in the `app_data` table, one row per user.
- The hub's Site URL belongs to Wealthy.

## Run and deploy

- Run locally: open `index.html` through any static server, for example
  `python3 -m http.server 4174` in this folder.
- Deploy: every push to `main` republishes the site through GitHub Pages
  ( `.github/workflows/deploy-pages.yml` ). Live at
  https://lotem-e.github.io/Wealthy/ - so a push to `main` IS a release.

## Rules

- Site content is Hebrew, RTL. Code, comments and commit messages are English.
- Because a push to `main` goes live immediately, work on a `topic/` branch
  and merge only when Lotem says so.
