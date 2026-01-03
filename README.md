# Web Development Tutorials

Comprehensive tutorials for fullstack web development covering HTML, CSS, JavaScript, Django, Python, SQL, and Git.

## Features

- **HTML** - Structure and content
- **CSS** - Styling and responsive design
- **JavaScript** - Interactivity and dynamic behavior
- **Django** - Python web framework
- **Python** - Programming fundamentals
- **SQL** - Database management
- **Git** - Version control

## Local Development

### Prerequisites

- Python 3.8+
- pip

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd webdev
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install mkdocs-material
pip install mkdocs
```

4. Serve the site locally:
```bash
mkdocs serve
```

Visit `http://127.0.0.1:8000` to view the site.

### Build

To build the static site:
```bash
mkdocs build
```

The site will be generated in the `site/` directory.

## Deployment to GitHub Pages

This repository is configured for automatic deployment to GitHub Pages using GitHub Actions.

### Automatic Deployment

The site automatically deploys when you push to the `main` branch. The workflow:

1. Builds the MkDocs site
2. Deploys to GitHub Pages
3. Updates the live site

### Manual Deployment

You can also trigger deployment manually:

1. Go to the **Actions** tab in GitHub
2. Select **Deploy to GitHub Pages** workflow
3. Click **Run workflow**

### GitHub Pages Settings

1. Go to your repository **Settings**
2. Navigate to **Pages** section
3. Under **Source**, select **GitHub Actions**

### Custom Domain

If you're using a custom domain (like `web.dataidea.org`):

1. Add a `CNAME` file in the `docs/` directory with your domain:
   ```
   web.dataidea.org
   ```

2. Configure DNS settings with your domain provider

3. The `site_url` in `mkdocs.yml` should match your domain

## Project Structure

```
webdev/
├── docs/              # Documentation source files
│   ├── HTML/
│   ├── CSS/
│   ├── JavaScript/
│   ├── Django/
│   ├── Python/
│   ├── SQL/
│   └── Git/
├── .github/
│   └── workflows/
│       └── deploy.yml # GitHub Actions workflow
├── mkdocs.yml         # MkDocs configuration
└── README.md          # This file
```

## Contributing

1. Make your changes
2. Test locally with `mkdocs serve`
3. Commit and push your changes
4. The site will automatically deploy

## License

[Add your license here]

