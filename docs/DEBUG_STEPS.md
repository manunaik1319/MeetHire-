# Debug Steps - Form Not Saving

## CRITICAL: Follow These Steps in Order

### Step 1: Update Apps Script with Debugging
1. Open your Google Sheet
2. Go to **Extensions > Apps Script**
3. **Delete ALL existing code**
4. Copy the ENTIRE updated code from `nextjs-app/google-apps-script.js`
5. Paste it into Apps Script
6. Click **Save** (💾)

### Step 2: Test Data Saving (Without Form)
1. In Apps Script, select `testAppendRow` from the dropdown
2. Click **Run** (▶️)
3. Grant permissions if asked
4. Check your Google Sheet - you should see a test row
5. If this works, the sheet connection is fine

### Step 3: Check Deployment
1. In Apps Script, click **Deploy > Manage deployments**
2. Verify settings:
   - **Execute as**: Me (your-email@gmail.com)
   - **Who has access**: **Anyone** ⚠️ MUST BE "Anyone"
3. If it says "Only myself", click **Edit** and change to "Anyone"
4. Click **Update** or **Deploy**
5. Copy the Web App URL

### Step 4: Verify URL in Form
1. Open `nextjs-app/components/waitlist/WaitlistForm.tsx`
2. Find line with `scriptURL`
3. Make sure it matches your deployment URL:
   ```typescript
   const scriptURL = 'https://script.google.com/macros/s/AKfycbyHwcDf79aw0xXb7PUNGoEY5g6nQIGDISN9LfBYgcsxlLTK93ZN1YeRhnnUQ1-kqyufsw/exec';
   ```

### Step 5: Test the Form
1. Open your browser's Developer Tools (F12)
2. Go to the **Console** tab
3. Go to your waitlist page
4. Fill out the form
5. Click Submit
6. Watch the Console for errors

### Step 6: Check Apps Script Logs
1. In Apps Script, click **View > Executions**
2. Look for recent executions
3. Click on the latest one
4. Check the logs - you should see:
   - "=== DOPOST CALLED ==="
   - "Sheet accessed: [sheet name]"
   - "Parsed data: {...}"
   - "✅ Row added successfully"

## Common Issues & Fixes

### Issue 1: "Redirect" or CORS Error
**Problem**: Deployment not set to "Anyone"
**Fix**: 
1. Deploy > Manage deployments
2. Edit deployment
3. Change "Who has access" to **Anyone**
4. Deploy

### Issue 2: Nothing Happens
**Problem**: Wrong URL or deployment not active
**Fix**:
1. Create a NEW deployment
2. Deploy > New deployment
3. Select "Web app"
4. Execute as: Me
5. Who has access: Anyone
6. Deploy
7. Copy NEW URL
8. Update form with new URL

### Issue 3: "Authorization Required"
**Problem**: Script needs permissions
**Fix**:
1. Run `testAppendRow` function
2. Grant all permissions
3. Redeploy

### Issue 4: Form Submits but No Data
**Problem**: Data format mismatch
**Fix**: Check browser console for the actual error

## Quick Test URL

Test if your script is running:
1. Open this URL in browser:
   ```
   https://script.google.com/macros/s/AKfycbyHwcDf79aw0xXb7PUNGoEY5g6nQIGDISN9LfBYgcsxlLTK93ZN1YeRhnnUQ1-kqyufsw/exec
   ```
2. You should see: "MeetHire Waitlist API is running ✅"
3. If you see an error, the deployment is wrong

## Manual Test with URL Parameters

Test the script directly:
```
https://script.google.com/macros/s/AKfycbyHwcDf79aw0xXb7PUNGoEY5g6nQIGDISN9LfBYgcsxlLTK93ZN1YeRhnnUQ1-kqyufsw/exec?name=Test&email=test@test.com&role=student&organization=TestOrg
```

This should add a row to your sheet.

## What to Share if Still Not Working

1. Screenshot of Apps Script **Executions** page
2. Screenshot of browser **Console** errors
3. Screenshot of **Deploy settings** (showing "Anyone" access)
4. Tell me: Does the test URL show "API is running ✅"?

---

**The most common issue is deployment not set to "Anyone" access!**
