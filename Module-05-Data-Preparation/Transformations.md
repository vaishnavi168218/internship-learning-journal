# Excel Data Cleaning

## Text Transformations
1. Removed unwanted suffixes like "[more]" by applying the Find & Replace feature.
2. Used the TRIM() function to eliminate unnecessary spaces within text fields.

## Structural Transformations
1. Removed rows where important columns contained blank or missing values.
2. Identified and deleted duplicate country records to maintain unique entries.

## Data Type Transformations
1. Converted columns containing numeric values from "General" format to "Number".
2. Standardized decimal formatting to maintain consistent precision across the dataset.

## Data Quality Improvements
1. Corrected inconsistent text formatting across records.
2. Ensured numeric columns were properly interpreted as numbers.
3. Reduced redundant entries within the dataset.
4. Removed incomplete records that could affect analysis.

---

# Data Transformation in Excel

## 1. Ratio Calculations

### A. Metro Area to City Area Ratio
- Formula applied:
```
=G2/D2
```
- Purpose: Evaluate how the metropolitan region expands relative to the city boundary.
- Example insight: Tokyo’s metropolitan region is nearly six times larger than the city area.
- Some rows generated errors where metro area values were unavailable.

---

### B. Metro Population to City Population Ratio
- Formula applied:
```
=F2/C2
```
- Purpose: Compare population size between the metropolitan area and the central city.
- Example insight: Tokyo produced an approximate ratio of 2.76.
- Values were extended to other rows using Excel’s AutoFill feature.

---

### C. Density Comparison (Crowding Indicator)
- Derived by analyzing the relationship between:
  - Metro Area / City Area ratio
  - Metro Population / City Population ratio
- This metric helps estimate differences in population density between the city core and surrounding metropolitan region.

---

## 2. Pivot Table Transformations

### Creating the Pivot Table
1. Select the entire dataset.
2. Navigate to Insert → Pivot Table.
3. Place the pivot table in a new worksheet.

---

### A. Aggregation by Country
- Added **Country** to the Rows section.
- Inserted **Country** again in the Values section with **Count** as the aggregation.
- This revealed the frequency of records for each country.
  - Example: China appeared about 20 times.
  - Angola appeared only once.

---

### B. City-Level Aggregation
- Placed **City** under the Country row grouping.
- Added **City Proper Population** into the Values section.
- Changed the aggregation method to **Sum**.
- This displayed both city-level population and total population aggregated by country.

---

## 3. Chart-Based Insights
1. Generated a bar chart from the pivot table output.
2. Applied filters to analyze countries such as China and the United States.
3. Observed extreme values:
   - Chongqing and Shanghai showed the largest population counts in China.
   - Los Angeles showed a high density ratio in the United States.

---

# Text to Columns in Excel

## Structural Transformations
1. Converted raw text stored in a single column into several structured columns.
2. Extracted multiple categorical fields from mixed text strings.

---

## Delimiter-Based Transformations
Different delimiters were used to separate the data elements:

1. "(" separated the **Senator Name**.
2. "-" extracted the **Political Party**.
3. ")" separated the **State**.
4. "," isolated the **Vote Status**.

---

## Data Structuring
1. Converted messy web-copied text into a well-organized table format.
2. Assigned clear column headers.
3. Removed extra columns that appeared during the splitting process.

---

## Analytical Readiness
1. Converted raw text into a structured dataset similar to a CSV file.
2. Enabled sorting, filtering, and aggregation in Excel.
3. Prepared the dataset for further analysis and visualization tasks.

---

# Data Aggregation in Excel

## 1. Weekly Aggregation using Pivot Table

Objective:
- Calculate the total **New Cases**
- Group data by **Country and Week**
- Separate results by **Year (2020 and 2021)**

### Pivot Configuration
- Rows → Location (Country)
- Columns → Week
- Values → Sum of New Cases
- Filter/Grouping → Year

