# Ontario_Economic_Trends
## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](data-cleaning)
- [Exploratory Data Analysis](exploratory-data-analysis)
- [Data Analysis](data-analysis)
- [Results/Findings](results/findings)

  
Exploring current and long-term economic trends to provide businesses and policymakers with a better understanding of their implication for the province 

### Project Overview
YEE

### Data Sources
Ontario Economic Accounts provides a querterly assesment on the current state of Ontario economy. This data set includes historical data that offers data spanning from January 1, 1981 to June 30, 2024. This dataset offers comprehensive insight into various economic indicators for Ontario. Each year is broken down by quarters to meausure the parameters. 

### Tools

- Excel - Data Cleaning, Pivot Chart 
- SQL Bigquery - Data Analysis
- Tableau - Creating Reports

### Data Cleaning 
In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection. 
2. Handled missing values.
3. Rounded lengthy numbers.
4. Checked for duplicates.
5. Made sure column header descriptions were descriptive and unique.

### Exploratory Data Analysis
EDA involved exploring the Fitbit data to answer key questions, such as:
1. Is there a significant correlation between employee compensation and GDP growth?
2. What are the trends in gross and net mixed income over the years? 
3. What is the relationship between taxes less subsidies and the GDP at market prices?
4. How has the Gross Domestic Product (GDP) at market prices changed year-over-year?
5. How has the consumption of fixed capital for corporations, government, nonprofit institutions, and unincorporated businesses changed over the years?
6. IDDDKDKDKDKD

### Data Analysis

The Data analysis was done in Excel and SQL. 

#### Excel
I downloaded the dataset in excel and made sure there were no duplicates, nulls or outliers. I also shortened the names of the columns since they were very long. The columns that have been shorteded are as follows: 
1. Gross Domestic Product at market prices: GDP_Market_Prices
2. Compensation of employees (domestic basis): Employee_Comp
3. Gross mixed income: Gross_Mixed_Income
4. Net mixed income: Net_Mixed_Income
5. Gross operating surplus: Gross_Op_Surplus
6. Net operating surplus: corporations: Net_Corp_Surplus
7. Consumption of fixed capital: corporations: Corp_Fixed_Cap
8. Consumption of fixed capital: government and nonprofit institutions: Gov_Nonprofit_Fixed_Cap
9. Consumption of fixed capital: unincorporated businesses: Unincorp_Fixed_Cap

The other columns used from this dataset are year and quarter. 

#### SQL 
In SQL I uploaded our fitbit data to do exploratory data analysis. The queries are shown and explained below and the results from these queries are presented and explained in the results/findings section. 

The first query I made was to see if there was a significant correlation between employee compensation and GDP growth. I first started by selecing the year because I wanted to see the trends in GDP from 1981 to 2024. Then I used SUM(GDP_Market_prices) to sum the GDP for all quarters within a year. I did the same for Employee_Comp. I used GROUP BY  so that the results are grouped by year which allows SUM to aggregate GDP for each year. 

``` SQL
SELECT ` Year`, SUM(GDP_Market_prices ) AS Total_GDP, SUM(Employee_Comp) AS Total_Employee_Comp
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
The next query is to examine the trends in gross and net mixed income over the years. To do this I first made sure to select year so we can get then use GROUP BY "year" to group the results by year. I also used SUM for Gross_mixed_income and for Total_gross_mixed_income and gave each of these variables an alias. 
``` SQL
SELECT ` Year`, SUM(Gross_mixed_income) AS Total_Gross_mixed_income, SUM(Net_mixed_income) AS Total_Net_mixed_income
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
In this query I wanted to see the relationship between taxes less subsidies and the GDP at market prices. The query for this was the same as the prevous one except that Gross_mixed_income and Net-Mixed_income are used instead. This query was also grouped by the year and the ORDER BY was used to sort the results by year in ascending order. 
``` SQl
SELECT ` Year`, SUM(GDP_Market_prices ) AS Total_GDP, SUM(Taxes_less_subsidies) AS Total_Taxes_less_subsidies
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
The next three queries are similar in how they are written. the first query is to see how the the Gross Domestic Product at market prices changes year over year. This query is very simple as all we have to do is select the year and SUM the GDP_Market_Prices. We also cant forget to group and order by the year. The same query structure is followed with the following two queries. In the second query I am trying to figure our trends in gross and net operating surplus for corpoorations over the years. I used the SUM function on both 'Gross_Op_Surplus' and 'Net_Corp_Surplus' to sum the total for each year. The last query is to look at how the consumption of fixed capital for corporations, government, nonprofit institutions, and unincorporated businesses changed over the years. The SUM function was used again in this query to SUM the 'Corp_Fixed_Cap', 'Gov_Nonprofit_Fixed_Cap', and the ' Unincorp_Fixed_Cap'. The GROUP BY function was used to group the aggregated results by the year. 

``` SQL
SELECT ` Year`, SUM(GDP_Market_prices ) AS Sum_GDP
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
```SQL
/*Question Six */
SELECT ` Year`, SUM(Gross_Op_Surplus) AS Total_Gross_Op_Surplus, SUM(Net_Corp_Surplus) AS Total_Net_Corp_Surplus
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
```SQL
SELECT  ` Year`, SUM(Corp_Fixed_Cap) AS Total_Corp_Fixed_Cap, SUM(Gov_Nonprofit_Fixed_Cap) AS Total_Gov_Nonprofit_Fixed_Cap,
SUM(` Unincorp_Fixed_Cap`) AS Total_Unincorp_Fixed_Cap
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
### Results/Findings
The analysis results are summarized as follows:
1. This graph  <img width="1612" alt="Q1" src="https://github.com/user-attachments/assets/d9931861-830c-4032-95e5-d260396104e4" />
2. <img width="1606" alt="Q2" src="https://github.com/user-attachments/assets/c6b0768b-23df-4777-bfa3-a59ff3d4fd29" />
3. <img width="1612" alt="Q3" src="https://github.com/user-attachments/assets/c4be77e6-608c-48b3-a650-da36fd42c027" />
4. <img width="1536" alt="Q5" src="https://github.com/user-attachments/assets/ad63d7e2-1946-46c7-b634-23340aba5a44" />
5. <img width="1610" alt="Q7" src="https://github.com/user-attachments/assets/aa5b9385-3acb-4f99-b722-151bc35c3875" />



