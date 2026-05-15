# Deploy to GitHub Pages — `jd3vi1div6/ttx-app`

Step-by-step. Run from inside the project folder. Replace `<YOUR_TOKEN>` only if you use HTTPS auth without a credential helper.

## Option A — Using `gh` CLI (recommended, fastest)

```bash
# 1. Install gh if you haven't: https://cli.github.com/
# 2. Authenticate once:
gh auth login

# 3. From inside the project folder:
cd "TTX app"

# 4. Initialize, commit, create repo, push, enable Pages:
git init
git add .
git commit -m "Initial commit — TTX app (dashboard, tracker, CREM demo)"
git branch -M main

gh repo create jd3vi1div6/ttx-app --public --source=. --remote=origin --push

# 5. Enable GitHub Pages on the main branch (root):
gh api -X POST /repos/jd3vi1div6/ttx-app/pages \
  -f "source[branch]=main" \
  -f "source[path]=/"

echo "Live in ~1 minute at: https://jd3vi1div6.github.io/ttx-app/"
```

## Option B — Plain `git` (no gh CLI)

```bash
cd "TTX app"

git init
git add .
git commit -m "Initial commit — TTX app"
git branch -M main

# Create the empty repo first via the GitHub web UI:
# https://github.com/new   →   name: ttx-app   →   Public   →   Create
# (Don't initialize with README/license/.gitignore — we already have them.)

git remote add origin https://github.com/jd3vi1div6/ttx-app.git
git push -u origin main

# Then in the GitHub web UI:
#   Settings → Pages → Source: Deploy from a branch
#   Branch: main / (root) → Save
```

## Updating later

```bash
git add -A
git commit -m "Update <what changed>"
git push
# GitHub Pages redeploys automatically — usually <60s.
```

## Verifying

After Pages activates, hit each URL in a browser:

- https://jd3vi1div6.github.io/ttx-app/                  ← landing
- https://jd3vi1div6.github.io/ttx-app/dashboard.html
- https://jd3vi1div6.github.io/ttx-app/tracker.html
- https://jd3vi1div6.github.io/ttx-app/crem-demo.html

If any page shows unstyled content, check that `assets/pipboy.css` was committed — `git ls-files assets/`.

## Custom domain (optional)

```bash
echo "ttx.yourdomain.com" > CNAME
git add CNAME && git commit -m "Add CNAME" && git push
# Then add a CNAME record at your DNS provider pointing to jd3vi1div6.github.io
```
