# Google Sheets Integration Setup Guide

## Step 1: Create Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet named "MeetHire Waitlist"
3. In the first row, add these headers:
   - A1: Timestamp
   - B1: Name
   - C1: Email
   - D1: Phone
   - E1: Role
   - F1: Organization
   - G1: City
   - H1: Message
   - I1: Updates

## Step 2: Create Google Apps Script

1. In your Google Sheet, click **Extensions** → **Apps Script**
2. Delete any existing code
3. Copy and paste this code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    // Add timestamp and form data
    sheet.appendRow([
      new Date(),
      data.name,
      data.email,
      data.phone || '',
      data.role,
      data.organization,
      data.city || '',
      data.message || '',
      data.updates ? 'Yes' : 'No'
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
  return ContentService.createTextOutput("Waitlist API is running");
}
```

4. Click **Save** (disk icon)
5. Name your project: "MeetHire Waitlist API"

## Step 3: Deploy as Web App

1. Click **Deploy** → **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Configure:
   - Description: "MeetHire Waitlist Form"
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Click **Deploy**
6. Click **Authorize access**
7. Choose your Google account
8. Click **Advanced** → **Go to [project name] (unsafe)**
9. Click **Allow**
10. **Copy the Web App URL** (looks like: https://script.google.com/macros/s/ABC.../exec)

## Step 4: Update Your Website

Replace `YOUR_GOOGLE_SCRIPT_URL` in `waitlist-script.js` with your copied URL.

## Step 5: Test

1. Submit a test form on your website
2. Check your Google Sheet - you should see the data appear!

## Troubleshooting

- **403 Error**: Make sure "Who has access" is set to "Anyone"
- **No data appearing**: Check the Apps Script execution logs (View → Executions)
- **CORS Error**: This is normal - the form will still work

## Security Note

This setup is suitable for waitlist forms. For production apps with sensitive data, consider using:
- Google Sheets API with OAuth
- Backend service (Node.js, Python)
- Form services like Formspree, Netlify Forms, or Tally
