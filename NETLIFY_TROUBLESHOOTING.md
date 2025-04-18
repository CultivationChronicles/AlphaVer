# Netlify Deployment Troubleshooting

## Common Deployment Errors

### "Could not resolve serverless-http" Error

If you see this error in your Netlify deployment logs:
```
✘ [ERROR] Could not resolve "serverless-http"
     netlify/functions/api.mjs:3:23:
       3 │ import serverless from "serverless-http";
         ╵                        ~~~~~~~~~~~~~~~~~
```

**Solution 1 - Update netlify.toml:**
1. Modify your netlify.toml file to include the serverless-http package in the build command:

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

2. Commit the changes to your Git repository:
   ```
   git add netlify.toml
   git commit -m "Update netlify.toml to handle serverless-http dependency"
   git push
   ```

**Solution 2 - Add to package.json:**
1. Make sure serverless-http is in your package.json dependencies:
   ```
   npm install serverless-http --save
   ```

2. Commit the changes to your Git repository:
   ```
   git add package.json package-lock.json
   git commit -m "Add serverless-http dependency"
   git push
   ```

**Solution 3 - Change Function Bundle Settings:**
1. In the Netlify Dashboard, go to Site Settings > Functions
2. Under "Function bundling", select "Netlify CLI bundler" instead of "esbuild"
3. Redeploy your site

3. Redeploy on Netlify or let your Git integration trigger a new build

### DATABASE_URL Not Found Error

If you see this message in your Netlify build logs:
```
⚠️ IMPORTANT: Missing environment variables:
  - DATABASE_URL: Required for the application to function properly
```

**Solution:**
1. Go to your Netlify site dashboard
2. Navigate to Site settings > Build & deploy > Environment
3. Add a new environment variable:
   - Key: `DATABASE_URL`
   - Value: Your PostgreSQL connection string (e.g., `postgres://username:password@hostname:port/database`)
4. Click "Save"
5. Trigger a new deployment

## General Netlify Deployment Tips

1. **Check build logs carefully**: Netlify provides detailed build logs that can help you identify what's going wrong.

2. **Test builds locally**: You can use the Netlify CLI to test your build process locally before deploying.
   ```
   npm install -g netlify-cli
   netlify build
   ```

3. **Use the Netlify dev environment**: The Netlify CLI can create a local development environment that closely matches production.
   ```
   netlify dev
   ```

4. **Check your netlify.toml file**: Make sure your configuration is correct, especially the build command and publish directory.

5. **Monitor function logs**: After deployment, check the Functions tab in your Netlify dashboard to see logs from your serverless functions.

6. **Verify your database connection**: Make sure your database is accessible from Netlify's servers and your connection string is correct.

## Getting Additional Help

If you continue to experience issues, you can:

1. Check the [Netlify documentation](https://docs.netlify.com/)
2. Search the [Netlify Community forum](https://answers.netlify.com/)
3. Contact Netlify support through your dashboard