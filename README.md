# SEC EDGAR Financial Data Analysis
### Quarterly Revenue & Profitability Dashboard: Big Tech + Healthcare

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![Excel](https://img.shields.io/badge/Excel-Dashboard-217346?logo=microsoft-excel)
![Data Source](https://img.shields.io/badge/Data%20Source-SEC%20EDGAR%20API-red)

---

## Overview

This project demonstrates how to pull **real financial data directly from SEC EDGAR's public XBRL API** — no paid data subscriptions, no scraping, no manual downloads. The SEC requires all large public companies to file structured, machine-readable financial data, and this project uses that infrastructure to build a multi-company profitability analysis.

**Companies analyzed:** Apple (AAPL) · Microsoft (MSFT) · Tesla (TSLA) · Amazon (AMZN) · Johnson & Johnson (JNJ)

**Metrics tracked:** Quarterly Revenue · Gross Profit · Operating Income · Net Income · EPS (Diluted) · Gross/Operating/Net Margins · YoY Revenue Growth

---

## What This Project Demonstrates

| Skill | How It's Applied |
|---|---|
| **SEC EDGAR API** | Live data pull via `requests`, XBRL taxonomy navigation, CIK lookup, fallback tag logic |
| **Data Engineering** | Multi-company data merge, period deduplication, quarterly filtering, derived metric calculation |
| **Financial Literacy** | Correct margin formulas, YoY growth calculation, cross-sector benchmarking |
| **Excel Dashboard** | Multi-sheet workbook, formula-driven YoY section, conditional formatting, financial modeling color standards |
| **Python/pandas** | Pivot tables, group-by transforms, safe division, data type handling |
| **Data Storytelling** | Narrative documentation, analytical framework, sector-aware interpretation |

---

## Project Structure

```
sec_financial_analysis/
├── sec_financial_analysis.ipynb   # Main analysis notebook
├── SEC_Financial_Dashboard.xlsx   # Output Excel dashboard
├── revenue_trend.png              # Revenue trend chart (8 quarters)
├── margin_trend.png               # Net margin trend chart
├── margin_comparison.png          # Side-by-side margin comparison
└── README.md
```

---

## Excel Dashboard Layout

The output workbook has four sheets:

| Sheet | Contents |
|---|---|
| **Dashboard** | Executive summary — most recent quarter, all 5 companies, color-coded margins |
| **Revenue Trend** | 8-quarter quarterly revenue by company, YoY growth formula row |
| **Margin Analysis** | Gross, Operating, and Net margins — all companies, all quarters |
| **Raw Data** | Complete dataset — every metric, every company, every quarter |

**Financial modeling color conventions followed:**
- 🔵 **Blue text** — hardcoded input values
- ⚫ **Black text** — all Excel formulas and calculations
- 🟢 **Green text** — cross-sheet references
- 🟢 **Green fill** — margins above 15%
- 🔴 **Red fill** — negative margins

---

## How to Run

### Prerequisites
```bash
pip install requests pandas openpyxl matplotlib numpy
```

### Run the notebook
```bash
jupyter notebook sec_financial_analysis.ipynb
```

The notebook makes live API calls to `data.sec.gov`. Runtime is approximately 2–3 minutes depending on connection speed. The SEC API is rate-limited to 10 requests/second — the notebook stays well under this with built-in delays.

**Note:** Update the `User-Agent` header in the configuration cell with your name and email. The SEC requests this in their [API documentation](https://www.sec.gov/os/accessing-edgar-data).

---

## About the SEC EDGAR XBRL API

The [EDGAR XBRL API](https://www.sec.gov/edgar/sec-api-documentation) is a free public API — no API key, no subscription, no scraping. The SEC's XBRL mandate (in effect since 2009) requires public companies to tag their financial data with standardized US-GAAP labels, which EDGAR exposes as structured JSON.

**Key API endpoints used:**

```
# Single financial concept for one company
GET https://data.sec.gov/api/xbrl/companyconcept/CIK{cik}/us-gaap/{concept}.json

# Example: Apple's full Revenues history
GET https://data.sec.gov/api/xbrl/companyconcept/CIK0000320193/us-gaap/Revenues.json
```

**Why this matters for analysts:** Most financial data sources (Bloomberg, FactSet, Refinitiv) cost thousands of dollars per year. EDGAR is the authoritative primary source — financial data providers literally pull from it. Knowing how to access it directly is a real skill gap most junior analysts don't have.

---

## Key Analytical Findings

*(Findings based on retrieved data — see notebook Section 7 for full narrative)*

The most important context for comparing these companies is that **margin benchmarks are sector-specific**:

| Company | Sector | Expected Gross Margin | Expected Net Margin |
|---|---|---|---|
| Microsoft | Software/Cloud | 65–75% | 30–40% |
| Apple | Consumer Hardware | 40–45% | 22–28% |
| Johnson & Johnson | Healthcare | 55–65% | 15–22% |
| Amazon | E-Commerce/Cloud | 45–50% blended | 5–10% |
| Tesla | Automotive | 15–25% | 5–15% |

A 10% net margin is excellent for Amazon, mediocre for Microsoft, and a red flag for Apple. Cross-sector analysis without this context misreads the data.

---

## Data Limitations & Methodology Notes

- **XBRL tag inconsistency:** Companies don't always use the same concept tag for equivalent metrics. This notebook implements fallback logic to handle the most common variants (e.g., `Revenues` vs. `SalesRevenueNet` vs. `RevenueFromContractWithCustomerExcludingAssessedTax`).
- **Quarterly deduplication:** Companies sometimes refile quarters; the notebook keeps the most recently filed value for each period.
- **EPS units:** EPS values are reported as `USD/shares` in EDGAR's unit taxonomy, not `USD` — the API function handles this automatically.
- **Values in millions:** All dollar values are divided by 1,000,000 for readability. Raw EDGAR values are reported in full dollars.

---

## Author

**Alejandro (Alex)**  
GitHub: [@chooseyourtacoday](https://github.com/chooseyourtacoday)  
Career transition: Logistics/Phlebotomy → Data Analytics  
Certifications: Codecademy BI Data Analyst (SQL · Python · Tableau · Power BI)  
Location: Dallas–Fort Worth, TX

---

*Part of a portfolio targeting Junior Data Analyst roles in DFW. Other projects: North DFW Housing Affordability Crisis (Python + Random Forest + Tableau), LoneStar Wireless Customer Churn (Databricks), The Coffee Crisis (NASA/FAO data + Tableau), Steam RPG Market Analysis.*
