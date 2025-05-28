# Content Performance - Word Count Analysis

A Python notebook that analyzes web content performance by counting English words on web pages and correlating with scroll behavior data from Google Analytics.

## Overview

This tool fetches URLs from a Google Sheet containing content performance data (including scroll percentages), scrapes each web page to count English words, and writes the results back to the Google Sheet. It's designed to help content creators understand the relationship between content length and user engagement.

## Features

- Scrapes web pages and counts English words using a comprehensive dictionary
- Integrates with Google Sheets for data input/output
- Handles multiple scroll percentage thresholds (75%, 90%, etc.)
- Cleans and processes HTML content to extract meaningful text
- Automatically creates output sheets with combined analytics and word count data

## Prerequisites

- Python 3.7+
- Google Cloud Platform account with Sheets API enabled
- Service account credentials (JSON file)
- Access to Google Sheets containing your analytics data

## Installation

1. Clone this repository:
```bash
git clone https://github.com/jaymurphy1997/content-performance-word-count.git
cd content-performance-word-count
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Set up Google Sheets API:
   - Create a service account in Google Cloud Console
   - Enable Google Sheets API and Google Drive API
   - Download the credentials JSON file
   - Rename it to `credentials.json` and place it in the project root

## Usage

### Quick Start

1. Prepare your Google Sheet with columns:
   - `page_location`: URLs to analyze
   - `page_title`: Page titles
   - `percent_scrolled`: Scroll threshold (75, 90, etc.)
   - `scrolls`: Number of scroll events

2. Update the notebook with your:
   - Google Sheet URL
   - Credentials file path

3. Run the notebook:
```bash
jupyter notebook notebooks/Content\ Performance\ -\ Word\ Count.ipynb
```

### Customization

**Change the Google Sheet URL:**
```python
sheet_url = 'your_google_sheet_url_here'
```

**Modify word counting logic:**
The `return_words()` function can be customized to change how words are counted or filtered.

**Adjust text cleaning:**
Modify the regex pattern in `return_words()` to change how text is cleaned before word counting.

## Data Structure

### Input Sheet Columns
- `page_location`: Full URL of the page to analyze
- `page_title`: Title of the page
- `percent_scrolled`: Scroll depth threshold (75, 90, etc.)
- `scrolls`: Number of users who scrolled to this depth

### Output Sheet Columns
All input columns plus:
- `words`: Count of English words found on the page

## How It Works

1. **Dictionary Loading**: Downloads a comprehensive English word list from GitHub
2. **Web Scraping**: Uses BeautifulSoup to extract text content from each URL
3. **Text Processing**: Cleans HTML, removes punctuation, converts to lowercase
4. **Word Counting**: Counts only words that exist in the English dictionary
5. **Data Export**: Writes results to a new 'output' sheet in your Google Spreadsheet

## Examples

### Sample Input Data
```
page_location: https://news.wm.edu/2025/04/08/william-mary-co...
page_title: William & Mary counted among 'New Ivies'
percent_scrolled: 75
scrolls: 2339
```

### Sample Output
```
page_location: https://news.wm.edu/2025/04/08/william-mary-co...
page_title: William & Mary counted among 'New Ivies'
percent_scrolled: 75
scrolls: 2339
words: 724
```

## Security Notes

- Keep your `credentials.json` file secure and never commit it to version control
- The notebook includes the credentials filename in the code - update this path as needed
- Consider using environment variables for sensitive configuration

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## Troubleshooting

**Common Issues:**

- **Authentication Error**: Ensure your service account has access to the Google Sheet
- **URL Access Error**: Some pages may block scraping - these will return 0 words
- **Memory Issues**: For large datasets, consider processing in batches

**Rate Limiting**: The script doesn't include delays between requests. Add `time.sleep()` if you encounter rate limiting.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Uses the [english-words](https://github.com/dwyl/english-words) dictionary
- Built with BeautifulSoup, pandas, and gspread

---

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yourusername/content-performance-word-count/blob/main/notebooks/Content%20Performance%20-%20Word%20Count.ipynb)