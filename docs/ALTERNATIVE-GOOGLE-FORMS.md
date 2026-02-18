# Alternative: Use Google Forms (Easier & More Reliable)

Google Forms is much simpler and more reliable than Apps Script. Here's how to set it up:

## Step 1: Create Google Form

1. Go to https://forms.google.com
2. Click **+ Blank form**
3. Title: "MeetHire Waitlist"

## Step 2: Add Form Fields

Add these questions:

1. **Name** (Short answer, Required)
2. **Email** (Short answer, Required, Email validation)
3. **Phone** (Short answer, Optional)
4. **Role** (Multiple choice, Required)
   - College / TPO
   - Company HR / Recruiter
   - Student Coordinator
   - Student
   - Other
5. **Organization** (Short answer, Required)
6. **City** (Short answer, Optional)
7. **Message** (Paragraph, Optional)
   - Question: "How can MeetHire help you?"
8. **Updates** (Checkboxes, Optional)
   - Option: "Send me product updates and announcements"

## Step 3: Link to Google Sheets

1. In your form, click **Responses** tab
2. Click the Google Sheets icon (green)
3. Select "Create a new spreadsheet"
4. Name it "MeetHire Waitlist Responses"
5. Click **Create**

Now all responses automatically save to this sheet!

## Step 4: Get Form Embed Code

1. Click **Send** button (top right)
2. Click the **< >** (embed) icon
3. Copy the iframe code

## Step 5: Embed in Your Website

Replace your current form with the Google Form iframe:

```html
<iframe 
  src="YOUR_GOOGLE_FORM_URL" 
  width="100%" 
  height="1200" 
  frameborder="0" 
  marginheight="0" 
  marginwidth="0">
  Loading…
</iframe>
```

## Benefits:

✅ No coding required
✅ 100% reliable
✅ Automatic spam protection
✅ Data validation built-in
✅ Automatic Google Sheets integration
✅ Can export to Excel/CSV
✅ Email notifications on submission
✅ Response charts and analytics

## Styling the Embedded Form:

You can customize the form colors:
1. In Google Forms, click the palette icon (top right)
2. Choose colors that match your brand
3. Upload your logo

## Want Me to Set This Up?

I can create a custom styled page that embeds the Google Form seamlessly into your design. Just let me know!
