# Deploying Flowise UI to Netlify

This guide will help you deploy the Flowise UI application to Netlify as a standalone frontend.

## Prerequisites

1. Create a [Netlify account](https://app.netlify.com/signup) if you don't already have one
2. Make sure you have your Flowise project on a Git repository (GitHub, GitLab, or Bitbucket)

## Steps to Deploy

### 1. Connect your Git repository to Netlify

1. Log in to your Netlify account
2. Click "Add new site" > "Import an existing project"
3. Connect to your Git provider (GitHub, GitLab, or Bitbucket)
4. Select your Flowise repository

### 2. Configure build settings

The netlify.toml file in the root of your project already contains the necessary configuration:

```toml
[build]
  base = "."
  command = "pnpm run netlify-build"
  publish = "packages/ui/dist"

[build.environment]
  NODE_VERSION = "18.15.0"
  NPM_FLAGS = "--version"
```

Make sure these settings match in the Netlify deploy configuration:
- Build command: `pnpm run netlify-build`
- Publish directory: `packages/ui/dist`

### 3. Configure environment variables

In your Netlify site settings, go to "Site settings" > "Environment variables" and add:

- `NPM_FLAGS`: `--version`
- `NODE_VERSION`: `18.15.0`

### 4. UI-only Deployment

Since we're deploying in UI-only mode (without an API backend), the UI will have limited functionality. To access full functionality in the future, you would need to:

1. Deploy the backend separately
2. Update the `VITE_API_BASE_URL` environment variable to point to your backend

### 5. Deploy

Click "Deploy site" in Netlify. The deployment process will start and you can monitor its progress.

### 6. Configure domain (Optional)

After deployment, you can configure a custom domain in the Netlify settings. 