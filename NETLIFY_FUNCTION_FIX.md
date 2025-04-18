# Fixing "Could not resolve serverless-http" Error in Netlify Functions

This document provides a step-by-step guide to fix the specific error you're encountering with Netlify Functions.

## Error Details

```
✘ [ERROR] Could not resolve "serverless-http"
     netlify/functions/api.mjs:3:23:
       3 │ import serverless from "serverless-http";
         ╵                        ~~~~~~~~~~~~~~~~~
```

## Solution: Change the Netlify Function Bundler

The most effective solution is to change how Netlify bundles your functions:

1. Go to your Netlify dashboard
2. Select your site
3. Go to **Site settings > Functions**
4. Under **Function bundling**, change from "esbuild" to "Netlify CLI bundler"
5. Save the changes and redeploy your site

This approach will use the default Netlify bundler, which handles external dependencies differently and should resolve the serverless-http issue.

## Alternative Solution: Force Install During Build

If changing the bundler doesn't work, modify your netlify.toml file:

```toml
[build]
  command = "npm install serverless-http && node netlify/build-deploy-info.js && vite build && node netlify/build-db.js && esbuild netlify/functions/api.ts --platform=node --packages=external --bundle --format=esm --outfile=netlify/functions/api.mjs"
  publish = "dist/public"
  functions = "netlify/functions"

[functions]
  node_bundler = "esbuild"
  
[functions.api]
  external_node_modules = ["serverless-http"]
```

The key changes:
1. Add `npm install serverless-http &&` to the beginning of the build command
2. Add `[functions.api]` section with `external_node_modules = ["serverless-http"]`

## Important Note About DATABASE_URL

Remember that after fixing the serverless-http issue, you'll still need to set up the DATABASE_URL environment variable in your Netlify dashboard:

1. Go to **Site settings > Build & deploy > Environment**
2. Add a new variable:
   - Key: `DATABASE_URL`
   - Value: Your PostgreSQL connection string

## Commit and Redeploy

After making these changes:
1. Commit them to your Git repository
2. Push to GitHub
3. Netlify will automatically redeploy your site

## Need Further Help?

If you continue to experience issues, please check the detailed troubleshooting guide in NETLIFY_TROUBLESHOOTING.md or contact Netlify support.