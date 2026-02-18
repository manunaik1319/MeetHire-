# MeetHire Email Automation Setup

## 📧 Automatic Thank You Email

When someone fills out the waitlist form, they will **automatically** receive this email:

---

**Subject:** Thank you for joining MeetHire! 🙌

**Message:**
> Thank you for joining the MeetHire waitlist! 🙌
> 
> We're excited to have you onboard.
> 
> You'll be among the first to get early access as we launch.
> More updates coming soon 🚀
> 
> — Team MeetHire

---

## 🚀 Setup Instructions

### Step 1: Prepare Your Google Sheet

1. Create a new Google Sheet
2. Add these column headers in Row 1:
   - A: `Timestamp`
   - B: `Name`
   - C: `Email`
   - D: `Phone`
   - E: `Role`
   - F: `Organization`
   - G: `City`
   - H: `Message`
   - I: `Updates`

### Step 2: Set Up Google Apps Script

1. Open your Google Sheet
2. Click **Extensions** > **Apps Script**
3. Delete any existing code
4. Copy the entire code from `google-apps-script.js` (in the nextjs-app folder)
5. Paste it into the Apps Script editor
6. Click **Save** (disk icon) and name your project "MeetHire Waitlist"

### Step 3: Test Email Sending (Optional but Recommended)

1. In the Apps Script editor, find the `testEmail()` function (at the bottom)
2. Change `your-test-email@gmail.com` to your actual email address
3. Click the dropdown next to "Debug" and select `testEmail`
4. Click **Run** (play button)
5. Grant permissions when prompted
6. Check your email - you should receive the test email!

### Step 4: Deploy as Web App

1. In the Apps Script editor, click **Deploy** > **New deployment**
2. Click the **gear icon** next to "Select type"
3. Select **Web app**
4. Fill in the settings:
   - **Description**: MeetHire Waitlist API
   - **Execute as**: Me (your email)
   - **Who has access**: Anyone
5. Click **Deploy**
6. **Copy the Web App URL** (it looks like: `https://script.google.com/macros/s/...`)

### Step 5: Add URL to Your Next.js App

1. Open `components/waitlist/WaitlistForm.tsx`
2. Find line ~18: `const scriptURL = 'YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE';`
3. Replace with your actual URL:
   ```typescript
   const scriptURL = 'https://script.google.com/macros/s/YOUR_ACTUAL_URL_HERE';
   ```
4. Save the file

### Step 6: Test the Complete Flow!

1. Make sure your Next.js app is running: `npm run dev`
2. Go to http://localhost:3000/waitlist
3. Fill out the form with your email
4. Submit
5. Check your Google Sheet - you should see the new entry
6. Check your email - you should get the thank you email! 🎉

## ✅ Features Included

- ✅ Automatic thank-you email with your custom message
- ✅ Data saved to Google Sheets
- ✅ Duplicate email prevention
- ✅ Professional HTML email template
- ✅ Error handling
- ✅ Test functions for debugging

## 🔧 Troubleshooting

**Email not sending?**
- Make sure you granted Gmail permissions to the script
- Check the Apps Script logs: View > Logs
- Run the `testEmail()` function to verify email works

**Form not submitting?**
- Check browser console for errors
- Verify the Web App URL is correct
- Make sure the deployment is set to "Anyone" access

**Sheet not updating?**
- Check Apps Script logs for errors
- Make sure the sheet tabs match (use active sheet or specify sheet name)

## 📞 Support

If you need help, check the console logs in your browser (F12) and the Apps Script logs (View > Logs in Apps Script editor).

Email: meethire.in@gmail.com
