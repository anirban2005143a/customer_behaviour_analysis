# 🛍️ Customer Behaviour Analysis

An end-to-end **Customer Behaviour Analysis** project using **Python, PostgreSQL, and Power BI** to transform raw customer shopping data into meaningful business insights through data cleaning, feature engineering, database integration, and interactive dashboard visualization.

---

## 📌 Project Overview

Understanding customer behaviour is essential for businesses looking to improve customer experience, increase sales, identify valuable customer segments, and make data-driven decisions.

This project analyzes a customer shopping behaviour dataset containing **3,900 customer records** with information related to:

* Customer demographics
* Products and categories
* Purchase amounts
* Subscription status
* Payment methods
* Shipping methods
* Discounts and promotions
* Purchase frequency
* Customer ratings

The project follows an end-to-end analytics workflow:

```text
Raw Data
   ↓
Data Cleaning & EDA
   ↓
Feature Engineering
   ↓
PostgreSQL
   ↓
Power BI Dashboard
   ↓
Business Insights
```

---

## 🎯 Business Objectives

The analysis focuses on answering important business questions such as:

* Who are the customers and how are they distributed across different age groups?
* Which product categories and products are purchased most frequently?
* How much do customers spend?
* How does purchasing behaviour vary across different age groups and genders?
* What payment methods are preferred by customers?
* How frequently do customers make purchases?
* How does subscription status relate to customer behaviour?
* What role do discounts and promotions play in purchasing behaviour?
* Which shipping methods are most commonly used?
* How do customer ratings vary across product categories?
* How can businesses use these insights to improve customer engagement and retention?

---

## 📊 Dataset

The project uses a customer shopping behaviour dataset containing **3,900 records** and **18 original columns**.

### Dataset Features

| Column                 | Description                             |
| ---------------------- | --------------------------------------- |
| Customer ID            | Unique identifier for each customer     |
| Age                    | Customer age                            |
| Gender                 | Customer gender                         |
| Item Purchased         | Product purchased by the customer       |
| Category               | Product category                        |
| Purchase Amount (USD)  | Amount spent on the purchase            |
| Location               | Customer location                       |
| Size                   | Product size                            |
| Color                  | Product color                           |
| Season                 | Season associated with the purchase     |
| Review Rating          | Customer review/rating                  |
| Subscription Status    | Whether the customer has a subscription |
| Shipping Type          | Shipping method selected                |
| Discount Applied       | Whether a discount was applied          |
| Promo Code Used        | Whether a promotional code was used     |
| Previous Purchases     | Number of previous purchases            |
| Payment Method         | Payment method used                     |
| Frequency of Purchases | Customer purchase frequency             |

---

## 🧹 Data Cleaning & Preparation

Data cleaning and feature engineering were performed using **Python, Pandas, and Jupyter Notebook**.

The complete workflow is available in:

```text
data_cleaning.ipynb
```

### 1. Data Loading

The raw CSV dataset is loaded into a Pandas DataFrame.

```python
df = pd.read_csv("customer_shopping_behavior.csv")
```

### 2. Exploratory Data Analysis

Initial inspection includes:

* Dataset preview
* Descriptive statistics
* Column inspection
* Missing-value analysis
* Numerical feature analysis

---

### 3. Missing Value Treatment

The `Review Rating` column contained **37 missing values**.

Instead of dropping these records, missing ratings were filled using the **median review rating within each product category**.

```python
df['Review Rating'] = (
    df.groupby("Category")['Review Rating']
    .transform(lambda x: x.fillna(x.median()))
)
```

This preserves the records while using category-specific information to handle missing ratings.

---

### 4. Column Standardization

Column names were converted into a consistent **lowercase and underscore-based format**.

For example:

```text
Purchase Amount (USD)
```

was transformed into:

```text
purchase_amount
```

This makes the dataset easier to work with in Python, PostgreSQL, and Power BI.

---

### 5. Age Group Feature Engineering

A new `age_group` feature was created to make demographic analysis easier.

| Age   | Age Group   |
| ----- | ----------- |
| ≤ 25  | Young Adult |
| 26–34 | Adult       |
| 35–54 | Middle Aged |
| 55+   | Senior      |

This enables customer behaviour to be compared across meaningful demographic segments.

---

### 6. Purchase Frequency Transformation

The categorical purchase frequency field was converted into an approximate number of days.