Insight:
This configuration revealed weekly COVID-19 case trends across different countries.

---

## 2. Monthly Aggregation using Pivot Table

Objective:
- Summarize new cases by month and country.

### Pivot Configuration
- Rows → Year → Month
- Columns → Location
- Values → Sum of New Cases

Insight:
Monthly infection waves became clearly visible through this summary.

---

## 3. Color Scales (Conditional Formatting)

Purpose:
Highlight areas with high and low numbers of cases.

Configuration:
3-Color Scale:
- Green → Lower case counts
- Yellow → Moderate case levels
- Red → Higher case counts

Insight:
Color variation helped quickly identify clusters of infection.

---

## 4. Sparklines (Trend Visualization)

Purpose:
Show weekly trends of new cases for each country.

Steps:
1. Insert → Line Sparkline.
2. Select the weekly data range.
3. Enable markers for highest and lowest points.

Insight:
Provided a quick comparison of case trends across different years.

---

## 5. Data Bars (Visual Indicators)

Purpose:
Provide graphical representation of monthly case totals.

Steps:
1. Select pivot values.
2. Apply Conditional Formatting → Data Bars.
3. Choose gradient or solid fill styles.

Insight:
Monthly waves of infections became easier to identify visually.

---

## Result
The raw COVID dataset was transformed into:
- Weekly and monthly summary tables
- Visual trend indicators
- Pattern recognition tools
- Comparative insights across countries and time periods

---

# Data Preparation using Shell Commands

## 1. File Retrieval
Downloaded a web server log dataset using the `curl` command.

Result:
A compressed dataset ready for processing.

---

## 2. File Decompression
Used `gzip` to convert the `.gz` archive into a readable log file.

Transformation:
Compressed archive → Plain text dataset.

---

## 3. Data Inspection
Used `head` and `tail` commands to examine sample lines.

Purpose:
Understand the structure of the log entries.

---

## 4. Record Counting
Used the `wc -l` command to determine the total number of entries.

Insight:
Number of requests recorded during the selected period.

---

## 5. Field Extraction
Applied the `cut` command to isolate specific columns.

Example:
Extracted IP addresses from the first column.

Transformation:
Multi-field log → Single-column dataset.

---

## 6. Sorting and Frequency Analysis
Executed a command pipeline:

```
cut → sort → uniq → sort
```

Transformation:
Raw IP list → Ranked list based on request frequency.

Insight:
Highlighted which IP addresses generated the most traffic.

---

## 7. Pattern Detection
Used the `grep` command with search patterns.

Purpose:
Identify automated bot traffic such as Googlebot.

---

## 8. Log Format Conversion
Used `sed` to modify brackets and formatting.

Transformation:
Original log structure → CSV-like format suitable for analysis.

---

# Data Preparation using a Text Editor

## 1. JSON Formatting
Reformatted compact JSON into a readable hierarchical structure.

Transformation:
Compressed JSON → Structured JSON layout.

Purpose:
Improved readability and easier navigation.

---

## 2. Field Extraction
Used multi-cursor selection to extract attributes like **City** and **Product**.

Transformation:
Complete dataset → Individual attribute lists.

---

## 3. Data Sorting
Sorted extracted city names alphabetically.

Transformation:
Unorganized list → Ordered dataset.

Purpose:
Help detect duplicates more easily.

---

## 4. Duplicate Removal
Removed repeated entries using the editor’s duplicate removal feature.

Transformation:
Repeated values → Unique value list.

---

## 5. Data Standardization
Corrected inconsistent spellings using multi-cursor editing.

Example:
Different spellings of Bangalore standardized to **Bangalore**.

Purpose:
Ensure consistent categorical data.

---

# Data Cleaning with OpenRefine

## 1. Dataset Import
Loaded the dataset into an OpenRefine project.

Transformation:
External file → OpenRefine working environment.

---

## 2. Frequency Analysis
Used **Text Facet** to examine value frequencies within columns.

