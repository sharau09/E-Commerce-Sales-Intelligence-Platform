# 🛒 E-Commerce Sales Intelligence Platform

**MCA — Data Science | Vishwakarma University, Pune**

**Author:** Sharau Jagtap

An end-to-end **E-Commerce Sales Intelligence and Analytics Platform** that transforms raw e-commerce transaction data into actionable business insights using **Python, SQL, Machine Learning, and interactive web analytics**.

The platform analyzes customers, orders, products, categories, revenue, and sales trends through an interactive **Flask-based dashboard**. It also uses **Linear Regression** to forecast product sales for the next three months.

---

## 📌 Overview

E-commerce businesses generate large volumes of transactional data. However, raw data alone does not provide meaningful business value.

The **E-Commerce Sales Intelligence Platform** processes this data and converts it into useful insights for understanding:

- Revenue performance
- Customer activity
- Order trends
- Product performance
- Category performance
- Monthly sales trends
- Top-selling products
- Future sales expectations

The system combines **SQL analytics, data processing, visualization, and Machine Learning** into a single web-based platform.

---

## 🎯 Project Objectives

The major objectives of the platform are:

1. Analyze e-commerce transaction and sales data.
2. Track important business KPIs.
3. Identify high-performing products and categories.
4. Analyze monthly revenue and order trends.
5. Perform business analysis using SQL.
6. Process and transform data using Pandas.
7. Forecast future product sales using Machine Learning.
8. Present insights through an interactive web dashboard.
9. Build an end-to-end data analytics workflow.

---

# 🚀 Key Features

## 📊 1. Executive Sales Dashboard

The dashboard provides an overview of the business through key performance indicators.

### KPIs

- 👥 Total Customers
- 🛒 Total Orders
- 💰 Total Revenue
- 📦 Total Products

These KPIs provide a quick snapshot of overall business performance.

---

## 📈 2. Monthly Sales Analysis

The platform analyzes sales performance month by month.

It provides:

- Monthly revenue
- Monthly order count
- Sales trends
- Revenue growth patterns

This helps identify changes in business performance over time.

---

## 🛍️ 3. Category Performance Analysis

The system analyzes product categories based on:

- Units sold
- Revenue generated
- Revenue contribution
- Category performance

This helps identify which categories contribute the most to overall revenue.

---

## 🏆 4. Top 10 Best-Selling Products

The platform identifies the top-performing products based on revenue.

The analysis includes:

| Metric | Description |
|---|---|
| Product | Product name |
| Category | Product category |
| Units Sold | Total quantity sold |
| Revenue | Total generated revenue |
| Rank | Product performance ranking |

This allows businesses to quickly identify their most valuable products.

---

# 🔮 5. Sales Forecasting

The platform includes a Machine Learning-based sales forecasting module.

### Algorithm

**Linear Regression**

The model learns from historical monthly product sales and predicts sales for the upcoming three months.

### Model Input

- Historical monthly sales
- Month number

### Model Output

- Forecasted units sold
- Future monthly sales predictions

### Example

```text
Historical Sales

2026-01 → 31 units
2026-02 → 32 units
2026-03 → 45 units
2026-04 → 53 units
...

Forecast

Future Month 1 → 24 units
Future Month 2 → 22 units
Future Month 3 → 21 units
```

> **Note:** Forecast values depend on the data available in the SQLite database and the trained model.

---

# 📉 6. Forecast Visualization

The forecasting module generates a visual comparison between historical and predicted sales.

The visualization includes:

- Historical sales
- Forecasted sales
- Monthly trend
- Future predictions

The generated visualization is stored in the `static` directory.

---

# 🧠 Machine Learning Workflow

The forecasting pipeline follows these steps:

```text
Raw Transaction Data
        │
        ▼
SQLite Database
        │
        ▼
SQL Data Extraction
        │
        ▼
Monthly Product Sales
        │
        ▼
Data Preprocessing
        │
        ▼
Feature Creation
        │
        ▼
Linear Regression
        │
        ▼
Future Sales Prediction
        │
        ▼
Forecast Visualization
```

