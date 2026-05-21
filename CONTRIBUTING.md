# Contributing to LLM-D Landing Page

Thank you for your interest in contributing! This is a simple static landing page for the LLM-D project.

## How to Contribute

### Reporting Issues

Found a typo, broken link, or design issue?

1. Check if the issue already exists in [GitHub Issues](https://github.com/llm-d/llm-d-landing-page/issues)
2. If not, create a new issue with:
   - Clear description of the problem
   - Screenshots if it's a visual issue
   - Steps to reproduce if applicable

### Submitting Changes

1. Fork the repository
2. Create a branch: `git checkout -b fix/your-fix-name`
3. Make your changes to `index.html`
4. Test locally: `open index.html` or `python3 -m http.server 8080`
5. Commit: `git commit -m "Fix: description of your fix"`
6. Push: `git push origin fix/your-fix-name`
7. Open a Pull Request

### Content Guidelines

When updating content:

- **Keep the tone technical but accessible** — target audience is platform engineers and AI infrastructure teams
- **Be specific, not fluffy** — avoid marketing buzzwords, focus on technical value
- **Match the design system** — use existing color palette, typography, and spacing
- **Test responsiveness** — verify the page works on mobile and desktop

### Design System

If you need to modify styles:

- **Colors:**
  - Blue `#58a6ff` — primary accent, request flows
  - Green `#3fb950` — success, response flows
  - Orange `#f0883e` — warnings, auth
  - Purple `#d2a8ff` — processing, special components
  - Red `#f85149` — errors
  - Gold `#e3b341` — secondary highlights

- **Typography:**
  - System fonts: `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
  - Hero title: 36px, weight 800
  - Card title: 18px, weight 700
  - Body: 14px, dim color

- **Spacing:**
  - Container: 900px max-width
  - Card padding: 28px
  - Card margin: 20px bottom
  - Section spacing: 32px bottom

### Code Style

- Use inline CSS (no external stylesheets)
- Keep HTML semantic and accessible
- Minimize file size (target <20KB for index.html)
- No JavaScript dependencies

### Testing Checklist

Before submitting a PR:

- [ ] HTML validates (no syntax errors)
- [ ] Page renders correctly in Chrome, Firefox, Safari
- [ ] Responsive layout works on mobile (320px), tablet (768px), desktop (1440px)
- [ ] All links work and open in new tabs where appropriate
- [ ] No broken images or missing assets
- [ ] File size remains small (<20KB)

### Release Process

1. PR is reviewed by maintainers
2. Once approved, PR is merged to `main`
3. Vercel auto-deploys the updated site
4. Changes are live within ~30 seconds

## Questions?

Open a [GitHub Discussion](https://github.com/llm-d/llm-d-landing-page/discussions) or reach out to the maintainers.

Thank you for contributing!
