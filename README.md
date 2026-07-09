# PUSH Hub

One URL for every PUSH: **https://allinalan.github.io/push-hub/**

Each PUSH gets its own folder of self-contained HTML docs (no build step, no
dependencies), all linked from the landing page (`index.html`).

```
push-hub/
├── index.html        ← landing page listing every PUSH
├── 2026-sc2/         ← one folder per PUSH
│   ├── blueprint.html      ← Alan's blueprint + planner
│   ├── rep-blueprint.html  ← team version: ONE link for all reps
│   └── precheck.html
└── README.md         ← this playbook
```

**Rep edition:** `rep-blueprint.html` is a single shared page for the whole
team. All data (name, levers, tracker) lives in each rep's own browser
(localStorage), so every rep who opens the link gets their own private
blueprint — no per-rep files needed. Note: localStorage is shared across
this whole GitHub Pages site, so each page's storage keys must be unique
(the rep page uses `push2026_rep_*` keys; keep keys year-scoped when
copying to a new PUSH folder).

> **Heads up:** this repo is public and the live site is world-readable.
> Don't commit anything you wouldn't want indexed by Google.
> Checklist progress saves in each device's browser (localStorage) — it does
> **not** sync between phone and laptop.

---

## Playbook: adding the next PUSH

Repeat these steps anytime a new PUSH is coming up. Or just tell Claude Code:
*"Add my new PUSH docs to the push-hub repo and publish"* — and point it at
this README.

1. **Make a folder** named `<year>-<campaign>` (e.g. `2027-sc3/`) in the repo
   root and drop the PUSH's HTML docs in it. Self-contained HTML only —
   inline CSS/JS, no external dependencies. Give each doc a home button at
   the top (copy the `a.home` styles + `← PUSH Hub` link from an existing
   doc) so every page links back to the hub.
2. **Edit `index.html`**: copy the `<div class="push">` block (there's a
   `TO ADD A NEW PUSH` comment above it with instructions), update the title,
   dates, and doc links. Move the `Live` badge to the new PUSH and mark the
   old one `Complete`.
3. **Commit and push:**
   ```bash
   cd push-hub
   git add .
   git commit -m "Add <year> <campaign> PUSH"
   TOKEN=$(security find-internet-password -s github.com -w)
   git push "https://x-access-token:$TOKEN@github.com/allinalan/push-hub.git" main
   ```
   (The token lives in the macOS keychain — no `gh` CLI needed.)
4. **Done.** GitHub Pages redeploys automatically in ~1 minute. The new docs
   are live at `https://allinalan.github.io/push-hub/<year>-<campaign>/`.

## One-time setup (already done — for reference only)

- Repo created as **public** (required for free GitHub Pages).
- Pages enabled: Settings → Pages → Deploy from branch → `main` / root.
- Auth: GitHub token stored in macOS keychain under `github.com`.
