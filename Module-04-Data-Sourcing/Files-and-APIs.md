# Files and APIs

## Topic: Getting Data by Scraping with Excel (From Web)

### Type of Source
- Web Source (Public Website)
- Structured HTML Table Data
- Live Connected Data Source

### Tool Used
- Microsoft Excel
- Power Query (Get & Transform)
- Data → Get Data → From Web

### Data Source Used
Website: https://www.timeanddate.com/weather/  
Example: Two Week Weather Forecast – Chennai

### What Was Done
- Connected Excel to a live website using From Web query
- Extracted structured table data (2-week forecast)
- Loaded data into Excel as a connected query
- Edited and transformed data inside Query Editor
- Removed unnecessary columns
- Created a refreshable data connection

### Key Concepts Covered
- Web scraping using Excel
- Query Editor
- Table View vs Web View
- Applied Steps tracking
- Data transformation
- Refreshable live data connection

### Important Feature
The imported table remains connected to the website. Using **Refresh**, Excel fetches the latest updated data.

---

# Topic: Scraping Data from IMDB using Python

### Type of Source
- Public Website
- HTML Structured Data
- Static Web Page

### Tools & Libraries Used
- Python
- Jupyter Notebook
- requests
- BeautifulSoup (bs4)
- pandas

### Purpose of the Exercise
To scrape the **Top Rated Movies list from IMDB** and convert:

- Movie Title
- Release Year
- IMDB Rating

into structured tabular format using Python.

### Technical Workflow

Import required libraries:

- requests → Access webpage  
- BeautifulSoup → Parse HTML  
- pandas → Create DataFrame  

Steps:

1. Load webpage content using requests.
2. Convert HTML content into BeautifulSoup object.
3. Inspect webpage elements using:
   - Right click → Inspect
   - Identify HTML tags and classes
4. Extract data using:

Higher level tag:  
`chart full-width`

Title & Year:  
`titleColumn`

Rating:  
`ratingColumn imdbRating`

Extraction methods:

- Title extraction → `a.text`
- Year extraction → `span.text`
- Rating extraction → `strong.text`

5. Store extracted data into lists.
6. Convert lists into a pandas DataFrame.
7. Display the table.

### Output
A structured DataFrame containing:

- Movie Title
- Year
- Rating

---

# Topic: Extracting Data Using the Wikipedia Python Library

### Type of Source
- Public Knowledge Base
- Wikipedia Articles
- Structured & Semi-Structured Web Data

### Tools & Libraries Used
- Python
- wikipedia (Python library)
- pandas
- Jupyter Notebook

### Installation

```bash
pip install wikipedia
```

### Purpose of the Exercise

To extract structured information directly from Wikipedia using the **wikipedia Python library** instead of manually scraping HTML.

### Functionalities Used

Search for keyword:
```
wikipedia.search()
```

Get article summary:
```
wikipedia.summary()
```

Limited summary using:
```
sentences argument
```

Get full page:
```
wikipedia.page()
```

Extract:

- URL → `page.url`
- References → `page.references`
- Images → `page.images`

Extract tables from page:

Use page HTML and:

```
pandas.read_html()
```

Select required table index.

### Key Advantage

Using the Wikipedia library simplifies data extraction:

- No manual HTML parsing
- No need for BeautifulSoup
- Direct access to structured page elements

---

# Topic: Scraping BBC Weather Data using Python

### Type of Source
- Public Website
- Dynamic Weather Data
- HTML Structured Data

### Libraries Used
- Python
- requests
- BeautifulSoup (bs4)
- pandas
- re (Regular Expressions)
- datetime

### Purpose of the Exercise

To scrape **14-day weather forecast data for Mumbai from BBC Weather** and store it in:

- pandas DataFrame
- CSV file
- Excel file

### Data Extracted

- Daily High Temperature (°C)
- Daily Low Temperature (°C)
- Daily Weather Summary
- Date

### Technical Workflow

Fetch HTML page using:

```
requests.get(URL)
```

Parse HTML using:

```
BeautifulSoup(response.content, "html.parser")
```

Inspect webpage elements to locate:

- High temp → `day-temperature-high`
- Low temp → `day-temperature-low`
- Summary → Specific span blocks

Use:

```
find_all()
```

List processing to clean unwanted text.

String split to remove Fahrenheit values.

Regular expressions to split long summary string.

Generate date column using:

```
pandas.date_range()
```

Create DataFrame using:

```
pandas.DataFrame()
```

Clean degree symbol and convert to float.

Save output as:

- `.csv`
- `.xlsx`

### Important Notes

Web scraping may not always be legally permitted.  
Always check website terms and conditions before scraping.

---

# GitHub Actions – Scheduled Workflows

### Required Folder Structure

