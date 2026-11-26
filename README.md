# Sales & Salesperson Ranking Analysis Dashboard

**Transforming raw operational data into a star-schema BI model and an interactive Power BI dashboard that tracks revenue, orders and salesperson performance from January 2019 to March 2021.**

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?logo=powerbi&logoColor=black) ![DAX](https://img.shields.io/badge/Language-DAX-7B7FDC) ![Status](https://img.shields.io/badge/Status-Complete-3FB58F) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## Project Overview

It turns a raw sales report into a business-intelligence engine. All preparation is handled in **Power Query**: header promotion, skipping report preamble rows, type casting, filtering blank product keys, cleaning duplicated dimensions, joining product-group image URLs and unpivoting the monthly budget workbook into a tidy Target table.

The normalized model uses two fact tables (`Sales` and `Target`) and three dimension tables (`dProducts`, `dSalesperson` and `dcalendar`). DAX measures calculate revenue, distinct orders, average transaction price, target achievement, contribution share and a dynamic salesperson rank that powers a top-three podium and ranking table.

A short portfolio-style write-up is available in [`docs/Sales_Ranking_Dashboard_Brief_Description.md`](docs/Sales_Ranking_Dashboard_Brief_Description.md).

---

## Project Structure

```
sales-salesperson-ranking-analysis-dashboard/
│
├── PowerBI/
│   └── Sales And Salesperson Analysis Dashboard.pbix  # Power BI report
│
├── data/
│   ├── SalesData.xlsx                    # Transactional sales report (2019-2021)
│   ├── Product.xlsx                      # Product dimension
│   ├── Photos.xlsx                       # Product-group and salesperson image URLs
│   └── Budget.xlsx                       # Monthly sales targets (2019-2021)
│
├── docs/
│   └── Sales_Ranking_Dashboard_Brief_Description.md
│
├── screenshots/
│   ├── Screenshot 2026-03-01 223823.png  # Dashboard main view
│   └── Screenshot 2026-03-01 224712.png  # Star schema data model
│
├── .gitignore
├── LICENSE
└── README.md
```

---

## Dashboard Preview

### Dashboard Main View

![Sales Dashboard](screenshots/Screenshot%202026-03-01%20223823.png)

### Star Schema Data Model

![Star Schema Data Model](screenshots/Screenshot%202026-03-01%20224712.png)

---

## Data Architecture

```
SalesData.xlsx ──► Sales (fact) ──► dProducts
                         │
                         ├────────► dSalesperson ◄── Target (from Budget.xlsx)
                         │
                         └────────► dcalendar (DAX CALENDARAUTO)
                                          │
                                   Key_Measure (DAX)
                                          │
                                  3 visible pages + 2 hidden tooltips
```

Power Query also standardizes several supervisor names (for example replacing Portuguese-language names with their localized equivalents), removes blank product keys, extracts salesperson IDs and deduplicates the salesperson dimension before loading.

### Star Schema Relationships

| From | To | Cardinality |
| --- | --- | --- |
| `Sales[SalespersonKey]` | `dSalesperson[SalespersonKey]` | Many-to-one |
| `Sales[ProductKey]` | `dProducts[ID]` | Many-to-one |
| `Target[SalespersonID]` | `dSalesperson[SalespersonKey]` | Many-to-one |

---

## Data Catalog

| Table | Role | Rows | Details |
| --- | --- | --- | --- |
| `Sales` | Fact | 260,096 lines / 52,560 orders | OrderDate (Jan 2019 – Mar 2021), OrderNumber, ProductKey, SalespersonKey, Salesperson, Supervisor, Manager, Channel, Quantity, UnitPrice |
| `dProducts` | Dimension | 798 | Product ID, ProductName, ProductGroup (22), ProductCategory (Food / Drink), URL |
| `dSalesperson` | Dimension | 12 | Channel, Manager, Salesperson, SalespersonKey, Supervisor, photo URL |
| `Target` | Fact / budget | 241 | SalespersonID, monthly Date, Target value, produced by unpivoting `Budget.xlsx` |
| `dcalendar` | Date table | Generated | Year, Quarter, Month, Month Number from `CALENDARAUTO()` |
| `Key_Measure` | Measure table | — | Hosts all eight DAX measures |

---

## DAX Measures

| Measure | Expression |
| --- | --- |
| `Revenue` | `SUMX(Sales, Sales[UnitPrice] * Sales[Quantity])` |
| `Orders` | `DISTINCTCOUNT(Sales[OrderNumber])` |
| `ATP` | `DIVIDE([Revenue], [Orders])` |
| `Target` | `SUMX(Target, Target[Target])` |
| `Acheivemnet %` | `DIVIDE([Revenue], [Target])` |
| `Total Revenue` | `CALCULATE([Revenue], ALL(dSalesperson))` |
| `Contribution %` | `DIVIDE([Revenue], [Total Revenue])` |
| `Rank` | `RANKX(ALL(dSalesperson), [Revenue])` |

`Rank` drives visual-level filters for ranks 1–3, so the ranking page's podium cards and Top-3 table update automatically with the slicer context.

---

## Dashboard Pages & Visuals

| Page | Type | Contents |
| --- | --- | --- |
| **Home** | Visible | Branded cover page |
| **Sales** | Visible | Revenue / Orders / ATP card, revenue & orders trend, product-group bar chart, supervisor/salesperson pivot, channel and category donuts |
| **Achievement Tooltip** | Hidden tooltip | Revenue vs. Target card and achievement gauge |
| **Product Tooltip** | Hidden tooltip | Product-group header, product URL table, Revenue / Orders / ATP card |
| **Sales Person Ranking** | Visible | Top-three podium cards, Top-3 pivot with contribution %, dynamic "best salesperson" narrative card |

---

## Key Findings

- **$17.9M** in revenue analyzed across **52,560 orders** from January 2019 to March 2021 (27 months); overall performance finished just above plan at **103.7% of target**.
- **Wheat Flour** was the top revenue product group at **$4.47M**; Food accounted for **90.21% of orders** versus Drink at **9.79%**.
- Channel mix: **Retail $8.70M (48.56%)**, **Distributor $6.10M (34.05%)** and **Online $3.11M (17.39%)**.
- Revenue peaked in **Q4 2020 ($3.24M)**, after Q3 2020 ($2.88M), with **October 2020** the strongest month ($1.17M); the transaction data ends in March 2021.
- The top **supervisor** was Diego Araujo at **$6.32M** (shown as Abdallah Mahmoud in the report after Power Query name standardization); the top **salesperson** was Carla Ferreira at **$4.71M**.
- The `RANKX`-based salesperson ranking surfaces clear performance gaps and supports targeted coaching decisions without hard-coding any individual into the report.

---

## Tools & Technologies

| Category | Tool | Purpose |
| --- | --- | --- |
| Data preparation | Power Query (M) | Cleaning, unpivoting, deduplication, merges, name standardization |
| Data modeling | Power BI Desktop | Star schema, relationships, report pages and tooltips |
| Calculation | DAX | Revenue, Orders, ATP, target, contribution and rank measures |
| Documentation | Markdown | Project brief and README |
| Version control | Git & GitHub | Project hosting |

---

## Getting Started

1. Clone this repository.
2. Open [`PowerBI/Sales And Salesperson Analysis Dashboard.pbix`](PowerBI/Sales%20And%20Salesperson%20Analysis%20Dashboard.pbix) in **Power BI Desktop**.
3. If prompted to refresh, repoint the Power Query sources to the local files in `data/` — the PBIX retains the original authoring paths.
4. Explore the Sales page, hover over the achievement and product visuals to see the tooltips, then open the Sales Person Ranking page.

---

## License

MIT License — see [`LICENSE`](LICENSE).

## Author

**Mohamed Basem**
