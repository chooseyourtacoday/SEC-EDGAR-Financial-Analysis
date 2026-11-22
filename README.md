# SEC EDGAR Financial Dashboard

Excel workbook of quarterly revenue and profitability figures for five public companies. The figures in the file are labeled as sample data.

This repository contains:

- `SEC_Financial_Dashboard.xlsx` — the workbook
- `README.md` — this file

The analysis notebook is not included yet. Footers inside the workbook refer to running a notebook locally to replace the sample figures with live SEC EDGAR output. That notebook is not in this repository.

## Workbook

`SEC_Financial_Dashboard.xlsx` has four sheets, in this order: **Raw Data**, **Dashboard**, **Revenue Trend**, and **Margin Analysis**. File properties list openpyxl as the creator and LibreOffice as the application that saved it.

Every sheet hides gridlines. There are no charts, images, pivot tables, defined names, or conditional-formatting rules. Formulas stay on the same sheet; nothing references another sheet. Where the Dashboard, Revenue Trend, and Margin Analysis repeat a figure from Raw Data, the number is typed in again.

Sheet headers name SEC EDGAR XBRL (`data.sec.gov`, US-GAAP) as the intended source, state that dollar amounts are in USD millions, and mark the numbers as sample data to be replaced with live API output. The descriptions below are of what is stored in the file.

Companies and quarters, on every sheet:

| Company | Ticker | Quarters |
|---|---|---|
| Apple | AAPL | Q1 2023 through Q4 2024 |
| Microsoft | MSFT | Q1 2023 through Q4 2024 |
| Tesla | TSLA | Q1 2023 through Q4 2024 |
| Amazon | AMZN | Q1 2023 through Q4 2024 |
| Johnson & Johnson | JNJ | Q1 2023 through Q4 2024 |

That is 5 companies × 8 quarters.

### Raw Data

Title in row 2: “Raw Data — All Companies · All Quarters · All Metrics”. Used range `A1:M47`.

Row 5 is the header. Rows 6–45 are the 40 company-quarter records. Columns:

| Column | Field |
|---|---|
| A | Company |
| B | Ticker |
| C | Sector |
| D | Quarter |
| E | Revenue ($M) |
| F | Gross Profit ($M) |
| G | Op. Income ($M) |
| H | Net Income ($M) |
| I | EPS Diluted |
| J | Gross Margin |
| K | Op. Margin |
| L | Net Margin |
| M | Rev YoY % |

Sector labels on this sheet: Apple and Microsoft are Technology, Tesla is Auto/Energy, Amazon is Tech/Retail, and Johnson & Johnson is Healthcare.

Revenue, profit, and EPS cells are hardcoded inputs in blue text (`#0000FF`). Revenue and the profit columns use the number format `#,##0`. EPS uses `$#,##0.00`.

Gross margin, operating margin, and net margin are hardcoded percentages (format `0.0%`), not formulas. Each stored margin equals the matching profit column divided by revenue.

Rev YoY % is blank for every 2023 quarter. Each 2024 quarter contains a formula of the form `(this quarter's revenue − the same quarter a year earlier) / that prior revenue`, pointing at cells in column E. Those formula cells use black text.

Row 47, merged across A–M: “Source: SEC EDGAR 10-Q/10-K filings | XBRL us-gaap taxonomy | Blue = hardcoded input | Black = formula | *Replace with live API output when running notebook locally”.

### Dashboard

Title in row 2: “SEC EDGAR Financial Dashboard — Quarterly Analysis”. Used range `B1:K23`.

Row 3 lists the five tickers, “Data Source: SEC EDGAR XBRL API”, “Figures in USD millions”, and “\*Sample data”.

Row 4 is a legend typed on the sheet: “Blue text = source data (hardcoded inputs) | Black text = Excel formulas | Green fill = margin >15% | Red fill = margin <0%”.

**Most recent quarter (Q4 2024) — key metrics** (rows 7–12). One hardcoded row per company: company, ticker, quarter, revenue, gross profit, operating income, net income, gross margin, operating margin, and net margin. EPS is not on this sheet. The Q4 2024 values match the Raw Data rows for that quarter.

**Year-over-year revenue growth (Q4 2024 vs Q4 2023)** (rows 16–21). Q4 2023 and Q4 2024 revenue are hardcoded and match Raw Data. YoY Growth % is the formula `(Q4 2024 revenue − Q4 2023 revenue) / Q4 2023 revenue` in column F, in black text. Column G, Context, holds a short note for each company:

