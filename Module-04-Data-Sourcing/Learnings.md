# Get the Data – Web Scraping Learnings

--------------------------------------------------

1. Scraping with Excel

Learnings
- Extracted live data from websites directly into Excel using Power Query
- Used Data Tab → Get Data → From Web
- Connected to a website by pasting a URL
- Identified available tables from the webpage

Data Transformation
- Used Query Editor to:
  - Preview data
  - Remove unnecessary columns
  - Transform data before loading
- Understood "Applied Steps":
  - Each transformation is recorded step-by-step

Data Loading
- Loaded cleaned table into Excel
- Used Refresh to fetch updated data from the website

Key Understanding
- Excel can act as a lightweight web scraping tool
- Data remains connected to the original source
- Refresh updates the dataset dynamically
- Transformations are automatically reapplied

Practical Use Case
- Imported Two Week Weather Forecast for Chennai

Applications
- Data analysis
- Visualization
- Dashboard creation
- Trend analysis

--------------------------------------------------

2. Scraping with Python (IMDB)

Learnings
- Introduced web scraping using Python
- Extracted structured data from IMDB

Libraries Used
- requests
- BeautifulSoup
- pandas

Technical Workflow
- Fetched webpage using requests
- Parsed HTML using BeautifulSoup
- Inspected webpage using browser developer tools

HTML Understanding
- Identified:
  - Tag names
  - Class names
  - Nested structure
- Understood hierarchy:
  - Parent containers hold multiple records
  - Child elements store specific values

Data Extraction
- Movie Title → a.text
- Movie Year → span.text
- Rating → strong.text

Data Processing
- Stored extracted data in lists
- Converted lists into pandas DataFrame
- Displayed structured output

Key Understanding
- Webpages are structured using HTML
- Correct tag identification is essential
- Higher-level containers enable bulk extraction
- pandas converts raw data into structured format

Practical Outcome
- Converted IMDB Top Movies list into structured table

Applications
- Data analysis
- Visualization
- Further processing

--------------------------------------------------

3. Wikipedia Data Extraction

Learnings
- Used wikipedia Python library for structured data extraction
- Avoided manual HTML scraping

Concepts Covered
- Installed external libraries using pip
- Used search() to find pages
- Used summary() for concise information
- Limited summary using sentences parameter
- Used page() for full article data

Data Access
- Extracted:
  - URL
  - References
  - Images

Table Extraction
- Used HTML content with pandas.read_html()
- Selected tables using index

Key Understanding
- Wikipedia library simplifies data extraction
- Provides structured access to information
- Tables are stored as lists
- Requires trial-and-error for correct table selection

Practical Outcome
- Extracted structured knowledge data for:
  - Research
  - Data analysis
  - Academic work
  - Automation

--------------------------------------------------

4. Scraping BBC Weather with Python

Learnings
- Extracted structured weather data from BBC Weather

Core Concepts
- Web scraping retrieves HTML content
- requests fetches webpage data
- BeautifulSoup parses HTML
- Browser Inspect tool helps identify structure

Technical Workflow
- Used find_all() to extract multiple elements
- Processed lists to extract required data

Data Cleaning
- Used:
  - String splitting
  - Indexing
  - Regular expressions
- Converted text to numerical values
- Handled special characters (degree symbol)

Data Structuring
- Generated date column using pandas
- Combined lists into DataFrame

Data Export
- Saved output to:
  - CSV
  - Excel

Key Takeaways
- requests → Fetch HTML
- BeautifulSoup → Extract data
- Data cleaning is essential
- Structured datasets enable analysis
- Legal considerations must be followed

Practical Outcome
- Created 14-day weather dataset for Mumbai

Applications
- Data analysis
- Forecast comparison
- Visualization
- Data storage

# GitHub Actions – Scheduling & Automation
- Core Learning: GitHub Actions allows automation of workflows based on events such as push, pull request, or schedule (cron).
- Workflows must be inside `.github/workflows/`
- YAML syntax is used to define jobs and triggers
- Cron expressions define time-based execution
- All schedules run in UTC timezone
- GitHub does NOT guarantee exact execution timing
- Cron Format: `Minute Hour Day Month Day-of-week`
- Example: `*/5 * * * *` → Runs every 5 minutes
- Insight: Scheduled workflows are not suitable for real-time monitoring due to delays
- Applications:
  - Automated deployments
  - Dependency scanning
  - Security checks
  - Monthly reports
  - Periodic backups
