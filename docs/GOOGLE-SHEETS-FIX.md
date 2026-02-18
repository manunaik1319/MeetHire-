# Fix Google Sheets Integration - Step by Step

## Problem
The form is not submitting data to Google Sheets properly.

## Solution - Follow These Steps Exactly

### Step 1: Update Your Google Apps Script

1. Open your Google Sheet
2. Click **Extensions** → **Apps Script**
3. **DELETE ALL EXISTING CODE**
4. Copy and paste this EXACT code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    
    // Parse the incoming data
    var data;
    if (e.postData && e.postData.contents) {
      data = JSON.parse(e.postData.contents);
    } else if (e.parameter) {
      data = e.parameter;
    } else {
      throw new Error('No data received');
    }
    
    // Add timestamp and form data to sheet
    sheet.appendRow([
      new Date(),
      data.name || '',
      data.email || '',
      data.phone || '',
      data.role || '',
      data.organization || '',
      data.city || '',
      data.message || '',
      data.updates || 'No'
    ]);
    
    // Return success response
    return ContentService
      .createTextOutput(JSON.stringify({ 
        'result': 'success',
        'message': 'Data saved successfully'
      }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // Return error response
    return ContentService
      .createTextOutput(JSON.stringify({ 
        'result': 'error', 
        'message': error.toString() 
      }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  return ContentService.createTextOutput("MeetHire Waitlist API is running");
}
```

5. Click **Save** (disk icon)

### Step 2: Test the Script

1. In Apps Script, click **Run** → Select `doGet`
2. Click **Run** button
3. You should see "Execution completed" - this means it works!

### Step 3: Deploy the Web App

1. Click **Deploy** → **New deployment**
2. Click gear icon ⚙️ → Select **Web app**
3. Settings:
   - Description: "MeetHire Waitlist v2"
   - Execute as: **Me (your email)**
   - Who has access: **Anyone**
4. Click **Deploy**
5. Click **Authorize access**
6. Choose your Google account
7. Click **Advanced** → **Go to [project name] (unsafe)**
8. Click **Allow**
9. **COPY THE WEB APP URL**

### Step 4: Verify Your Sheet Headers

Make sure Row 1 has these EXACT headers:

| A | B | C | D | E | F | G | H | I |
|---|---|---|---|---|---|---|---|---|
| Timestamp | Name | Email | Phone | Role | Organization | City | Message | Updates |

### Step 5: Test with Simple HTML

1. Open `test-google-sheet.html` in your browser
2. Fill in name and email
3. Click Submit
4. Check your Google Sheet - data should appear!

### Step 6: If Still Not Working

**Check these:**

1. **Apps Script Deployment:**
   - Go to Apps Script → Deploy → Manage deployments
   - Make sure "Who has access" = **Anyone**
   - If not, click Edit → Change to Anyone → Deploy

2. **Check Execution Log:**
   - In Apps Script, click **Executions** (left sidebar)
   - Look for errors in recent executions

3. **Test the URL directly:**
   - Open your Web App URL in browser
   - You should see: "MeetHire Waitlist API is running"
   - If you see an error, the deployment is wrong

4. **Browser Console:**
   - Open waitlist page
   - Press F12 → Console tab
   - Submit form
   - Look for errors

### Common Issues:

**Issue:** "Authorization required"
**Fix:** Redeploy with "Execute as: Me" and "Who has access: Anyone"

**Issue:** "Script function not found"
**Fix:** Make sure you saved the script before deploying

**Issue:** Data not appearing in sheet
**Fix:** Check that column headers match exactly (case-sensitive)

**Issue:** Form refreshes/reloads
**Fix:** Already fixed in the new waitlist-script.js

## After Fixing

Run this command to deploy:
```bash
vercel --prod
```

Your form should now work perfectly!
