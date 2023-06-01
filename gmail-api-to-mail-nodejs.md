## Step 1: Install required packages

```bash
npm install googleapis google-auth-library
```

Step 2: Create `sendEmail.js` file

Step 3: Import necessary modules

```javascript
const { google } = require('googleapis');
const { authenticate } = require('@google-cloud/local-auth');
const fs = require('fs');
```

Step 4: Define the `sendEmail` function

```javascript
async function sendEmail() {
  // Authenticate using the Google Cloud client library
  const auth = await authenticate({
    keyfilePath: '<path-to-your-credentials-file>',
    scopes: ['https://www.googleapis.com/auth/gmail.send'],
  });

  // Create a Gmail API client
  const gmail = google.gmail({ version: 'v1', auth });

  // Construct the email message
  const email = [
    'From: "<your-email>"',
    'To: "<recipient-email>"',
    'Subject: Test email',
    '',
    'This is the body of the email.',
  ].join('\n');

  // Encode the email as base64
  const encodedEmail = Buffer.from(email).toString('base64')
    .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=+$/, '');

  try {
    // Send the email using the Gmail API
    const response = await gmail.users.messages.send({
      userId: 'me',
      requestBody: {
        raw: encodedEmail,
      },
    });

    console.log('Email sent:', response.data);
  } catch (error) {
    console.error('Error sending email:', error);
  }
}
```

Step 5: Call the `sendEmail` function

```javascript
sendEmail();
```

Make sure to replace the following placeholders in the code:
- `<path-to-your-credentials-file>`: Path to your JSON credentials file obtained from the Google Cloud Console.
- `<your-email>`: Your Gmail email address.
- `<recipient-email>`: Email address of the recipient.

This code uses the `googleapis` library to authenticate with the Gmail API, construct the email message, and send it using the `users.messages.send` endpoint. The email is base64 encoded before sending.

Before running the code, make sure you have completed the necessary setup steps in the Google Cloud Console, including enabling the Gmail API and obtaining credentials.
