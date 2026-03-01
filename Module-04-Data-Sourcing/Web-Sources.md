# Data Sources and Extraction Methods

--------------------------------------------------

1. Time and Date – Weather Forecast

Website
- https://www.timeanddate.com/weather/

Example Used
- Two Week Weather Forecast – Chennai

Type of Data Extracted
- Date
- Temperature
- Weather Conditions
- Wind
- Forecast Information

Method of Extraction
- Excel Power Query
- Data → Get Data → From Web
- Selected "Table 0" from detected tables
- Removed unnecessary columns
- Loaded as refreshable table

Live Data Connection
- Excel file remains connected to the website

Update Methods
- Data → Refresh
- Right click table → Refresh

Key Feature
- Fetches latest forecast data automatically on refresh

--------------------------------------------------

2. IMDB – Top Rated Movies

Website
- https://www.imdb.com/chart/top/

Data Extracted
- Movie Title
- Release Year
- IMDB Rating

Method Used
- Loaded webpage using requests
- Parsed HTML using BeautifulSoup
- Inspected elements using browser developer tools

Data Extraction
- a tag → Title
- span tag → Year
- strong tag → Rating

Data Processing
- Stored data in lists
- Converted into pandas DataFrame

Type of Extraction
- HTML tag-based scraping
- Class-based element selection
- Static web scraping

Nature of Data
- Live website data
- Not auto-refreshable
- Requires re-running Python script for updates

--------------------------------------------------

3. Wikipedia Data Extraction

Website
- https://www.wikipedia.org/

Example Used
- Article search (e.g., IIT Madras)

Data Extracted
- Search results
- Page summaries
- Full article content
- Article URL
- References
- Images
- Tables

Extraction Method
- Used wikipedia Python library
- Avoided manual scraping with requests and BeautifulSoup

Table Extraction
- Retrieved page HTML
- Used pandas.read_html()
- Selected table using index
- Converted into DataFrame

Nature of Data
- Live Wikipedia data
- Requires script re-execution for updates
- Structured access via API-like interface

--------------------------------------------------

4. BBC Weather

Website
- https://www.bbc.com/weather

Example Used
- Mumbai – 14 Day Weather Forecast

Data Extracted
- High Temperature (°C)
- Low Temperature (°C)
- Daily Summary
- Forecast Dates

Extraction Method
- Fetched HTML using requests
- Parsed using BeautifulSoup
- Located elements using:
  - Span tags
  - Specific class names

Data Processing
- Used regular expressions for cleaning text
- Structured into pandas DataFrame

Output
- Saved as CSV file
- Saved as Excel file

Nature of Data
- Live weather data
- Requires script re-execution for updates
- Extracted using HTML tag-based scraping

# References and Resources

--------------------------------------------------

## GitHub Actions
- GitHub Actions Documentation: https://docs.github.com/en/actions
- Workflow Syntax: https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
- Schedule Event: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule
- Cron Expression Builder: https://crontab.guru/
- GitHub Status Page: https://www.githubstatus.com/

--------------------------------------------------

## Screen Scraping with Gemini
- Google AI Studio: https://aistudio.google.com/
- Gemini Overview: https://deepmind.google/technologies/gemini/
- Gemini API Documentation: https://ai.google.dev/docs
- Simon Willison (AI & scraping research inspiration): https://simonwillison.net/
- OCR Reference: https://en.wikipedia.org/wiki/Optical_character_recognition
- Multimodal Learning: https://en.wikipedia.org/wiki/Multimodal_learning

--------------------------------------------------

## Microsoft MarkItDown
- Microsoft MarkItDown GitHub Repository: Search "Microsoft MarkItDown GitHub"
- Markdown Guide: https://www.markdownguide.org/
- OpenAI Platform: https://platform.openai.com/
- IBM Docling (Comparison Tool): https://github.com/IBM/docling
- RAG Concept: https://www.pinecone.io/learn/retrieval-augmented-generation/

--------------------------------------------------

