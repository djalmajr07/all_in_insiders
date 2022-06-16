# **BUSINESS UNDERSTANDING**

## **COMPANY NAME?**

`All In One Place`

## **WHAT IS THE BUSINESS MODEL?**

All in One Place is a multi-brand 'outlet' company that sells second-line products from different brands at a lower price through an 'e-commerce'.

![image](https://user-images.githubusercontent.com/85264359/153950509-554ea347-eab1-4d11-9877-8cd8057b2e63.png)

## **WHAT IS THE BUSINESS PROBLEM?**

In just over one year of operation, the marketing team realized that some customers from its base buy more expensive products, with high frequency and end up contributing a significant portion of the company's revenue.
Based on this perception, the marketing team will launch a `loyalty program` for the best customers in the base, called `Insiders`. But the team does not have the advanced knowledge in data analysis to elect program participants.
For this reason, the marketing team asked the data team to select a selection of eligible customers for the program, using advanced data manipulation techniques.

**References:**
https://sejaumdatascientist.com/como-criar-um-programa-de-fidelidade-para-empresa/

# **MAIN PROBLEM**

## **WHAT CHALLENGE DOES THIS PROJECT AIM TO OVERCOME?**

All In One Place's team of data scientists needs to suggest who will be the eligible customers to participate of Insiders(a group with the most loyal customers). In possession of this list, the Marketing team will carry out a sequence of personalized and exclusive actions for the group, in order to increase revenue and purchase frequency.
As a result for this project, the delivery of a list of people eligible to participate in the Insiders program is expected, along with a report answering the following questions:
* *Who are the people eligible to participate in the Insiders program?*
* *How many customers will be part of the group?*
* *What are the main characteristics of these clients?*
* *What percentage of revenue contribution comes from Insiders?*
* *What are the conditions for a person to be eligible for Insiders?*
* *What are the conditions for a person to be removed from Insiders?*

# **BUSINESS ASSUMPTIONS**

```
- purchases with negative quantity will be treated separately
- purchases with zero price will not be considered (removed)
- purchases whose items do not have a description will not be considered (removed)
- purchases whose customer id is unknown will not be considered (removed),
as they cannot be identified later.
- the negative quantity attribute means a return of the product and consequently
the company needs to refund the customer, which implies that the price attribute
also have a negative value
- customers who return more products than they buy will not be considered (removed).
This indicates that the temporal cut of the data collected was not able to capture the purchases
past made by these customers
- items whose stock code has only alphabetic characters (like W', 'CRUK', 'J', 'BL')
appear not to have a related product. These items will not be considered in the calculations.
of the total items purchased per customer
- items with stock codes like 47566 and 47566B will be treated as different products
- the currency used was the US dollar
- purchases whose invoice_no starts with the letter C indicate a transaction with negative quantity,
therefore they will be treated separately.
```

# *MIND MAP*
![2022-02-03_07-39](https://user-images.githubusercontent.com/85264359/155852352-9a75edf5-6a37-4611-b681-8f47247965d3.png)


### **Dataset Description**

|Feature | Definition |  
|-------------| -------------- |
|InvoiceNo | unique identifier for each transaction |
|StockCode | product code (item) |
|Description | product name and description |
|Quantity | quantity of items of each product per transaction |
|InvoiceDate | date (day) on which the transaction was carried out |
|UnitPrice | unit price of each product (item) |
|CustomerID | unique identifier for each customer |
|Country | name of the country where the customer resides | 

**References:**
https://www.kaggle.com/vik2012kvs/high-value-customers-identification

# **SOLUTION STRATEGY**

### IOT METHOD

### Input
- **Business problem**: segment customers into groups and find the most valuable ones.
- **Business questions**: described in the previous section
- **Data available**: dataset of transactions that took place between Nov-2016 and Dec-2017.

### Output
- **Dashboard** with information from the Insiders group
- **Report** with the answers to the following business questions:
* *Who are the people eligible to participate in the Insiders program?*
* *How many customers will be part of the group?*
* *What are the main characteristics of these clients?*
* *What percentage of revenue contribution comes from Insiders?*
* *What are the conditions for a person to be eligible for Insiders?*
* *What are the conditions for a person to be removed from Insiders?*

### Tasks
> Who are the customers eligible to participate in the Insiders program?
* What does it mean to be eligible? For the company, what exactly is a valuable customer?
* We will assume that high value is synonymous with Lifetime Value (LTV)
> How many customers will be part of the group?
 * Determine the Insiders cluster
 * Count how many customers are in the group and what percentage of the total number of customers
> What are the main characteristics of these customers?
* Determine the Insiders cluster
* Describe the group's customers in terms of the average values of the attributes used in clustering
> What percentage of revenue is contributed by Insiders?
* Determine the Insiders cluster
* Calculate the accumulated revenue obtained by the group and divide by the total revenue obtained by the base
> What are the conditions for a person to be eligible for Insiders?
* Determine the Insiders cluster
* Determine the confidence interval (variation of attributes) to be considered for eligibility and verify how close the customer behavior is to the group mean
> What are the conditions for a person to be removed from Insiders?
* Determine the Insiders cluster
* Determine the confidence interval (variation of attributes) to be considered for eligibility and verify how far from the group mean the customer behavior is

# **PROJECT CYCLE**

## `Step 00. Settings and Data Extraction`
* Import of required libraries, packages and functions.
* Loading and checking available data via a CSV file.

## `Step 01. Data Description`
* Renaming of columns and checking the size of the dataset (assessing the need for tools to handle large volumes of data).
* Verification of data types in each column and type changes that are necessary for better treatment by the algorithms later
* Verification of missing data and decision on how to treat them (removal, artificial resampling, solution infeasibility)
* Brief statistical description of the numerical and categorical attributes in order to detect anomalies that are outside the scope of the problem, as well as the presence of possible outliers that will impact the performance of the algorithms later.

## `Step 02. Data Filtering`
* Filtering rows and deleting columns that do not contain information relevant to modeling or do not help to solve the problem.

## `Step 03. Feature Engineering`
Creation of variables (features) relevant to solving the problem

## `Step 04. Exploratory Data Analysis
* Isolated analysis of each feature and its relationship with the others.
* Exploration of the data in order to obtain an intuition of their distribution in the data space (embedding exploration).

## `Step 05. Data Preparation`
* Data preparation to help machine learning models learn and perform more accurately.
* Selection of the embedding space best suited to the problem

## `Step 06. Feature Selection`
* Selection of the most relevant features to train the models

## `Step 07. Model Training`
* Testing different machine learning models and selecting the one with the best performance based on the chosen metrics (silhouette score)
* Choosing the best values for each parameter from the tested models that maximize performance

## `Step 08. Hyperparameter Fine Tuning`
* Training the models with the best parameters found and measuring their performance

## `Step 09. Cluster Analysis`
* Visual inspection of the data space assembled by each model
* Analysis of the profile (attributes) of each cluster for each model trained
* Choice of the final model that presents the best performance

## `Step 10. Exploratory Data Analysis for Business`
* Creation and testing of business hypotheses and elaboration of answers to business questions

## `Step 11. Deploy to Production`
* Planning and implementation of the model deployment architecture
* Creation of the database that will be used to solve the problem


# **TOP 3 INSIGHTS**
- **The Insiders group contributes 30.33% of the company's revenue,** equivalent to $2.3 million
- **On average, revenue generated by customers in the Insiders group is 185x greater than revenue generated by customers in the cluster who spend less**
- **On average, the purchase frequency of the Insiders group is 14.36% and 117% higher than the purchase frequency of the second and third best performing customer groups, respectively**


# **BUSINESS RESULTS**

**Answering the proposed business questions**

### Who are the people eligible to participate in the Insiders program?
```
Customer_id list
[15311, 16029, 17511, 13408, 13694, 12748, 14911, 17841, 13777, 17381,
15061, 14156, 13798, 14680, 16013, 17949, 15769, 13081, 13089, 16422,
17450, 15838, 18102, 17857, 14298, 17404, 16684, 12931, 14646, 13027,
12415, 14088, 13098, 16333, 12901, 14096]
```
### How many customers will be part of the group?
Total Customers that will be part of the Insiders group: `36` `(1.30 % of the base)`

### What are the main characteristics of these customers?
| Attribute | Value | Unit |
|----------|-------:|---|
|Invoicing(Purchases) Average | 66,079.42 | $
|Billing(returns) Average | -1,914.10 | $
|Average Recency | 10.03 | days
|Average Quantity of Purchases | 49.72 | purchases
|Average Variety of Purchased Products| 366.64 | products
|Average Quantity of Items Purchased | 38,902.06 | items
|Average of the Average Ticket | 205.74 | $/purchase
|Average Recency between purchases | 16.14 | days
|Average Purchase Frequency | 0.14 | shopping/day
|Average Quantity of Items Returned | 962.92 | items
|Average Return Frequency | 0.14 | returns/day
|Average Basket Size Medium | 1,124.21 | items/purchase
|Average of Basket Variety Medium | 8.85 | products/purchase
|Average Percentage of Returned Items | 0.03 | % (returns/purchases)
|Average Percentage of Billed Balance | 0.97 | % (balance/gross revenue)

### What percentage of revenue contribution comes from Insiders?
- Insiders billing percentage: `30.33 % of Total`


### What are the conditions for a person to be eligible for Insiders?
- Billing range to be eligible for Insiders: `$44836.16 to $87322.68`
- Recency range to be eligible for Insiders: `3 to 17 days`
- Frequency range to be eligible for Insiders: `0.101 to 0.182 purchases/day`


### What are the conditions for a person to be removed from Insiders?
- Show performance below the eligibility range of Insiders metrics


# **BUSINESS SOLUTION**

**The following image explains the deployment architecture used to solve this problem**

![image](https://user-images.githubusercontent.com/85264359/155851902-5f2dcb15-42e4-4d50-b50f-5d02782407e5.png)
### **Dashboard**

The following image shows the dashboard built in the Metabase tool. With this resource, the marketing team can monitor the performance of each cluster and see which clusters are closer to reaching the revenue target set for each group of customers.
![image](https://user-images.githubusercontent.com/85264359/155851202-e9019dc0-3f60-4b3e-9d68-8f94281d946b.png)

# **CONCLUSIONS**
Clustering problems are significantly more complex to solve, since the absence of a response variable, typical of unsupervised problems, forces us to delve deeper into the understanding of the business in order to guide us in making decisions about which models to implement. , which *features* to derive and which information is actually relevant to the problem. Data analysis is no longer merely mathematical and statistical and demands more interpretation and intuition in relation to the business and the problem at hand.


# **LESSONS LEARNED**
* **How to develop an unsupervised Data Science project**

* **How to use AWS tools (S3, EC2 and RDS), which offer a more robust solution platform for companies**

* **How to create a dashboard in the Metabase tool**

* **How to develop intermediate solutions and gradual improvements throughout the project, delivering value more quickly to the business team until presenting the final robust and better finished solution.**

* **Focus on solving business problems more fundamentally than using tools**

* **Understand the decisive importance of the cyclical development of projects and realize that the improvement of both the performance of the models and the results obtained in the business is gradually obtained as more cycles are implemented**

# **NEXT STEPS**

**Streamlit**: create a user-friendly page in Streamlit that allows the user to upload data via a link, in addition to validating this data before sending it to the AWS hosted S3 bucket.

**Dashboard**: talk to the business team in order to know the most relevant information to be presented.

**Embeddings**: test other embeddings that facilitate the grouping done by ML models

**Machine Learning Models**: Test more ML models for better results.

**Hypothesis**: develop and validate more business hypotheses in order to deepen the understanding of the problem.

**Code**: review and rewrite the code in order to improve readability, as well as reduce the consumption of computational resources.
