# Excel Data Cleaning

## Text Transformations
- Removed the unwanted suffix **"[more]"** using the **Find & Replace** feature.
- Used the **TRIM()** function to eliminate extra internal spaces within text values.

## Structural Transformations
- Deleted rows containing blank values in important fields.
- Removed duplicate entries in the **Country** column to maintain unique records.

## Data Type Transformations
- Converted numeric columns from **General** format to **Number** format.
- Standardized numeric values to display **two decimal places**.

## Data Quality Improvements
- Corrected inconsistent text formatting.
- Ensured numeric values were interpreted correctly.
- Reduced redundant data entries.
- Removed incomplete rows to improve dataset reliability.

---

# Excel Data Transformation

## 1. Ratio Calculations

### A. Metro Area to City Area Ratio
**Formula used**

```
=G2/D2
```

**Purpose**

Measure the extent of metropolitan expansion compared to the core city boundary.

**Example Insight**

Tokyo’s metropolitan area is approximately **6 times larger** than its city area.

Some calculation errors occurred where metro area data was missing.

---

### B. Metro Population to City Population Ratio

**Formula used**

```
=F2/C2
```

**Purpose**

Compare metropolitan population with the population of the main city.

**Example Insight**

Tokyo’s ratio is approximately **2.76**, indicating a much larger population in the metro region.

The formula was applied to the entire column using **AutoFill (double-click)**.

---

### C. Density Comparison (Crowding Indicator)

This comparison was derived from the relationship between:

- **Metro Area / City Area Ratio**
- **Metro Population / City Population Ratio**

**Purpose**

Evaluate how population density differs between metropolitan areas and city centers.

---

## 2. Pivot Table Transformations

### Creating the Pivot Table

Steps:

1. Select the complete dataset.
2. Navigate to **Insert → Pivot Table**.
3. Place the Pivot Table in a **new worksheet**.

---

### A. Country-Level Aggregation

- Drag **Country** into the **Rows** section.
- Drag **Country** again into the **Values** section and set the calculation to **Count**.

**Purpose**

Identify how frequently each country appears in the dataset.

**Example**

- China appeared **20 times**.
- Angola appeared **once**.

---

### B. City-Level Aggregation

Steps:

- Place **City** below **Country** in the Rows area.
- Add **City Proper Population** to the **Values** section.
- Change aggregation to **Sum**.

**Output**

- Population totals at the **city level**.
- Aggregated population values at the **country level**.

---

## 3. Chart-Based Insights

A **bar chart** was generated from the Pivot Table.

Filters were applied to analyze individual countries such as **China** and the **United States**.

**Observations**

- In China, **Chongqing** and **Shanghai** showed the highest population values.
- In the United States, **Los Angeles** showed the highest crowding ratio.

---

# Text to Columns in Excel

## Structural Transformations

- Converted raw text from a **single column** into multiple structured columns.
- Extracted categorical fields from combined text strings.

---

## Delimiter-Based Transformations

Different delimiters were used to separate data fields:

| Delimiter | Extracted Field |
|-----------|----------------|
| "("       | Senator Name |
| "-"       | Party |
| ")"       | State |
| ","       | Vote Status |

---

## Data Structuring

- Converted unstructured web data into a structured tabular format.
- Created clear column headers for each field.
- Removed unnecessary columns created during the splitting process.

---

## Analytical Readiness

- Transformed scraped text into a **CSV-like dataset**.
- Enabled **sorting, filtering, and aggregation** operations.
- Prepared the dataset for further analysis or visualization.

---

# Data Aggregation in Excel

## 1. Weekly Aggregation with Pivot Table

### Objective

- Calculate the **sum of New Cases**
- Group results by **Country and Week**
- Separate results by **Year (2020 and 2021)**

### Pivot Configuration

- **Rows:** Location (Country)
- **Columns:** Week
- **Values:** Sum of New Cases
- **Filter/Grouping:** Year

### Insight

Revealed **weekly COVID-19 case trends across different countries**.

---

## 2. Monthly Aggregation with Pivot Table

### Objective

- Calculate **sum of New Cases**
- Group data by **Month and Country**
- Separate results by **Year**

### Pivot Configuration

- **Rows:** Year → Month
- **Columns:** Location
- **Values:** Sum of New Cases

### Insight

Highlighted **monthly waves of COVID-19 infections**.

---

## 3. Color Scales (Conditional Formatting)

### Purpose

Identify clusters of high and low infection rates.

### Configuration

3-Color Scale:

- **Green** → Low cases
- **Yellow** → Medium cases
- **Red** → High cases

### Insight

