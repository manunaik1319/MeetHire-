# Vercel Deployment Guide

## Quick Deploy

### Option 1: Deploy via Vercel CLI (Recommended)

1. **Install Vercel CLI**
   ```bash
   npm i -g vercel
   ```

2. **Navigate to your app directory**
   ```bash
   cd nextjs-app
   ```

3. **Deploy**
   ```bash
   vercel
   ```
   
   Follow the prompts:
   - Set up and deploy? **Y**
   - Which scope? Select your account
   - Link to existing project? **N** (first time)
   - What's your project's name? **nextjs-app** (or your preferred name)
   - In which directory is your code located? **./** 
   - Want to override settings? **N**

4. **Deploy to Production**
   ```bash
   vercel --prod
   ```

### Option 2: Deploy via Vercel Dashboard

1. **Go to [vercel.com](https://vercel.com)**
2. **Sign in** with GitHub, GitLab, or Bitbucket
3. **Click "Add New Project"**
4. **Import your Git repository**
5. **Configure Project:**
   - Framework Preset: **Next.js**
   - Root Directory: **nextjs-app**
   - Build Command: **npm run build** (auto-detected)
   - Output Directory: **out** (auto-detected)
6. **Add Environment Variables** (if needed):
   - Click "Environment Variables"
   - Add any required variables
7. **Click "Deploy"**

## Environment Variables

If your app uses environment variables, add them in Vercel:

### Via CLI:
```bash
vercel env add VARIABLE_NAME
```

### Via Dashboard:
1. Go to your project settings
2. Navigate to "Environment Variables"
3. Add your variables for Production, Preview, and Development

## Custom Domain Setup

1. **Go to your project in Vercel Dashboard**
2. **Navigate to Settings → Domains**
3. **Add your custom domain**
4. **Update your DNS records** as instructed by Vercel:
   - For root domain: Add A record pointing to Vercel's IP
   - For subdomain: Add CNAME record pointing to `cname.vercel-dns.com`

## Automatic Deployments

Once connected to Git:
- **Production**: Pushes to `main` branch auto-deploy to production
- **Preview**: Pushes to other branches create preview deployments
- **Pull Requests**: Each PR gets a unique preview URL

## Post-Deployment Checklist

- [ ] Verify deployment at your Vercel URL
- [ ] Test all pages and functionality
- [ ] Check environment variables are set correctly
- [ ] Set up custom domain (optional)
- [ ] Configure analytics (optional)
- [ ] Set up monitoring (optional)

## Useful Commands

```bash
# Deploy to preview
vercel

# Deploy to production
vercel --prod

# List deployments
vercel ls

# View deployment logs
vercel logs [deployment-url]

# Remove deployment
vercel rm [deployment-name]

# Link local project to Vercel project
vercel link
```

## Troubleshooting

### Build Fails
- Check build logs in Vercel dashboard
- Ensure all dependencies are in `package.json`
- Verify Node.js version compatibility

### Environment Variables Not Working
- Make sure variables are added for the correct environment (Production/Preview/Development)
- Redeploy after adding new variables

### 404 Errors
- Verify `output: 'export'` is set in `next.config.ts`
- Check that all routes are properly defined

## Performance Optimization

Vercel automatically provides:
- ✅ Global CDN
- ✅ Automatic HTTPS
- ✅ Edge caching
- ✅ Image optimization (if enabled)
- ✅ Compression

## Support

- [Vercel Documentation](https://vercel.com/docs)
- [Next.js on Vercel](https://vercel.com/docs/frameworks/nextjs)
- [Vercel Support](https://vercel.com/support)