## Nominatim – OpenStreetMap
- OpenStreetMap: https://www.openstreetmap.org/
- Nominatim Documentation: https://nominatim.org/
- Geopy Documentation: https://geopy.readthedocs.io/
- OpenStreetMap Licensing: https://www.openstreetmap.org/copyright
- Google Maps Geocoding (Comparison): https://developers.google.com/maps/documentation/geocoding

--------------------------------------------------

## DocSearch Scraping Tutorial

### Primary Website
- Insider Intelligence Archive
- ~369 pages
- ~7000 articles
- Structured content pages
- Used as real-world scraping target for semantic search demo

### Tools Referenced
1. httpx Documentation  
   - HTTP requests  
   - Redirect handling  
   - Timeout management  

2. lxml Documentation  
   - XPath parsing  
   - HTML tree navigation  

3. tqdm Documentation  
   - Progress monitoring in loops  

4. Stack Overflow  
   - Debugging httpx  
   - Redirect issues  
   - XPath troubleshooting  

### LLM Tools Mentioned
- ChatGPT  
- Bing AI  
- Phind  

### Usage
- Generating Python snippets  
- Debugging assistance  
- Research-based answers  

### Concepts Referenced
- Rubber Duck Debugging  
- Ignobel Prize  
- Friday Night Experiments  
- Discovery of Graphene  

### Key Philosophy
- Build fast prototypes  
- Show working demos  
- Use AI as coding copilots  
- Iterate with small correct steps  

--------------------------------------------------

## Scraping PDFs

### Primary Website
- Premier League Publications Page  
- Contains:
  - Seasonal handbooks  
  - Fixtures documents  
  - Competition documentation  
- 25–30 downloadable PDFs  

### Libraries Used
1. BeautifulSoup (bs4)  
   - HTML parsing  
   - Extracting links  

2. tabula  
   - read_pdf()  
   - convert_into()  
   - area parameter  
   - pages parameter  

3. pandas  
   - DataFrame processing  
   - Tabular data handling  

### Key Concepts
- PDF vs HTML scraping  
- File handling in Python  
- Binary file writing  
- Page-specific extraction  
- Region-based table detection  

### Techniques
- HTML parsing  
- String manipulation  
- File I/O  
- Structured data conversion  
- Batch downloading  

--------------------------------------------------

## Vibe Coding

### Documentation
- OpenAI API Docs: https://platform.openai.com/docs
- Python Docs: https://docs.python.org/3/
- FastAPI Docs: https://fastapi.tiangolo.com/
- Requests Docs: https://docs.python-requests.org/
- GitHub Docs: https://docs.github.com/

### Tools Used
- Visual Studio Code: https://code.visualstudio.com/
- Postman: https://www.postman.com/

### Purpose
- API integration  
- Backend development  
- AI-assisted coding workflows  

# Advanced Topics and Technical Notes

--------------------------------------------------

## GitHub Actions – Scheduled Workflows

### Folder Structure
project-root/
│
└── .github/
    └── workflows/
        └── main.yml

- GitHub detects workflows ONLY inside `.github/workflows/`

### Example Workflow (main.yml)
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

### Cron Format
- Minute (0–59)
- Hour (0–23)
- Day of month (1–31)
- Month (1–12)
- Day of week (0–7)

Example:
0 8 1 * * → Runs at 8 AM on 1st of every month (UTC)

### Environment
- GitHub-hosted Ubuntu VM
- YAML configuration
- UTC timezone
- Execution time not exact

### Use Cases
- Automated deployments
- Security scans
- Vulnerability checks
- Periodic reports

--------------------------------------------------

## Screen Scraping with Gemini (Vision-Based)

### Concept
- Capture screen → extract data using AI (no HTML parsing)

### Files Used
- screen_recording.mp4
- JSON output

### Recording Settings
- 1 frame per second
- Scroll once per second
- Short MP4 recordings

### Platform
- Google AI Studio (Gemini Flash)

### Prompt Example
"Extract all information in these tweets as JSON."

