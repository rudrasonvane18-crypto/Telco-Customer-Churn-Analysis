# Telco Customer Churn Analysis | Power BI

## Project Overview
This project analyzes telecom customer churn using **Microsoft Power BI**. It explores churn patterns, monthly charges, contract types, tenure, internet services, payment methods, and support services to identify opportunities to improve customer retention.

The report contains three interactive dashboard pages designed to turn customer-level data into business insights.

## Business Objectives
- Measure customer churn and retention.
- Compare churn across contract types, tenure groups, internet services, and payment methods.
- Examine monthly charges associated with churned customers.
- Identify customer segments that may benefit from targeted retention efforts.
- Present findings through KPIs and interactive visuals.

## Tools and Skills
- **Power BI Desktop** — dashboard design and visualization
- **Power Query** — data cleaning and transformation
- **DAX** — measures and calculated columns
- **Data analysis** — segmentation, KPI analysis, and recommendations
- **GitHub** — project documentation and portfolio presentation

## Dashboards

### 1. Customer Churn Overview
**Purpose:** Give an executive-level view of churn and retention.

Includes:
- Total customers, churned customers, retained customers, and churn rate
- Customer churn distribution
- Churn rate by contract
- Churn rate by internet service
- Slicers for gender, contract, and internet service

Screenshot: `Screenshots/01_Churn_Overview.png`

### 2. Revenue & Customer Value
**Purpose:** Explore customer charges and monthly-charge exposure associated with churn.

Includes:
- Total monthly charges
- Average monthly charges
- Average customer tenure
- Monthly charges associated with churned customers
- Monthly charges by contract
- Churned monthly charges by internet service
- Average monthly charges by payment method
- Customer tenure versus monthly charges, segmented by churn

Screenshot: `Screenshots/02_Revenue_Analysis.png`

> Note: Churned monthly charges indicate charges associated with customers who left. They are not confirmed lost revenue or profit.

### 3. Customer Retention & Risk Drivers
**Purpose:** Compare churn patterns across customer segments and support services.

Includes:
- Churn rate by tenure group
- Churn rate by technical support status
- Churn matrix by contract and internet service
- Customer-level detail table
- Segment-level findings and retention recommendations

Screenshot: `Screenshots/03_Retention_Insights.png`

## Data Preparation
Dataset: `WA_Fn-UseC_-Telco-Customer-Churn.csv`

Key preparation steps:
1. Checked column names and data types in Power Query.
2. Kept customer IDs as text.
3. Converted numeric fields such as `tenure` and `MonthlyCharges` to appropriate numeric types.
4. Reviewed blank values in `TotalCharges`. The original dataset contains 11 blank/non-numeric entries in this field; retain them as null unless a justified treatment is documented.
5. Checked customer IDs for blanks and duplicates.
6. Validated row counts and KPI measures after loading the data.

## Key DAX Measures
The formulas below assume the imported table is named `Customers` and the original column names are unchanged. Update names if your model differs.

### Total Customers
```dax
Total Customers =
DISTINCTCOUNT(Customers[customerID])
```

### Churned Customers
```dax
Churned Customers =
CALCULATE(
    [Total Customers],
    Customers[Churn] = "Yes"
)
```

### Retained Customers
```dax
Retained Customers =
CALCULATE(
    [Total Customers],
    Customers[Churn] = "No"
)
```

### Churn Rate
```dax
Churn Rate =
DIVIDE(
    [Churned Customers],
    [Total Customers],
    0
)
```
Format this measure as **Percentage** in Power BI. Do not multiply the result by 100 in the formula.

### Retention Rate
```dax
Retention Rate =
DIVIDE(
    [Retained Customers],
    [Total Customers],
    0
)
```

### Total Monthly Charges
```dax
Total Monthly Charges =
SUM(Customers[MonthlyCharges])
```

### Average Monthly Charges
```dax
Average Monthly Charges =
AVERAGE(Customers[MonthlyCharges])
```

### Average Tenure
```dax
Average Tenure =
AVERAGE(Customers[tenure])
```

### Churned Monthly Charges
```dax
Churned Monthly Charges =
CALCULATE(
    [Total Monthly Charges],
    Customers[Churn] = "Yes"
)
```

## Findings to Validate
With all report filters cleared, verify these baseline figures against your model before publishing:
- Expected customer records in the original dataset: **7,043**
- Churned customers: **1,869**
- Retained customers: **5,174**
- Overall churn rate: approximately **26.54%**

The analysis suggests churn is higher among month-to-month customers than among customers on longer contracts. Higher churn is also associated with certain internet-service and payment-method segments. These observed relationships do not, by themselves, prove causation.

## Business Recommendations
Based on patterns confirmed in the report, a telecom business could consider:
1. Testing incentives for eligible month-to-month customers to move to longer contracts.
2. Improving onboarding and early support for customers with short tenure.
3. Reviewing the experience of customers without technical support or online security services.
4. Investigating payment friction and offering convenient payment options.
5. Monitoring churn by segment over time to evaluate retention initiatives.

These are recommendations to test, not guarantees of churn reduction.

## Repository Structure
```text
Telco-Customer-Churn-Analysis/
├── README.md
├── Dashboard/
│   └── Telco_Customer_Churn_Analysis.pbix
├── Screenshots/
│   ├── 01_Churn_Overview.png
│   ├── 02_Revenue_Analysis.png
│   └── 03_Retention_Insights.png
├── DAX/
│   └── Measures.md
└── Report/
    └── Telco_Churn_Analysis.pdf
```

Create these folders and add the files as you produce them. Only include the dataset if its licence and sharing terms allow redistribution.

## How to Use
1. Download or clone this repository.
2. Open `Dashboard/Telco_Customer_Churn_Analysis.pbix` in Power BI Desktop.
3. If Power BI requests the source CSV, point it to your local copy of the dataset.
4. Refresh the data and review the report pages and slicers.

## Limitations
- This is a portfolio analysis of a sample telecom churn dataset, not a live operational system.
- Monthly charges associated with churned customers are not the same as audited lost revenue or profit.
- Segment-level patterns show association, not causation.
- Verify measures and visuals with slicers cleared before sharing screenshots or conclusions.

## Author
**Rudra Sonvane**  
Aspiring Data Analyst | Power BI | SQL | Python

---
If you find this project useful, feel free to explore the report and its analysis.
