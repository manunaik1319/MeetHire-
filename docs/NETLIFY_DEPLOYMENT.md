# Deploy to Netlify - Quick Guide

## Option 1: Deploy via Netlify CLI (Fastest)

### 1. Install Netlify CLI
```bash
npm install -g netlify-cli
```

### 2. Login to Netlify
```bash
netlify login
```

### 3. Deploy from the nextjs-app directory
```bash
cd nextjs-app
netlify deploy --prod
```

Follow the prompts:
- Create & configure a new site? **Yes**
- Team: Select your team
- Site name: Choose a unique name (or leave blank for random)
- Publish directory: **.next**

---

## Option 2: Deploy via Netlify Dashboard (Recommended for beginners)

### 1. Push your code to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

### 2. Connect to Netlify
1. Go to [https://app.netlify.com](https://app.netlify.com)
2. Click **"Add new site"** → **"Import an existing project"**
3. Choose **GitHub** and authorize Netlify
4. Select your repository

### 3. Configure Build Settings
Netlify should auto-detect Next.js, but verify:
- **Base directory**: `nextjs-app`
- **Build command**: `npm run build`
- **Publish directory**: `.next`
- **Node version**: 20

**Important**: The `netlify.toml` file is already configured in the `nextjs-app` directory with the correct settings and the `@netlify/plugin-nextjs` plugin.

### 4. Add Environment Variables (if needed)
If you have any environment variables (like API keys), add them in:
- Site settings → Environment variables

Common variables for your app:
- `NEXT_PUBLIC_GOOGLE_SHEETS_URL` (if using Google Sheets)
- Any other API keys or secrets

### 5. Deploy
Click **"Deploy site"** and wait for the build to complete (usually 2-3 minutes)

---

## Option 3: Drag & Drop (Quick Test)

### 1. Build locally
```bash
cd nextjs-app
npm install
npm run build
```

### 2. Deploy
1. Go to [https://app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag and drop the `.next` folder

**Note**: This method doesn't support continuous deployment.

---

## Post-Deployment Checklist

### ✅ Verify Deployment
- [ ] Site loads correctly
- [ ] All pages are accessible
- [ ] Forms work (test waitlist submission)
- [ ] Images load properly
- [ ] No console errors

### ✅ Configure Custom Domain (Optional)
1. Go to Site settings → Domain management
2. Add your custom domain
3. Update DNS records as instructed

### ✅ Enable HTTPS
- Netlify automatically provisions SSL certificates
- Force HTTPS: Site settings → Domain management → HTTPS → Force HTTPS

### ✅ Set up Redirects
Your `netlify.toml` already includes redirect rules for:
- SEO-friendly URLs
- Security headers
- Cache optimization

### ✅ Monitor Performance
- Check Netlify Analytics (if enabled)
- Test with Google PageSpeed Insights
- Verify SEO with Google Search Console

---

## Troubleshooting

### Build fails?
- Check Node version (should be 20)
- Verify all dependencies are in `package.json`
- Check build logs in Netlify dashboard

### Environment variables not working?
- Ensure they start with `NEXT_PUBLIC_` for client-side access
- Redeploy after adding environment variables

### 404 errors on routes?
- Verify `netlify.toml` is in the root of `nextjs-app`
- Check that Next.js plugin is installed

### Need help?
- Netlify Docs: https://docs.netlify.com/frameworks/next-js/overview/
- Netlify Support: https://answers.netlify.com/

---

## Quick Commands Reference

```bash
# Install dependencies
npm install

# Build for production
npm run build

# Test production build locally
npm start

# Deploy to Netlify
netlify deploy --prod

# Check deployment status
netlify status

# Open site in browser
netlify open:site
```

---

## Your Site is Live! 🎉

Once deployed, your site will be available at:
- `https://YOUR-SITE-NAME.netlify.app`
- Or your custom domain if configured

Share your waitlist and start collecting signups!