| Purchase Frequency | Days |
| ------------------ | ---: |
| Weekly             |    7 |
| Fortnightly        |   14 |
| Bi-Weekly          |   14 |
| Monthly            |   30 |
| Quarterly          |   90 |
| Every 3 Months     |   90 |
| Annually           |  365 |

A new feature called `purchase_frequency_days` was created from this mapping.

---

### 7. Redundant Column Removal

The notebook checks whether `discount_applied` and `promo_code_used` contain different information.

Since the values were found to be redundant, `promo_code_used` was removed from the cleaned dataset.

---

## 🏗️ Project Architecture

```text
                 ┌──────────────────────┐
                 │   Customer CSV Data  │
                 │     3,900 Records    │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │    Python + Pandas   │
                 │                      │
                 │ • Data Cleaning      │
                 │ • EDA               │
                 │ • Missing Values     │
                 │ • Feature Engineering│
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │     PostgreSQL       │
                 │                      │
                 │   customer table     │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │       Power BI       │
                 │                      │
                 │ Interactive Dashboard│
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │   Business Insights  │
                 │ & Decision Making    │
                 └──────────────────────┘
```

---

## 📊 Power BI Dashboard

The cleaned customer data is connected to **Power BI** to create an interactive dashboard for exploring customer behaviour and purchasing patterns.

The dashboard provides an overview of key business metrics and allows analysis across multiple dimensions.

### Dashboard Analysis

The dashboard covers areas such as:

* Customer demographics
* Age-group distribution
* Gender-based analysis
* Product and category performance
* Purchase amounts
* Subscription behaviour
* Payment methods
* Purchase frequency
* Shipping preferences
* Discounts and promotions
* Customer ratings
* Seasonal purchasing behaviour
* Customer locations

### 🖼️ Dashboard Preview

![Customer Behaviour Dashboard](dashboard/Screenshot%202026-09-05%20215157.png)

### 🎥 Dashboard Walkthrough

A dashboard walkthrough recording is available in the repository:

`dashboard/dashboard_recording.mp4`

---

## 📁 Repository Structure

```text
customer_behaviour_analysis/
│
├── dashboard/
│   ├── Screenshot 2026-09-05 215157.png
│   └── dashboard_recording.mp4
│
├── Business Problem Document.pdf
├── customer_behaivior_analysis.pbix
├── customer_shopping_behavior.csv
├── data_cleaning.ipynb
└── README.md
```

### File Description

| File                                         | Purpose                                            |
| -------------------------------------------- | -------------------------------------------------- |
| `customer_shopping_behavior.csv`             | Raw customer shopping behaviour dataset            |
| `data_cleaning.ipynb`                        | Python-based data cleaning and feature engineering |
| `customer_behaivior_analysis.pbix`           | Power BI dashboard                                 |
| `Business Problem Document.pdf`              | Project/business problem documentation             |
| `dashboard/Screenshot 2026-09-05 215157.png` | Dashboard preview                                  |
| `dashboard/dashboard_recording.mp4`          | Dashboard walkthrough                              |
| `README.md`                                  | Project documentation                              |

---

## 🛠️ Tech Stack

### 🐍 Programming & Data Analysis

* Python
* Pandas
* NumPy
* Jupyter Notebook

### 🗄️ Database

* PostgreSQL
* SQLAlchemy
* Psycopg2

### 📊 Business Intelligence

* Microsoft Power BI

### 📁 Data & Reporting

* CSV
* Data Visualization
* Interactive Dashboards
* Business Analysis

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

* Python 3.x
* Jupyter Notebook / JupyterLab
* PostgreSQL
* Power BI Desktop

### 1. Clone the Repository

```bash
git clone https://github.com/anirban2005143a/customer_behaviour_analysis.git
```

### 2. Navigate into the Project

```bash
cd customer_behaviour_analysis
```

### 3. Install Python Dependencies

```bash
pip install pandas numpy sqlalchemy psycopg2-binary
```

### 4. Run the Data Cleaning Notebook

Open:

```text
data_cleaning.ipynb
```

Run the notebook sequentially.

The notebook performs:

```text
Load Dataset
      ↓
Explore Dataset
      ↓
Check Missing Values
      ↓
Handle Missing Ratings
      ↓
Standardize Columns
      ↓
Create Age Groups
      ↓
Create Purchase Frequency Days
      ↓
Remove Redundant Columns
      ↓
Load Cleaned Data into PostgreSQL
```

