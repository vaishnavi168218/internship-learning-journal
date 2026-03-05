# Module 4 – Web Sources

## Time and Date – Weather Forecast
**URL:** https://www.timeanddate.com/weather/

**Example Page Used:** Two Week Weather Forecast – Chennai

### Type of Data Extracted
- Date
- Temperature
- Weather conditions
- Wind
- Forecast information

### Method of Extraction
- Excel Power Query  
- Data → Get Data → From Web  
- Selected "Table 0" from detected webpage tables  
- Removed unnecessary columns  
- Loaded as refreshable table  

### Live Data Connection
The Excel file remains connected to the webpage.

**To update:**
- Data → Refresh  
- OR  
- Right click table → Refresh  

This fetches the latest forecast data.

---

## IMDB – Top Rated Movies
**Source:** https://www.imdb.com/chart/top/

### Data Extracted
- Movie Title
- Release Year
- IMDB Rating

### Method Used
- Copied IMDB Top Movies URL.
- Loaded webpage using `requests`.
- Parsed HTML using `BeautifulSoup`.
- Identified required tags using Inspect tool.

**Extracted:**
- `a` tag → Title
- `span` tag → Year
- `strong` tag → Rating

Converted extracted data into a **pandas DataFrame**.

### Type of Extraction
- HTML Tag Based Scraping
- Class-based element selection
- Static Web Scraping

### Nature of Data
- Live website data
- Not automatically refreshable
- Requires re-running Python script for updated data

---

## Wikipedia
**Website:** https://www.wikipedia.org/

**Example Used:** Wikipedia article search (e.g., IIT Madras)

### Data Extracted
- Search results
- Page summaries
- Full article content
- Article URL
- References (external links)
- Images
- Tables (using pandas)

### Extraction Method
Instead of traditional scraping using:
- `requests`
- `BeautifulSoup`

Used:
- **wikipedia Python library**

### Table Extraction Method
- Retrieve page HTML.
- Use `pandas.read_html()` to read all tables.
- Select required table by index.
- Convert into DataFrame.

### Nature of Data
- Live Wikipedia data
- Requires script re-execution for updated content
- Structured access via API-like interface

---

## BBC Weather
**Website:** https://www.bbc.com/weather

**Example Used:** Mumbai – 14 Day Weather Forecast

### Data Extracted
- High Temperature (°C)
- Low Temperature (°C)
- Daily Summary
- Forecast Dates

### Extraction Method
- Used `requests` to fetch HTML content.
- Parsed HTML using `BeautifulSoup`.
- Located data using:
  - Span tags
  - Specific class names
- Used regular expressions to process summary text.
- Structured cleaned data into a **pandas DataFrame**.
- Saved output as **CSV and Excel files**.

### Nature of Data
- Live weather data
- Requires script re-execution for updates
- Structured through HTML tag-based scraping

---

# GitHub Actions

### Documentation
- https://docs.github.com/en/actions
- https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
- https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule
- https://crontab.guru/
- https://www.githubstatus.com/

---

# Screen Scraping with Gemini

### Resources
- https://aistudio.google.com/
- https://deepmind.google/technologies/gemini/
- https://ai.google.dev/docs
- https://simonwillison.net/

### Concepts
- https://en.wikipedia.org/wiki/Optical_character_recognition
- https://en.wikipedia.org/wiki/Multimodal_learning

---

# Microsoft MarkItDown

### References
- Microsoft MarkItDown GitHub Repository (Search: "Microsoft MarkItDown GitHub")
- https://www.markdownguide.org/
- https://platform.openai.com/
- https://github.com/IBM/docling
- https://www.pinecone.io/learn/retrieval-augmented-generation/

---

# Nominatim – OpenStreetMap

### Resources
- https://www.openstreetmap.org/
- https://nominatim.org/
- https://geopy.readthedocs.io/
- https://www.openstreetmap.org/copyright
- https://developers.google.com/maps/documentation/geocoding

---

# DocSearch Scraping Tutorial

### Primary Website
**Insider Intelligence Archive**
- ~369 pages
- ~7000 articles
- Structured content pages
- Used as real-world scraping target for semantic search demo.

### Tools Referenced

#### 1. httpx Documentation
Used for:
- HTTP requests
- Redirect handling
- Timeout management

#### 2. lxml Documentation
Used for:
- XPath parsing
- HTML tree navigation

#### 3. tqdm Documentation
Used for:
- Progress monitoring in loops

#### 4. Stack Overflow
Used indirectly via LLM search tools for:
- Debugging httpx
- Redirect issues
- XPath troubleshooting

### LLM Tools Mentioned
- ChatGPT
- Bing AI
- Phind

Used for:
- Generating short Python snippets
- Debugging assistance
- Research-backed answers

### Referenced Concepts
- Rubber Duck Debugging
- Ignobel Prize
- Friday Night Experiments
- Discovery of Graphene (example of experimental research culture)

### Key Philosophy
- Build fast prototypes.
- Show working demos.
- Use AI tools as coding copilots.
- Iterate with small correct steps.

---

# Scraping PDFs

### Primary Website
**Premier League Publications Page**

Contains:
- Seasonal handbooks
- Fixtures documents
- Competition documentation
- 25–30 downloadable PDFs

### Libraries Referenced

#### 1. BeautifulSoup (bs4)
Documentation:
- HTML parsing
- Extracting anchor tags
- Filtering file links

#### 2. tabula
Key Features:
- Extract tables from PDF
- `read_pdf()`
- `convert_into()`
- `area parameter`
- `pages parameter`

#### 3. pandas
Used for:
- DataFrame inspection
- Structured tabular processing

### Key Concepts
- PDF scraping vs HTML scraping
- File handling in Python
- Binary file writing
- Page-specific extraction
- Region-based table detection

### Tools & Techniques
- HTML parsing
- String manipulation
- File I/O
- Structured data conversion
- Automated batch downloading

---

# Vibe Coding

### Documentation References
- https://platform.openai.com/docs
- https://docs.python.org/3/
- https://fastapi.tiangolo.com/
- https://docs.python-requests.org/
- https://docs.github.com/

### Tools Referenced
- Visual Studio Code: https://code.visualstudio.com/
- Postman API Testing Tool: https://www.postman.com/

These resources were used to understand API integration, backend development, and AI-assisted coding workflows demonstrated in the workshop.
