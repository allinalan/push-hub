# GitHub Handoff — 2026 PUSH Pre-Check Checklist

## What this is
A single self-contained HTML file: `2026_PUSH_PreCheck.html`.
- No build step, no dependencies, no server. Pure HTML/CSS/JS.
- Saves user progress via browser `localStorage` (per-device, does NOT sync across devices).
- Goal: host it so it's reachable from any device at a URL (GitHub Pages).

## Privacy note (read first)
The file's "Personal" tab contains private personal info. GitHub Pages on a **free** plan requires a **public** repo (world-readable + indexable). Options:
- Private repo + Pages → requires GitHub Pro (paid).
- Public repo → free but fully public. If going public, consider removing/genericizing the Personal tab first.

Ask the owner which they want before pushing.

---

## Paste this into Claude Code

> I have a single self-contained HTML file called `2026_PUSH_PreCheck.html` (I'll place it in the project folder). I want to publish it to GitHub Pages so I can open it from any device.
>
> Please:
> 1. Confirm the file is in the repo root, then copy it to `index.html` (GitHub Pages serves `index.html` by default). Keep the original filename too if easy.
> 2. Initialize a git repo, make an initial commit.
> 3. Create the GitHub repo named `push-checklist` — ask me whether it should be **private** (I have GitHub Pro) or **public** before creating. Use the `gh` CLI if available (`gh repo create`), otherwise walk me through creating it on github.com and adding the remote.
> 4. Push `main` to the remote.
> 5. Enable GitHub Pages on the `main` branch, root folder. Give me the final live URL.
> 6. Verify the page loads and note that progress is stored in the browser (localStorage) and will not sync between devices.
>
> If I later want checkmarks to sync across my phone and laptop, tell me what that would take (a lightweight backend or a hosted DB) but don't build it now.

---

## Reference commands (if not using the `gh` CLI)
```bash
# in the folder containing the HTML file
cp 2026_PUSH_PreCheck.html index.html
git init
git add .
git commit -m "Add 2026 PUSH pre-check checklist"
git branch -M main
# create the repo on github.com first, then:
git remote add origin https://github.com/<your-username>/push-checklist.git
git push -u origin main
```
Then on github.com: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / root → Save.**
Live URL will be: `https://<your-username>.github.io/push-checklist/`

## With the `gh` CLI (faster)
```bash
cp 2026_PUSH_PreCheck.html index.html
git init && git add . && git commit -m "Add 2026 PUSH pre-check checklist"
git branch -M main
gh repo create push-checklist --private --source=. --remote=origin --push   # or --public
gh api -X POST repos/<your-username>/push-checklist/pages -f "source[branch]=main" -f "source[path]=/"
```

## File location
The HTML file is in your Cowork outputs folder. Move or copy it into whatever local folder Claude Code is working in before running the steps above.
