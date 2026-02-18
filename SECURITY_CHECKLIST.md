# 🔒 PRODUCTION SECURITY CHECKLIST

## ⚠️ CRITICAL - DO BEFORE DEPLOYMENT

- [ ] **Rotate Exposed Vercel Token**
  - Go to: https://vercel.com/account/tokens
  - Revoke token: `eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Im1yay00MzAyZWMxYjY3MGY0OGE5OGFkNjFkYWRlNGEyM2JlNyJ9...`
  - Generate new token
  - Update in Vercel environment variables

- [ ] **Set Environment Variables in Vercel**
  ```
  NEXT_PUBLIC_FORM_ENDPOINT=your_google_apps_script_url
  ```

- [ ] **Verify .gitignore**
  - Ensure `.env*.local` is listed
  - Ensure `.vercel` is listed
  - Never commit secrets

## 🚀 DEPLOYMENT STEPS

- [ ] **Install Dependencies**
  ```bash
  cd nextjs-app
  npm install
  ```

- [ ] **Run Security Audit**
  ```bash
  npm audit
  npm audit fix
  ```

- [ ] **Build Application**
  ```bash
  npm run build
  ```

- [ ] **Test Locally**
  ```bash
  npm run start
  # Visit http://localhost:3000
  ```

- [ ] **Deploy to Production**
  ```bash
  vercel --prod
  ```

## ✅ POST-DEPLOYMENT VERIFICATION

- [ ] **Test HTTPS Redirect**
  - Visit: http://meethire.in
  - Should redirect to: https://meethire.in

- [ ] **Verify Security Headers**
  - Visit: https://securityheaders.com/?q=meethire.in
  - Target Score: A or A+
  - Check for:
    - ✅ Strict-Transport-Security
    - ✅ Content-Security-Policy
    - ✅ X-Frame-Options
    - ✅ X-Content-Type-Options
    - ✅ Referrer-Policy

- [ ] **SSL/TLS Test**
  - Visit: https://www.ssllabs.com/ssltest/analyze.html?d=meethire.in
  - Target Score: A or A+
  - Verify TLS 1.2/1.3 only

- [ ] **Test Rate Limiting**
  - Submit waitlist form 4+ times rapidly
  - Should show error: "Too many submission attempts"

- [ ] **Test CSRF Protection**
  - Open browser console
  - Try submitting form without page load
  - Should fail validation

- [ ] **Test Form Validation**
  - Try invalid email: `test@test`
  - Try XSS: `<script>alert('xss')</script>`
  - Try SQL injection: `' OR '1'='1`
  - All should be sanitized/rejected

- [ ] **Check CSP Violations**
  - Open browser console (F12)
  - Navigate through site
  - Look for CSP violation errors
  - Fix any violations found

- [ ] **Test on Multiple Browsers**
  - [ ] Chrome/Edge
  - [ ] Firefox
  - [ ] Safari
  - [ ] Mobile browsers

## 🔐 SECURITY ENHANCEMENTS

- [ ] **Submit to HSTS Preload**
  - Visit: https://hstspreload.org
  - Enter domain: meethire.in
  - Submit for preload list inclusion

- [ ] **Set Up Security Monitoring**
  - Configure Vercel Analytics
  - Set up error tracking (e.g., Sentry)
  - Monitor rate limit violations

- [ ] **Configure Alerts**
  - Set up alerts for:
    - High error rates
    - Rate limit violations
    - CSRF failures
    - Unusual traffic patterns

- [ ] **Document Incident Response**
  - Create incident response plan
  - Define escalation procedures
  - Set up emergency contacts

## 📊 ONGOING MAINTENANCE

### Weekly
- [ ] Review error logs
- [ ] Check rate limiting effectiveness
- [ ] Monitor form submissions for spam

### Monthly
- [ ] Run `npm audit` and update dependencies
- [ ] Review security headers (securityheaders.com)
- [ ] Check SSL certificate expiry
- [ ] Review CSP violations

### Quarterly
- [ ] Full security scan with OWASP ZAP
- [ ] Review and update security policies
- [ ] Audit third-party dependencies
- [ ] Test disaster recovery procedures

### Annually
- [ ] Complete security audit
- [ ] Penetration testing
- [ ] Review and rotate all secrets
- [ ] Update security documentation

## 🛠️ TROUBLESHOOTING

### If Security Headers Not Working

1. **Check Vercel Deployment**
   ```bash
   curl -I https://meethire.in
   ```

2. **Verify middleware.ts is deployed**
   - Check Vercel deployment logs
   - Ensure middleware.ts is in nextjs-app folder

3. **Clear CDN Cache**
   - In Vercel dashboard: Deployments → ... → Redeploy

### If Rate Limiting Not Working

1. **Check middleware configuration**
   - Verify middleware.ts is active
   - Check rate limit thresholds

2. **Test with different IPs**
   - Use VPN or mobile network
   - Rate limiting is per-IP

### If CSRF Failing

1. **Check sessionStorage**
   - Open browser console
   - Run: `sessionStorage.getItem('csrf_token')`
   - Should return a token

2. **Verify token generation**
   - Check WaitlistForm.tsx useEffect
   - Ensure crypto.getRandomValues is supported

## 📞 EMERGENCY CONTACTS

### Security Incident
1. Take affected systems offline
2. Rotate all secrets immediately
3. Review logs for attack vectors
4. Document incident timeline
5. Notify affected users if data compromised

### Vercel Support
- Dashboard: https://vercel.com/support
- Email: support@vercel.com

### Security Resources
- OWASP: https://owasp.org
- CVE Database: https://cve.mitre.org
- Security Headers: https://securityheaders.com

## ✅ SIGN-OFF

- [ ] All critical items completed
- [ ] All post-deployment checks passed
- [ ] Security monitoring configured
- [ ] Team trained on security procedures
- [ ] Incident response plan documented

**Deployment Date:** _______________  
**Deployed By:** _______________  
**Verified By:** _______________  

---

**Status:** Ready for Production ✅
