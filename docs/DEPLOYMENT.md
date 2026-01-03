# Deployment Guide

This guide explains how to deploy the MkDocs site to GitHub Pages.

## Automatic Deployment

The site is configured to automatically deploy to GitHub Pages when you push changes to the `main` branch.

### How It Works

1. **Push to main branch** - When you commit and push changes to the `main` branch
2. **GitHub Actions triggers** - The workflow automatically starts
3. **Site builds** - MkDocs builds the static site
4. **Deploys to GitHub Pages** - The site is automatically published

### Workflow File

The deployment workflow is located at `.github/workflows/deploy.yml`. It:

- Checks out your repository
- Sets up Python
- Installs MkDocs and dependencies
- Builds the site
- Deploys to GitHub Pages

## Manual Deployment

You can also trigger deployment manually:

1. Go to your repository on GitHub
2. Click on the **Actions** tab
3. Select **Deploy to GitHub Pages** workflow
4. Click **Run workflow** button
5. Select the branch (usually `main`)
6. Click **Run workflow**

## GitHub Pages Configuration

### Initial Setup

1. Go to your repository **Settings**
2. Navigate to **Pages** in the left sidebar
3. Under **Source**, select **GitHub Actions** (not "Deploy from a branch")
4. Save the settings

### Custom Domain

If you're using a custom domain (like `web.dataidea.org`):

1. **Create CNAME file** in the `docs/` directory:
   ```
   web.dataidea.org
   ```

2. **Update mkdocs.yml** - Ensure `site_url` matches your domain:
   ```yaml
   site_url: https://web.dataidea.org/
   ```

3. **Configure DNS** - Add a CNAME record pointing to your GitHub Pages URL:
   - Type: `CNAME`
   - Name: `web` (or `@` for root domain)
   - Value: `your-username.github.io` (or your repository's GitHub Pages URL)

4. **Wait for DNS propagation** - This can take up to 24 hours

## Troubleshooting

### Deployment Not Working

1. **Check Actions tab** - Look for any errors in the workflow run
2. **Verify branch name** - Ensure your default branch is `main` (or update the workflow file)
3. **Check permissions** - Ensure GitHub Actions has write permissions
4. **Review logs** - Check the workflow logs for specific error messages

### Site Not Updating

1. **Wait a few minutes** - Deployment can take 1-2 minutes
2. **Clear browser cache** - Hard refresh (Ctrl+F5 or Cmd+Shift+R)
3. **Check GitHub Pages status** - Go to Settings > Pages to see deployment status

### Build Errors

Common issues:

- **Missing dependencies** - Ensure all required packages are in the workflow
- **Syntax errors** - Check `mkdocs.yml` for YAML syntax errors
- **Missing files** - Ensure all referenced files exist

## Local Testing

Before deploying, always test locally:

```bash
# Serve locally
mkdocs serve

# Build and check
mkdocs build
```

## Branch Configuration

If your default branch is not `main`, update the workflow file:

```yaml
on:
  push:
    branches:
      - master  # Change to your default branch name
```

## Additional Resources

- [MkDocs Documentation](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

