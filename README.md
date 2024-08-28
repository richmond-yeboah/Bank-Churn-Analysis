# Bank Churn Analysis


# Introduction
Customer Churn (or customer attrition) refers to the rate at which customers discontinue their association with a business during a specified timeframe. In simpler terms, it quantifies the loss of customers previously engaged with a company’s products or services.
Companies and businesses need to know why customers are churning to implement measures to sustain or keep the customers satisfied enough to stay.
This project dives into a customer churn dataset from ABC multinational bank to unveil hidden insights and identify trends to help business leaders make data-driven decisions and not just guesswork.

# Dataset
This dataset contains 10,000 rows and 12 columns namely;
Customer ID, credit score, country, gender, age, tenure, balance, products, credit card (1 for yes and 0 for no), active member (1 for yes and 0 for no), estimated salary and churn (1 for yes and 0 for no).

# Data Collection and Preparation
I connect to, clean, and transform the raw data in Power Query to make it ideal and ready for data modeling and analysis. I import the data locally as I have already downloaded it.
 
Since the values in the ‘estimated salary’ column are estimated, I removed that column because it is not relevant to this analysis. I changed the data types of some columns to fit the values in the column perfectly. I renamed some columns for clearer understanding. In the ‘Churn’, ‘Active’ and ‘Credit Card’ columns (1 for yes and 0 for no), I changed the values in those columns, replacing ‘1’ with ‘Churned’ and ‘0’ with ‘Not churned’  under the ‘Churn’ column, ‘1’ for ‘Active’ and ‘0’ for ‘Inactive’ under the ‘Active’ column( which I later changed column name to ‘Activity Status’, also replaced ‘1’ with ‘Owned’ and ‘0’ with ‘Not owned’ under the ‘Credit card’ column ( which I later renamed as ‘Credit card status’). Due to the huge range of values in the ‘Balance’ and ‘Credit Score’ columns, I inserted columns where I broke them down into ranges with the help of the ‘conditional column’ tab. I inserted an ‘Age group’ Column for age ranges. 

# Data Modelling
After inserting the columns with ranges(Age groups, Acct Balance groups, and Credit score groups) , values in these columns are impossible to sort properly whether in ascending or descending order.
 
So I created a new table that contains the range-based column, I got rid of duplicates to help get the distinct values of the column and added a conditional column which I  filled with whole numbers based on the arrangements of the ranges. 
 
I did this for the ‘Age Groups’, ‘Acct Balance’, and ‘Credit Score’ columns. This will help us to sort our visualizations appropriately when working on these columns.
After this, I click on ‘close and apply’ to apply these changes to the data and load it from Power Query into Power BI for analysis and visualization.


# Creating Measures Using DAX
First I calculated the total number of customers using the ‘count’ function on the ‘Customer ID’.
Customers = COUNT('Customer Churn Data'[Customer ID])


Then I calculated for the number of churned customers (customers lost) with the help of the ‘COUNT’ function nested into the ‘CALCULATE’ function.
Customers Lost = CALCULATE(COUNT('Customer Churn Data'[Churn Status]), 'Customer Churn Data'[Churn Status]="Churned")

With the help of these two measures, I go ahead to calculate for the Churned rate, which is the rate at which we lose customers or the rate at which customers leave. I do this by dividing the number of customers lost by the number of customers.
Churned rate = 'Customer Churn Data'[Customers Lost] / 'Customer Churn Data'[Customers]


# Data Visualization
First, I visualized customers, customers lost, and churned rate on cards. I then went ahead to insert doughnut charts for customers by gender, customers by activity status, customers by country, customers by credit card status, and the customers by product.

I then went ahead to insert a line and clustered column chart which visualizes the customers by age group in column bars, and churned rate by age group on a line chart all in one. I did same for customers and churned rate by credit scores and then customers and churned rate by account balance.

I then inserted a slicer for churn status and a gauge chart for churned rate.

[Link-to-dashboard](https://app.powerbi.com/view?r=eyJrIjoiYTZkYjg4MmMtMjAxYi00ZTdjLTllNDItMjZiZGNkODE3ZDJiIiwidCI6IjFjZTU4MjFjLTE5NDItNDczMy1hNmRjLTBmYzNhODJiNzRkYiJ9)

# Insights and Recommendations.
 
Out of the 10,000 customers the bank has, 54.57% are males while 45.43% are females. 51.51% of the customers are very active, 70.55% of customers own a credit card. Out of the three countries the customers are from, 50% of the customers are from France, 25.09% are from Germany and 24.77% are from Spain.
 

The bank has lost 2,037 customers to customer churn, with a churn rate of 20.4% which is alarming because it is a little bit above the target churn rate of 15%.



 
As shown in the above charts, a lot of customers are of the age group of 31 to 40 (4,451), and the age group ranging from 51 to 60 achieved the highest churn rate (56.2%). Customers in this age group may be experiencing significant life changes like retirement and relocation changes leading to altered needs and priorities. Also, they might have specific expectations regarding service quality, personalized attention, and product quality. Engage directly with customers in this age range, understand their pain points, and foster solutions. Incentivize long-term commitments through loyalty rewards, discounts, and exclusive bonuses.

Also, the second graph shows that 3.8K of the total customers have a credit score between 601 and 700 and a churn rate of 19.7% which is quite alarming because with this credit score, they are of moderate risk and have the potential to grow. Losing customers of such criteria is not good for business. The bank should focus on engaging people in this credit score range as they have potential for growth leading to higher credit scores and gaining access to a broader range of credit and loans at better rates that will keep them satisfied and sustain them as customers. People with a credit score below 400 have a churn rate of 100% because with such credit scores they probably won’t get the best offers or sometimes no offers at all which will lead to most of them leaving. Customers of such credit score range should be advised on measures to take to improve their credit score like consistently paying bills on time and also secured credit cards and credit-builder loans.

Customers with account balances ranging from 1K to 10K have a churn rate of 100%, meaning that every single customer in this account balance range has discontinued their association with the bank. This is such a critical finding which needs immediate attention. Customers in such account balance range might probably be facing financial difficulties causing them to churn or other banks are giving them better terms, interest rates, and incentives. The bank should evaluate and enhance existing products to better meet their needs and if possible offer personalized incentives.

The visualization shows 4,765 customers with an account balance ranging from 100k to 200k but a churn rate of 25% while customers with an account balance above 200k have a churn rate of 55.9% which is quite alarming and should be looked at.
Product 2 has the lowest churn rate (7.6%) which is very impressive while Product 3 has the highest churn rate with 82.7%. Management should have a close look at this product in comparison to product 2 which has the lowest churn rate and come up with a customer retention strategy for this product
