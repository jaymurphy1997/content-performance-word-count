# Setup Guide

## Google Sheets API Setup

### Step 1: Create a Google Cloud Project

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Click "Select a project" → "New Project"
3. Enter a project name and click "Create"

### Step 2: Enable APIs

1. In the Google Cloud Console, go to "APIs & Services" → "Library"
2. Search for and enable:
   - Google Sheets API
   - Google Drive API

### Step 3: Create Service Account

1. Go to "APIs & Services" → "Credentials"
2. Click "Create Credentials" → "Service Account"
3. Enter a name for your service account
4. Click "Create and Continue"
5. Skip the optional steps and click "Done"

### Step 4: Generate Credentials

1. Click on your newly created service account
2. Go to the "Keys" tab
3. Click "Add Key" → "Create New Key"
4. Select "JSON" and click "Create"
5. Save the downloaded file as `credentials.json` in your project root

### Step 5: Share Google Sheet

1. Open your Google Sheet
2. Click "Share" in the top right
3. Add the service account email (found in your credentials.json file under "client_email")
4. Give it "Editor" permissions

## Project Structure

Create this folder structure:

```
content-performance-word-count/
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
├── SETUP_GUIDE.md
├── credentials.json (create this from Google Cloud)
├── notebooks/
│   └── Content Performance - Word Count.ipynb
└── examples/
    └── sample_data.csv (optional)
```

## Installation Steps

1. **Clone/Download the repository**
2. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Set up Google credentials** (follow steps above)
4. **Update the notebook** with your specific Google Sheet URL
5. **Test the setup** with a small dataset first

## Configuration

### Update Notebook Settings

In the notebook, update these variables:

```python
# Your credentials file
credentials = Credentials.from_service_account_file(
    'credentials.json',  # Update this path if needed
    scopes=scopes
)

# Your Google Sheet URL
sheet_url = 'YOUR_GOOGLE_SHEET_URL_HERE'
```

### Test Your Setup

1. Create a test Google Sheet with a few URLs
2. Run the first few cells of the notebook
3. Verify it can connect to your sheet and process a few URLs

## Troubleshooting

### Common Errors

**"Forbidden" Error:**
- Make sure your service account email has access to the Google Sheet
- Check that both APIs are enabled in Google Cloud Console

**"File not found" Error:**
- Verify `credentials.json` is in the correct location
- Check the file path in your notebook

**Import Errors:**
- Run `pip install -r requirements.txt` again
- Consider using a virtual environment

### Rate Limiting

If you're processing many URLs, consider adding delays:

```python
import time

# Add this inside your processing loop
time.sleep(1)  # Wait 1 second between requests
```

## Security Best Practices

1. **Never commit credentials.json to version control**
2. **Use environment variables for production:**
   ```python
   import os
   credentials_path = os.getenv('GOOGLE_CREDENTIALS_PATH', 'credentials.json')
   ```
3. **Limit service account permissions** to only necessary scopes
4. **Regularly rotate service account keys**

## Need Help?

- Check the main README.md for usage examples
- Review Google's [Sheets API documentation](https://developers.google.com/sheets/api)
- Look at the [gspread documentation](https://docs.gspread.org/)