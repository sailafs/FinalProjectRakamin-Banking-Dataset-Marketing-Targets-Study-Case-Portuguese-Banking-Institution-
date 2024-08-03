# Final Project - Banking Marketing Analysis

## Project Overview
This project, conducted by Pattern Pioneers, analyzes a Portuguese banking institution's marketing campaign data to optimize their deposit program subscription rates through telemarketing.

## Table of Contents
1. [Project Background](#project-background)
2. [Goals and Objectives](#goals-and-objectives)
3. [Data Overview](#data-overview)
4. [Methodology](#methodology)
5. [Key Findings](#key-findings)
6. [Business Impact](#business-impact)
7. [Recommendations](#recommendations)

## Project Background
The Portuguese bank aims to identify customers most likely to subscribe to their deposit program through telemarketing campaigns. The project focuses on improving campaign efficiency and profitability beyond 81%.

## Goals and Objectives
- Identify high-potential customers for subscription
- Develop a customer classification model
- Provide business recommendations to the Marketing team
- Increase deposit program subscription rate by over 12%
- Reduce telemarketing operational costs by over 50%

## Data Overview
- Dataset: 45,211 rows and 18 columns of customer data
- Features: Mix of categorical and numerical data including age, balance, job, loan status, etc.

### Detailed Column Descriptions bank client data:
1. age (numeric)
2. job : type of job (categorical: "admin.","unknown","unemployed","management","housemaid","entrepreneur","student","blue-collar","self-employed","retired","technician","services")
3. marital : marital status (categorical: "married","divorced","single"; note: "divorced" means divorced or widowed)
4. education (categorical: "unknown","secondary","primary","tertiary")
5. default: has credit in default? (binary: "yes","no")
6. balance: average yearly balance, in euros (numeric)
7. housing: has housing loan? (binary: "yes","no")
8. loan: has personal loan? (binary: "yes","no")
### Related with the Last Contact of the Current Campaign:
9. contact: contact communication type (categorical: "unknown","telephone","cellular")
10. day: last contact day of the month (numeric)
11. month: last contact month of year (categorical: "jan", "feb", "mar", …, "nov", "dec")
12. duration: last contact duration, in seconds (numeric)
### Other Attributes:
13. campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
14. pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric, -1 means client was not previously contacted)
15. previous: number of contacts performed before this campaign and for this client (numeric)
16. poutcome: outcome of the previous marketing campaign (categorical: "unknown","other","failure","success")
### Output variable (desired target):
17. y - has the client subscribed a term deposit? (binary: "yes","no")

## Methodology
1. Exploratory Data Analysis (EDA)
   - Descriptive Analysis
   <img width="801" alt="Screenshot 2024-08-03 at 1 58 54 PM" src="https://github.com/user-attachments/assets/07caa6ed-f24a-471f-bf09-fce66df63896">
      
         *  There are no empty rows
         *  There are 9 Categorical Features and 7 Numeric Features
         *  Feature 'y' as the target

   <img width="802" alt="Screenshot 2024-08-03 at 2 01 18 PM" src="https://github.com/user-attachments/assets/6a5150c8-ef59-4565-8d0a-a038c124b49b">
      
         *  Feature 'y' as the target
         *  Numerical Features do not have missing values
         *  The 'age' feature shows that the majority of customers are still of productive age
         *  There is an anomaly in the 'balance' feature, the minimum value indicates that there are customers who have debt to the bank. Additionally, the minimum and maximum values have a considerable range compared to the lower and upper quartile values, indicating potential outliers.
         *  There are potential outliers in the 'duration' feature, with the maximum value of 4918 being significantly higher than its lower and upper quartile values.
         *  There are potential outliers in the 'pdays' feature, with the maximum value of 871 being significantly higher than its upper quartile value.
         *  There are potential outliers in the 'previous' feature, with the maximum value of 275 being considerably higher than its upper quartile value.
   
   <img width="784" alt="Screenshot 2024-08-03 at 2 02 25 PM" src="https://github.com/user-attachments/assets/f66cb51d-ef5a-470c-b677-d4cf427389fe">
      
         *  Categorical Features have missing values in the 'poutcome', 'contact', 'education', and 'job' features, which are represented by the value "unknown".
         *  There is a Class Imbalance in the feature 'y', with 39,922 "no" values compared to 5,289 "yes" values.

   - Univariate Analysis
   <img width="1438" alt="Screenshot 2024-08-03 at 2 12 25 PM" src="https://github.com/user-attachments/assets/b60b02bd-b5e9-4c75-8fbc-c4ea0c20cf17">
   <img width="1440" alt="Screenshot 2024-08-03 at 2 12 34 PM" src="https://github.com/user-attachments/assets/79933bfe-ab7e-4000-b15f-1870c2f3c403">
   
         *  Distribution of Age 
              1. Has a normal distribution
              2. Well distributed between ages 20 - 60 years
              3. Has outliers

         *  Distribution of balance
              1. Has a positive skew graph
              2. There are negative balance values (debt)
              3. Has outliers
              4. The data is spread out

         *  Distribution of day 
              1. Data is distributed quite well (normal)
              2. No outliers present

         *  Distribution of duration 
              1. Has a positive skew distribution
              2. Has outliers
              3. Some customers have short durations in contacting the bank, as evidenced by data distributed between 0 - 400 compared to the total number of customers which is 45,211
              4. Data is fairly spread out

         *  Distribution of campaign 
              1. Shows the number of campaign interactions that took place with customers
              2. Has a positive skew distribution
              3. During the campaign, more customers were contacted fewer times by the bank, as evidenced by the visible distribution between 0 - 10
              4. Has outliers

         *  Distribution of pdays 
              1. The pdays column shows the number of days passed after the customer interacted with the campaign
              2. Has a positive skew distribution
              3. Possible presence of outliers
              4. The graph shows many customers in a short period after interacting with the campaign, as evidenced by the visible distribution between 0 - 90

         *  Distribution of previous 
              1. The previous column represents the number of customers who interacted with previous campaigns. These customers are the same as those in the current campaign
              2. Has a positive skew distribution
              3. There are customers with few interactions in previous campaigns, and some with no interactions at all. This is evidenced by the distribution around 0 - 10
              4. Possible presence of outliers

   <img width="1440" alt="Screenshot 2024-08-03 at 2 21 08 PM" src="https://github.com/user-attachments/assets/7ff14cdd-3210-4604-afb8-e64b8b966235">
   
         *  Job Distribution
              1. The most common job in the dataset is "admin.", followed by "services", "unknown", "management", and "ent."
              2. There are some less common jobs, such as "preneular", "retir", "Je-conowned", and "housemalent".

         *  Marital Status Distribution
              1. The most common marital status is "married", followed by "single" and "divorced".
              2. There are some marital statuses with low distribution, such as "widowed" and "separated".

         *  Education Level Distribution
              1. The highest education level is "tertiary", followed by "secondary" and "primary".

         *  Default Distribution
              1. Most people in the dataset do not have a default.

         *  Housing Distribution
              1. Most people in the dataset have housing.
              2. Few people do not have housing.

         *  Loan Distribution
              1. Most people in the dataset do not have a loan.
              2. Not many people have a loan.

         *  Contact Distribution
              1. The highest contact method is "cellular", followed by "telephone".

         *  Month Distribution
              1. The month with the most data is "Mar", followed by "Feb", "Jan", "Dec", "Sep", and "Apr".
              2. There are some months with less data, such as "Oct", "Nov", "May", "Jun", "Aug", and "Jul".

#### Here are the insights that can be obtained from the Univariate Analysis of the numeric section:
      - We can use the age feature (with an age range of 20-60), negative balance, and duration to build a model that can classify customers based on their likelihood of subscribing to a term deposit.
      - We can use low campaign frequency, pdays, previous, and short duration to provide more detailed information. Outliers can be considered (removed or not) to improve model performance.
      - To reduce churn, we can look at customers who have short durations and negative balances to increase the likelihood of subscription.
      
- Multivariate Analysis
   <img width="874" alt="Screenshot 2024-08-03 at 4 32 54 PM" src="https://github.com/user-attachments/assets/328d807d-401f-474d-b505-3f75a64003c9">

        *  'days' and 'campaign' have a scatter plot that shows a pattern, which proves that these two categories are correlated.
        *  'duration' and 'campaign' have a pattern where the scatter plot points become more spread out as the campaign duration increases, while it can be seen that many campaign durations are short-term.  
   
5. Data Preprocessing
   - Handling missing values
      - Handling duplicates: Only one duplicates detected, decided to retain as unique.
      - Handling 'unknown' or 'NaN' values which were treated as missing values: values are changed into the mode of the unique values.
      - Handling outliers: Visualisation in terms of bar chart was done to detect outliers and decisiion to handle ouliers using IQR was derived. However, significant numbers of data were deleted due to handling of outliers which makes handling of outliers was not done at last. Instead, standardisation was done to help with outliers.
   - Addressing imbalanced data
      - Oversampling was done using SMOTE.
   - Feature engineering
      - Drop 'day' and 'campaign' due to negative correlation.
      - Grouping to drop complexity for 'age'
      - Label encoding for 'education', 'default', 'housing', and 'loan'.
      - One Hot Encoding for 'month', 'marital', 'job', 'contact', and 'poutcome'.
      - Standardisation for 'duration', 'pdays', 'balance', and 'previous'.
6. Modeling
   - Logistic Regression
   - Random Forest
   - XGBoost
7. Hyperparameter Tuning
8. Model Evaluation using Recall, F1-Score, ROC AUC, and Cross-Validation

## Key Findings
- Customer segments with higher subscription rates identified
- Duration of contact significantly impacts subscription likelihood
- Balance and age are important factors in predicting subscriptions

## Business Impact
- 82.4% increase in customer acquisition accuracy
- 88.9% reduction in potential cost loss
- 710% improvement in conversion rate
- 95.3% increase in profit

## Recommendations
1. Aim for contact duration over 8 minutes
2. Target medium to high balance customers
3. Execute deposit offers early in the month
4. Focus on active-age customers with secondary and tertiary education
5. Prioritize customers without existing home loans
6. Develop exclusive offers for customers outside the active age range

For more detailed information, please refer to the full project report.