---

## 🗄️ PostgreSQL Setup

Create a PostgreSQL database named:

```text
customer_behaviour
```

The notebook is configured to connect using:

```text
Host:     localhost
Port:     5432
Database: customer_behaviour
```

Update the database credentials in the notebook before running the PostgreSQL loading step.

> **Security Note:** Never commit real database passwords, API keys, or other credentials to GitHub.

The cleaned dataset is written to the PostgreSQL table:

```text
customer
```

---

## 📈 Key Analytical Dimensions

### 👥 Customer Demographics

Analyze customer behaviour by:

* Age
* Age group
* Gender
* Location

### 🛒 Product Behaviour

Analyze:

* Product category
* Individual products
* Product size
* Product color
* Season

### 💰 Purchasing Behaviour

Analyze:

* Purchase amount
* Previous purchases
* Purchase frequency
* Purchase frequency in days

### 💳 Payment Behaviour

Compare customer preferences across:

* Credit Card
* PayPal
* Cash
* Venmo
* Other available payment methods

### 📦 Delivery Behaviour

Analyze customer preferences across different shipping methods.

### 🎁 Promotions

Evaluate purchasing behaviour in relation to:

* Discounts
* Promotional activity

### ⭐ Customer Experience

Use review ratings to understand customer satisfaction across different product categories.

---

## 💡 Business Insights

The project is designed to support real-world business decisions through customer behaviour analysis.

### Customer Segmentation

Grouping customers by age and purchasing behaviour can help businesses create more targeted marketing campaigns.

### Product Strategy

Category and product-level analysis can help identify products with higher purchasing activity and customer engagement.

### Customer Retention

Purchase frequency and previous purchase behaviour can help identify highly engaged customers and customers who may require targeted retention campaigns.

### Subscription Strategy

Comparing subscribed and non-subscribed customers can help businesses understand the relationship between subscription status and purchasing behaviour.

### Payment Optimization

Understanding preferred payment methods can help businesses optimize the checkout experience and prioritize popular payment options.

### Promotional Strategy

Analyzing discounts and promotional activity can help businesses understand how promotional strategies relate to customer purchases.

---

## 🔍 Key Data Quality Findings

During the cleaning process:

* The dataset contains **3,900 records**.
* The original dataset contains **18 columns**.
* `Review Rating` contained **37 missing values**.
* Missing review ratings were filled using **category-level medians**.
* Column names were standardized for easier database and analytical use.
* An `age_group` feature was created.
* A `purchase_frequency_days` feature was created.
* `promo_code_used` was removed because it duplicated the information contained in `discount_applied`.
* The cleaned dataset was prepared for PostgreSQL storage.

---

## 📊 Project Deliverables

This repository provides the complete project assets:

* ✅ Raw customer shopping dataset
* ✅ Python data-cleaning notebook
* ✅ Feature engineering workflow
* ✅ PostgreSQL integration
* ✅ Power BI dashboard
* ✅ Dashboard screenshot
* ✅ Dashboard walkthrough recording
* ✅ Business problem documentation

---

## 🔮 Future Improvements

The project can be extended further with:

* Customer Lifetime Value (CLV) analysis
* RFM customer segmentation
* Customer churn prediction
* Purchase amount prediction
* Product recommendation systems
* Customer propensity modelling
* Advanced customer segmentation using clustering
* Automated Power BI data refresh
* SQL-based analytical queries
* Time-series sales analysis
* Predictive analytics and machine learning

---

## 📚 Skills Demonstrated

This project demonstrates practical skills in:

* Data Cleaning
* Exploratory Data Analysis
* Feature Engineering
* Data Transformation
* Customer Behaviour Analysis
* Business Intelligence
* PostgreSQL
* Python
* Pandas
* NumPy
* Power BI
* Data Visualization
* Dashboard Development
* Business Problem Solving
* Data-driven Decision Making

---

## 👨‍💻 Author

### Anirban Das

**GitHub:**
https://github.com/anirban2005143a

---

## ⭐ Project Highlights

If you found this project useful, consider giving the repository a ⭐ on GitHub.

This project demonstrates how raw customer data can be transformed into a structured analytical dataset and ultimately into an interactive business intelligence solution.

---

## 📄 License

This project is intended for **educational, portfolio, and data analytics demonstration purposes**.
