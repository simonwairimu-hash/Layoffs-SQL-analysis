# 📉 Layoffs SQL Analysis
Clean, explore, and analyze global tech layoff data using SQL to derive trends, insights, and recommendations. Ideal for roles in data analytics, business intelligence, or data engineering.

## 🧠 Project Overview
This project processes a dataset of company layoffs, cleans inconsistencies, and investigates key patterns across time, industries, and regions. It showcases skills in:

SQL-based data cleansing and transformation

Exploratory data analysis (EDA) with advanced queries

Creating datasets suitable for dashboards or reports

## 🛠 Datasets
layoffs — Raw layoff records: company, location, industry, total layoffs, percentage, date, company stage, country, funds raised

## 🔧 Data Preparation & Cleaning
Staging Table Setup

Loaded raw data into layoffs_staging for safe transformations

Duplicate Detection & Removal

Used window functions (ROW_NUMBER() OVER (...)) to detect and squash duplicates

Data Standardization

Trimmed whitespace; harmonized industry tags (e.g., 'Crypto%'); normalized country names to consistent formats

Date Conversion

Transformed date strings to SQL DATE type

Null Imputation

Used self-joins to backfill missing industry values based on other entries from the same company

Cleanup

Dropped auxiliary columns (row_num) once done

Verified data consistency and preparation via validation queries

## 📊 Exploratory Data Analysis
Performed deep dives to answer business-relevant questions:

Full workforce layoffs (percentage_laid_off = 1), displaying by highest funding

Companies and industries with the largest total layoffs

Layoff incidence across dates, including yearly and monthly trends

Rolling monthly layoffs to track cumulative impacts

Layoffs by company × year, identifying major layoff events

### Sample query:

sql

**WITH Rolling_Total AS (
  SELECT DATE_FORMAT(`date`, '%Y-%m') AS `month`,
         SUM(total_laid_off) AS total_off
  FROM layoffs_staging2
  GROUP BY `month`
)
SELECT `month`, total_off,
       SUM(total_off) OVER (ORDER BY `month`) AS rolling_total
FROM Rolling_Total;*
## 💡 Key Insights
Spike in layoffs during key periods—highlighting economic downturns

Identified heavily affected companies and sectors, such as tech and consumer industries

Geographic concentration: US saw the bulk of job cuts from 2020–2023, often in startup-heavy cities

Post‑IPO companies saw outsized layoffs, despite ample funding—revealing strategic cost-cutting trends


### 🚀 Business Impact & Next Steps
Hiring & Workforce Planning: Understand layoff timing to support rehiring strategies

Investor Monitoring: Layoff trends signal market shifts and funding climate

Economic Planning: Data helps regional agencies mitigate job loss impacts

Scalable Extension: Pipeline can ingest new layoff data monthly, enabling trend tracking

### 🛠 Technologies
SQL (MySQL / SQL Server) — CTEs, window functions, string ops, date formatting

SQL best practices in data cleaning and validation
