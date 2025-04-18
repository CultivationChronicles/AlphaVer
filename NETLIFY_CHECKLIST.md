# Netlify Deployment Checklist

This checklist will help ensure a smooth deployment of your Wuxia Cultivation Game to Netlify.

## Pre-Deployment Preparation

✅ Fixed code issues (duplicate keys in martial-techniques.tsx)
✅ Updated build-db.js to use ES module syntax (import instead of require)
✅ Fixed game mechanics bugs (cultivation upgrades not applying correctly)
✅ Build script works properly (`npm run build`)
✅ Full Netlify build process runs without errors
✅ Netlify configuration file (netlify.toml) is configured properly
✅ Netlify function (api.ts/api.mjs) builds successfully
✅ All required packages are installed (serverless-http, esbuild, etc.)

## Required Packages

- `serverless-http`: Required for Netlify Functions to work
  - Install with: `npm install serverless-http --save`
  - This package allows Express to work with Netlify Functions

## Required Environment Variables

- `DATABASE_URL`: Your PostgreSQL connection string
  - Format: `postgres://username:password@hostname:port/database`
  - You'll need to create a PostgreSQL database with Neon, Supabase, or another provider

## Deployment Steps

1. Push your code to a Git repository (GitHub, GitLab, or Bitbucket)
2. Log in to your Netlify account
3. Create a new site from Git
4. Connect to your Git repository
5. Configure build settings:
   - All settings should be automatically loaded from netlify.toml
6. Add environment variables:
   - `DATABASE_URL`: Your PostgreSQL connection string
7. Deploy the site

## Post-Deployment Verification

1. Wait for the build to complete
2. Check the deployment logs for any errors
3. Visit your site URL (provided by Netlify)
4. Test game functionality:
   - Character creation
   - Cultivation
   - Saving and loading game state
5. Monitor Netlify function logs for any backend issues

## Potential Issues to Watch For

- Database connection problems
  - Check if your PostgreSQL connection string is correct
  - Verify that your database is accessible from Netlify's servers
- Build failures
  - Check if all dependencies are installed correctly
  - Look for syntax errors in your code
- API errors
  - Verify that the Netlify functions are working correctly
  - Check the function logs for details

## Useful Commands

- `netlify login` - Log in to your Netlify account via CLI
- `netlify init` - Initialize a new Netlify site
- `netlify env:set KEY VALUE` - Set environment variables
- `netlify deploy --prod` - Deploy to production

Remember to check the full deployment guide in NETLIFY_DEPLOYMENT.md for more detailed instructions.