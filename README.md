# Project : Data Analysis for Sales Insights of AtliQ Hardware
## Table of Contents:
-	[Problem Statement](#problem-statement)
-	[Data Discovery](#data-discovery)
-	[Data Analysis using MySQL](#data-analysis-using-mysql)
-	[Data Cleaning](#data-cleaning) 
-	[Build Dashboard Using Tableau](#build-dashboard-using-tableau)
-	[Tools Used](#tools-used)
-	[References](#references)
## Problem Statement 
In this project, we performed a data analysis for AtliQ Hardware, an India-based company that supplies computer hardware and peripherals to various clients, including surge stores and Nomad stores, across the country. AtliQ Hardware's head office is located in Delhi, India, with several regional offices throughout the country.
The sales director of AtliQ Hardware is facing challenges due to the dynamic growth of the market. He is having issues tracking sales in this rapidly changing market, and overall sales have been declining. The company has regional managers for North India, South India, and Central India. However, the communication about sales insights from these regions to the sales director has been mainly verbal, without any factual proof or data visualization. This lack of clear insights has frustrated the sales director, as he is unable to get a complete picture of the business's performance. To address this issue, the sales director is looking for a simple data visualization tool that he can access daily to make data-driven decisions and increase sales.
In this project, we will help the company create its own sales dashboard using Tableau, enabling them to visualize their sales data and make informed decisions to improve their business performance.
## Data Discovery 
### •	Project Planning using AIMS Grid -
It is a project management tool which consists of four components-
o	Purpose - (What to do exactly)
o	Stackholder - (Who will be involved)
o	End result - (What do you want to achieve)
o	Success Criteria - (Cost optimization and time save)
### •	AIMS Grid -
#### 1. Purpose :-
To unlock sales insights that are not visible before for the sales them for decision support and automate them to reduced manual time spent in data gathering.
#### 2. Stakeholders :-
-	Sales Director
-	Marketing Team
-	Customer Service Team
-	Data and Analytics Team
-	IT
#### 3. End result :- 
An automated dashboard providing quick and latest sights in order to support Data driven decision making.
#### 4. Success Criteria :-
-	Dahboard uncovering sales order insights with latest data available
-	Sales team able to take better decisions and prove 10% cost saving of total spend.
-	Sales analysis stop data gathering manually in order to save 20% business time andreinvest it value added activity.
## Data Analysis using MySQL 
Completed the Data discovery and then used mySQL for data analysis.
SQL database dump is in db_dump.sql file above. Download db_dump.sql file to your local computer
•	Importing Data to MySQL workbench
![atliq data import](https://github.com/ektad08/Sales-Insights/assets/161217589/363d4da7-576c-439d-889e-54b1db693561)

The import of data is done from an already existing MySQL file. This file has to be loaded into MySQL workbench for further data analysis.
Then go to Navigator panel, under schemas you will see sales. Right click on sales and select, set as default schemas.
-	Analysis of data by looking into different tables and reflecting garbage values
We can see that garbage value that the table market contains certain values which are incorrect.
```sql
SELECT * FROM market;
```
And then we can check that transaction table we can see that certain negative value in amount which is not possible. and we can see that certain transactions are in USD. Hence, filtration of that is also needed by converting into INR.
```sql
SELECT * FROM transactions;
```
-	Analysis of different SQL statement on data base
1.	To find of all customers records
```sql
SELECT * FROM customers;
```
2.	To find total number of customers
```sql
SELECT count(*) From customers;
```
3.	To find transactions for Chennai market (market code for chennai is Mark001
 ```sql
SELECT * FROM transactions where market_code='Mark001';
```
4.	To find distrinct product codes that were sold in chennai
   ```sql
SELECT distinct product_code FROM transactions where
market_code='Mark001';
```
5.	To find transactions for Mumbai market (market code for chennai is Mark002
   ```sql
SELECT * FROM transactions where market_code='Mark002';
```
6.	To find distrinct product codes that were sold in mumbai
```sql
SELECT distinct product_code FROM transactions where market_code='Mark002';
```
7.	To find transactions where currency is US dollars
```sql
SELECT * from transactions where currency="USD";
```
8.	Show transactions in 2020 join by date table
```sql
SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;
```
9.	Show total revenue in year 2020
```sql
SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date
ON transactions.order_date=date.date where date.year=2020 and
transactions.currency="INR\r" or transactions.currency="USD\r";
```
10.	Show total revenue in year 2020, January Month
```sql
SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date
ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and
(transactions.currency="INR\r" or transactions.currency="USD\r");
```
11.	Show total revenue in year 2020 in Chennai
```sql
SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date
ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";
```
## Data Cleaning 
In this process, we are work on data cleaning and ETL.
Step 1: Connect the MySQL database with the Tableau desktop.
Step 2: Loading data into the Tableau. 
#### ![tableau relationship](https://github.com/ektad08/Sales-Insights/assets/161217589/9fe82d7a-908b-4adb-872c-d23042107b7a)
Setp 3: Transform data 
- Here we can see that we have some zero and negative values in sales amount column, which is garbage value as sales amount should at least be 1 and be a positive number.
Go to Data &rarr; select Edit Data Source Filters &rarr; Add &rarr; Sales Amount &rarr; At Least &rarr; fill value 1 &rarr; hit Ok

- Now at the market code column, since the company is india based we need to remove New York and Paris which are not Indian location.
Go to Data &rarr; select Edit Data Source Filters &rarr; Add &rarr; Market code &rarr; uncheck Market code 097 and Market code 099 &rarr; hit Ok

- Convert USD into INR in the transaction’s table: the AtliQ Hardware only works in India so the USD values are not possible. we need to convert those USD values into INR by using Calculated Fields. 
Click on the arrow above sales amount &rarr; create Calculated Field &rarr; name it Normalised Amount &rarr; write formula &rarr; IF [currency]==’USD’ THEN [Sales Amount] x 74 ELSE [Sales Amount] END &rarr; Ok
New Column ‘Normalised Amount’ is created
## Build Dashboard using Tableau
#### Revenue Analysis
#### ![Revenue Dashboard](https://github.com/ektad08/Sales-Insights/assets/161217589/e68a39e3-fdfb-46ed-a151-f79f8b89bc1c)
#### Profit Analysis
#### ![Profit Analysis](https://github.com/ektad08/Sales-Insights/assets/161217589/f6b687a1-f7a6-4c2f-8e62-ead97ff54ae7)

## Tools Used
-	MySQL Workbench 8.0.36 
-	Tableau 2024.1.0 
-	Excel version 2021

## References
- https://codebasics.io/panel/webinars/purchases
- https://dev.mysql.com/doc/










