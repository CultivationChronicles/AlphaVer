# Fixing "vite: command not found" Error in Netlify Deployment

This document provides a step-by-step guide to fix the "vite: command not found" error that occurs when Netlify is in production mode.

## Error Details

```
bash: line 1: vite: command not found
```

This error occurs because:
1. Netlify sets `NODE_ENV=production` during builds
2. When `NODE_ENV` is set to production, npm only installs regular dependencies, not devDependencies
3. Vite is typically listed as a devDependency in package.json

## Solution 1: Update Netlify Build Command (Recommended)

The most effective solution is to modify your netlify.toml file to explicitly install the required packages:

```toml
[build]
  command = "npm install --include=dev serverless-http vite esbuild @vitejs/plugin-react && node netlify/build-deploy-info.js && ./node_modules/.bin/vite build && node netlify/build-db.js && ./node_modules/.bin/esbuild netlify/functions/api.ts --platform=node --packages=external --bundle --format=esm --outfile=netlify/functions/api.mjs"
  publish = "dist/public"
  functions = "netlify/functions"
```

Key changes:
1. `npm install --include=dev` forces npm to install devDependencies even in production mode
2. We explicitly list all critical packages needed for the build
3. We use `./node_modules/.bin/vite` and `./node_modules/.bin/esbuild` to ensure we're using the local installations

## Solution 2: Move Vite to Regular Dependencies

An alternative solution is to update your package.json to move Vite and related packages from devDependencies to regular dependencies:

```json
{
  "dependencies": {
    // ... existing dependencies
    "vite": "^5.4.14",
    "@vitejs/plugin-react": "^4.3.2",
    "esbuild": "^0.25.0"
  }
}
```

This ensures these packages are always installed, even in production mode.

## Solution 3: Disable Production Mode

You can also tell Netlify to not use production mode for npm installs:

1. Go to Netlify dashboard → Site settings → Build & deploy → Environment
2. Add a new variable:
   - Key: `NPM_CONFIG_PRODUCTION`
   - Value: `false`

This will cause npm to install all dependencies including devDependencies.

## Important Note About Vite Configuration

Make sure your vite.config.ts is correctly set up to handle production builds. Check for any settings that might be environment-specific.

## After Fixing the Vite Error

Remember that after fixing the Vite build error, you'll still need to:

1. Address the "serverless-http" dependency issue for Netlify Functions
2. Set up the DATABASE_URL environment variable

## Commit and Redeploy

After making these changes:
1. Commit them to your Git repository
2. Push to GitHub
3. Netlify will automatically redeploy your site

## Need Further Help?

If you continue to experience issues, please check the detailed troubleshooting guide in NETLIFY_TROUBLESHOOTING.md or contact Netlify support.