## Step 1: Set up your Node.js project and install Puppeteer

```bash
npm init
npm install puppeteer
```

## Step 2: Create a JavaScript file, e.g., `generatePDF.js`, and require Puppeteer

```javascript
const puppeteer = require('puppeteer');
```

## Step 3: Define an async function to generate the PDF

```javascript
async function generatePDF() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();

  // Load the HTML content or URL
  await page.goto('https://example.com', { waitUntil: 'networkidle0' });

  // Generate the PDF
  await page.pdf({ path: 'output.pdf', format: 'A4' });

  // Close the browser
  await browser.close();
}
```

## Step 4: Call the `generatePDF` function

```javascript
generatePDF().then(() => {
  console.log('PDF generated successfully!');
}).catch((error) => {
  console.error('Error generating PDF:', error);
});
```

This example loads the HTML content from `https://example.com` and generates a PDF named `output.pdf` in the current working directory. You can modify the `page.goto()` method to load local HTML files or other URLs.

Make sure you have a stable internet connection when running Puppeteer, as it requires downloading a version of Chromium.

Save the file and run it using Node.js:

```bash
node generatePDF.js
```

After executing the script, you should see the message "PDF generated successfully!" if everything goes well.
