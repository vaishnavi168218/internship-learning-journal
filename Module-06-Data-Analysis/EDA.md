# Exploratory Data Analysis (EDA): Correlation Analysis with Excel

## Overview
This tutorial demonstrates how to perform **correlation analysis** and basic **visual exploration** using Microsoft Excel on a COVID-19 dataset. Correlation analysis measures the **statistical relationship between two variables** and determines how strongly they are linearly related.

The dataset contains the following variables used in the analysis:
- `new_cases`
- `new_deaths`
- `new_vaccinations`

---

## What is Correlation?

Correlation measures the **degree of linear association between two variables**.

Correlation coefficient values range between:

| Value | Meaning |
|------|--------|
| +1 | Perfect positive correlation |
| 0 | No correlation |
| -1 | Perfect negative correlation |

Example:
- `0.84` → Strong positive correlation  
- `0.23` → Weak positive correlation  

---

## Dataset

The COVID-19 dataset contains daily records including:

| Column | Description |
|------|-------------|
| new_cases | Number of new COVID-19 cases reported |
| new_deaths | Number of new COVID-19 deaths reported |
| new_vaccinations | Number of vaccinations administered |

For this analysis, only these three columns are used.

---

## Step 1: Enable Excel Data Analysis ToolPak

1. Open **Excel**
2. Click **File**
3. Select **Options**
4. Go to **Add-ins**
5. In **Manage**, select **Excel Add-ins**
6. Click **Go**
7. Check **Analysis ToolPak**
8. Click **OK**

After enabling, the **Data Analysis** option appears in the **Data tab**.

---

## Step 2: Prepare the Dataset

Keep only the required columns:

new_cases  
new_deaths  
new_vaccinations  

Remove other columns to simplify the analysis.

---

## Step 3: Generate Correlation Matrix

Steps:

1. Go to **Data**
2. Click **Data Analysis**
3. Select **Correlation**
4. Click **OK**
5. Select the input range containing:

new_cases  
new_deaths  
new_vaccinations  

6. Check **Labels in First Row**
7. Select an **Output Range**
8. Click **OK**

---

## Correlation Matrix Example

| Variable | new_cases | new_deaths | new_vaccinations |
|---------|-----------|------------|------------------|
| new_cases | 1 | 0.84 | 0.31 |
| new_deaths | 0.84 | 1 | 0.23 |
| new_vaccinations | 0.31 | 0.23 | 1 |

---

## Interpretation

### New Cases vs New Deaths
- Correlation = **0.84**
- Indicates **strong positive correlation**
- When cases increase, deaths tend to increase.

### New Vaccinations vs New Deaths
- Correlation = **0.23**
- Indicates **weak positive correlation**
- Relationship exists but is not strong.

---

## Step 4: Visualize Using Scatter Plot

Scatter plots help visualize relationships between variables.

### Plot 1: New Cases vs New Deaths

Steps:

1. Select `new_cases` and `new_deaths`
2. Go to **Insert**
3. Select **Recommended Charts**
4. Choose **Scatter Plot**

Add a **Trendline**:

- Click **Chart Elements (+)**
- Select **Trendline**
- Format line:
  - Color: Red
  - Style: Solid dash
  - Increase thickness

Interpretation:

The upward slope shows **strong positive correlation**.

---

### Plot 2: New Vaccinations vs New Deaths

Steps:

1. Select `new_vaccinations` and `new_deaths`
2. Insert **Scatter Plot**
3. Add **Trendline**

Interpretation:

- Trendline slope is **less steep**
- Indicates **weaker correlation**

Observation:
- Early period: Low vaccinations, high deaths  
- Later period: Increased vaccinations correspond with reduced deaths  

---

## Key Insights

- **New Cases ↔ New Deaths**
  - Strong positive relationship
  - Increased cases are associated with increased deaths

- **New Vaccinations ↔ New Deaths**
  - Weak correlation
  - Vaccinations may contribute to lowering deaths but require deeper analysis

---

## Limitations

Correlation **does not imply causation**.

From this analysis alone, we **cannot conclude** that vaccinations directly reduced deaths. Further analysis such as:

- Regression analysis  
- Time-series analysis  
- Causal modeling  

is required.

---

## Tools Used

