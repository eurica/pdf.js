# GitHub Pages Deployment

This repository includes a GitHub Actions workflow to automatically deploy the PDF.js viewer to GitHub Pages.

## Features

The deployed viewer includes custom modifications:

- **Hidden Toolbar**: Toolbar is hidden by default, press `Esc` to toggle visibility
- **Text Layer Opacity Control**: Floating slider in the top-right corner to control text layer visibility (0-100%)
- **Smooth Animations**: Color transitions for text layer visibility changes

## Setup

### 1. Enable GitHub Pages

1. Go to your repository's **Settings** tab
2. Navigate to **Pages** in the left sidebar
3. Under **Source**, select **GitHub Actions**
4. The workflow will automatically deploy when you push to the `master` branch

### 2. Repository Settings

The workflow requires these permissions:
- `contents: read` - To checkout the code
- `pages: write` - To deploy to GitHub Pages
- `id-token: write` - To verify deployment origin

These are automatically configured in the workflow file.

## Workflow Details

The deployment workflow (`deploy-pages.yml`) does the following:

1. **Build Process**:
   - Checks out the repository
   - Sets up Node.js 20
   - Installs dependencies with `npm ci`
   - Builds the generic viewer with `npx gulp generic`
   - Builds the website with `npx gulp web`

2. **Deployment**:
   - Uploads the built files to GitHub Pages
   - Deploys to the `github-pages` environment
   - Provides the deployment URL

## Manual Deployment

You can manually trigger the deployment by:

1. Going to the **Actions** tab in your repository
2. Selecting the **Deploy to GitHub Pages** workflow
3. Clicking **Run workflow**

## Custom Features

### Hidden Toolbar
- Press `Esc` to show/hide the toolbar
- Click outside the toolbar to hide it
- Smooth slide animations

### Text Layer Opacity Slider
- Located in the top-right corner
- Controls text layer visibility from 0% (invisible) to 100% (fully visible)
- Smooth color transitions instead of opacity changes
- Real-time updates as you move the slider

## Troubleshooting

If the deployment fails:

1. Check the **Actions** tab for error details
2. Ensure GitHub Pages is enabled in repository settings
3. Verify the `master` branch exists and has the latest code
4. Check that all required files are committed

## Local Development

To test the deployment locally:

```bash
# Install dependencies
npm ci

# Build the generic viewer
npx gulp generic

# Build the website
npx gulp web

# The built files will be in build/gh-pages/
```
