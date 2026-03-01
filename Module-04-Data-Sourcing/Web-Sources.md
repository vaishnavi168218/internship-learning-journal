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

