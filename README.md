# Supply Chain & Logistics KPI Tracker 📦

An end-to-end Data Analytics project analyzing supply chain performance and logistics KPIs using Python for ETL & EDA and Microsoft Power BI for interactive dashboard development.

---

## 📌 Problem Statement

Inefficient supply chains lead to delayed deliveries, excess inventory, and lost revenue. This project analyzes the DataCo Smart Supply Chain dataset from Kaggle to compute critical logistics KPIs, identify bottlenecks, underperforming regions, and delivery inefficiencies, and presents actionable insights through an interactive Power BI dashboard to support data-driven supply chain decisions.

---

## 📁 Project Structure

```
supply-chain-kpi-tracker/
├── data/
│   └── supply_chain_clean.csv          # Cleaned & transformed dataset
├── notebooks/
│   └── supply_chain_eda.ipynb          # Full ETL & EDA notebook (Google Colab)
├── visuals/
│   ├── delivery_status.png             # Delivery Status Distribution
│   ├── late_by_region.png              # Late Delivery Rate by Region
│   ├── monthly_trend.png               # Monthly Revenue Trend
│   └── profit_category.png             # Profit by Product Category
├── powerbi/
│   └── SupplyChain_Dashboard.pbix      # Power BI Dashboard file
└── README.md
```

---

## 🛠️ Tools & Technologies

| Category | Tools |
|---|---|
| Language | Python |
| Libraries | pandas, NumPy, Matplotlib, Seaborn |
| BI Tool | Microsoft Power BI |
| DAX | Custom KPI measures |
| Environment | Google Colab |
| Version Control | Git, GitHub |

---

## 📊 Dataset

- **Source:** [DataCo Smart Supply Chain for Big Data Analysis — Kaggle](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)
- **Size:** 180,000+ rows × 53 columns
- **Key Features:** Order Date, Shipping Date, Delivery Status, Actual vs Scheduled Shipping Days, Order Total, Profit, Product Category, Customer Segment, Region

---

## 🔧 ETL Process

- Dropped columns with excessive nulls and irrelevant PII fields (`Customer Password`, `Customer Email`)
- Parsed and standardized date columns (`OrderDate`, `ShippingDate`)
- Renamed columns for readability and Power BI compatibility
- Engineered new KPI features:
  - `OnTime` — whether actual shipping days ≤ scheduled shipping days
  - `LateDelivery` — flag for delayed shipments
  - `FulfillmentGap` — difference between actual and scheduled shipping days

---

## 📈 KPIs Computed

| KPI | Description |
|---|---|
| On-Time Delivery Rate | % of orders delivered within scheduled time |
| Late Delivery Rate | % of orders delayed, broken down by region |
| Avg Fulfillment Gap | Avg days by which shipments exceed schedule |
| Total Revenue | Sum of all order totals |
| Total Profit | Sum of profit across all orders |
| Avg Order Value | Revenue per unit quantity by category |

---

## 🔍 Key Findings

- **On-Time Delivery Rate: ~40%** — majority of orders face delays
- **Central America and Western Europe** have the highest late delivery rates
- **Fishing and Cleats** are the most profitable product categories
- Orders from the **Consumer segment** account for the highest revenue share
- A clear **seasonal revenue spike** is observed in Q4 across all years
- Average fulfillment gap of **~2 days** indicates systemic scheduling underestimation

---

## 📋 Power BI Dashboard

**Page 1 — Executive Overview**
- KPI Cards: Total Orders, On-Time Delivery Rate %, Total Revenue, Total Profit
- Donut chart: Delivery Status breakdown
- Bar chart: Orders by Region
- Slicers: Region, Customer Segment

**Page 2 — Logistics Performance**
- Bar chart: Late Delivery Rate by Region (conditional formatting — red/green)
- Clustered bar: Actual vs Scheduled Shipping Days by Category
- Line chart: Monthly On-Time Delivery Rate trend
- Slicers: Delivery Status, Category

**Page 3 — Product & Revenue Analysis**
- Bar chart: Total Profit by Category
- Table: Category, Total Revenue, Total Quantity, Avg Order Value
- Line chart: Monthly Revenue Trend
- Slicers: Region, Category

---

## 📐 DAX Measures

```DAX
Total Orders = COUNT('supply_chain_clean'[Order Id])

On-Time Delivery Rate =
DIVIDE(
    CALCULATE(COUNT('supply_chain_clean'[OnTime]),
    'supply_chain_clean'[OnTime] = TRUE()),
    COUNT('supply_chain_clean'[OnTime]),
    0
) * 100

Total Revenue = SUM('supply_chain_clean'[OrderTotal])

Total Profit = SUM('supply_chain_clean'[Profit])

Avg Fulfillment Gap = AVERAGE('supply_chain_clean'[FulfillmentGap])

Late Delivery Rate =
DIVIDE(
    CALCULATE(COUNT('supply_chain_clean'[LateDelivery]),
    'supply_chain_clean'[LateDelivery] = TRUE()),
    COUNT('supply_chain_clean'[LateDelivery]),
    0
) * 100
```

---

## 🚀 How to Run

1. Clone the repository
```bash
git clone https://github.com/varadmore23/supply-chain-kpi-tracker.git
cd supply-chain-kpi-tracker
```

2. Open `notebooks/supply_chain_eda.ipynb` in Google Colab or Jupyter Notebook

3. Upload the raw dataset from Kaggle and run all cells sequentially

4. Open `powerbi/SupplyChain_Dashboard.pbix` in Microsoft Power BI Desktop

---

## 👤 Author

**Varad More**
- 📧 varad.more23@spit.ac.in
- 🔗 [LinkedIn](https://www.linkedin.com/in/varad-more-450777398/)
- 🐙 [GitHub](https://github.com/varadmore23)