- Microsoft Excel  
- Excel Data Analysis ToolPak  
- Scatter Plot Visualization  

---

# Exploratory Data Analysis (EDA) for Regression using Excel

## Overview
Before performing regression analysis, it is important to conduct **Exploratory Data Analysis (EDA)** to understand the structure, patterns, and relationships in the dataset. In this tutorial, the **COVID-19 dataset** is explored to identify how different variables may influence the number of deaths.

The dataset used in the analysis has already been **cleaned** and contains only the relevant variables required for modeling.

---

## Dataset Variables

The following variables are used for the regression analysis:

| Variable | Type | Description |
|--------|------|-------------|
| new_deaths | Dependent Variable | Number of new COVID-19 deaths reported |
| new_cases_per_1000 | Independent Variable | Number of new cases per 1000 people |
| new_tests_per_1000 | Independent Variable | Number of new tests conducted per 1000 people |
| new_vaccinations_per_1000 | Independent Variable | Number of vaccinations administered per 1000 people |
| stringency_index | Independent Variable | Government policy strictness index |

The variables **new_cases**, **new_tests**, and **new_vaccinations** were divided by **1000** to simplify interpretation during regression analysis.

---

## Data Transformation

To make the regression coefficients easier to interpret, the following transformations were applied:

- `new_cases_per_1000 = new_cases / 1000`
- `new_tests_per_1000 = new_tests / 1000`
- `new_vaccinations_per_1000 = new_vaccinations / 1000`

This scaling ensures that regression coefficients represent the effect **per 1000 units** rather than per single unit.

---

## Purpose of EDA

The purpose of performing EDA before regression includes:

- Understanding the dataset structure
- Identifying important variables
- Observing possible relationships between variables
- Detecting unusual patterns or anomalies
- Preparing variables for regression modeling

---

## Observations from the Data

### 1. Relationship Between Cases and Deaths
A higher number of **new COVID-19 cases** tends to correspond with an increase in **new deaths**, indicating a likely positive relationship between these variables.

### 2. Relationship Between Testing and Deaths
The number of **tests conducted** may influence the detection of cases and indirectly impact the number of reported deaths.

### 3. Relationship Between Vaccinations and Deaths
Vaccination data is analyzed to observe whether an increase in vaccinations may correspond with a decrease in deaths.

### 4. Government Stringency Measures
The **stringency index** reflects the strictness of government policies such as lockdowns, travel restrictions, and social distancing rules. It is included to evaluate whether stricter policies impact the number of deaths.

---

## Preparing for Regression

After exploring the dataset, the following decisions were made for regression modeling:

- **Dependent Variable (Y):** new_deaths
- **Independent Variables (X):**
  - new_cases_per_1000
  - new_tests_per_1000
  - new_vaccinations_per_1000
  - stringency_index

Since multiple predictors are used, the analysis will use **Multiple Linear Regression**.

---

## Key Takeaways from EDA

- The dataset was cleaned and reduced to relevant variables.
- Important predictors related to COVID-19 outcomes were identified.
- Variables were scaled to improve interpretability.
- Relationships between variables were explored conceptually before modeling.

---

# Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) is the process of examining datasets to understand their structure, characteristics, patterns, and potential issues before applying statistical models or machine learning techniques.

EDA helps in identifying trends, relationships, anomalies, missing values, and data quality problems.

## Objectives of EDA

- Understand the overall structure of the dataset
- Identify important variables and their distributions
- Detect missing values and inconsistencies
- Discover relationships between variables
- Identify outliers and anomalies
- Generate insights for feature selection and modeling

## Data Inspection

Initial exploration includes examining dataset size, column names, and data types.

Typical steps:

- View first and last few records
- Check number of rows and columns
- Inspect data types (numeric, categorical, date/time)
- Verify data consistency

## Data Cleaning

Data cleaning ensures accuracy and reliability of analysis.

Key tasks:

- Handling missing values (removal or imputation)
- Removing duplicate records
- Correcting inconsistent entries
- Converting data types where necessary
- Standardizing formats

## Univariate Analysis

Univariate analysis examines each variable independently.

For numerical variables:

- Mean, median, mode
- Standard deviation and variance
- Minimum and maximum values
- Distribution shape (normal, skewed)

For categorical variables:

- Frequency counts
- Category proportions

