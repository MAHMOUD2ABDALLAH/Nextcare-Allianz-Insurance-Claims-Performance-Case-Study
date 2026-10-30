# Nextcare Helpline Performance Case Study Dashboard

## Project Overview

This project involves a comprehensive analysis of call center helpline data for Nextcare & Allianz Partners. The goal was to transform nine days of raw call center data (37K calls) into a single, interactive Power BI dashboard. The dashboard provides actionable insights into call volume, agent efficiency, abandonment rates, and queue performance to drive strategic staffing decisions.

## Business Tasks

The analysis aimed to:
1. Display 5 to 10 key data points / KPIs within multiple time frames (hour, day, weekday, day × hour).
2. Allow users to filter and drill down by **Hotline # (Application Name)** and **Queue Name**.
3. Build an interactive, single-page dashboard to present a clear business story and staffing recommendations.

---

## Page 1: Single Dashboard Overview

<img width="1000" height="550" alt="Helpline Dashboard" src="https://github.com/user-attachments/assets/a729c346-21e8-47a4-a4a0-e8f48c61cc52" />

### Key Visuals & Metrics

| Analysis | Description |
|----------|-------------|
| Core KPIs (6 Scorecards) | Calls Offered (37K), Calls Handled (29K), Abandonment (21.7%), Service Level 20s (50.3%), ASA (42s), AHT (215s) |
| Calls by Hour vs Abandonment | Combo chart tracking call volume (columns) and abandonment rate (line). Highlights the evening gap. |
| Calls & Abandonment by Day | Clustered column chart showing the Monday volume spike. |
| Queue Performance | Matrix table comparing Member, Payer, and Provider lines across all 6 KPIs. |
| Slicer Buttons | Interactive buttons for **Queue Name** and **Application Name** (Hotline #) to filter the whole page. |
| Heat Map | Matrix showing Abandonment rate by Day of Week × Hour. |
| Calls by Hotline | Bar chart showing Hotline #1 dominating volume (30.8K) vs. Hotline #3 (6.0K). |
| AHT vs Speed of Answer | Stacked column chart tracking ASA (green) and AHT (navy) by date. Shows AHT is steady while ASA fluctuates. |

---

## Data Sources

The analysis uses a single primary dataset:

1. **Task 2 Sheet.xlsx** – Call center data (`Start_Time`, `End_Time`, `Contact_Disposition`, `Application_Name`, `Queue_Name`, `Queue_Time`, `Talk_Time`, `Hold_Time`, `Work_Time`)

## Data Model

A streamlined model was built in Power BI:

- **Fact Table:** `dataTable` (Call-log level)
- **Dimension Tables:** `Date` (custom calendar), `Time` (Hour buckets)
- **Relationships:** One-to-many between dimensions and the fact table.
- **Measures:** Created DAX measures for Calls Offered, Calls Handled, Calls Abandoned, ASA, AHT, Service Level 20s, and Abandonment Rate.

## Key Metrics & Advanced Analysis

### Core KPIs

- **Calls Offered:** 36,872 (Counts callers, not legs)
- **Calls Handled:** 28,864 (78.3% of callers reached an agent)
- **Abandonment Rate:** 21.7% (8,008 callers hung up before an answer)
- **Service Level 20s:** 50.3% (Half of all offered calls were answered within 20 seconds)
- **ASA Seconds:** 42 (Average speed of answer)
- **AHT Seconds:** 215 (Average handle time: 177s talk + 35s hold + 3s wrap-up)

### Advanced Analysis

1. **The Evening Gap (Staffing Timing)** – Abandonment triples late in the day. It stays around 20% during business hours but climbs to 43.4% by 11 PM. The 6-11 PM window is 33% of volume but 37% of everything we lose.
2. **The Monday Spike** – Mondays carry almost double the volume of any other day (9,500 calls vs 4,000–5,000). Monday's abandonment (21%) is no better than average, meaning the extra volume is not being absorbed.
3. **Queue Uniformity** – The three queues (Member, Payer, Provider) are statistically identical (~12,300 calls each, ~21.5% abandonment). No single queue is the problem.
4. **Hotline Concentration** – Hotline #1 carries 83.6% of all calls (30,820 calls) and performs better (19.5% abandon). Hotline #3 handles 16.2% of calls and abandons 1 in 3 (33.5%). 
5. **Stable Handle Time** – AHT is steady every single day (187 to 228 seconds). Agents' work is consistent; the variability is entirely in the Speed of Answer (ASA).

## Tools & Technologies

- **Power BI** – Data modeling, DAX, visualizations, dashboard design, button slicers
- **Power Query (M)** – Data transformation, time parsing, and cleaning
- **Excel** – Initial data exploration and validation

## How to Use

1. Download the `Helpline_Analytics.pbix` file from this branch.
2. Open it in Power BI Desktop.
3. Use the **Slicer Buttons** (Queue Name and Application Name) to drill down into specific lines. Note that selecting "Payer Line" doesn't move the abandonment metrics (which is a finding in itself).
4. Hover over the heat map to see the exact abandonment rate for a specific day and hour.

## Insights & Recommendations

1. **Shift Coverage into the Evening** – Move part of the roster into the 6-11 PM window, where abandonment climbs from 20% to 43%. The line should flatten toward the daytime 20%.
2. **Add Monday-Specific Coverage** – Add coverage on Mondays to handle the 9,500 call spike. Also, check the Friday and Sunday rosters, which show the thinnest coverage (ASA 62s and 87s).
3. **Prioritize Hotline #1** – Point any staffing or system investment at Hotline #1 first (83.6% of all calls). Put Hotline #3 (33.5% abandonment) on the watch list.

## Project Structure
```
Nextcare-Allianz-Task2-Helpline/
│
├── Data/
│ └── Task 2 Sheet.xlsx
│
├── Assets/
│ └── helpline_dashboard.png
│
├── Helpline_Analytics.pbix
├── Nextcare-Allianz-Mahmoud_Abdallah-Task2.pdf
└── README.md
```

# Author
**Mahmoud Abdallah**
Data Intelligence Reporting Specialist @ Nextcare Allianz Partners

## Any Questions
**Mahmoud_Abdallah20@outlook.com**