| Company | Context text |
|---|---|
| Apple | iPhone 16 cycle + Services growth |
| Microsoft | Azure cloud acceleration |
| Tesla | Volume growth offset by price cuts |
| Amazon | AWS + advertising surge |
| Johnson & Johnson | MedTech strength; pharma pipeline |

Those notes are typed labels. They are not calculated from the numbers.

Row 23, merged across B–K, cites SEC EDGAR 10-Q/10-K filings and `data.sec.gov/api/xbrl`, and says “\*Sample data — run notebook locally to populate with live figures”.

### Revenue Trend

Title in row 2: “Quarterly Revenue Trend — 8 Quarters (Q1 2023 – Q4 2024) | USD Millions”. Used range `A1:H22`. There is no chart on the sheet; revenue is a table.

Row 5 headers: Quarter, then Apple (AAPL), Microsoft (MSFT), Tesla (TSLA), Amazon (AMZN), Johnson & Johnson (JNJ). Rows 6–13 are Q1 2023 through Q4 2024. Each revenue cell is a hardcoded input in blue text and matches Raw Data.

Rows 17–20 are a year-over-year block:

- Q4 2024 vs Q4 2023, formula `(row 13 − row 9) / row 9` for each company
- Q3 2024 vs Q3 2023, formula `(row 12 − row 8) / row 8` for each company

Row 3 says the YoY percent is an Excel formula referencing 4 rows above, and marks the sheet as sample data. Row 22 says: “YoY % uses Excel formula: =(current - prior) / prior | Black text = formula | Blue text = source data”.

### Margin Analysis

Title in row 2: “Profitability Margin Analysis — Gross · Operating · Net Margins”. Used range `A1:H48`.

Row 3 says: “Margin = Profit Metric ÷ Revenue | Green fill = >15% | Red fill = negative | Cross-sector benchmarks vary significantly”.

Three blocks list every quarter down the rows and the five companies across columns B–F. Every margin cell is a hardcoded percentage. None of the cells on this sheet contain a formula. The values match Raw Data.

| Block | Header row | Data rows |
|---|---|---|
| Gross margin | 5 | 7–14 (Q1 2023–Q4 2024) |
| Operating margin | 17 | 19–26 |
| Net margin | 29 | 31–38 |

**Sector benchmark context** (rows 41–48) is a typed table of typical ranges. It is not calculated from the quarterly rows.

| Company | Sector label on this table | Typical gross margin | Typical operating margin | Typical net margin |
|---|---|---|---|---|
| Apple (AAPL) | Consumer Hardware | 38–43% | 25–30% | 22–28% |
| Microsoft (MSFT) | Software / Cloud | 65–72% | 40–45% | 30–38% |
| Tesla (TSLA) | Automotive / Energy | 15–25% | 5–12% | 5–12% |
| Amazon (AMZN) | E-Commerce / Cloud | 45–50% | 5–10% | 4–8% |
| Johnson & Johnson (JNJ) | Healthcare | 55–65% | 20–28% | 15–22% |

These sector labels differ from the Raw Data sheet, which uses Technology, Auto/Energy, Tech/Retail, and Healthcare.

Row 48 says: “Note: A 10% net margin is strong for Amazon but weak for Microsoft — cross-sector comparison requires sector context.”

## Formatting stored in the file

- Titles are Arial in navy (`#1F3864`). Column-header rows use white text on navy (`#1F3864`) or blue (`#2E75B6`).
- Body text is Arial. Alternating data rows use a light blue fill (`#F2F7FB`).
- Hardcoded dollar and EPS inputs use blue text (`#0000FF`). Year-over-year formula cells use black text.
- Margin cells above 15% use a light green fill (`#E2EFDA`). The only negative margin in the workbook is Johnson & Johnson’s Q3 2024 net margin, on Raw Data and again on Margin Analysis. That cell uses a light orange fill (`#FCE4D6`). The legends call a negative margin a red fill; the fill in the file is this orange. Fills are ordinary cell styles, so they do not change if a value changes.
- On Revenue Trend, the Microsoft and Amazon year-over-year cells also use the light green fill. The other companies on those rows do not. That fill is not limited to rates above 15%.
- Percent cells (margins and year-over-year) use the format `0.0%`.

## Author

Alejandro Molina — GitHub [@chooseyourtacoday](https://github.com/chooseyourtacoday)