---

# 🗄️ Database Design

The platform uses **SQLite** as the relational database.

## Main Tables

```text
Customers
Products
Orders
OrderItems
```

## Database Relationship

```text
┌──────────────┐
│  Customers   │
└──────┬───────┘
       │
       │ customer_id
       ▼
┌──────────────┐
│    Orders    │
└──────┬───────┘
       │
       │ order_id
       ▼
┌──────────────┐
│  OrderItems  │
└──────┬───────┘
       │
       │ product_id
       ▼
┌──────────────┐
│   Products   │
└──────────────┘
```

---

# 🔍 SQL Analytics

SQL is used extensively to extract and analyze business information.

The platform performs queries for:

- Total customers
- Total orders
- Total revenue
- Total products
- Monthly revenue
- Monthly orders
- Category-wise revenue
- Product-level sales
- Top-performing products

---

## 💰 Revenue by Category

```sql
SELECT
    p.category,
    SUM(oi.quantity * oi.price_at_purchase) AS revenue
FROM Products p
JOIN OrderItems oi
    ON p.product_id = oi.product_id
GROUP BY p.category
ORDER BY revenue DESC;
```

---

## 🏆 Top 10 Products

```sql
SELECT
    p.product_id,
    p.name,
    p.category,
    SUM(oi.quantity) AS units_sold,
    SUM(oi.quantity * oi.price_at_purchase) AS revenue
FROM Products p
JOIN OrderItems oi
    ON p.product_id = oi.product_id
GROUP BY
    p.product_id,
    p.name,
    p.category
ORDER BY revenue DESC
LIMIT 10;
```

---

## 📅 Monthly Sales

```sql
SELECT
    strftime('%Y-%m', order_date) AS month,
    COUNT(order_id) AS orders,
    SUM(total_amount) AS revenue
FROM Orders
GROUP BY strftime('%Y-%m', order_date)
ORDER BY month;
```

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Python** | Core development and analytics |
| **SQL** | Data querying and business analysis |
| **SQLite** | Relational database |
| **Pandas** | Data manipulation and preprocessing |
| **Scikit-learn** | Machine Learning |
| **Linear Regression** | Sales forecasting |
| **Matplotlib** | Data visualization |
| **Flask** | Backend web application |
| **HTML** | Dashboard structure |
| **CSS** | Dashboard styling |
| **Git** | Version control |
| **GitHub** | Source code management |

---

# 📁 Project Structure

```text
Ecommerce-Sales-Intelligence/
│
├── analysis/
│   └── sales_forecasting.py
│
├── data/
│   └── ecommerce.db
│
├── database/
│   └── queries.sql
│
├── static/
│   ├── forecast_data.json
│   ├── product_107_forecast.png
│   └── sales_forecast.png
│
├── templates/
│   └── dashboard.html
│
├── app.py
├── README.md
└── .gitignore
```

---

# ⚙️ Installation & Setup

## 1. Clone the Repository

```bash
git clone https://github.com/datasnitch/Ecommerce-Sales-Intelligence.git
```

Navigate into the project:

```bash
cd Ecommerce-Sales-Intelligence
```

---

## 2. Create a Virtual Environment

### macOS / Linux

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

### Windows

```bash
python -m venv .venv
```

Activate:

```bash
.venv\Scripts\activate
```

---

## 3. Install Dependencies

```bash
pip install flask pandas matplotlib scikit-learn
```

---

# ▶️ Run the Application

Start the Flask application:

```bash
python app.py
```

The application will run locally.

Open the following URL in your browser:

```text
http://127.0.0.1:5000
```

You can then access the **E-Commerce Sales Intelligence Dashboard**.

---

# 🔮 Generate Sales Forecast

Run:

```bash
python analysis/sales_forecasting.py
```

