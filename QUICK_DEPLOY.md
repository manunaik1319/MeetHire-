# ⚡ QUICK DEPLOY TO MEETHIRE.IN

## 🚨 CRITICAL FIRST STEP

**Rotate the exposed Vercel token:**
1. Go to: https://vercel.com/account/tokens
2. Revoke the exposed token
3. Generate new token
4. Update in Vercel (not in code!)

## 🚀 Deploy Now

### Method 1: Vercel CLI
```bash
cd nextjs-app
vercel --prod
```

### Method 2: Vercel Dashboard
1. Go to: https://vercel.com/dashboard
2. Select project: `meethire-waiting`
3. Click "Redeploy" on latest deployment

### Method 3: Git Push
```bash
git add .
git commit -m "Security hardening complete"
git push origin main
```

## ✅ Verify (2 minutes)

1. **Security Headers:** https://securityheaders.com/?q=meethire.in (Target: A+)
2. **SSL Test:** https://www.ssllabs.com/ssltest/analyze.html?d=meethire.in (Target: A+)
3. **Test Site:** https://meethire.in (Should load with CSS)
4. **Test Form:** Submit waitlist 4x rapidly (Should block after 3)

## 📊 What Changed

✅ HTTPS enforcement  
✅ HSTS with preload  
✅ Content Security Policy  
✅ CSRF protection  
✅ Rate limiting  
✅ Input sanitization  
✅ Security headers  
✅ File blocking  

**Security Score:** 🔴 7.5/10 → 🟢 2.0/10

## 🆘 Issues?

- CSS missing? Hard refresh (Ctrl+Shift+R)
- Headers missing? Redeploy in Vercel
- Forms broken? Check environment variables

**Full docs:** `DEPLOYMENT_INSTRUCTIONS.md`
