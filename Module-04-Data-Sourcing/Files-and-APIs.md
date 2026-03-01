# Data Extraction & Web Scraping Projects


--------------------------------------------------

1. Web Scraping Using Excel

Source Type
- Public Website
- Structured HTML Table
- Live Data Connection

Tools Used
- Microsoft Excel
- Power Query (Get & Transform)

Data Source
- Website: https://www.timeanddate.com/weather/
- Example: Two Week Weather Forecast – Chennai

Workflow
- Connected Excel to website using Data → Get Data → From Web
- Extracted structured table data
- Loaded data into Excel as a query
- Transformed data using Power Query Editor
- Removed unnecessary columns
- Created a refreshable data connection

Key Concepts
- Web scraping using Excel
- Query Editor
- Table View vs Web View
- Applied Steps tracking
- Data transformation

Key Feature
- The dataset remains connected to the website
- Using Refresh updates the data automatically

--------------------------------------------------

2. IMDB Data Scraping Using Python

Source Type
- Public Website
- Static HTML Data

Libraries Used
- Python
- requests
- BeautifulSoup (bs4)
- pandas

Objective
- Extract Movie Title, Release Year, and IMDB Rating from IMDB

Workflow

1. Import Libraries
import requests
from bs4 import BeautifulSoup
import pandas as pd

2. Fetch Webpage
response = requests.get(URL)

3. Parse HTML
soup = BeautifulSoup(response.content, "html.parser")

4. Extract Data
- Title: a.text
- Year: span.text
- Rating: strong.text

5. Store Data
- Save into lists
- Convert into pandas DataFrame

Output
- Structured table containing Title, Year, Rating

--------------------------------------------------

3. Data Extraction Using Wikipedia Library

Source Type
- Wikipedia Articles
- Structured and Semi-Structured Data

Libraries Used
- Python
- wikipedia
- pandas

Installation
pip install wikipedia

Objective
- Extract structured data without manual HTML scraping

Functionalities
- Search: wikipedia.search()
- Summary: wikipedia.summary()
- Full Page: wikipedia.page()
- URL: page.url
- Images: page.images
- References: page.references

Table Extraction
import pandas as pd
tables = pd.read_html(page.html())

Advantage
- No manual HTML parsing
- No BeautifulSoup required
- Direct structured data access

--------------------------------------------------

4. BBC Weather Data Scraping

Source Type
- Public Website
- Dynamic Weather Data

Libraries Used
- Python
- requests
- BeautifulSoup
- pandas
- re
- datetime

Objective
- Scrape 14-day weather forecast data for Mumbai

Data Extracted
- High Temperature (°C)
- Low Temperature (°C)
- Weather Summary
- Date

Workflow

1. Fetch Data
requests.get(URL)

2. Parse HTML
BeautifulSoup(response.content, "html.parser")

3. Extract Elements
- High Temp: day-temperature-high
- Low Temp: day-temperature-low
- Summary: span elements

4. Data Cleaning
- Remove unwanted text
- Convert temperature values
- Use regex for formatting

5. Create Date Range
pd.date_range()

6. Save Data
df.to_csv()
df.to_excel()

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

