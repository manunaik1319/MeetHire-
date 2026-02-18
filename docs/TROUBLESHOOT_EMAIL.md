# Email Not Sending Automatically - Troubleshooting Guide

## Quick Diagnosis Steps

### Step 1: Check Apps Script Logs
1. Open your Google Sheet
2. Go to **Extensions > Apps Script**
3. Click **View > Executions** (or **View > Logs**)
4. Look for recent executions when you submitted the form
5. Check if there are any errors related to `sendThankYouEmail`

### Step 2: Verify Gmail Permissions
The most common issue is missing Gmail permissions.

1. In Apps Script editor, click **Run** > Select `testEmail` function
2. Change the test email to your actual email first:
   ```javascript
   var testEmail = 'your-actual-email@gmail.com'; // Change this!
   ```
3. Click **Run** (▶️ button)
4. You should see a permission dialog - **Grant all permissions**
5. If you see "This app isn't verified", click **Advanced** > **Go to [Project Name] (unsafe)**
6. Grant Gmail permissions
7. Check if you receive the test email

### Step 3: Check Deployment Settings
1. In Apps Script, click **Deploy > Manage deployments**
2. Verify:
   - **Execute as**: Me (your-email@gmail.com)
   - **Who has access**: Anyone
3. If settings are wrong, create a new deployment with correct settings

### Step 4: Test Email Function Manually

Run this in Apps Script to test email sending:

```javascript
function testEmail() {
    var testEmail = 'YOUR_EMAIL@gmail.com'; // ⚠️ CHANGE THIS
    Logger.log('Testing email to: ' + testEmail);

    try {
        sendThankYouEmail(testEmail, 'Test User');
        Logger.log('✅ Test email sent successfully to ' + testEmail);
        return 'Email sent to ' + testEmail;
    } catch (error) {
        Logger.log('❌ ERROR: ' + error.toString());
        return 'Error: ' + error.toString();
    }
}
```

## Common Issues & Solutions

### Issue 1: "Exception: Service invoked too many times"
**Solution**: You've hit Gmail's daily sending limit
- Free Gmail: 100 emails/day
- Google Workspace: 1,500 emails/day
- Wait 24 hours or upgrade to Google Workspace

### Issue 2: "Exception: Authorization is required"
**Solution**: Grant Gmail permissions
1. Run `testEmail()` function
2. Click **Review Permissions**
3. Choose your Google account
4. Click **Advanced** > **Go to [Project Name]**
5. Click **Allow**

### Issue 3: Email goes to spam
**Solution**: 
- Check your spam folder
- Add meethire.in@gmail.com to contacts
- The "from" email must match your Google account

### Issue 4: "TypeError: Cannot read property 'postData'"
**Solution**: Form data format issue
- The current form sends URL-encoded data
- The script expects this format
- This should work correctly

### Issue 5: Form submits but no email
**Solution**: Email error is caught silently
1. Check Apps Script logs for errors
2. The script saves data even if email fails
3. Look for "Error sending email:" in logs

## Enhanced Debugging Script

Replace your `sendThankYouEmail` function with this version that logs more details:

