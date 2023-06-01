## Step 1: Set up your Node.js project and install Puppeteer

```bash
npm init
npm install puppeteer
```

## Step 2: Create a JavaScript file, e.g., `generatePDF.js`, and require Puppeteer

```javascript
const fs = require('fs');
const puppeteer = require('puppeteer');

async function generatePDF(htmlFilePath, outputFilePath) {
  // Read the HTML file
  const html = fs.readFileSync(htmlFilePath, 'utf-8');

  // Launch Puppeteer
  const browser = await puppeteer.launch();
  const page = await browser.newPage();

  // Set the HTML content of the page
  await page.setContent(html);

  // Generate PDF from the page
  await page.pdf({ path: outputFilePath, format: 'A4' });

  // Close the browser
  await browser.close();

  console.log(`PDF generated successfully at ${outputFilePath}`);
}
```

## Step 4: Call the `generatePDF` function

```javascript
const htmlFilePath = '/path/to/custom.html';
const outputFilePath = '/path/to/output.pdf';

generatePDF(htmlFilePath, outputFilePath)
  .catch(error => console.error(error));
```

Make sure you have Puppeteer and fs installed in your Node.js project by running `npm install puppeteer fs`. Also, replace `'/path/to/custom.html'` with the actual path to your custom HTML file, and `'/path/to/output.pdf'` with the desired path for the generated PDF.

This code reads the HTML file using the `fs` module, launches a Puppeteer browser instance, sets the HTML content of a new page, and generates a PDF from that page. Finally, the browser is closed, and a success message is logged to the console.
