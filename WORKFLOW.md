# Auto-Update Workflow Documentation

## Overview

This repository includes a GitHub Actions workflow that automatically updates the `links` and `README.md` files whenever new images are added to the repository.

## How It Works

### Workflow Trigger

The workflow is triggered automatically when:
- A push is made to the `main` branch
- The push includes changes to image files (`.png`, `.jpg`, `.jpeg`, `.gif`, or `.svg`)

### What It Does

1. **Scans for Images**: Finds all image files in the root directory
2. **Updates `links` file**: Generates a list of raw GitHub URLs for all images
3. **Updates `README.md`**: Creates a formatted README with:
   - A list of all available images with clickable links
   - Human-readable names derived from filenames
   - Usage instructions

### Workflow File

Location: `.github/workflows/update-image-links.yml`

## Manual Testing

To test the workflow logic locally without triggering the workflow:

```bash
# Find all image files
find . -maxdepth 1 -type f \( -iname "*.png" -o -iname "*.jpg" \
  -o -iname "*.jpeg" -o -iname "*.gif" -o -iname "*.svg" \) | sort

# This would be the logic that generates the links and README
```

## Adding New Images

Simply add your image files to the root directory and push to the `main` branch:

```bash
# Add your image
cp /path/to/your/image.png .

# Commit and push
git add image.png
git commit -m "Add new image"
git push origin main
```

The workflow will automatically run and update the `links` and `README.md` files.

## Permissions

The workflow requires:
- `contents: write` permission to commit and push changes back to the repository

This is granted automatically by the `GITHUB_TOKEN` secret in GitHub Actions.

## Customization

To modify what gets included in the README or links file:
1. Edit `.github/workflows/update-image-links.yml`
2. Modify the bash script in the "Update links and README" step
3. Commit and push your changes

## Troubleshooting

If the workflow fails to run:
1. Check the Actions tab in GitHub to view the workflow run logs
2. Ensure the workflow has proper permissions
3. Verify that image files are in the root directory (not in subdirectories)
