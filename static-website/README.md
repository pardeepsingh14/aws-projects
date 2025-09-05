# Static Website Template

A minimal, responsive static website template ready for GitHub Pages.

## What it includes
- `index.html` — clean homepage with hero, features, projects section and contact
- `about.html` — optional about page
- `404.html` — custom 404 page
- `assets/css/styles.css` — simple responsive CSS

## How to use
1. Create a new GitHub repo (e.g., `static-website`).
2. Copy these files into the repo and commit.
3. Push to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: static website"
   git branch -M main
   git remote add origin https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git
   git push -u origin main
   ```
4. Enable GitHub Pages:
   - Go to `Settings` → `Pages` → `Source` → select `main` branch and `/ (root)` folder → Save.
   - Your site will be available at `https://<YOUR_USERNAME>.github.io/<REPO_NAME>/`.

## Optional: Use custom domain
- Add `CNAME` file with your domain name.
- Configure DNS `CNAME`/`A` records as per GitHub Pages docs.

## License
MIT
