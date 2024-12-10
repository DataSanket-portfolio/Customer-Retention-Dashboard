
# Customer Retention Dashboard

## Problem Statement

The goal of this project was to analyze and visualize customer churn data for a telecom company. The primary aim was to identify key factors influencing customer retention, provide actionable insights, and forecast potential customer churn. This proactive approach would enable the company to address customer concerns and prevent terminations before they occur.

### Steps followed 

- Data Understanding

    Dataset included: Customer ID, gender, Senior Citizen status, Partner status, Dependent status, tenure, various service subscriptions (e.g., phone, internet, streaming), billing details, ticket data (admin, tech, total), and churn status.


- With SQL Queries extracted KPIs such as:

    - Total customers.

    - Total churn.

    - Number of Senior Citizens.

    - Total tickets, admin tickets, and tech tickets.

- Queried and documented data outputs for:

    - Churn comparisons based on tenure, billing type, contract type, and payment methods.

    - Monthly and total charges analysis.

- Generated insights on churn tendencies using SQL for data preparation and validation.


# Power BI Visualizations

- KPI Indicators:

    - Total Customers.

    - Total Churn.

    - Senior Citizens.

    - Total Tickets (Admin and Tech).

- Demographics Visualization:

    - Male vs. Female percentage.

    - Senior Citizen percentage.

    - Percentage of customers with Partners and/or Dependents.

- Churn Comparisons:

    - Churn vs. Tenure.

    - Churn for Billing Types (Paperless vs. Paper).

    - Churn vs. Contract Types.

    - Churn by Payment Methods.

    - Average Monthly and Total Charges.

- Additional Charts:

    - Donut charts for churn percentages by demographics.

    - Column charts for churn vs. tenure and billing methods.

    - Bar graphs for admin and tech ticket analysis.

- Interactive Features:

    - Slicers for demographic categories, service types, and time periods.
        
# SQL queries
### KPIs

    (1) Total Customers

select COUNT(customerID) as Total_Customers from churn_dataset
select AVG(Satisfaction_rating) as Overall_Customer_Rating from call_center

![image](https://github.com/user-attachments/assets/38c2b5bc-b8e1-4db2-a53d-553b4a803aae)


    (2) Total Churn

select COUNT(Churn) as Total_Churn from churn_dataset
where(Churn)= 'Yes'

![image](https://github.com/user-attachments/assets/caf21eca-a2a4-4620-ac98-bcba6b2e1ffd)


    (3) Average Number of services

select AVG(Total_Services) as Avg_No_Of_Services from churn_dataset

![image](https://github.com/user-attachments/assets/c61b4999-4702-4cd5-b25b-bb9bb5178ed6)



    (4) Senior Citizens

select COUNT(SeniorCitizen) as Senior_Citizens from churn_dataset
where(SeniorCitizen)='1'

![image](https://github.com/user-attachments/assets/28f599c4-1046-4a70-b9f8-c9ff03aad42c)

 
    (5) Percentage of Males and Females

select(count(case when gender='Male' then 1 end) * 100.0 / COUNT(customerID)) as Male_Percentage,
(count(case when gender='Female' then 1 end) * 100.0 / COUNT(customerID)) as Female_Percentage from churn_dataset

![image](https://github.com/user-attachments/assets/ebf6e43f-8e97-4b56-9560-a9dc9fd1e636)

    (6) Tenure vs Churn

select case when tenure >=1 And tenure<=12 then 'Less than a Year'

when tenure > 12 And tenure<=24 then '1-2 years'

when tenure > 24 And tenure<=36 then '2-3 years'

when tenure > 36 And tenure<=48 then '3-4 years'

when tenure > 48 And tenure<=60 then '4-5 years'

when tenure > 60 then 'More than 5 years'

Else 'Unknown'
End as Tenure_Categories,

 

Count(*) as Churn_Number from churn_Dataset

where Churn = 'Yes'

Group by case when tenure >=1 And tenure<=12 then 'Less than a Year'

when tenure > 12 And tenure<=24 then '1-2 years'

when tenure > 24 And tenure<=36 then '2-3 years'

when tenure > 36 And tenure<=48 then '3-4 years'

when tenure > 48 And tenure<=60 then '4-5 years'

when tenure > 60 then 'More than 5 years'

Else 'Unknown'

End

Order by Tenure_Categories ASC

![image](https://github.com/user-attachments/assets/6410715d-f1a6-4397-b401-b84044773e00)



    (7) Payment Method vs Churn

select PaymentMethod, count(Churn) as Customer_Churn from churn_Dataset

where Churn ='Yes'

group by PaymentMethod

![image](https://github.com/user-attachments/assets/cee03d72-035b-4281-a7b0-2957aaf5a12f)



    (8) Administrative/Technical Total Queries comparison

select sum(numAdminTickets) as Total_Admin_Tickets,

sum(numTechTickets) as Total_Tech_Tickets,

sum(Total_Queries) as Total_Queries,

(sum(numAdminTickets) * 100.0/Sum(Total_Queries)) as PCT_AdminTickets,

(sum(numTechTickets) * 100.0/Sum(Total_Queries)) as PCT_TechTickets

from churn_Dataset

![image](https://github.com/user-attachments/assets/133ea484-6360-4a48-b812-2b533fe30046)


# Snapshot of Dashboard (Power BI) - Customer Churn Dashboard
![image](https://github.com/user-attachments/assets/9c708f8d-27d1-4925-91c4-fcfd28a47fd0)


# Insights Window

#### A dedicated Power BI window for actionable insights, summarizing:
- High churn rates among customers with paperless billing and month-to-month contracts.
- Customers with DSL internet service tend to stay more than the ones with Fiber Optics connection.
- Customers with multiple tickets (admin or tech) showing a higher likelihood of churn.
- Customers with Automatic transactions have approximately three times less churn rate than Electronic Mailed check transactions.

![image](https://github.com/user-attachments/assets/ee8d5988-ec67-40e4-a157-25cf724ecdaf)



# Key Visuals
- High Churn (Paperless Billing & Month-to-Month Contracts):
    - Offer discounts for switching to long-term contracts.
    - Simplify paperless billing and improve clarity.
    -  Target month-to-month customers with loyalty incentives.

- DSL Customers Stay Longer than Fiber Optics:
    - Investigate and address Fiber Optics service issues.
    - Highlight DSL reliability in marketing.
    - Provide premium bundle offers for Fiber Optics users.

- High Churn Among Customers with Multiple Tickets:
    - Enhance support quality to resolve issues faster.
    - Assign dedicated agents for frequent ticket raisers.
    - Introduce chatbots and self-help tools for common problems.

- Auto-Pay Reduces Churn:
    - Incentivize auto-pay adoption with discounts or rewards.
    - Educate customers on the convenience of auto-pay.
    - Simplify the auto-pay setup process.


# Tools Used
SQL: Data extraction and transformation.

Power BI: KPI dashboard creation and interactive visualizations.

Excel: Supplementary data preprocessing and documentation.
