# Deployment Guide

This guide will help you deploy your documentation site to GitHub Pages.

## Initial Setup (One-Time)

### Step 1: Enable GitHub Pages

1. Go to your repository on GitHub: `https://github.com/YesselmanLab/lab-docs`
2. Click on **Settings** (top right of the repository page)
3. Scroll down to **Pages** in the left sidebar
4. Under **Source**, select **"GitHub Actions"** (NOT "Deploy from a branch")
5. Click **Save**

### Step 2: Trigger the First Deployment

The GitHub Actions workflow will automatically run when you push to the `main` branch. To trigger it:

**Option A: Push any change**
```bash
git add .
git commit -m "Trigger initial deployment"
git push origin main
```

**Option B: Manually trigger the workflow**
1. Go to the **Actions** tab in your repository
2. Click on **"Deploy to GitHub Pages"** workflow
3. Click **"Run workflow"** button
4. Select the branch (usually `main`) and click **"Run workflow"**

### Step 3: Wait for Deployment

1. Go to the **Actions** tab
2. You should see a workflow run in progress
3. Wait for it to complete (usually 2-3 minutes)
4. Once it shows a green checkmark ✅, your site is deployed!

### Step 4: Access Your Site

Your documentation will be available at:
**https://yesselmanlab.github.io/lab-docs/**

Note: It may take a few minutes after deployment for the site to be accessible.

---

## Updating the Documentation

### Method 1: Edit on GitHub (Easiest)

1. Navigate to the file you want to edit in the `docs/` folder
2. Click the **pencil icon** (✏️) to edit
3. Make your changes
4. Scroll down and click **"Commit changes"**
5. The site will automatically rebuild and deploy (check the Actions tab)

### Method 2: Edit Locally

1. **Clone the repository** (if you haven't already):
   ```bash
   git clone https://github.com/YesselmanLab/lab-docs.git
   cd lab-docs
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Preview locally** (optional):
   ```bash
   mkdocs serve
   ```
   Then open http://127.0.0.1:8000 in your browser

5. **Make your edits** to files in the `docs/` directory

6. **Commit and push**:
   ```bash
   git add .
   git commit -m "Update documentation"
   git push origin main
   ```

7. **Wait for deployment**: Check the Actions tab - the site will automatically rebuild

---

## Troubleshooting

### Site shows 404 error

- **Check Actions tab**: Make sure the workflow completed successfully
- **Check Pages settings**: Ensure "GitHub Actions" is selected as the source
- **Wait a few minutes**: Sometimes it takes 5-10 minutes for changes to propagate

### Workflow fails

1. Go to **Actions** tab
2. Click on the failed workflow run
3. Check the error message
4. Common issues:
   - Missing dependencies: Check `requirements.txt`
   - YAML syntax error: Check `mkdocs.yml`
   - Missing files: Ensure all files referenced in `mkdocs.yml` exist

### Changes not showing up

1. **Clear browser cache**: Hard refresh (Ctrl+Shift+R or Cmd+Shift+R)
2. **Check deployment**: Go to Actions tab and verify the latest deployment succeeded
3. **Check URL**: Make sure you're visiting `https://yesselmanlab.github.io/lab-docs/`

### Need to rebuild manually

1. Go to **Actions** tab
2. Click **"Deploy to GitHub Pages"** workflow
3. Click **"Run workflow"**
4. Select branch and click **"Run workflow"**

---

## File Structure

- `docs/` - All your documentation markdown files
- `mkdocs.yml` - Configuration file (navigation, theme, etc.)
- `.github/workflows/ci.yml` - GitHub Actions deployment workflow
- `requirements.txt` - Python dependencies

## Common Tasks

### Adding a New Page

1. Create a new `.md` file in the appropriate `docs/` subdirectory
2. Add it to the `nav:` section in `mkdocs.yml`
3. Commit and push

### Changing the Theme

Edit the `theme:` section in `mkdocs.yml`

### Changing Navigation

Edit the `nav:` section in `mkdocs.yml`

---

## Need Help?

- Check the [MkDocs documentation](https://www.mkdocs.org/)
- Check the [Material theme documentation](https://squidfunk.github.io/mkdocs-material/)
- Review GitHub Actions logs in the Actions tab

