# Identifying-Top-Revenue-Generating-Customers-for-a-Multinational-E-Commerce-Company
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe.

# project overview
This data science research project presents a comprehensive sales analysis of a leading multinational e-commerce company headquartered in the United States, with operations spanning across North and South America, as well as Europe. 


The objective of the study is to analyze and identify the **Top 10 highest revenue-generating customers**, offering critical business insights into customer value, regional sales dynamics, and strategic growth opportunities.


Leveraging advanced data analytics techniques, including data preprocessing, aggregation, and visualization, this project uncovers key patterns in customer spending behavior across diverse markets. 


By ranking customers based on total revenue contribution, the analysis empowers business stakeholders with actionable intelligence to optimize customer relationship management, tailor marketing strategies, and enhance profitability in a globally competitive landscape.

This project serves as a practical application of data science principles in the domain of e-commerce, showcasing the impact of data-driven decision-making on strategic business outcomes.

### Problem Statement
**Who are Top 10 Customers of the Company in terms of Total Revenue generated since the company started ?**

### Project Objectives 
1. **To Identify Top Revenue-Generating Customers**

   * By Analyzing sales data to determine the top 10 customers contributing the highest total revenue across all regions.


2. **To Understand Revenue Concentration**

   * By Analyzing how much of the company's total revenue is concentrated among top customers.


3. **To Uncover Geographic Patterns**

   * By Assessing the global distribution of high-value customers across the Countries to identify key markets and regional revenue   clusters.


4. **To Support Strategic Decision-Making**

   * By Providing actionable insights to the company’s sales and marketing teams for developing targeted retention, loyalty, and upselling strategies.



5. **To Demonstrate Real-World Data Science Application**

   * By Showcasing the use of data science tools and techniques (data preprocessing, aggregation, visualization) in solving a real-world business problem.


6. **To Enable Stakeholder Communication**

   * By Creating intuitive visualizations and summaries that allow non-technical stakeholders to understand key findings and insights.


7. **To Lay the Groundwork for Predictive Modeling**

   * By Establishing a foundational dataset and insights that could be extended into customer lifetime value prediction or churn modeling in future phases.
 
  ### Data Source
  **The Company's central transaction database**
  ### Project Methodology
  - **Data Collection**: Data was collected from the Company's Central Transaction Database

- **Data Pre-processing**: Loaded the data from a CSV file into a Pandas Dataframe

- **Data Inspection and Cleaning**: Checked for Missing values, Checked for Duplicates.

- - Handled missing values
  - Handled duplicate values

- **Data Modification**: generated some  core metrics which were NOT provided from the dataset, and would be required for the purpose of the data   analysis

- **Data Aggregation**: To Compute the major metric : Total Revenue by Customer**

- **Data Sorting/ Data Ranking**: To Determine the Most Importat Metric:  **Top 10 highest revenue-generating customers**

- **Data Visualization**: To uncover the **Top 10 highest revenue-generating customers** in a pictorial form.

- **Data Interpretation**:

- **Key Findings**

- **Conclusions**

- **Recommendation**
  
### Data Collection
Sales data was obtained from a central transaction database of the company representing orders placed by customers across multiple countries. Each record included attributes such as:

* `Customer ID`
* `OrderNo`
* `OrderQuantity`
* `CostPrice_usd`
* `SellingPrice_usd`
* `OrderDate`
* `CustomerName`
* `CustomerCity`
* `CustomerState`
* `CustomerCountry`
* `ProductCategory`
* `ProductColor`
* `Model`
  
### Data Pre-processing
**Data Loading**: 
Reading the Raw Dataset which originally existed as a CSV file into a Pandas Dataframe

Task: Follow the appropriate steps in reading a CSV file into a pandas Dataframe,

and Read the data stored in the csv file named: `bikes` From your computer.

The resulting Dataframe should be named :`bikes_df`
     
```python
# solution

import pandas as pd

bikes_df = pd.read_csv('C:/Users/HP/Downloads/bikes.csv')

bikes_df.head()
```
<img width="739" height="202" alt="Data Pre-processing" src="https://github.com/user-attachments/assets/e492245e-bc32-4b10-b33f-b3008c45aeb3" />


### Data Inspection and Cleaning
* **1.check for Missing values**:

```python
# solution 

bikes_df.isna().any()
```
<img width="156" height="167" alt="Data Inspection and Cleaning 2" src="https://github.com/user-attachments/assets/a33e84af-33b7-478f-9c25-b259b9df9963" />


