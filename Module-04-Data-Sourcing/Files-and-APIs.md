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

