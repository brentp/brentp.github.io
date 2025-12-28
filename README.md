A static personal site built with [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) and deployed using GitHub Actions with [mike](https://github.com/jimporter/mike).

## Features

- Material Design theme with dark/light mode
- Mobile-responsive design
- Code syntax highlighting
- Search functionality
- Versioned deployments via mike
- Draft posts in dev branch

## Local Development

### Setup with uv

1. **Install uv** (if not already installed):
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
   Or follow the [official installation guide](https://docs.astral.sh/uv/getting-started/installation/).

2. **Create and activate virtual environment**:
   ```bash
   uv venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   uv pip install -r requirements.txt
   ```

4. **Start the development server**:
   ```bash
   mkdocs serve
   ```

   The site will be available at `http://127.0.0.1:8000`

5. **Optional: Enable live reloading**:
   ```bash
   mkdocs serve --livereload
   ```

### Alternative: Using pip without uv

If you prefer not to use uv:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
```

## Adding Content

### Blog Posts
Add new blog posts as markdown files in the `docs/blog/` directory. Include frontmatter with title, date, and description:

```markdown
---
title: Your Post Title
date: 2024-01-01
description: Brief description of the post
---

# Your Post Title

Content goes here...
```

### Draft Posts
Add draft posts to the `docs/drafts/` directory. These will only be visible when deploying from the `dev` branch.

## Deployment

### GitHub Pages Setup
1. Go to your repository Settings → Pages
2. Set Source to "Deploy from a branch"
3. Set Branch to `gh-pages` and folder to `/ (root)`
4. Save settings

### Main Site
- Push to `main` or `master` branch to deploy to the main site
- Tag releases with `v*` (e.g., `v1.0.0`) to create versioned deployments
- Site will be available at `https://yourusername.github.io/`

### Dev Site
- Push to `dev` branch to deploy a development version with drafts visible
- Access dev version at `/dev/` path on your GitHub Pages site

**Note**: The `gh-pages` branch is created automatically after the first successful deployment.

## GitHub Actions

The site is automatically deployed via GitHub Actions:

- **Production deployments**: Main branch pushes and tagged releases
- **Development deployments**: Dev branch pushes (includes drafts)
- **Version management**: Uses mike for versioned documentation

## Configuration

Edit `mkdocs.yml` to customize:
- Site information (title, description, author)
- Theme settings (colors, fonts, features)
- Navigation structure
- Plugins and extensions

## Theme Features

This blog uses mkdocs-material with the following features enabled:
- Navigation tabs and sections
- Search with highlighting
- Code copying
- Dark/light mode toggle
- Mobile responsiveness
- Instant navigation
- Auto-hiding header

## License

This content is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
