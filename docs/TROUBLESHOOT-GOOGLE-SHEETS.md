# Troubleshooting Google Sheets - Not Saving Data

## Let's Fix This Step by Step

### Step 1: Check Your Apps Script Deployment

1. Go to https://script.google.com
2. Open your "MeetHire Waitlist API" project
3. Click **Deploy** → **Manage deployments**
4. Check these settings:
   - **Execute as:** Must be "Me (your email)"
   - **Who has access:** Must be "Anyone"
   
If these are wrong:
- Click **Edit** (pencil icon)
- Change settings
- Click **Deploy**
- **COPY THE NEW URL** (it will be different!)

### Step 2: Update the URL in Your Code

The URL you gave me was:
```
https://script.google.com/macros/s/AKfycbzsJBbCC27wT05hJyO5YlHQ9jOsvBU9_1L84qqDhdKeKuVEagiVzkQCqHU6VtvvtXZ1/exec
```

**Test if this URL works:**
1. Open this URL in your browser
2. You should see: "MeetHire Waitlist API is running"
3. If you see an error or login page, the deployment is wrong

### Step 3: Check Apps Script Code

Make sure your Apps Script has this EXACT code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    
    // Get data from form
    var data = e.parameter;
    
    // Add row to sheet
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
    
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'success' }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'error', 'error': error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  return ContentService.createTextOutput("MeetHire Waitlist API is running");
}
```

### Step 4: Check Sheet Headers

Your Google Sheet Row 1 must have these headers:

| A | B | C | D | E | F | G | H | I |
|---|---|---|---|---|---|---|---|---|
| Timestamp | Name | Email | Phone | Role | Organization | City | Message | Updates |

### Step 5: Test Manually

In Apps Script:
1. Click **Run** → Select `doGet`
2. Click **Run**
3. Should say "Execution completed"

### Step 6: Check Execution Log

1. In Apps Script, click **Executions** (left sidebar)
2. Look for recent executions when you submitted the form
3. If you see errors, tell me what they say

### Step 7: Alternative - Use Google Forms

If Apps Script is too complicated, we can use Google Forms instead:

1. Create a Google Form
2. Link it to a Google Sheet
3. Embed the form on your website

Would you like me to set this up instead?

## Common Issues:

**Issue:** URL shows login page
**Fix:** Redeploy with "Who has access: Anyone"

**Issue:** No executions showing up
**Fix:** The form isn't reaching the script - check the URL

**Issue:** Execution shows error
**Fix:** Check the error message in Executions log

## Need Help?

Tell me:
1. What happens when you open the Apps Script URL in browser?
2. Do you see any errors in browser console (F12)?
3. Are there any executions in the Apps Script Executions log?