Allowed visual identification of infection waves and patterns.

---

## 4. Sparklines (Trend Visualization)

### Purpose

Display **weekly case trends** for each country.

### Steps

1. Insert → **Line Sparkline**
2. Select weekly aggregated values as the data range
3. Enable **High Point** and **Low Point** markers

### Insight

Provided quick comparison of trends across years, including **India’s peak around mid-2021**.

---

## 5. Data Bars (Visual Comparison)

### Purpose

Provide graphical representation of **monthly aggregated values**.

### Steps

- Select pivot table values
- Apply **Conditional Formatting → Data Bars**
- Use gradient or solid fills

### Insight

Made it easier to observe **peaks and declines in case counts across months**.

---

## Result

The raw COVID dataset was transformed into:

- Weekly and monthly aggregated summaries
- Visual trend indicators
- Cluster identification tools
- Comparative analysis across countries and years

---

# Data Preparation Using Shell Commands

## 1. File Retrieval

Downloaded the web log dataset from a remote server using the **curl** command.

**Result**

Obtained a compressed log file for analysis.

---

## 2. File Decompression

Used **gzip** to convert the compressed `.gz` file into a readable log file.

**Transformation**

Compressed file → Plain text log data.

---

## 3. Dataset Inspection

Used **head** and **tail** commands to preview the beginning and end of the dataset.

**Purpose**

Understand file structure without opening the entire dataset.

---

## 4. Record Counting

Used:

```
wc -l
```

**Purpose**

Determine the total number of requests recorded in the log file.

---

## 5. Field Extraction

Used the **cut** command to extract specific columns.

Example: Extracted **IP addresses** from the first column.

**Transformation**

Multi-field log file → Single-column IP dataset.

---

## 6. Sorting and Frequency Analysis

Command pipeline used:

```
cut → sort → uniq → sort
```

**Purpose**

Identify the number of requests generated by each IP address.

---

## 7. Pattern Detection

Used **grep** with regular expressions to identify bot traffic.

**Example**

Detected crawlers such as **Googlebot** and **Applebot**.

---

## 8. Log Format Conversion

Used **sed** to replace brackets with quotation marks.

**Transformation**

Web log format → CSV-like structured format suitable for analysis.

---

# Data Preparation Using a Text Editor

## 1. JSON Formatting

Formatted a compressed JSON dataset into a readable hierarchical structure.

**Transformation**

Compact JSON → Structured JSON.

---

## 2. Field Extraction

Extracted attributes such as **City** and **Product** using multi-selection editing.

**Purpose**

Focus analysis on specific variables.

---

## 3. Sorting Data

Sorted extracted city values alphabetically.

**Transformation**

Unordered list → Sorted dataset.

---

## 4. Duplicate Removal

Used editor commands to remove repeated lines.

**Result**

Generated a list of **unique city names**.

---

## 5. Data Standardization

Corrected spelling variations using multi-cursor editing.

**Example**

Different spellings of **Bangalore** were standardized.

**Purpose**

Ensure consistency in categorical values.

---

# Data Cleaning with OpenRefine

## 1. Dataset Import

Loaded the raw dataset into **OpenRefine**.

**Transformation**

External dataset → OpenRefine project environment.

---

## 2. Frequency Analysis

Used **Text Facets** to view frequency distribution of column values.

**Purpose**

Identify repeated or inconsistent entries.

---

## 3. Similarity Detection

Applied **Clustering algorithms** to detect similar records.

**Example**

- "XYZ Limited"
- "XYZ Ltd"

---

## 4. Entity Resolution

Merged clustered records into standardized entries.

**Transformation**

Multiple variations → Single consistent entity.

---

# Data Profiling with Pandas Profiling

## 1. Dataset Import

Loaded the dataset into a **pandas DataFrame**.

**Transformation**

Raw dataset → Structured DataFrame.

---

## 2. Automated Profiling

Generated a profiling report using **Pandas Profiling**.

**Output**

A comprehensive report summarizing dataset characteristics.

---

## 3. Distribution Analysis

The report visualized distributions for categorical and numerical variables.

**Examples**

- Country frequency distribution
- City population distribution

---

## 4. Outlier Detection

Highlighted extreme values in numerical variables.

**Examples**

- **Chongqing** identified as a population outlier
- **Manila** identified as an outlier for population density

---

## 5. Missing Value Analysis

Detected columns with missing data.

Example:

- **Metropolitan population** column contained roughly **50% missing values**.

---

## 6. Correlation Analysis

Generated correlation matrices between variables.

**Purpose**

Identify strong positive or negative relationships between features.