- Takeaway: Design automation with execution delays in mind

# Screen Scraping with Gemini – Vision-Based Data Extraction
- Core Learning: Use video frames instead of HTML scraping for structured data extraction
- Recording at 1 FPS converts video into analyzable images
- Each frame ~250 tokens
- JSON mode required for structured output
- Cost-efficient (1000 frames ≈ few cents)
- Advantages:
  - Works on dynamic websites
  - No DOM parsing required
  - Handles JS-rendered content
- Limitations:
  - Depends on visible content
  - Not real-time
  - May skip frames
- Insight: Shift from code-based scraping → vision-based extraction

# Microsoft MarkItDown – Document Standardization
- Core Learning: Converts files into Markdown for LLM-friendly processing
- Why Markdown:
  - Lightweight
  - Easy to chunk
  - Ideal for RAG
- Modes:
  - Without LLM → fast parsing
  - With LLM → OCR + better formatting
- Applications:
  - Enterprise document cleaning
  - Knowledge base creation
  - Dataset generation
- Takeaway: Data preprocessing is critical for LLM performance

# Nominatim – Geocoding with OpenStreetMap
- Core Learning: Converts text locations into structured geographic data
- Powered by OpenStreetMap
- Requires `user_agent`
- Returns structured JSON
- Extractable:
  - Latitude / Longitude
  - Address
  - Bounding box
  - Class / Type
- Applications:
  - Mapping
  - Delivery systems
  - Geo-tagging
- Takeaway: Text → Geographic intelligence

# Overall Technical Insights
- Automation enables scalable DevOps workflows
- Vision-based scraping reduces dependency on HTML parsing
- Markdown improves LLM pipelines
- Geocoding enables spatial intelligence
- Structured outputs (JSON/Markdown) are essential
- Data preprocessing directly impacts AI performance

# DocSearch Scraping Tutorial

## Semantic vs Keyword Search
- Keyword search → exact match
- Semantic search → meaning via embeddings
- Enables intelligent search systems

## Caching Strategy
- Save HTML locally
- Avoid repeated downloads
- Faster debugging
- Resume-safe scraping
- Pattern:
  - If exists → load
  - Else → fetch + save

## Scraping Workflow
- Extract archive URLs
- Collect article links
- Deduplicate
- Fetch content
- Parse data
- Store output
- Principle: Small steps > complex logic

## XPath Usage
- Use DevTools for inspection
- Target stable containers
- Use `contains()` instead of exact matches

## Debugging Techniques
- Print variables frequently
- Use breakpoints
- Rubber duck debugging

## Using LLMs Effectively
- Ask specific questions
- Mention tools/libraries
- Request concise code

## Proof of Concept
- Working demos > presentations
- Faster validation and deployment

## Incremental Saving
- Save JSON inside loop
- Prevent data loss
- Enable early inspection

## Edge Case Handling
- Redirects
- Empty responses
- Deduplication issues
- Imperfect HTML

## Insight
- Rapid prototyping creates advantage
- Small projects → big opportunities

# Scraping PDFs

## Extracting PDFs
- Use BeautifulSoup
- Filter `.pdf` links
- Extract filenames via `split("/")[-1]`

## File Handling
- Create directories
- Save in binary mode
- Automate downloads

## Table Extraction
- Use Tabula
- `read_pdf()` for reading
- `convert_into()` for CSV

## Issues Faced
- Incorrect table detection
- Layout misinterpretation
- Extra content included

## Solution
- Use `area=[top, left, bottom, right]`
- Restrict extraction region

## Key Learnings
- Layout matters in PDFs
- Always inspect extracted data
- Fine-tuning improves accuracy

## Workflow
- Webpage → PDF → Table extraction → Cleaning → CSV

# Vibe Coding

## Core Concepts
- Idea-first development
- AI-assisted rapid prototyping
- Prompt-driven coding

## Technical Learnings
- API integration in Python
- JSON handling
- Secure API key management
- Scalable project structure
- Debugging AI-generated code

## Practical Skills
- Product-oriented thinking
- Breaking problems into modules
- Faster development workflows
- Writing maintainable code

## Outcome
- Improved confidence in building applications
- Better understanding of AI-assisted development
- Stronger problem-solving and logical thinking