```javascript
function sendThankYouEmail(email, name) {
    Logger.log('=== EMAIL FUNCTION CALLED ===');
    Logger.log('Recipient: ' + email);
    Logger.log('Name: ' + name);
    
    try {
        var subject = "Thank you for joining MeetHire! 🙌";
        
        Logger.log('Preparing email content...');

        var htmlBody = `
      <!DOCTYPE html>
      <html>
      <head>
        <style>
          body { 
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; 
            line-height: 1.8; 
            color: #333; 
            margin: 0;
            padding: 0;
          }
          .container { 
            max-width: 600px; 
            margin: 0 auto; 
            padding: 20px; 
          }
          .header { 
            background: linear-gradient(135deg, #1C1C1C 0%, #2A2A2A 100%); 
            color: white; 
            padding: 40px; 
            text-align: center; 
            border-radius: 10px 10px 0 0; 
          }
          .header h1 { 
            margin: 0; 
            font-size: 32px; 
            font-weight: 700;
          }
          .content { 
            background: #ffffff; 
            padding: 40px; 
            border: 1px solid #e0e0e0; 
            border-top: none; 
            text-align: center; 
          }
          .content p { 
            margin: 20px 0; 
            font-size: 18px; 
            line-height: 1.8; 
          }
          .highlight {
            color: #FBCB6A;
            font-weight: 600;
          }
          .footer { 
            text-align: center; 
            padding: 20px; 
            color: #666; 
            font-size: 14px; 
          }
        </style>
      </head>
      <body>
        <div class="container">
          <div class="header">
            <h1>Welcome to MeetHire! 🙌</h1>
          </div>
          <div class="content">
            <p><strong>Thank you for joining the MeetHire waitlist! 🙌</strong></p>
            
            <p>We're excited to have you onboard.</p>
            
            <p>You'll be among the first to get early access as we launch.<br/>More updates coming soon 🚀</p>
            
            <p style="margin-top: 40px;">— <strong>Team MeetHire</strong></p>
          </div>
          <div class="footer">
            <p>© 2026 MeetHire. All rights reserved.</p>
            <p style="margin-top: 10px; font-size: 12px;">
              If you have any questions, reach out to us at 
              <a href="mailto:meethire.in@gmail.com">meethire.in@gmail.com</a>
            </p>
          </div>
        </div>
      </body>
      </html>
    `;

        var plainBody = `
Thank you for joining the MeetHire waitlist! 🙌

We're excited to have you onboard.

You'll be among the first to get early access as we launch.
More updates coming soon 🚀

— Team MeetHire

---
© 2026 MeetHire. All rights reserved.
Questions? Email us at meethire.in@gmail.com
    `;

        Logger.log('Attempting to send email via GmailApp...');
        
        // Send email
        GmailApp.sendEmail(email, subject, plainBody, {
            htmlBody: htmlBody,
            name: 'MeetHire Team'
        });

        Logger.log('✅ Email sent successfully to: ' + email);
        return true;

    } catch (error) {
        Logger.log('❌ ERROR sending email: ' + error.toString());
        Logger.log('Error stack: ' + error.stack);
        // Don't throw - we don't want email failure to break form submission
        return false;
    }
}
```

## Step-by-Step Fix Process

### Fix 1: Update Script with Better Logging
1. Copy the enhanced `sendThankYouEmail` function above
2. Replace it in your Apps Script
3. Save the script

### Fix 2: Test Email Manually
1. Update the test email in `testEmail()` function
2. Run `testEmail()` function
3. Grant permissions if asked
4. Check logs: **View > Executions**
5. Verify email received

### Fix 3: Redeploy the Script
1. Click **Deploy > Manage deployments**
2. Click **Edit** (pencil icon) on your deployment
3. Change **Version** to "New version"
4. Add description: "Fixed email permissions"
5. Click **Deploy**
6. Copy the new URL (if it changed)

### Fix 4: Test from Form
1. Submit a test entry through your waitlist form
2. Check Google Sheet - entry should be saved
3. Check Apps Script logs - look for email logs
4. Check your email inbox (and spam)

## Still Not Working?

### Check Gmail Settings
1. Go to https://myaccount.google.com/security
2. Ensure "Less secure app access" is not blocking (if using old Gmail)
3. Check if 2-factor authentication is interfering

### Alternative: Use a Different Email Service
If Gmail continues to fail, you can:
1. Use SendGrid API
2. Use Mailgun
3. Use your own SMTP server

### Get Help
If none of this works:
1. Share your Apps Script execution logs
2. Share any error messages from browser console
3. Email: meethire.in@gmail.com

## Prevention Checklist

✅ Gmail permissions granted
✅ Script deployed as "Anyone" access  
✅ Test email function works
✅ Logs show no errors
✅ Email not in spam folder
✅ Daily sending limit not exceeded
✅ Script redeployed after changes

---

**Last Updated**: February 2026
