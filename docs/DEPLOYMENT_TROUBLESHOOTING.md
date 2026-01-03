# Deployment Troubleshooting

If your site is not automatically deploying, check the following:

## 1. GitHub Pages Configuration

**Critical:** GitHub Pages must be configured to use GitHub Actions, not a branch.

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under **Source**, select **GitHub Actions** (NOT "Deploy from a branch")
4. Save the settings

If you see "Deploy from a branch" selected, that's the problem! Change it to "GitHub Actions".

## 2. Check Branch Name

The workflow triggers on pushes to `main` or `master` branches. Verify your default branch:

1. Go to **Settings** → **Branches**
2. Check what your default branch is named
3. If it's not `main` or `master`, update the workflow file:

```yaml
on:
  push:
    branches:
      - your-branch-name
```

## 3. Check Workflow Permissions

The workflow needs proper permissions. Verify in `.github/workflows/deploy.yml`:

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

## 4. Check Actions Tab

1. Go to the **Actions** tab in your repository
2. Check if the workflow is running
3. If it's not running, check for any error messages
4. If you see "Workflow run is waiting for a runner", wait a moment

## 5. Manual Trigger

Try triggering the workflow manually:

1. Go to **Actions** tab
2. Select **Deploy to GitHub Pages** workflow
3. Click **Run workflow** button
4. Select your branch
5. Click **Run workflow**

## 6. Check Workflow Logs

If the workflow runs but fails:

1. Click on the workflow run
2. Check each step for errors
3. Common issues:
   - Missing dependencies
   - Build errors
   - Permission errors

## 7. Verify Workflow File Location

Ensure the workflow file is at:
```
.github/workflows/deploy.yml
```

## 8. First Time Setup

If this is your first deployment:

1. Make sure you've pushed the workflow file to GitHub
2. Go to **Settings** → **Pages**
3. Select **GitHub Actions** as the source
4. Push a change to trigger the workflow

## 9. Check Repository Settings

Ensure GitHub Actions is enabled:

1. Go to **Settings** → **Actions** → **General**
2. Under **Workflow permissions**, select:
   - "Read and write permissions"
   - "Allow GitHub Actions to create and approve pull requests"
3. Save changes

## Still Not Working?

If none of the above works:

1. Check the Actions tab for specific error messages
2. Verify your repository is public (or you have GitHub Pro/Team for private repos)
3. Try deleting and recreating the workflow file
4. Check GitHub status page for any service issues

