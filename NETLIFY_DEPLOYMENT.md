# Deploying to Netlify

This guide will help you deploy the Wuxia Cultivation Game to Netlify.

## Prerequisites

1. A Netlify account (free tier is sufficient)
2. A PostgreSQL database (we recommend [Neon](https://neon.tech) or [Supabase](https://supabase.com) for serverless PostgreSQL)

## Setup Steps

### 1. Set Up Your PostgreSQL Database

1. Create a database in Neon, Supabase, or your preferred PostgreSQL provider
2. Get your PostgreSQL connection string (should look something like `postgres://user:password@host/database`)

### 2. Deploy to Netlify

#### Option 1: Deploy with Netlify CLI

1. Install the Netlify CLI: `npm install -g netlify-cli`
2. Login to Netlify: `netlify login`
3. Link your project: `netlify init`
4. Set up your environment variables: `netlify env:set DATABASE_URL "your_postgres_connection_string"`
5. Deploy your site: `netlify deploy --prod`

#### Option 2: Deploy via Netlify UI

1. Push your code to a Git repository (GitHub, GitLab, or Bitbucket)
2. Log in to your Netlify account
3. Click "New site from Git"
4. Connect to your Git provider and select your repository
5. Configure build settings:
   - Build command will be automatically set from the netlify.toml file
   - Publish directory will be automatically set from the netlify.toml file
6. Click "Show advanced" and add your environment variables:
   - Key: `DATABASE_URL`
   - Value: Your PostgreSQL connection string
7. Click "Deploy site"

### 3. Verify Your Deployment

1. Once deployment is complete, Netlify will provide you with a URL (e.g., `https://your-site-name.netlify.app`)
2. Visit your site to ensure everything is working correctly
3. Test the game functionality to verify the database connection is working

## Required Packages

Before deploying, make sure these packages are installed in your project:
```
npm install serverless-http --save
```

The `serverless-http` package is required for Netlify Functions to work correctly. Without it, you'll get a "Could not resolve serverless-http" error during deployment.

## Troubleshooting

### Missing Dependencies Errors

If you see errors like "Could not resolve serverless-http":
1. Add the missing package to your dependencies:
   ```
   npm install serverless-http --save
   ```
2. Commit the updated package.json and redeploy

### Database Connection Issues

If you encounter database connection issues:

1. Verify your `DATABASE_URL` is correctly set in Netlify's environment variables
2. Ensure your database is accessible from Netlify's servers (check firewall settings)
3. Check Netlify's Function logs for detailed error messages

### Build Failures

If your build fails:

1. Check the build logs in the Netlify dashboard
2. Ensure all dependencies are correctly installed
3. Verify your PostgreSQL connection string is correct

## Custom Domain Setup (Optional)

To use a custom domain:

1. Go to "Site settings" > "Domain management" in your Netlify dashboard
2. Click "Add custom domain"
3. Follow the instructions to configure your DNS settings

## Monitoring and Maintenance

- Monitor your application's performance in the Netlify dashboard
- Check your database usage regularly to stay within free tier limits
- Update your application as needed by pushing changes to your Git repository or redeploying

## Need Help?

If you encounter any issues during deployment, consult the [Netlify documentation](https://docs.netlify.com/) or reach out to Netlify support.