Visualization methods:

- Histograms
- Bar charts
- Box plots

## Bivariate Analysis

Bivariate analysis studies relationships between two variables.

Techniques include:

- Scatter plots for numeric variables
- Correlation analysis
- Cross-tabulation for categorical variables
- Comparison of group statistics

Correlation coefficients indicate strength and direction of relationships.

## Multivariate Analysis

Multivariate analysis explores interactions among multiple variables simultaneously.

Common methods:

- Correlation matrices
- Pair plots
- Dimensionality reduction techniques
- Clustering analysis

This helps uncover complex patterns not visible in simpler analyses.

## Outlier Detection

Outliers are extreme values that differ significantly from other observations.

Detection methods:

- Interquartile Range (IQR) method
- Z-score method
- Box plots
- Visual inspection

Handling outliers improves model performance and prevents misleading conclusions.

## Data Visualization

Visualization is a key component of EDA because it reveals patterns that may not be apparent from numerical summaries.

Common visualization techniques:

- Line charts for trends over time
- Scatter plots for relationships
- Heatmaps for correlation analysis
- Box plots for distribution comparison
- Pie charts for categorical proportions

## Insights and Feature Selection

EDA helps identify:

- Important predictors
- Redundant variables
- Potential transformations
- Data preparation requirements

These insights guide the selection of features for modeling and improve predictive accuracy.
----
# Exploratory Data Analysis (EDA) — Forecasting Dataset

## Dataset Overview

Two datasets were analyzed:

1. Heights and Weights Dataset
   - Contains physical measurements of individuals
   - Variables: Height (inches), Weight (pounds)
   - Sample size used: ~1,000 records
   - Converted to metric units: centimeters and kilograms

2. Traffic Time-Series Dataset
   - Contains hourly vehicle counts at road junctions
   - Variables: Date/Time, Number of Vehicles
   - Used to study temporal patterns and seasonality

---

## Data Preparation

- Height converted from inches to centimeters using:
  Height (cm) = Inches × 2.54
- Weight converted from pounds to kilograms using:
  Weight (kg) = Pounds ÷ 2.204
- Decimal precision reduced for readability
- Data formatted for visualization and analysis

---

## Univariate Analysis

### Heights and Weights Dataset

- Heights ranged approximately from 160 cm to 185 cm
- Weights ranged approximately from 50 kg to 65 kg
- Values showed moderate spread with no extreme anomalies
- Distributions appeared roughly continuous

### Traffic Dataset

- Vehicle counts varied significantly across time
- Data showed high variability with sharp peaks and troughs
- Indicates non-uniform distribution

---

## Bivariate Analysis

### Height vs Weight Relationship

- Scatter plot revealed a strong positive relationship
- As height increases, weight also increases
- Relationship appears approximately linear
- Suitable for linear regression modeling

---

## Correlation Insights

- Positive correlation between height and weight
- Suggests weight can be predicted from height
- Supports use of linear forecasting methods

---

## Trend Analysis

### Heights and Weights

- No time component; trend reflects physical relationship
- Linear increase observed between variables

### Traffic Dataset

- Clear temporal patterns observed
- Daily cycles (peak and low traffic hours)
- Weekly patterns (weekday vs weekend differences)
- Holiday effects causing unusually low traffic

---

## Seasonality Detection

Traffic data exhibited strong seasonal behavior:

- Repeating patterns every 24 hours (daily cycle)
- Weekly periodic patterns
- Event-driven fluctuations (holidays)

Linear models fail to capture these repeating patterns.

---

## Outlier Analysis

### Heights and Weights

- No major outliers observed in the sample
- Data appears relatively consistent

### Traffic Dataset

- Occasional unusually high or low vehicle counts
- May correspond to accidents, events, or holidays

---

## Model Suitability Insights

- Linear regression suitable for height–weight prediction
- Linear forecasting ineffective for cyclical traffic data
- Time-series methods required for seasonal datasets

---

## Visualization Insights

- Scatter plot effectively revealed linear relationships
- Line charts exposed temporal fluctuations in traffic data
- Comparison plots showed differences between actual and predicted values

---

## Key Findings

- Physical measurement data shows stable linear relationships
- Time-series data exhibits strong seasonality and variability
- Choice of forecasting method must match data characteristics

---

