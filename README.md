# Adidas Customer Behaviour Analytics

## Project Overview

This project analyzes Adidas customer purchasing behavior using Python, SQL Server, and Power BI. The objective is to transform raw customer transaction data into actionable business insights that can support marketing, customer retention, product strategy, and revenue optimization decisions.

The project follows a complete analytics workflow:

**Data Cleaning & Feature Engineering (Python) → Data Storage & Analysis (SQL Server) → Interactive Dashboarding (Power BI)**

---

## Business Problem

Understanding customer behavior is critical for retail organizations. Adidas collects large volumes of customer transaction data, but raw data alone does not provide meaningful business insights.

This project aims to answer key business questions such as:

* Which customer segments generate the most revenue?
* Do subscribers spend more than non-subscribers?
* Which products receive the highest ratings?
* How effective are discounts in driving purchases?
* Which age groups contribute the most revenue?
* What purchasing patterns exist across customer segments?

---

## Dataset Overview

The dataset contains customer-level purchase information including:

* Customer ID
* Age
* Gender
* Category
* Product Purchased
* Purchase Amount
* Review Rating
* Shipping Type
* Subscription Status
* Discount Applied
* Previous Purchases
* Frequency of Purchases

---

## Tech Stack

### Python

* Pandas
* NumPy
* SQLAlchemy
* PyODBC

### Database

* Microsoft SQL Server

### Business Intelligence

* Power BI

### Version Control

* Git
* GitHub

---

## Data Cleaning & Feature Engineering

The data preparation phase was performed using Python.

### Handling Missing Values

Review ratings contained missing values.

Missing ratings were replaced using:

```python
df['Review Rating'] = df.groupby('Category')['Review Rating'].transform(
    lambda x: x.fillna(x.median())
)
```

This approach preserves category-level behavior and avoids introducing bias.

---

### Column Standardization

Columns were converted to snake_case naming convention.

Example:

```python
Purchase Amount (EUR)
```

became:

```python
purchase_amount
```

---

### Customer Age Segmentation

Customers were divided into four age groups:

* Young Adult
* Adult
* Middle-aged
* Senior

Using:

```python
pd.qcut()
```

This enables demographic analysis and customer segmentation.

---

### Purchase Frequency Transformation

Purchase frequency categories were converted into numerical values.

Examples:

| Frequency | Days |
| --------- | ---- |
| Weekly    | 7    |
| Monthly   | 30   |
| Quarterly | 90   |
| Annually  | 365  |

This transformation supports quantitative customer behavior analysis.

---

## SQL Analysis

The cleaned dataset was loaded into SQL Server for business analysis.

### Q1. Revenue by Gender

Business Question:

Which gender contributes the most revenue?

Analysis:

```sql
select gender,
sum(purchase_amount) as revenue
from customer
group by gender
```

---

### Q2. High-Spending Discount Customers

Business Question:

Which customers used discounts but still spent above average?

Purpose:

Identify valuable customers who respond positively to promotions.

---

### Q3. Highest Rated Products

Business Question:

Which products have the highest average customer ratings?

Purpose:

Identify customer favorites and potential flagship products.

---

### Q4. Shipping Type Performance

Business Question:

How does average spending differ across shipping methods?

Purpose:

Understand whether premium shipping customers spend more.

---

### Q5. Subscriber vs Non-Subscriber Analysis

Business Question:

Do subscribers generate more revenue?

Metrics:

* Total Customers
* Average Purchase Amount
* Total Revenue

Purpose:

Evaluate subscription program effectiveness.

---

### Q6. Products Most Frequently Purchased with Discounts

Business Question:

Which products are most dependent on discounts?

Purpose:

Optimize discount strategy.

---

### Q7. Customer Segmentation

Customers were classified as:

| Segment   | Criteria                |
| --------- | ----------------------- |
| New       | ≤ 1 Previous Purchase   |
| Returning | 2–10 Previous Purchases |
| Loyal     | >10 Previous Purchases  |

Purpose:

Measure customer loyalty distribution.

---

### Q8. Top Products Within Each Category

Used SQL Window Functions:

```sql
ROW_NUMBER()
```

Purpose:

Identify category leaders.

---

### Q9. Repeat Buyer Subscription Analysis

Business Question:

Are repeat customers more likely to subscribe?

Purpose:

Understand loyalty-program adoption.

---

### Q10. Revenue Contribution by Age Group

Business Question:

Which demographic segments drive revenue?

Purpose:

Support targeted marketing campaigns.

---

## Power BI Dashboard

The dashboard provides an executive-level overview of customer behavior.

### KPI Cards

* Average Purchase Amount
* Average Review Rating
* Total Customers
* Total Sales

### Interactive Filters

* Subscription Status
* Gender
* Product Category
* Shipping Type

### Visualizations
<img width="653" height="371" alt="image" src="https://github.com/user-attachments/assets/06173f3b-d993-4f17-a483-44c21ad6508e" />

#### Subscription Analysis

* Subscriber vs Non-Subscriber Distribution

#### Revenue by Category

* Category-wise revenue contribution

#### Sales by Category

* Customer count by category

#### Revenue by Age Group

* Revenue contribution by demographic segment

#### Customer Distribution by Age Group

* Customer volume across age groups

---

## Key Insights

* Clothing generates the highest revenue among all product categories.
* Subscription customers represent a significant portion of total sales.
* Young Adult customers contribute the largest customer base.
* Discounts influence purchasing behavior for several product categories.
* Customer behavior varies considerably across age segments and product categories.

---

## Future Enhancements

* Customer Lifetime Value (CLV) Analysis
* RFM Segmentation
* Churn Prediction
* Product Recommendation System
* Predictive Revenue Forecasting
* Power BI Incremental Refresh

---

## Author

Shashank Raman

Data Analyst | SQL | Power BI | Python | Business Intelligence

Open to Data Analytics and Business Intelligence opportunities in Germany.
