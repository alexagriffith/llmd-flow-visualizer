# Deployment Guide

This site is a static HTML page designed to be deployed to any static hosting platform.

## Deploy to Vercel

### Via Vercel Dashboard

1. Push this repo to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Click "New Project"
4. Import your GitHub repository
5. Click "Deploy"

The site will be live at `https://your-project.vercel.app`

### Via Vercel CLI

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy to production
vercel --prod
```

## Deploy to Netlify

### Via Netlify Dashboard

1. Push this repo to GitHub
2. Go to [netlify.com](https://netlify.com)
3. Click "Add new site" → "Import an existing project"
4. Connect to GitHub and select your repository
5. Click "Deploy"

### Via Netlify CLI

```bash
# Install Netlify CLI
npm i -g netlify-cli

# Deploy
netlify deploy

# Deploy to production
netlify deploy --prod
```

## Deploy to GitHub Pages

1. Push this repo to GitHub
2. Go to repository Settings → Pages
3. Under "Source", select the branch (usually `main`)
4. Click "Save"

The site will be live at `https://your-username.github.io/repo-name`

## Deploy to Cloudflare Pages

1. Push this repo to GitHub
2. Go to [pages.cloudflare.com](https://pages.cloudflare.com)
3. Click "Create a project"
4. Connect to GitHub and select your repository
5. Click "Begin setup" → "Save and Deploy"

## Local Development

Since this is a static HTML site with no build process, you can open it directly in a browser:

```bash
# Option 1: Open directly
open index.html

# Option 2: Use a simple HTTP server
python3 -m http.server 8000
# Then visit http://localhost:8000

# Option 3: Use Node.js http-server
npx http-server
```

## Custom Domain

### Vercel

1. Go to your project settings
2. Click "Domains"
3. Add your custom domain
4. Update DNS records as instructed

### Netlify

1. Go to "Domain settings"
2. Click "Add custom domain"
3. Update DNS records as instructed

### GitHub Pages

1. Add a `CNAME` file to the root with your domain
2. Update DNS to point to GitHub's servers
3. Enable "Enforce HTTPS" in repository settings

## Environment Variables

This site has no environment variables or build-time configuration. It's a fully static page.

## Performance Tips

The site is already optimized:

- Inline CSS (no external stylesheets to fetch)
- No JavaScript dependencies
- No images (uses emoji icons)
- Small HTML size (~15KB)

For further optimization:

- Enable compression (gzip/brotli) on your CDN
- Set cache headers for long-term caching
- Enable HTTP/2 or HTTP/3

## Troubleshooting

**Problem:** Site doesn't load

- Check that `index.html` is in the root directory
- Verify the hosting platform is serving HTML files correctly

**Problem:** Styles don't apply

- Ensure the `<style>` block in `index.html` is intact
- Check browser console for errors

**Problem:** Links don't work

- Verify GitHub repository URLs are correct
- Update placeholder links to actual project repositories
