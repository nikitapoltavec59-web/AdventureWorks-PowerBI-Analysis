#  AdventureWorks: Sales & Profitability Power BI Dashboard

![Dashboard Preview](screenshots/dashboard_main.png)

##  Executive Summary
An interactive analytical dashboard built for **AdventureWorks** leadership to monitor key financial performance indicators, analyze geographical sales distribution, and track product category profitability across 2015–2017[cite: 1, 2].

---

##  Key Performance Indicators (KPIs)
* **Total Revenue:** $24.91M[cite: 1, 2]
* **Total Profit:** $10.46M[cite: 1, 2]
* **Profit Margin:** 41.97%[cite: 1, 2]
* **Total Units Sold:** 84k[cite: 1, 2]

---

## 🛠 Tech Stack & Architecture

* **BI Tool:** Power BI Desktop
* **Data Modeling:** Star Schema Design[cite: 1, 2]
* **Languages & Querying:** DAX, Power Query (M)

### Data Model Structure
* **Fact Table:** `Sales` (transactions, quantity, prices, relational keys)[cite: 1, 2]
* **Dimension Tables:**[cite: 1, 2]
  * `AdventureWorks_Products` (categories, subcategories, cost, models)[cite: 1, 2]
  * `AdventureWorks_Territory` (regions, countries)[cite: 1, 2]
  * `AdventureWorks_Customers` (customer demographics)[cite: 1, 2]
  * `AdventureWorks_Calendar` (date dimension with customized Year and Quarter fields)[cite: 1, 2]

---

##  Core DAX Measures & Logic

### 1. Total Profit Calculation (Row-by-Row Iteration)
```dax
Profit = 
SUMX(
    'Sales', 
    'Sales'[OrderQuantity] * (RELATED('Products'[Price]) - RELATED('Products'[Cost]))
)
```[cite: 1, 2]

### 2. Dynamic Product Ranking (ABC Analysis)
```dax
Product_Rank = 
RANKX(
    ALL('AdventureWorks_Products'), 
    [Profit], 
    , 
    DESC
)
```[cite: 1, 2]

### 3. Share of Total Profit (% Share)
```dax
Profit_Share = 
DIVIDE(
    [Profit], 
    CALCULATE([Profit], ALL('AdventureWorks_Products'))
)
```[cite: 1, 2]

### 4. Profit Margin Percentage
```dax
Profit Margin % = 
DIVIDE([Profit], [Revenue])
```[cite: 1, 2]

---

##  Key Business Insights

* **Top Geographical Market:** The United States generated the highest revenue ($7.94M), followed closely by Australia[cite: 1, 2].
* **Profit Concentration:** The top 10 product models account for over 70% of total margin profitability[cite: 1, 2].
* **Growth Trend:** Consistent revenue acceleration began in Q3 2016, peaking in Q2 2017[cite: 1, 2].

---

##  Repository Structure

```text
├── screenshots/
│   └── dashboard_main.png       # High-resolution dashboard screenshot
├── AdventureWorks_Report.pbix   # Source Power BI file
├── AdventureWorks_Case_Study.pdf# Comprehensive project case study & documentation
└── README.md                    # Project overview
