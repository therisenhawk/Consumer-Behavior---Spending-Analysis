# 📊 Consumer Behavior & Spending Analysis

## 📌 Project Overview

In this project, I analyzed real-world credit card transaction data to understand **how consumers spend**, **how spending behavior differs across users**, and **which patterns emerge when customers are grouped by spending intensity**.

Rather than focusing solely on descriptive statistics, the analysis progresses from data preparation to exploratory analysis and finally to behavioral insights that highlight meaningful differences between low, mid, and high spending customers.

The project is placed across three Jupyter notebooks, each building on the previous one to form a complete analytical narrative.

---

## 📂 Dataset

- **Source:** Kaggle — *Credit Card Transactions Dataset*
- **Observations:** ~1.3 million transactions
- **Key Fields:**
  - Transaction amount  
  - Transaction timestamp  
  - Spending category  
  - Customer ID  
  - Merchant information  

---

## 🛠️ Tools & Libraries Used

- Python  
- Pandas (data manipulation)  
- Matplotlib & Seaborn (visualization)  
- Jupyter Notebook  

---

## 🧹 Notebook 1: Data Cleaning & Preparation

The first notebook focuses on preparing the dataset for analysis by:

Renaming columns for clarity

Removing unnecessary index columns

Handling missing values

Converting date columns to proper datetime format

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


## 🔍 Notebook 2: Exploratory Data Analysis (EDA)

The EDA notebook explores spending behavior at multiple levels.

### **Category Level**

- Total spending by category

- Average transaction size per category

📌 Insert figure: Horizontal bar chart of total spending by category


### **Time Based Analysis**

- Monthly total spending trends

- Transaction volume over time

📌 Insert figure: Monthly spending trend line chart


### **Transaction-Level Analysis**

- Distribution of transaction amounts

- Identification of extreme outliers using a 99th percentile cutoff

``` python

cutoff = df["amt"].quantile(0.99)
sns.histplot(df[df["amt"] <= cutoff], x="amt", bins=50)

```


📌 Insert figure: Histogram of transaction amounts


### **User-Level Analysis**

- Total spending per customer

- Number of transactions per customer

- Average transaction size per customer

This notebook establishes the patterns that inform deeper behavioral analysis.

## 🧠 Notebook 3: Behavioral Insights

The final notebook shifts the attention from what is happening to why it may be happening by analyzing behavior at the customer segment level.

### **Spender Segmentation**

Customers are grouped based on total spending:

- Low Spenders (Bottom 50%)

- Mid Spenders (50–90%)

- High Spenders (Top 10%)

## Key Behavioral Analysis
### **🔹 Spending Intensity vs Frequency**

A scatter plot highlights the relationship between:

Number of transactions

- Total spending per customer

📌 Insert figure: Scatter plot of total spend vs number of transactions

### **🔹 Spending Volatility by Segment**

- Boxplots compare how volatile spending is across spender groups.

📌 Insert figure: Boxplot of spending volatility by spender group

### **🔹 Category Diversity Across Segments**

This analysis examines how broadly customers spend across categories.

Key findings:

- Low spenders show the greatest variability in category usage

- High spenders are consistently diversified, using nearly all categories over time

📌 Insert figure: Category diversity boxplot


### **🔹 Contribution to Total Spending**

Each spender group’s share of overall spending is calculated and visualized.

```python

spend_by_group["spending_pct"] = (
    spend_by_group["total_spend"] / spend_by_group["total_spend"].sum()
) * 100

```

📌 Insert figure: Bar chart of spending share by spender group


## 📈 Key Insights

- A relatively small group of mid spenders contributes a disproportionately large share of total spending

- Higher spending is associated with more consistent and diversified behavior

- Lower spenders exhibit greater behavioral variability

- Differences in spending are driven more by transaction frequency and size than by category count alone