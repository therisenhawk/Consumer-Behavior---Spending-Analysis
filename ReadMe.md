# Consumer Behavior & Spending Analysis

## Project Overview

In this project, I analyzed real world credit card transaction data to understand how consumers spend, how spending behavior differs across users, and which patterns emerge when customers are grouped by spending intensity.

Rather than focusing solely on descriptive statistics, the analysis progresses from data preparation to exploratory analysis and finally to behavioral insights that highlight meaningful differences between low, mid, and high spending customers.

The project is placed across three Jupyter notebooks, each building on the previous one to form a complete analytical narrative.

---

## Dataset

- **Source:** Kaggle — *Credit Card Transactions Dataset*
- **Observations:** ~1.3 million transactions
- **Key Fields:**
  - Transaction amount  
  - Transaction timestamp  
  - Spending category  
  - Customer ID  
  - Merchant information  

---

## Tools & Libraries Used

- Python  
- Pandas (data manipulation)  
- Matplotlib & Seaborn (visualization)  
- Jupyter Notebook  

---

## Notebook 1: Data Cleaning & Preparation

The first notebook focuses on preparing the dataset for analysis by:

- Renaming columns for clarity

- Removing unnecessary index columns

- Handling missing values

- Converting date columns to proper datetime format

``` python


df = df.rename(columns={
    "first": "first_name",
    "last": "last_name",
    "category": "spending_type"
})

df["merch_zipcode"] = df["merch_zipcode"].fillna("Unknown")
df["trans_date_trans_time"] = pd.to_datetime(df["trans_date_trans_time"])

```


This step is neccesary for consistency and reliability before performing any analysis.

---

## Notebook 2: Exploratory Data Analysis (EDA)

The EDA notebook explores spending behavior at multiple levels.

### **Category Level**

- Total spending by category

- Average transaction size per category

---

### **Time Based Analysis**

- Monthly total spending trends

- Transaction volume over time


---

### **Transaction-Level Analysis**

- Distribution of transaction amounts

- Identification of extreme outliers using a 99th percentile cutoff

``` python

cutoff = df["amt"].quantile(0.99)
sns.histplot(df[df["amt"] <= cutoff], x="amt", bins=50)

```


<img width="879" height="550" alt="image" src="https://github.com/user-attachments/assets/0dac88f3-895a-46aa-866d-c532eb04dbb5" />


---

### **User-Level Analysis**

- Total spending per customer

- Number of transactions per customer

- Average transaction size per customer

This notebook establishes the patterns that inform deeper behavioral analysis.

<img width="984" height="1984" alt="image" src="https://github.com/user-attachments/assets/693ff756-5f53-45a9-a879-f44dac89955d" />


---

## Notebook 3: Behavioral Insights

The final notebook shifts the attention from what is happening to why it may be happening by analyzing behavior at the customer segment level.

---

### **Spender Segmentation**

Customers are grouped based on total spending:

- Low Spenders (Bottom 50%)

- Mid Spenders (50–90%)

- High Spenders (Top 10%)

---

## Key Behavioral Analysis
### **Spending Intensity vs Frequency**

A scatter plot highlights the relationship between:

- Number of transactions

- Total spending per customer

<img width="1990" height="1790" alt="image" src="https://github.com/user-attachments/assets/8332b3e4-98e4-4ed2-a0bc-85598af74f28" />


---

### **Spending Volatility by Segment**

- Boxplots compare how volatile spending is across spender groups.

<img width="843" height="547" alt="image" src="https://github.com/user-attachments/assets/f08c083b-0060-49a2-a4d4-6cdde46dd92c" />


---

### **Category Diversity Across Segments**

This analysis examines how broadly customers spend across categories.

Key findings:

- Low spenders show the greatest variability in category usage

- High and Mid spenders are consistently diversified, using nearly all categories over time

<img width="843" height="547" alt="image" src="https://github.com/user-attachments/assets/9796349d-6758-4727-ae62-8b97fe50e8ee" />


---


### **Contribution to Total Spending**

Each spender group’s share of overall spending is calculated and visualized.

```python

spend_by_group["spending_pct"] = (
    spend_by_group["total_spend"] / spend_by_group["total_spend"].sum()
) * 100

```

<img width="1461" height="855" alt="image" src="https://github.com/user-attachments/assets/8c940610-eb00-4d73-800f-c1f632c3560b" />



---


## Key Insights

- A relatively small group of mid spenders contributes a disproportionately large share of total spending

- Higher spending is associated with more consistent and diversified behavior

- Lower spenders exhibit greater behavioral variability

- Differences in spending are driven more by transaction frequency and size than by category count alone