The forecasting script performs the following steps:

```text
Connect to SQLite
       ↓
Retrieve Sales Data
       ↓
Aggregate Monthly Sales
       ↓
Prepare ML Dataset
       ↓
Train Linear Regression
       ↓
Predict Future Sales
       ↓
Generate Visualization
       ↓
Save Forecast Output
```

---

# 📊 Dashboard Architecture

```text
                    E-Commerce Data
                           │
                           ▼
                   SQLite Database
                           │
                           ▼
                    SQL Analytics
                           │
             ┌─────────────┴─────────────┐
             ▼                           ▼
       Business KPIs              ML Forecasting
             │                           │
             ▼                           ▼
      Flask Backend              Linear Regression
             │                           │
             └─────────────┬─────────────┘
                           ▼
                  Interactive Dashboard
                           │
                           ▼
                Business Intelligence
```

---

# 💡 Business Insights

The platform can help businesses answer important questions such as:

### Revenue

- What is the total revenue?
- How is revenue changing month by month?
- Which categories generate the most revenue?

### Products

- Which products sell the most?
- Which products generate the highest revenue?
- What are the top-performing products?

### Customers & Orders

- How many customers are active?
- How many orders have been placed?
- How does order volume change over time?

### Forecasting

- What could future product sales look like?
- Is a product's sales trend increasing or decreasing?
- What sales levels can be expected over the next three months?

---

# 📈 Potential Business Applications

This platform can be extended for real-world e-commerce use cases such as:

- Sales performance monitoring
- Inventory planning
- Product performance analysis
- Revenue forecasting
- Business reporting
- Category optimization
- Demand planning
- Management dashboards

---

# 🔮 Future Enhancements

The platform can be further enhanced with advanced analytics and AI capabilities.

### Advanced Machine Learning

- Multiple product forecasting
- Time-series forecasting using ARIMA
- Prophet-based forecasting
- XGBoost forecasting
- LSTM-based demand forecasting

### Customer Analytics

- Customer segmentation
- RFM analysis
- Customer Lifetime Value
- Churn prediction
- Customer behavior analysis

### Advanced Intelligence

- Sales anomaly detection
- Demand prediction
- Product recommendation system
- Personalized product recommendations
- Automated business insights
- Natural Language querying of business data

### Dashboard Enhancements

- Interactive filters
- Date-range filtering
- Product filtering
- Category filtering
- Drill-down analytics
- Exportable reports

### Deployment

Potential deployment options include:

- Docker
- AWS
- Azure
- Google Cloud
- Streamlit
- Render
- Railway

---

# 🌟 Skills Demonstrated

This project demonstrates practical experience in:

- Python Development
- SQL
- Database Management
- Data Cleaning
- Data Analysis
- Exploratory Data Analysis
- Business Intelligence
- Data Visualization
- Machine Learning
- Regression
- Sales Forecasting
- Flask Development
- Dashboard Development
- Git & GitHub

---

# 👨‍💻 Author

## Sharayu Jagtap

**MCA — Data Science**  
**Vishwakarma University, Pune**

Interested in:

- Artificial Intelligence
- Machine Learning
- Data Science
- Generative AI
- LLM Applications
- AI Agents
- Data Analytics

### GitHub

https://github.com/datasnitch

---

# 🎓 Academic Information

| Field | Details |
|---|---|
| **Project** | E-Commerce Sales Intelligence Platform |
| **Program** | MCA — Data Science |
| **University** | Vishwakarma University, Pune |
| **Project Area** | Data Science, Machine Learning & Business Intelligence |
| **Application Type** | Web-Based Analytics Platform |

---

# 📜 License

This project is developed for **educational and academic purposes**.

---

## ⭐ Project Summary

**E-Commerce Sales Intelligence Platform** is an end-to-end analytics solution that combines **SQL, Python, Machine Learning, data visualization, and Flask** to transform e-commerce transaction data into actionable business intelligence and future sales predictions.