### Example Output
[
  {
    "username": "example_user",
    "handle": "@example",
    "text": "Sample tweet",
    "likes": 120
  }
]

### Cost Estimation
- ~250 tokens/image
- ~0.075 USD per 1M tokens
- Example: 4750 tokens ≈ very low cost

### Advantages
- No HTML parsing
- No Selenium
- Works on dynamic content

### Limitations
- May skip frames
- Not real-time
- Depends on visible data
- Needs good prompts

--------------------------------------------------

## Microsoft MarkItDown

### Purpose
- Convert files into Markdown for LLM/RAG pipelines

### Installation
pip install markitdown

### Supported Formats
- PDF, DOCX, XLSX, PPT
- Images (OCR)
- HTML, XML, JSON, CSV
- ZIP, Audio

### Basic Usage
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("file.pdf")
print(result.text_content)

### With LLM
from markitdown import MarkItDown
from openai import OpenAI

client = OpenAI()

md = MarkItDown(llm_client=client, llm_model="gpt-4o")
result = md.convert("image.png")
print(result.text_content)

### CLI
markitdown file.pdf
cat file.pdf | markitdown

### Use Cases
- RAG pipelines
- PDF cleaning
- Knowledge base conversion
- Dataset creation

### Insight
Unstructured → Markdown → Better LLM performance

--------------------------------------------------

## Nominatim – OpenStreetMap Geocoding

### Purpose
- Convert address → coordinates + metadata

### Installation
pip install geopy

### Example
from geopy.geocoders import Nominatim

locator = Nominatim(user_agent="my_geocoder")
location = locator.geocode("Eiffel Tower")

print(location.latitude)
print(location.longitude)
print(location.address)
print(location.raw)

### Output Fields
- Latitude / Longitude
- Address
- Bounding box
- Class / Type

### Example
Input: IIT Madras  
Output: Coordinates + full address + classification

### Applications
- Geo analytics
- Delivery optimization
- Mapping systems

### Notes
- Free and open-source
- Rate limited
- Needs user_agent

--------------------------------------------------

## Overall Technical Takeaways
- Automation using cron workflows
- Vision-based scraping as alternative
- Markdown improves LLM pipelines
- Geocoding converts text → geo data
- Data preprocessing is critical
- Structured outputs (JSON/Markdown) are essential

--------------------------------------------------

## DocSearch Scraping Tutorial

### Files
1. scrape2.py → Main scraping script  
2. cache2/ → Cached HTML files  
3. urls2.txt → Stored URLs  
4. scraped2.json → Final output  
5. scraped2.csv → Optional CSV  

### Libraries
- httpx → HTTP requests  
- lxml → HTML parsing  
- tqdm → Progress bar  
- hashlib → Caching  
- os → File handling  
- json → Data storage  
- pandas → CSV export  

### Website
- Insider Intelligence archive  
- ~369 pages  
- ~7000 articles  

### Workflow
- Loop archive pages  
- Extract article links  
- Deduplicate  
- Scrape content  
- Save JSON  

--------------------------------------------------

## Scraping PDFs

### Files
- 25–30 PDF files (Premier League)
- pl_interactive_combine.pdf
- table_output.csv

### Libraries
- BeautifulSoup → HTML parsing  
- requests → Download PDFs  
- tabula → Extract tables  
- pandas → Data handling  

### Workflow
- Parse webpage  
- Extract PDF links  
- Download files  
- Extract tables  
- Convert to CSV  

--------------------------------------------------

## Vibe Coding

### Files
- main.py → Core logic  
- requirements.txt → Dependencies  
- .env → Environment variables  
- README.md → Documentation  

### APIs
- OpenAI API → AI assistance  
- REST APIs → GET/POST handling  
- GitHub API → Automation concepts  

### Tools
- VS Code  
- GitHub  
- Postman  
- Python  
- AI coding assistants  

### Purpose
- API integration  
- Backend development  
- AI-assisted workflows  