Purpose:
Identify repeated or inconsistent entries.

---

## 3. Similarity Detection
Applied clustering algorithms to group similar text values.

Example:
"XYZ Limited" and "XYZ Ltd" were grouped together.

---

## 4. Entity Resolution
Merged clustered records into a single standardized value.

Transformation:
Multiple variations → One unified entry.

---

# Data Profiling using Pandas Profiling

## 1. Dataset Import
Loaded the dataset into a pandas DataFrame.

Transformation:
Raw data → Structured DataFrame.

---

## 2. Automated Profiling
Generated a dataset report using the Pandas Profiling library.

Transformation:
Dataset → Comprehensive analytical report.

---

## 3. Distribution Analysis
Visualized distributions for categorical and numerical variables.

Examples:
- Frequency of countries
- Distribution of city populations

---

## 4. Outlier Detection
Detected unusually large or small values in numerical variables.

Examples:
- Chongqing with extremely high population
- Manila with very high population density

---

## 5. Missing Value Analysis
Examined columns with significant missing data.

Example:
Metropolitan population column contained nearly 50% missing values.

---

## 6. Correlation Analysis
Generated a correlation matrix to analyze relationships between variables.

Purpose:
Identify strongly related variables.

---

# JSON API Data Analysis with Python

## 1. API Data Retrieval
Fetched JSON data from the Homebrew API.

Transformation:
Remote JSON response → Python objects.

---

## 2. JSON Formatting
Formatted JSON output for easier readability.

Purpose:
Understand the structure of returned data.

---

## 3. Dynamic URL Generation
Constructed package-specific URLs using package names.

Transformation:
Package list → Individual API endpoints.

---

## 4. Data Extraction
Parsed nested JSON structures to extract installation statistics.

Example:
Install counts for 30, 90, and 365 days.

---

## 5. Data Aggregation
Combined extracted data into structured dictionaries.

Transformation:
Multiple API responses → Organized dataset.

---

## 6. Data Storage
Saved processed results to a JSON file.

Purpose:
Avoid repeated API requests and speed up future analysis.

---

## 7. Data Sorting
Sorted packages based on installation counts.

Transformation:
Unordered dataset → Ranked popularity list.

---

# Image Processing with Pillow

## 1. Image Loading
Opened image files in Python using the Pillow library.

Transformation:
Image files → Python image objects.

---

## 2. Format Conversion
Converted images between formats.

Example:
JPEG → PNG.

---

## 3. Batch Processing
Applied loops to process multiple images in a directory.

Transformation:
Single image processing → Automated batch workflow.

---

## 4. Image Resizing
Generated thumbnails with specific dimensions.

Example:
300px and 700px image sizes.

Purpose:
Optimize images for web applications.

---

## 5. Image Rotation
Rotated images by specified angles.

Example:
90-degree rotation.

---

## 6. Color Conversion
Converted colored images into grayscale.

Purpose:
Create black-and-white versions for analysis.

---

## 7. Image Filtering
Applied effects such as Gaussian blur.

Purpose:
Modify the visual appearance of images.

---

# Media Processing with FFMPEG

## 1. Format Conversion
Converted multimedia files between formats.

Example:
AVI → MP4.

Purpose:
Ensure compatibility across different platforms.

---

## 2. Quality Adjustment
Adjusted video quality using quantizer or CRF parameters.

Purpose:
Balance video clarity with file size.

---

## 3. Bitrate Configuration
Specified audio and video bitrate values.

Example:
Video bitrate set to **1000k**.

Purpose:
Control compression level and playback quality.

---

## 4. Audio Processing
Applied audio filters including:

1. Volume adjustments  
2. Channel remapping  

Purpose:
Enhance or modify audio output.

---

## 5. Video Editing
Applied video filters such as:

1. Cropping  
2. Scaling  
3. Rotation  

Purpose:
Modify video dimensions and orientation.
