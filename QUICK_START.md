# Quick Start - Get Your Site Live in 5 Minutes

## Step 1: Enable GitHub Pages (2 minutes)

1. Go to: https://github.com/YesselmanLab/lab-docs/settings/pages
2. Under **"Source"**, select **"GitHub Actions"**
3. Click **Save**

## Step 2: Trigger Deployment (1 minute)

**Option A - Via GitHub:**
1. Go to: https://github.com/YesselmanLab/lab-docs/actions
2. Click **"Deploy to GitHub Pages"** on the left
3. Click **"Run workflow"** → **"Run workflow"**

**Option B - Via Command Line:**
```bash
git commit --allow-empty -m "Trigger deployment"
git push origin main
```

## Step 3: Wait (2 minutes)

1. Go to: https://github.com/YesselmanLab/lab-docs/actions
2. Watch the workflow run
3. Wait for the green checkmark ✅

## Step 4: Visit Your Site

Open: **https://yesselmanlab.github.io/lab-docs/**

That's it! 🎉

---

## Updating Content

Just edit files in the `docs/` folder and push to GitHub. The site will automatically rebuild!

