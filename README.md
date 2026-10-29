Here is the `README.md` file for your **Branch 1 (Task 1: Claims Dashboard)**, perfectly styled after the Elezaby Pharmacy Case Study, incorporating all the insights and images from your Nextcare Task 1 presentation and PDF.

***

```markdown
# Nextcare Claims & Policy Performance Case Study Dashboard

## Project Overview

This project involves a comprehensive analysis of health insurance claims data for Nextcare & Allianz Partners. The goal was to transform two years of raw medical claims data (AED 51.3M across 105K claim lines for 3,468 covered members) into an interactive Power BI dashboard. The dashboard provides actionable insights into cost drivers, operational bottlenecks, abnormal spending patterns, and policy performance to drive strategic business decisions.

## Business Tasks

The analysis aimed to:
1. Clean and prepare raw claims data for analysis.
2. Highlight abnormal findings (e.g., the October Spike, Cost Concentration, Automation Rates).
3. Analyze the data to understand high utilization reasons (e.g., back/neck pain, paediatric therapy).
4. Provide a clear trend analysis across underwriting years (UwY).
5. Build an interactive 5-page dashboard to present a clear business story with a claim-line level drill-through.

---

## Page 1: Policy Performance

<img width="1000" height="580" alt="Page 1 - Policy Performance" src="https://github.com/user-attachments/assets/placeholder-claims-page1" />

### Key Visuals & Metrics

| Metric | Description |
|--------|-------------|
| Core KPIs | Total Paid (AED 51.3M), Claim Count (105K), Covered Members (3.4K), Cost per Member (AED 15K), Avg TAT (23.4 days), Paid YoY % (11.3%) |
| Total Paid by policy month | Line chart tracking spend against the policy month (Nov to Oct) across two UwYs |
| Family of Benefit | Clustered column chart breaking down spend by Out-Patient, In-Patient, Dental, and Optical |
| Claim Type by count | Donut chart showing Provider Claims vs. Member Claims (Reimbursement) |
| Slicer Panel | 5 synced drop-downs (UwY, Year Month, Sub_Policy_Number, Provider_Type, Dependency) |

---

## Page 2: Abnormal Findings

<img width="1000" height="580" alt="Page 2 - Abnormal Findings" src="https://github.com/user-attachments/assets/placeholder-claims-page2" />

### Key Visuals & Metrics

| Analysis | Description |
|----------|-------------|
| The October Spike | Clustered column chart highlighting a 25-30% jump in claims every October (benefit-reset behavior) |
| Cost Concentration | Pareto chart showing extreme concentration (Top 1% of members drive 13.2% of spend) |
| Automation Rate | Donut chart showing 51.41% Automated vs. 48.59% Manual claims |
| Zero Value Claims | Bar chart showing 7,398 claims settled at AED 0, mostly Out-Patient |
| Data Quality Table | Reconciliation table showing 104,965 Complete and 20 Incomplete records |

---

## Page 3: High Utilisation Drivers

<img width="1000" height="580" alt="Page 3 - High Utilisation Drivers" src="https://github.com/user-attachments/assets/placeholder-claims-page3" />

### Key Visuals & Metrics

| Analysis | Description |
|----------|-------------|
| Interactive Centrepiece | Decomposition tree drilling from Total Paid down to ICD Description and Provider Type |
| Outliers Finder | Scatter plot identifying outliers by claims-per-member (X) vs. paid-per-member (Y) |
| Top 10 Diagnoses | Bar and line chart highlighting high-cost areas like Low Back Pain, Cervicalgia, and Delayed Milestone |
| Demographics | Matrix table showing frequency and cost per member split by Dependency and Gender |
| Most Common Outlier | Card highlighting "Multiple myeloma not having achieved remission" |

---

## Page 4: Trend Analysis

<img width="1000" height="580" alt="Page 4 - Trend Analysis" src="https://github.com/user-attachments/assets/placeholder-claims-page4" />

### Key Visuals & Metrics

| Analysis | Description |
|----------|-------------|
| UwY Month No Split | Area chart comparing the two underwriting years, highlighting the widest gaps in April and July |
| Cost per Member Trend | Line chart showing the monthly cost per member fluctuating between AED 490 and 840 |
| Avg TAT by Settlement | Line chart showing processing times improving in year two (averaging 22.4 days vs. 25.0) |
| KPI Tiles | 5 KPI visuals filtering by Benefit Family, Provider Type, Network, Dependency, and Emergency Flag |

---

## Page 5: Claim Details Drill-Through

<img width="1000" height="580" alt="Page 5 - Claim Details" src="https://github.com/user-attachments/assets/placeholder-claims-page5" />

### Key Visuals & Metrics

| Analysis | Description |
|----------|-------------|
| Drill-Through Table | A granular table showing one row per claim line, reached by right-clicking any visual on the previous pages |
| Detailed Columns | Claim Line Key, Claim Number, Member ID, Provider ID, ICD Description, Claim Value, TAT Days, Value Band, Processing Channel |
| Live Audit | Allows case managers or auditors to view the exact claim lines behind any aggregate finding (e.g., Delayed Milestone in childhood) |

---

## Data Sources

The analysis uses raw health insurance claims data:

1. **sheet_1.xlsx** – Claims and policy data (`Claim_Value`, `Member_ID`, `Provider_ID`, `ICD_Description`, `Total_TurnAroundTime_Days`, `Processing_Channel`, etc.)

## Data Model

A **Star Schema** was built in Power BI:

- **Fact Table:** `Claims` (Claim-line level)
- **Dimension Tables:** `Date`, `Members`, `Providers`, `Diagnosis`
- **Relationships:** One-to-many between dimensions and the fact table.

## Key Metrics & Advanced Analysis

### Core KPIs

- Total Paid, Claim Count, Covered Members, Cost per Member, Avg TAT Days, Paid YoY %
- Claim Count vs. Member Count (Distinguishing between all enrolments vs. active claimants)

### Advanced Analysis

1. **Cost Concentration** – Pareto analysis proves that the top 1% of members (35 people) carry 13.2% of all spend, and the top 10% carry 42%.
2. **Automation vs. Manual** – Automated claims settle in a median of 18 days versus 30 days for manual, yet manual claims carry 26% of the paid value.
3. **Benefit Reset Behavior** – Every October, claims and paid value jump 25-30% above the normal month average.

## Tools & Technologies

- **Power BI** – Data modeling, DAX (Time Intelligence, Cumulative Totals), visualizations, dashboard design
- **Power Query (M)** – Data cleaning, handling nulls, creating the Underwriting Year (UwY) calendar
- **Excel** – Initial data exploration and validation

## How to Use

1. Download the `Claims_Analytics.pbix` file from this branch.
2. Open it in Power BI Desktop.
3. Use the 5 synced slicers to filter the entire report by UwY, Provider, or Dependency.
4. Right-click on any data point (e.g., a specific diagnosis or member) and select **Drill Through -> Claim Details** to view the line-level evidence.

## Insights & Recommendations

1. **Review Step on Therapy Claims** – Back/neck pain (M54.5 / M54.2) is AED 4.6M (8.9% of spend) and up 38% YoY. Implement a clinical review step for physiotherapy claims once they pass a few sessions.
2. **Case Manager for the Top List** – Assign a dedicated case manager to the top 1% of members (35 people) who carry 13% of the spend. The severity corner of the scatter plot points to a handful of people with serious conditions (cancer, pulmonary hypertension).
3. **October Pricing & Benefit Design** – Re-examine October pricing and plan claims capacity for month 12. Members are clearly using up benefits before they reset.
4. **Reimbursement Channel Control** – Reimbursement claims are 14% of lines but 30% of paid value. They take longer to process and should be a fourth lever for cost control.

**Limitations:** We currently do not have premium or benefit-limit data, so we cannot calculate a loss ratio yet. This is the natural next step once the data is available. 

## Project Structure
```
Nextcare-Allianz-Task1-Claims/
│
├── Data/
│ └── sheet_1.xlsx
│
├── Assets/
│ ├── page1_policy_performance.png
│ ├── page2_abnormal_findings.png
│ ├── page3_high_utilisation.png
│ ├── page4_trend_analysis.png
│ └── page5_claim_details.png
│
├── Claims_Analytics.pbix
├── Nextcare-Allianz-Mahmoud_Abdallah-Task1.pdf
└── README.md
```

# Author
**Mahmoud Abdallah**
Data Intelligence Reporting Specialist @ Nextcare Allianz Partners

## Any Questions
**Mahmoud_Abdallah20@outlook.com**

<img width="200" height="200" alt="Nextcare Allianz" src="https://github.com/user-attachments/assets/347e2fb5-3c83-43c1-8c5c-bb63a200bf67" />
```