```python
# counting the nuber of the missing values

total_number_of_missing_values_by_colunms = bikes_df.isna().sum()

total_number_of_missing_values_by_colunms
```
<img width="141" height="160" alt="Number of missing values " src="https://github.com/user-attachments/assets/05c57997-ec52-4cc8-be6f-5527f160299b" />

```python
# visualizing the total number of missing values

import matplotlib.pyplot as plt

# using a bar plot to visualize the missing values

total_number_of_missing_values_by_colunms.plot(kind = "bar")

# to show the plot

plt.show()
```
<img width="424" height="323" alt="visualizing missing values" src="https://github.com/user-attachments/assets/06cea19e-faca-497c-9554-55d6a2af35f6" />

- **2.Handling Missing values**
  
```python
# solution 

# bikes_df ["ProductColor"].mode()

bikes_df = bikes_df.fillna("Black")

bikes_df
```

<img width="662" height="355" alt="Handling missing values" src="https://github.com/user-attachments/assets/3e653b98-5edd-4b27-8216-ecf917d81202" />


```python
# to verify that there are no more missing values on our dataset

bikes_df.isna().any()
```

<img width="570" height="163" alt="checked for complete dataset" src="https://github.com/user-attachments/assets/3f5fe107-2f03-473c-b5d6-1ea3fe6c007b" />

- **3. Check for  Duplicates**:

```python
# solution

# counting the total number of our datapoint

len(bikes_df)
```

```python
bikes_cleaned_data_df = bikes_df.drop_duplicates()

bikes_cleaned_data_df
```

```python
# dropping any duplicates if any exists

bikes_df.drop_duplicates(inplace = True)
````

- **4. Handling Duplicates**:
  
```python
# solution

# re-counting  our data point again
len(bikes_df)

# This shows that there was NO duplicates on our dataset
```

### Data Modification

```python
# generating some core metrics which were NOT provided from the dataset, which would be required for the purpose of the data analysis

# solution 

# (1) TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 



# (2) SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 


# (3) Profit : To be obtained by (SalesRevenue - TotalCostPrice)


bikes_df["Profit"] = bikes_df["SalesRevenue"]  - bikes_df["TotalCostPrice"]


# Displaying the result

bikes_df.head()
```
<img width="869" height="233" alt="Data modification" src="https://github.com/user-attachments/assets/d4cc8c3a-4c0a-474d-a9f6-9d4435f79f59" />

### Data Aggregation

```python
# Computing/ Aggregating the sales data to show Total Revenue by Customer , including their City, State and Country. 

# solution 

# computing the total revenue by customers

total_revenue_by_customer = bikes_df.groupby(["CustomerName", "CustomerCity", "CustomerState","CustomerCountry"])["SalesRevenue"].sum().reset_index()

total_revenue_by_customer
```

<img width="347" height="249" alt="Data Aggregation" src="https://github.com/user-attachments/assets/9346b475-03af-4315-9446-4015cc795c25" />


### Data Sorting/ Data Ranking

```python
# To Determine the Most Importat Metric: Top 10 highest revenue-generating customers 

# solution 

the_top_10_customers = total_revenue_by_customer.sort_values("SalesRevenue", ascending = False).head(10)

the_top_10_customers
```

<img width="381" height="212" alt="Data sorting" src="https://github.com/user-attachments/assets/f39ac9e7-84b2-464b-b31f-6cc1dc0b29bb" />


### Comparing of the Total Revenue Generated by the Top -10 Customers to the Entire Total Revenue of the Company

```python
# The Total Revenue Generated by the Top -10 Customers

revenue_sum_of_top_10_customers = the_top_10_customers["SalesRevenue"].sum().round(1)

revenue_sum_of_top_10_customers
```

```python
# Entire Total Revenue of the company

revenue_sum_of_the_entire_company = bikes_df["SalesRevenue"].sum().round(1)

revenue_sum_of_the_entire_company
```

```python
percentage_rev_top_10_customers = (revenue_sum_of_top_10_customers / revenue_sum_of_the_entire_company)* 100

ratio = percentage_rev_top_10_customers.round(2)

ratio
```
<img width="685" height="326" alt="Total revenue of top 10 customers" src="https://github.com/user-attachments/assets/efe02917-f9bf-4d40-8f6c-ad6150f46c74" />



```python
print (f"The Total Revenue generated by the top 10 Customers, accounts for {ratio}% of the company's total revenue")
```
<img width="528" height="45" alt="print call" src="https://github.com/user-attachments/assets/a4646b90-d474-48af-909c-f6ff13f0243a" />



### Data Visualization

```python
#  To uncover the Top 10 highest revenue-generating customers in a pictorial form.

