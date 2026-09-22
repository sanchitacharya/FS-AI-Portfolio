# Formula Student AI — portfolio

Public write-up of my Formula Student driverless work (planning & control).

**This repo does not contain team source code.**

## Live page

After you enable GitHub Pages, open:

`https://YOUR_USERNAME.github.io/FS-AI-Portfolio/`

(Replace `YOUR_USERNAME`. If the repo name differs, match it in the URL.)

## What’s on the page

- What Formula Student AI / driverless missions are
- **Acceleration** planning & control (worked)
- **Skidpad** attempt (did not hold on the real car)
- High-level stack only

## Local preview

```bash
cd ~/FS-AI-Portfolio
python3 -m http.server 8080
```

Open http://localhost:8080

## Publish

```bash
git init
git add .
git commit -m "Add Formula Student AI portfolio page"
git branch -M main
git remote add origin git@github.com:YOUR_USERNAME/FS-AI-Portfolio.git
git push -u origin main
```

Then: GitHub repo → **Settings** → **Pages** → Deploy from branch **main** / **root**.
