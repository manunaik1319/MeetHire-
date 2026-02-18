# Google Sheets & Apps Script Setup Guide

## Step 1: Create Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it "MeetHire Waitlist"
4. Add these column headers in Row 1:
   - A1: `Timestamp`
   - B1: `Name`
   - C1: `Email`
   - D1: `Phone`
   - E1: `Role`
   - F1: `Organization`
   - G1: `City`
   - H1: `Message`
   - I1: `Updates`

## Step 2: Setup Apps Script

1. In your Google Sheet, go to **Extensions > Apps Script**
2. Delete any existing code
3. Copy the entire code from `google-apps-script.js` file
4. Paste it into the Apps Script editor
5. Click **Save** (💾 icon)
6. Name your project "MeetHire Waitlist Handler"

## Step 3: Deploy as Web App

1. Click **Deploy > New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Configure:
   - **Description**: MeetHire Waitlist API
   - **Execute as**: Me (your email)
   - **Who has access**: Anyone
5. Click **Deploy**
6. **Authorize** the app (you'll need to grant permissions)
7. Copy the **Web app URL** (it should look like: `https://script.google.com/macros/s/...../exec`)

## Step 4: Update Your Form

1. Open `nextjs-app/components/waitlist/WaitlistForm.tsx`
2. Find this line:
   ```typescript
   const scriptURL = 'https://script.google.com/macros/s/AKfycbzHZe98JoNkYzvy8e_mG-cVRSyblBuzI5KZB0q7BI0DB0wE91IOiHnyP7CgjC7f7-7E9Q/exec';
   ```
3. Replace it with your new Web app URL

## Step 5: Test the Integration

### Test 1: Test Data Saving
1. In Apps Script editor, select `testAppendRow` function from dropdown
2. Click **Run** (▶️)
3. Check your Google Sheet - you should see a test row added

### Test 2: Test Email Sending
1. In Apps Script, find the `testEmail` function
2. Change `'your-test-email@gmail.com'` to your actual email
3. Select `testEmail` from dropdown
4. Click **Run** (▶️)
5. Check your email inbox (and spam folder)

### Test 3: Test Form Submission
1. Go to your waitlist page
2. Fill out the form with test data
3. Submit the form
4. Check:
   - Google Sheet should have new row
   - Email should be received
   - Success message should appear

## Troubleshooting

### Email Not Sending?
- Make sure you authorized the script with Gmail permissions
- Check if Gmail is enabled in your Google account
- Try running `testEmail()` function manually
- Check Apps Script logs: **View > Logs**

### Data Not Saving?
- Make sure column headers match exactly
- Check Apps Script logs for errors
- Verify the sheet is the active sheet
- Run `testAppendRow()` to test

### Form Shows Error?
- Check browser console for errors (F12)
- Verify the Web app URL is correct
- Make sure deployment is set to "Anyone" access
- Check if you need to redeploy after code changes

### CORS Errors?
- Make sure Web app is deployed with "Anyone" access
- The script must be deployed as Web app, not just saved
- Try redeploying with a new version

## Important Notes

1. **Redeploy After Changes**: If you modify the Apps Script code, you must create a new deployment or update the existing one
2. **Email Limits**: Google has daily email sending limits (100-1500 depending on account type)
3. **Duplicate Prevention**: The script checks for duplicate emails automatically
4. **Privacy**: Only you can access the Google Sheet data

## Email Configuration

The script sends emails from your Gmail account. To customize:

1. Edit the `sendThankYouEmail` function in Apps Script
2. Modify the HTML template as needed
3. Change the sender name in the `GmailApp.sendEmail` call
4. Save and redeploy

## Support

If you encounter issues:
1. Check Apps Script logs: **View > Logs** or **View > Executions**
2. Test individual functions using the test functions provided
3. Verify all permissions are granted
4. Check your Google Sheet for any manual errors

---

**Last Updated**: February 2026