# solution 

import matplotlib.pyplot as plt

the_top_10_customers.plot(kind = "bar", x = "CustomerName", y = "SalesRevenue",color = "blue")

# axis label

plt.xlabel("Customer Names")
plt.ylabel("Total Revenue in US Dollars")

# title label

plt.title("The Top 10 Customers by Total Revenue Since the Company Started")

# to show the plot

plt.show()
```
<img width="320" height="289" alt="Data viz of the top 10 customers" src="https://github.com/user-attachments/assets/766494bd-0245-48c9-bbc2-2bcfff608967" />




### Data Interpretation

The Result from the data visualization above shows that all the **Top 10 Customers** are all bases in **France**

### Key Findings
---

1. **France Dominates among Top-Tier-High-Value-Customers**: 
   All **The Top 10 Customers** are based in **France**, indicating a strong customer base and market penetration in this region.


2. The Company's **Top 10 Customers** Contribute Less Than **1% of Total Revenue of the entire company**.

   
   Despite **France** being the **top revenue generators**, these customers collectively account for a **very small fraction** of the company's overall sales — indicating **broad and diversified revenue streams**.

4. **Revenue is Distributed, Not Concentrated**
   Unlike typical e-commerce businesses that follow the Pareto Principle (80% of revenue from 20% of customers), this company’s revenue is **evenly spread across thousands of customers**, highlighting a mass-market model.


5. **High-Value Customers Are Geographically Clustered**
   The top revenue-generating customers are concentrated in specific cities and departments such as:

   * **Tremblay-en-France**, **Les Ulis**, and **Saint-Denis** in **Seine Saint Denis** and **Essonne**
   * Major urban centers like **Paris**, **Metz**, and **Dunkerque**

6. **Narrow Revenue Spread Among Top Customers**
   The revenue range of the top 10 customers is relatively narrow—from **\$13,144.88** to **\$13,708.12**, suggesting consistent purchasing behavior across the top customer tier.

7. **Top Customers Still Exhibit Stable Purchasing Behavior**
   While their individual contribution is small relative to total revenue, the top customers show **stable, high-value purchasing patterns** — useful for identifying ideal customer personas or retention targets.

8. **Customer Loyalty and Repeat Purchases Likely**
   Given the similar revenue volumes, it’s likely that these customers have regular or subscription-based purchasing behavior.

---

### Conclusions
---
The company's sales data analysis reveals that the company operates a **high-volume, low-concentration revenue model**, where no single customer or small group significantly influences total revenue. 

This suggests a **wide customer base**, possibly driven by individual, one-time, or small-ticket purchases.

Furthermore, the sales data reveals that the company’s **top 10 most valuable customers are concentrated entirely in France**, with a significant cluster in **Île-de-France** and surrounding regions. 


This concentration indicates a **strong local market presence**, but also highlights a **potential risk** if the company's sales efforts are overly dependent on a single region.

While the **top 10 customers** do not represent a **major share of total sales**, understanding their behavior is still useful for profiling ideal, repeat-purchase customers. Moreover, the fact that all top performers are from France indicates a **regional pattern** in customer loyalty or market engagement.


However, the **absence of high-revenue customers** from other regions such as the **United States, Canada, Germany, UK, and Australia** points to a **potential gap in customer acquisition** or expansion strategy.

---

### Reconmendation
---
### 1. **Expand High-Value Customer Acquisition Beyond France**

* Launch targeted marketing campaigns in **United States, Canada, Germany, UK, and Australia** to balance regional revenue dependency.
* Use the profile of these French customers to find “look-alike” customers in other countries.

### 2. **Focus on Scaling Average Customer Spend**

* Instead of concentrating only on top customers, create **broad-based incentives** (e.g., product bundles, loyalty points) to **lift the average order value** across all customers.

### 3. **Replicate High-Value Customer Traits Across the Base**

* Analyze what makes the top 10 customers spend more (location, product type, frequency) and **apply that insight to encourage similar behavior** in the general customer base.


### 4. **Strengthen Customer Retention in France**

* Reward top customers in France with loyalty programs, premium services, or early-access deals.
* Consider customer interviews or surveys to understand what keeps them engaged.


### 5. **Run Regional A/B Tests**

* Test localized marketing efforts in other regions using the same product mix that appeals to French customers.

### 6. **Mitigate Regional Risk**

* Relying heavily on France puts the company at risk in the event of regional disruptions (economic, political, or logistical).
* Diversify revenue sources across other major European and American markets.
---





  
