# CRITICAL: Fix Deployment Issue

## The Problem
Your error "Event object is undefined" means the deployment is NOT configured correctly as a Web App.

## SOLUTION: Complete Redeployment

### Step 1: Delete Old Deployments
1. Open your Google Sheet
2. Go to **Extensions > Apps Script**
3. Click **Deploy > Manage deployments**
4. For EACH deployment listed:
   - Click the **Archive** button (trash icon)
5. Close the deployments window

### Step 2: Update the Script
1. In Apps Script editor, **SELECT ALL** (Ctrl+A / Cmd+A)
2. **DELETE** everything
3. Open `nextjs-app/google-apps-script.js` in your code editor
4. **COPY ALL** the code
5. **PASTE** into Apps Script editor
6. Click **Save** (💾 icon)
7. Name it "MeetHire Waitlist" if prompted

### Step 3: Create Fresh Deployment
1. Click **Deploy** button (top right)
2. Select **New deployment**
3. Click the **gear/settings icon** ⚙️ next to "Select type"
4. Choose **Web app**
5. Fill in these settings EXACTLY:
   ```
   Description: MeetHire Waitlist v1
   Execute as: Me (your-email@gmail.com)
   Who has access: Anyone
   ```
6. Click **Deploy**

### Step 4: Authorize the App
1. You'll see "Authorization required"
2. Click **Authorize access**
3. Choose your Google account
4. You may see "Google hasn't verified this app"
   - Click **Advanced**
   - Click **Go to [Project Name] (unsafe)**
5. Click **Allow** to grant permissions

### Step 5: Copy the Web App URL
1. After authorization, you'll see "Deployment successfully created"
2. **COPY** the Web App URL (it looks like):
   ```
   https://script.google.com/macros/s/AKfycby.../exec
   ```
3. Click **Done**

### Step 6: Update Your Form
1. Open `nextjs-app/components/waitlist/WaitlistForm.tsx`
2. Find this line (around line 60):
   ```typescript
   const scriptURL = 'https://script.google.com/macros/s/...';
   ```
3. Replace with your NEW URL from Step 5
4. Save the file

### Step 7: Test the Deployment
1. Open your NEW Web App URL in a browser
2. You should see: **"MeetHire Waitlist API is running ✅"**
3. If you see an error or login page, the deployment is wrong

### Step 8: Test with Manual Data
Test the script directly by adding parameters to the URL:
```
YOUR_WEB_APP_URL?name=TestUser&email=test@example.com&role=student&organization=TestOrg
```

Replace `YOUR_WEB_APP_URL` with your actual URL. This should add a row to your sheet.

### Step 9: Test the Form
1. Make sure your Next.js app is running
2. Go to the waitlist page
3. Fill out the form
4. Submit
5. Check your Google Sheet for the new entry

### Step 10: Check Logs
1. In Apps Script: **View > Executions**
2. Click on the latest execution
3. You should see:
   - "=== DOPOST CALLED ==="
   - "Sheet accessed: Sheet1"
   - "Parsed data: {...}"
   - "✅ Row added successfully"

## Common Mistakes

### ❌ Wrong: "Who has access" = "Only myself"
This will cause the event object to be undefined.
**✅ Correct: "Anyone"**

### ❌ Wrong: Not deploying as "Web app"
If you just save the script without deploying, it won't work.
**✅ Correct: Deploy > New deployment > Web app**

### ❌ Wrong: Not authorizing
If you skip authorization, the script can't access Gmail or Sheets.
**✅ Correct: Complete the authorization flow**

### ❌ Wrong: Using old deployment URL
After creating a new deployment, you must use the NEW URL.
**✅ Correct: Copy the new URL and update your form**

## Verification Checklist

Before testing the form, verify:

- [ ] Old deployments archived/deleted
- [ ] New deployment created as "Web app"
- [ ] "Who has access" is set to **"Anyone"**
- [ ] Authorization completed (granted all permissions)
- [ ] Web App URL opens and shows "API is running ✅"
- [ ] Form has the correct NEW URL
- [ ] Manual URL test adds a row to sheet

## Still Getting "Event object is undefined"?

This means one of these is wrong:
1. Deployment is not set to "Anyone" access
2. Deployment is not a "Web app" type
3. You're using an old/archived deployment URL
4. The script wasn't saved before deploying

**Solution**: Delete ALL deployments and start fresh from Step 1.

## Need Help?

Share:
1. Screenshot of your deployment settings (showing "Anyone" access)
2. What happens when you open the Web App URL in browser
3. Screenshot of Apps Script Executions page

---

**The #1 cause of this error is "Who has access" not set to "Anyone"!**
