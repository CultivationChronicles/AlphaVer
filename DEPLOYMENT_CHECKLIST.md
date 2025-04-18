# Wuxia Cultivation Game Deployment Checklist

Use this checklist to ensure your game deploys successfully to Vercel.

## Before Deploying

- [ ] Update all dependencies to their latest versions
- [ ] Make sure all environment variables are documented in `.env.example`
- [ ] Test the application locally with `npm run dev`
- [ ] Check that all client-side routes work correctly
- [ ] Ensure database migrations are working with `npm run db:push`
- [ ] Commit all changes to your git repository

## Setting Up Vercel

- [ ] Sign up for a Vercel account at [vercel.com](https://vercel.com)
- [ ] Install the Vercel CLI: `npm install -g vercel`
- [ ] Log in to Vercel CLI: `vercel login`

## Database Setup

- [ ] Set up a PostgreSQL database (Neon, Supabase, or Railway recommended)
- [ ] Get your database connection string in this format:
      `postgres://username:password@hostname:port/database`
- [ ] Test connecting to your database from your local machine

## Deployment Process

- [ ] Run `vercel` from your project directory
- [ ] Follow the CLI prompts to link to your Vercel project
- [ ] Set the following environment variables when prompted:
  - [ ] `DATABASE_URL`: Your PostgreSQL connection string
  - [ ] `SESSION_SECRET`: A random string for session encryption
  - [ ] `NODE_ENV`: Set to `production`
- [ ] Complete the initial deployment

## Post-Deployment

- [ ] Run database migrations: `DATABASE_URL=your_production_db_url npx drizzle-kit push`
- [ ] Visit your deployed application at the Vercel URL
- [ ] Test user registration and login
- [ ] Verify that game state saves correctly
- [ ] Test all game mechanics (cultivation, combat, map exploration)
- [ ] Set up a custom domain (optional)

## Troubleshooting Common Issues

### Database Connection Problems

```
Error: Could not connect to database
```

**Solution:**
- Check your `DATABASE_URL` environment variable in Vercel
- Ensure your database allows connections from Vercel's IP addresses
- Check if your database requires SSL connections

### Static Assets Not Loading

```
404 errors for CSS, JavaScript, or image files
```

**Solution:**
- Check the routes in your `vercel.json` file
- Ensure the build process generated all expected files in the output directory
- Look for path issues in your HTML and JavaScript files

### API Routes Not Working

```
404 or 500 errors when calling API endpoints
```

**Solution:**
- Verify your API routes are correctly defined in `vercel.json`
- Check server logs in the Vercel dashboard
- Test the API endpoints locally before deploying

### Build Errors

```
Error: Build failed with exit code X
```

**Solution:**
- Check the build logs in Vercel for specific error messages
- Ensure all dependencies are correctly listed in package.json
- Test your build process locally: `npm run build`