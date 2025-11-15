# GitHub Pages Hosting Setup

## Quick Start

Your website is now optimized for GitHub Pages hosting! Here's how to deploy:

### Step 1: Enable GitHub Pages

1. Go to your repository settings: `https://github.com/ak-ake/free-code-resource/settings`
2. Scroll to **"Pages"** section (left sidebar)
3. Select:
   - **Source**: `Deploy from a branch`
   - **Branch**: `main` and folder: `/ (root)`
4. Click **Save**

### Step 2: Your Site Will Be Live At:
```
https://ak-ake.github.io/free-code-resource/
```

## Important Files Included

- **.nojekyll** - Tells GitHub Pages to serve files as-is without Jekyll processing
- **GITHUB_PAGES_SETUP.md** - This setup guide
- All HTML, CSS, and image files are GitHub Pages compatible

## URL Structure

GitHub Pages will serve your website with URLs like:
- Homepage: `https://ak-ake.github.io/free-code-resource/`
- About: `https://ak-ake.github.io/free-code-resource/assets/pages/about.html`
- Codes: `https://ak-ake.github.io/free-code-resource/assets/pages/codes.html`

### To Add Clean URLs (Optional)

If you want clean URLs like `/codes/` instead of `/assets/pages/codes.html`:

**Option 1: Using GitHub Actions (Recommended)**

Create `.github/workflows/jekyll-deploy.yml`:
```yaml
name: Build and Deploy Jekyll site

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: 3.1
          bundler-cache: true
      - name: Build Jekyll
        run: jekyll build --baseurl /free-code-resource
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site
```

**Option 2: Keep Current Structure**

Keep your current directory structure and reference files with full paths in HTML. (Already implemented in your code!)

## Notes

- **.nojekyll** file prevents Jekyll from processing your site - this keeps your exact file structure
- All relative paths in your HTML use `assets/` which work perfectly with GitHub Pages
- Your website will work immediately after enabling Pages in settings
- No build process needed - your HTML, CSS, and images deploy as-is

## Performance Tips

GitHub Pages automatically serves files with:
- ✅ HTTPS enabled
- ✅ Gzip compression
- ✅ CDN caching
- ✅ Automatic SSL certificate

## Testing Before Deployment

To test locally if you have GitHub CLI installed:
```bash
cd /home/ake/Desktop/Github/free-code-resource
python3 -m http.server 8000
```

Then visit: `http://localhost:8000/`

## Domain Setup (Optional)

If you want a custom domain like `code-source.com`:

1. In GitHub Settings → Pages → Custom domain
2. Enter your domain (e.g., `code-source.com`)
3. Configure your domain provider's DNS records as GitHub instructs

## Troubleshooting

**Site not appearing?**
- Wait 1-2 minutes for GitHub Pages to build
- Check repository is public
- Verify `.nojekyll` file exists in root

**Assets not loading?**
- Check browser console for 404 errors
- Verify all paths use `assets/` prefix (already done)
- Clear browser cache

**URLs showing .html extension?**
- This is normal on GitHub Pages without Jekyll plugins
- Files still work and are fully functional
