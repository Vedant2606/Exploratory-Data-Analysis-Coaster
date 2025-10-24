# **Roller Coaster Exploratory Data Analysis (EDA)**

## **🚀 Project Overview and Context**

This project delivers a comprehensive Exploratory Data Analysis (EDA) of a global roller coaster dataset (coaster\_db.csv). The primary objective was to thoroughly understand the data structure, ensure data quality, and extract meaningful insights into global roller coaster trends, performance metrics, and historical patterns.

The key deliverable of this analysis is a cleaned dataset suitable for downstream modeling and a set of data-driven insights related to roller coaster speed and height relationships.

## **🛠️ Technical Stack**

* **Language:** Python  
* **Data Manipulation:** Pandas  
* **Visualization:** Matplotlib, Seaborn  
* **Environment:** Jupyter Notebook (EDA in Python.ipynb)

## **1\. Data Sourcing, Import, and Initial Inspection**

This initial phase focused on acquiring the data and establishing its baseline quality and structure.

### **1.1 Data Import and Acquisition**

* The dataset was loaded from the provided source file: coaster\_db.csv.  
* The raw dataset dimensions were confirmed: **1087 rows and 56 columns**.

### **1.2 Initial Data Overview**

Initial inspection using methods like df.head(), df.dtypes, and df.describe() revealed:

* A significant number of columns (56 total), many of which contained redundant or sparsely populated measurements (e.g., multiple columns for speed and height units).  
* A mixed collection of data types, including object (strings/categorical), int64, and float64.

## **2\. Data Preparation and Quality Check (Wrangling)**

The raw data required significant cleaning, type conversion, and feature selection to create a high-quality analysis foundation.

### **2.1 Feature Selection and Reduction**

To focus the analysis on core performance and location metrics, the dataset was reduced from 56 columns to 13 essential features. Redundant and low-utility columns were proactively dropped.

The final selected features include: Coaster\_Name, Location, Manufacturer, Year\_Introduced, Speed\_mph, Height\_ft, Inversions, and Gforce.

### **2.2 Data Type and Format Standardization**

* The opening\_date\_clean column (renamed to Opening\_Date) was successfully converted from the object (string) type to the appropriate **datetime64\[ns\]** format to enable time-series analysis.  
* Relevant columns were standardized using PascalCase (Coaster\_Name, Speed\_mph, etc.) for improved readability.

### **2.3 Handling Missing Values**

Analysis using df.isna().sum() confirmed substantial missing data in key performance metrics:

* Height\_ft: 916 missing values  
* Gforce: 725 missing values

These missing values were handled appropriately during correlation and specific feature analyses by filtering out nulls (dropna()) on a case-by-case basis.

### **2.4 Deduplication**

A critical data quality check was executed to identify and remove duplicate entries based on the key identifying features: \['Coaster\_Name', 'Location', 'Opening\_Date'\].

* **97 duplicate rows** were identified and successfully removed.  
* The final cleaned dataset contains **990 rows and 13 columns**, ready for analysis.

## **3\. Exploratory Data Analysis (EDA)**

This phase focused on visualizing and summarizing the key characteristics of the cleaned dataset.

### **3.1 Univariate Distribution Analysis**

| Feature | Insight | Visualization Used |
| :---- | :---- | :---- |
| **Year Introduced** | The year **1999** saw the highest number of new roller coaster introductions globally. | Bar Plot |
| **Speed (mph)** | Coaster speeds are heavily clustered around **50 mph**, with a long-tail distribution indicating a few extreme-speed coasters. | Histogram and KDE Plot |
| **Coaster Type (Type\_Main)** | The vast majority of coasters are **Steel** (728), followed by **Wood** (191). | Value Counts |

### **3.2 Bivariate and Multivariate Relationship Analysis**

* **Correlation Heatmap:** A correlation matrix confirmed a **strong positive correlation between Speed\_mph and Height\_ft**. This is an expected and statistically significant relationship within the coaster design dataset.  
* **Scatter Plots:** Visual inspection using scatter plots further confirmed the linear positive trend between speed and height. By introducing Year\_Introduced as a hue, the analysis demonstrated a consistent increase in both speed and height over time.  
* **Pair Plots:** A holistic view of key numerical variables (Speed, Height, Inversions, Year) segmented by Type\_Main (Steel/Wood) provided simultaneous insights into how different coaster material types relate to performance metrics.

## **4\. Key Insight: Average Speed by Location**

To answer the business question, "What are the locations with the fastest roller coasters?", a targeted analysis was performed:

1. Coasters were grouped by Location.  
2. The calculation required that a location have a minimum of **10 coasters** to be included in the ranking (to ensure statistical relevance).  
3. The locations were ranked by their **mean Speed\_mph**.

The resulting horizontal bar chart visually presented the locations with the highest average roller coaster speeds.

## **5\. 🎯 Key Findings and Next Steps**

### **Key Findings**

* **Data Quality:** Significant effort was required for deduplication and handling missing data, particularly in Height\_ft and Gforce.  
* **Design Trend:** There is a clear and strong positive correlation between a roller coaster's speed and its height, which has generally increased across all coaster types over time.  
* **Historical Peak:** The year 1999 was a peak year for new coaster introductions.

### **Next Steps**

1. **Imputation:** Explore robust imputation techniques (e.g., K-Nearest Neighbors) to fill in the missing Height\_ft and Gforce values, allowing for a complete dataset for modeling.  
2. **Predictive Modeling:** Use the cleaned data to build regression models to predict Speed\_mph based on features like Height\_ft, Manufacturer, and Type\_Main.  
3. **Time Series Analysis:** Further analyze the Year\_Introduced and Opening\_Date features to model the historical growth rate and predict future coaster introduction rates.