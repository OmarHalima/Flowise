# Deploying Flowise to Netlify

This guide will help you deploy your Flowise application to Netlify.

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
  command = "pnpm install && pnpm build"
  publish = "packages/ui/dist"

[build.environment]
  NODE_VERSION = "18.15.0"
  NPM_FLAGS = "--version"
```

Make sure these settings match in the Netlify deploy configuration:
- Build command: `pnpm install && pnpm build`
- Publish directory: `packages/ui/dist`

### 3. Configure environment variables

In your Netlify site settings, go to "Site settings" > "Environment variables" and add:

- `NPM_FLAGS`: `--version`
- `NODE_VERSION`: `18.15.0`

### 4. Update the UI environment variables

Before deploying, make sure to update the `.env` file in the `packages/ui` directory with the correct API URL:

```
VITE_API_BASE_URL=https://your-backend-api-url.com
VITE_UI_BASE_URL=https://your-netlify-site-name.netlify.app
```

**Note**: For the frontend to work properly, you'll need to deploy the backend (Flowise API server) separately to a platform like Heroku, Railway, Render, etc., and update the VITE_API_BASE_URL accordingly.

### 5. Deploy

Click "Deploy site" in Netlify. The deployment process will start and you can monitor its progress.

### 6. Configure domain (Optional)

After deployment, you can configure a custom domain in the Netlify settings.

## Backend Deployment

Remember that this only deploys the UI. You need to deploy the backend separately:

1. Choose a platform that supports Node.js applications (Heroku, Railway, Render, etc.)
2. Deploy the backend following the platform's instructions
3. Update the VITE_API_BASE_URL in the UI environment variables to point to your backend URL
4. Redeploy the UI if necessary 