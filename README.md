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
Ontario Economic Accounts provides a quarterly assessment of the current state of Ontario economy. This data set includes historical data that offers data spanning from January 1, 1981 to June 30, 2024 and can be found [here](https://www.kaggle.com/datasets/noeyislearning/ontario-economic-accounts/data?select=gross_domestic_product_income_based.csv). This dataset offers comprehensive insight into various economic indicators for Ontario. Each year is broken down by quarters to measure the parameters. 

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

### Data Analysis

The Data analysis was done in Excel and SQL. 

#### Excel
I downloaded the dataset in excel and made sure there were no duplicates, nulls or outliers. I also shortened the names of the columns since they were very long. The columns that have been shortened are as followed: 
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
I uploaded the cleaned Ontario Economic Accounts data to SQL to do exploratory data analysis. The queries are shown and explained below and the results from these queries are presented and explained in the results/findings section. 

The first query I made was to see if there was a significant correlation between employee compensation and GDP growth. I first started by selecting the year because I wanted to see the trends in GDP from 1981 to 2024. Then I used SUM(GDP_Market_prices) to sum the GDP for all quarters within a year. I did the same for 'Employee_Comp'. I used GROUP BY so that the results are grouped by year which allows SUM to aggregate GDP for each year. 

``` SQL
SELECT ` Year`, SUM(GDP_Market_prices ) AS Total_GDP, SUM(Employee_Comp) AS Total_Employee_Comp
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
The next query is to examine the trends in gross and net mixed income over the years. To do this I selected 'year' and then used GROUP BY 'year' to group the results by year. I also used SUM for 'Gross_mixed_income' and for 'Total_gross_mixed_income' and gave each of these variables an alias. 
``` SQL
SELECT ` Year`, SUM(Gross_mixed_income) AS Total_Gross_mixed_income, SUM(Net_mixed_income) AS Total_Net_mixed_income
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
In this query I wanted to see the relationship between taxes less subsidies and the GDP at market prices. The query for this was the same as the previous query stated above, except that Gross_mixed_income and Net-Mixed_income are used instead. This query was also grouped by the year and the ORDER BY was used to sort the results by year in ascending order. 
``` SQl
SELECT ` Year`, SUM(GDP_Market_prices ) AS Total_GDP, SUM(Taxes_less_subsidies) AS Total_Taxes_less_subsidies
FROM `axial-keep-445022-e1.Ontario_Economics.Ontario_data`  
GROUP BY 1
ORDER BY 1;
```
The next three queries are similar in how they are written. The first query is to see how the Gross Domestic Product at market price changes year over year. This query is very simple as all we have to do is select the year and SUM the ‘GDP_Market_Prices’. We also can't forget to group and order by the year. The same query structure is followed with the following two queries. In the second query I am trying to figure out trends in gross and net operating surplus for corporations over the years. I used the SUM function on both 'Gross_Op_Surplus' and 'Net_Corp_Surplus' to sum the total for each year. The last query is to look at how the consumption of fixed capital for corporations, government, nonprofit institutions, and unincorporated businesses changed over the years. The SUM function was used again in this query to SUM the 'Corp_Fixed_Cap', 'Gov_Nonprofit_Fixed_Cap', and the ' Unincorp_Fixed_Cap'. The GROUP BY function was used to group the aggregated results by the year.  
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
1. This first scatter plot shows the correlation between employee compensation and GDP growth. Total GDP is on the x-axis and on the Y-axis we have "Total Employee Compensation". We can see on the graph there is a positive correlation. This positive correlation suggests that as employee compensation increases, GDP also tends to increase. The cause of this correlation is not known however, since correlation does not imply causation. We can infer that greater overall economic output and productivity is associated with higher employee compensation. A cause for this could be that higher employee compensation leads to more disposable income. This increase in disposable income then increased consumer spending which then contributes to a higher GDP. Higher wages can also increase employee morale, which would then increase productivity and efficiency.    <img width="1612" alt="Q1" src="https://github.com/user-attachments/assets/d9931861-830c-4032-95e5-d260396104e4" />
2. In the next graph we have two line charts that show the the trends in gross and net mixed income over the years. The data starts in 1981 and ends in the second quarter of 2024. We can see that both of these charts have a line with an upward trajectory as the years pass by. This consistent upward trend indicates overall long term economic growth. This stability in the economy implies that self employed individuals and unincorporated businesses have been generating more and more income throughout the years. The gradual increase of net mixed income is a positive sign of businesses practicing long-term planning by investing and maintaining their capital assets effectively. Economic policies that support small business and entrepreneurs such as tax incentives and access to credit could be fostering development.     <img width="1606" alt="Q2" src="https://github.com/user-attachments/assets/c6b0768b-23df-4777-bfa3-a59ff3d4fd29" />
3. In the next graph we are analyzing the correlation between taxes less subsidies and GDP at market price. The graph shows a positive correlation which would indicate that as taxes less subsidies increases, so does GDP. We do have to remember that correlation does not mean causation and there can be outside policies and economic factors that could influence this. An increased revenue from Taxes less subsidies is crucial for funding various government programs and services which can further stimulate the economy.   <img width="1612" alt="Q3" src="https://github.com/user-attachments/assets/c4be77e6-608c-48b3-a650-da36fd42c027" />
4. For the next bar chart we can see the year over year change in the GDP Market. This chart starts in 1981 and ends in 2024. We can see there is a steep drop at 2024 since we do not have the data for the third and fourth quarters of 2024. We can see that there is a steady increase in the GDP which suggests strong and consistent economic growth. There are some dips in which growth is not as prominent compared to other years. These growth curves are signs of when Ontario has had economic recessions. The first recession we are able to see with a decline in GDP growth is the early 1990s followed by the great recession that started in 2008. Ontario has been able to recuperate from both of these recessions rather quickly. We can see that for the 2020 economic recession due to the covid-19 pandemic, Ontario was able to bounce back in 2021 with higher GDP than in 2019 and 2020. This further indicates Ontario has a strong and resilient economy..  <img width="1536" alt="Q5" src="https://github.com/user-attachments/assets/ad63d7e2-1946-46c7-b634-23340aba5a44" />
5. The last chart shows the changes in the consumption of fixed capital over the years. It has three charts, all starting in 1981 and ending in 2024. The first graph is for the consumption of fixed capital: corporations, the second one is the consumption of fixed capital:government and nonprofit institutions, and the third one is the consumption of fixed capital: Unincorporated Businesses. All three graphs show a generally positive trend, which indicates overall economic growth. These trends in the consumption of capital can be signals of a healthy economy. If we look at the GDP Chart we can see a similar positive trend. As we saw before, higher GDP is positively correlated with higher Taxes less subsidies and employee compensation. As GDP, taxes and employee comp increase, the opportunity and need for investments in fixed assets like building, machinery and equipment increase as well. All of which could then yield GDP growth. As corporations and small businesses see this circle of investment, it encourages investors to reinvest. <img width="1610" alt="Q7" src="https://github.com/user-attachments/assets/aa5b9385-3acb-4f99-b722-151bc35c3875" />