```
project-root/
│
└── .github/
    └── workflows/
        └── main.yml
```

GitHub **ONLY detects workflow files inside `.github/workflows/`**.

### Example Workflow File (main.yml)

```yaml
name: Scheduled Workflow

on:
  push:
    branches:
      - main
  schedule:
    - cron: "*/5 * * * *"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: echo "Running scheduled workflow"
```

### Cron Format

```
| | | | |
| | | | └── Day of week (0-7)
| | | └──── Month (1-12)
| | └────── Day of month (1-31)
| └──────── Hour (0-23)
└────────── Minute (0-59)
```

Example:

```
0 8 1 * *
```

Runs at **8 AM on the 1st of every month (UTC)**.

### Environment

- GitHub-hosted Ubuntu VM
- YAML configuration
- UTC timezone
- Execution time not guaranteed exactly

### Use Cases

- Automated deployments
- Security scans
- Vulnerability checks
- Periodic reports

---

# Screen Scraping with Gemini (Vision-Based Scraping)

### Concept

Instead of scraping HTML using code, record the screen and let Gemini extract structured data from frames.

### Files Used

- screen_recording.mp4
- JSON output generated by Gemini

### Recording Settings

- 1 frame per second
- Scroll once per second
- Save short MP4

Platform Used:

**Google AI Studio (Gemini Flash model)**

### Prompt Example

```
Extract all information in these tweets as JSON.
```

### Example Output

```json
[
  {
    "username": "example_user",
    "handle": "@example",
    "text": "Sample tweet",
    "likes": 120
  }
]
```

### Cost Estimation

~250 tokens per image  
$0.075 per 1M tokens

Example:

19 frames × 250 tokens = 4750 tokens  
Cost ≈ 0.04 cents

### Advantages

- No HTML parsing
- No Selenium required
- Works visually
- Handles dynamic web apps

### Limitations

- May skip frames
- Not real-time
- Depends on visible content
- Requires good prompt formatting

---

# Microsoft MarkItDown – File to Markdown Conversion

### Purpose

Convert multiple document types into clean **Markdown format** for LLM pipelines, indexing, and RAG systems.

### Installation

```bash
pip install markitdown
```

### Supported Formats

- PDF
- Word (.docx)
- Excel (.xlsx)
- PowerPoint
- Images (OCR)
- HTML
- XML
- JSON
- CSV
- ZIP
- Audio files

### Basic Usage (Without LLM)

```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("file.pdf")
print(result.text_content)
```

### With LLM (OCR)

```python
from markitdown import MarkItDown
from openai import OpenAI

client = OpenAI()

md = MarkItDown(llm_client=client, llm_model="gpt-4o")
result = md.convert("image.png")

print(result.text_content)
```

### CLI Usage

```
markitdown file.pdf
```

Using pipe:

```
cat file.pdf | markitdown
```

### Use Cases

- Preparing documents for RAG
- Cleaning enterprise PDFs
- Converting Excel knowledge bases
- Standardizing document formats
- Dataset generation

### Key Insight

Unstructured documents → Structured Markdown → Better LLM performance

---

# Nominatim – OpenStreetMap Geocoding API

### Purpose

Convert text addresses into geographic coordinates and structured location data.

### Installation

```bash
pip install geopy
```

### Python Example

```python
from geopy.geocoders import Nominatim

locator = Nominatim(user_agent="my_geocoder")
location = locator.geocode("Eiffel Tower")

print(location.latitude)
print(location.longitude)
print(location.address)
print(location.raw)
```

### Example JSON Structure

```json
{
 "lat": "48.8582602",
 "lon": "2.2944991",
 "display_name": "Eiffel Tower, Paris, France",
 "class": "tourism",
 "type": "attraction",
 "boundingbox": [...]
}
```

### Extractable Fields

- Latitude
- Longitude
- Full formatted address
- Bounding box
- Class (tourism, amenity)
- Type (attraction, university)

Example:

Input: **IIT Madras**

Output:

- Coordinates
- Full address with pincode
- Class: amenity
- Type: university

### Applications

- Location-based analytics
- Delivery optimization
- Geo-tagging datasets
- Urban planning
- Mapping systems

### Important Notes

- Free & open-source
- Rate limited
- Requires user_agent parameter
- Alternative to Google Maps Geocoding API

---

# OVERALL TECHNICAL TAKEAWAYS

- Automation can be scheduled using GitHub cron workflows.
- Vision-based scraping is an alternative to HTML scraping.
- Converting documents to Markdown improves LLM pipeline quality.
- Geocoding converts unstructured text into structured geographic intelligence.
- Data preprocessing is critical for AI/ML applications.
- Structured output (JSON / Markdown) is essential for scalable systems.
