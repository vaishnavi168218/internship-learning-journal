# Excel Data Cleaning and Transformation

## Dataset Overview
- **Source:** Wikipedia city population dataset  
- **Columns:** City Name, Country, Population Estimates, City Definition (Municipality / Capital / Autonomous), Area, etc.  
- The dataset contains a **combination of text and numeric values**, which required cleaning and formatting before performing analysis.

---

# Data Cleaning in Excel

## 1. Find and Replace

**Purpose:** Remove unwanted text such as `[more]` appearing in the *Country* column.

### Steps
1. Select the dataset or the specific column.
2. Press **Ctrl + H** to open the **Find and Replace** window.
3. Enter `[more]` in the **Find what** field.
4. Leave the **Replace with** field blank.
5. Click **Replace All**.
6. Verify the number of replacements performed.

---

## 2. Convert Data Types

**Purpose:** Ensure numeric values are stored as numbers instead of text.

### Steps
1. Select numeric columns (for example **E to N**).
2. Go to the **Home** tab.
3. Change the format from **General** to **Number**.
4. Adjust decimal places if required.

---

## 3. Remove Extra Spaces with TRIM()

**Purpose:** Clean unnecessary spaces from text values.

### Steps
1. Insert a new column next to the original column.
2. Use the formula:

```
=TRIM(D2)
```

3. Drag the formula down to apply it to all rows.
4. Replace the original column with the cleaned data if necessary.

---

## 4. Remove Blank Rows

**Purpose:** Delete rows where important fields are empty.

### Steps
1. Select the column that should contain values.
2. Go to **Home → Find & Select → Go To Special**.
3. Choose **Blanks**.
4. Right-click a highlighted blank cell.
5. Select **Delete → Entire Row**.

---

## 5. Remove Duplicates

**Purpose:** Keep only unique country entries.

### Steps
1. Copy the **Country** column to a new worksheet.
2. Select the column.
3. Go to **Data → Remove Duplicates**.
4. Confirm the column selection.
5. Excel will display how many duplicates were removed.

---

# Excel Data Transformation

## Step 1: Calculate Ratios

Two ratios were created to analyze population distribution:

- **Metro Area / City Area**
- **Metro Population / City Population**

Formulas were entered in the first row and applied to the remaining rows using **AutoFill**. Missing values were handled carefully to avoid incorrect calculations.

---

## Step 2: Create a Pivot Table

Steps:

1. Select the entire dataset.
2. Go to **Insert → Pivot Table**.
3. Place the Pivot Table in a **new worksheet**.

Pivot tables help summarize and explore large datasets efficiently.

---

## Step 3: Check Duplicate Records

To identify how often each country appears:

1. Drag **Country** to the **Rows** area.
2. Drag **Country** again to the **Values** area.
3. Change the calculation to **Count**.

This shows the number of records associated with each country.

---

## Step 4: Aggregate Numerical Data

The **City Proper Population** field was added to the **Values** section and summarized using **Sum**.

This provides the **total city population grouped by country**.

---

## Step 5: Detect Outliers

A **Pivot Chart (Bar Chart)** was created for visualization.

Steps:

1. Insert a Pivot Chart from the Pivot Table.
2. Apply filters by country.
3. Look for extreme values in:
   - Population
   - Density ratios

These unusually high values may indicate **outliers**.

---

# Converting Text to Columns in Excel

## Dataset Overview

- **Source:** U.S. Senate voting records copied from a website  
- All information was initially pasted into **a single column**, making the dataset unstructured.

Each record contained:

- Senator Name  
- Party  
- State  
- Vote (Yea / Nay / Not Voting)

The values were separated using the characters:

```
(
-
)
,
```

---

## Step 1: Split Using "("

1. Select the column.
2. Go to **Data → Text to Columns**.
3. Choose **Delimited**.
4. Select **Other** and enter `(`.
5. Click **Finish**.

Result: Senator names are separated from the remaining information.

---

## Step 2: Split Using "-"

Repeat the Text to Columns process using **"-"** as the delimiter.

Result: The **Party** column is separated.

---

## Step 3: Split Using ")"

Use **")"** as the delimiter.

Result: The **State** value is extracted.

---

## Step 4: Split Using ","

Select **Comma** as the delimiter.

Result: The **Vote** field is separated.

---

## Step 5: Final Formatting

- Remove unnecessary columns created during splitting.
- Add column headers:

```
Senator | Party | State | Vote
```

- Apply formatting for clarity and readability.
