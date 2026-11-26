# Sales & Salesperson Ranking Analysis Dashboard — Project Description

**Tool:** Microsoft Power BI | **Type:** Sales Analytics Portfolio Project

## Overview
The Sales & Salesperson Ranking Analysis Dashboard turns an operational sales report into a normalized star-schema model and a Power BI dashboard covering revenue, orders, achievement against target and salesperson performance from January 2019 to March 2021.

## What It Does
- Cleans the raw sales workbook in Power Query: promotes headers, skips preamble rows, filters blank product keys, deduplicates dimensions and standardizes supervisor names.
- Unpivots the monthly budget workbook into a tidy `Target` table and joins product-group and salesperson photo URLs from a separate workbook.
- Models `Sales` and `Target` as fact tables with `dProducts`, `dSalesperson` and `dcalendar` as dimension tables.
- Builds DAX measures for Revenue, Orders, ATP, Target, achievement percentage, contribution percentage and a dynamic `RANKX` salesperson rank.
- Delivers a Home page, an analytical Sales page, two hidden tooltip pages and a Sales Person Ranking page with podium cards and a Top-3 table.

## Data Model
A star schema with a 260,096-row sales fact table, 798 products, 12 salespeople, 241 monthly target rows and a DAX calendar table, driven by eight DAX measures.

## Key Findings
- $17.9M revenue analyzed across 52,560 orders from January 2019 to March 2021, finishing at 103.7% of target.
- Wheat Flour was the top revenue product group at $4.47M; Food made up 90.21% of orders.
- Channel revenue split: Retail $8.70M (48.56%), Distributor $6.10M (34.05%), Online $3.11M (17.39%).
- Revenue peaked in Q4 2020 ($3.24M), with October 2020 the strongest individual month ($1.17M).
- The top supervisor was Diego Araujo at $6.32M (renamed Abdallah Mahmoud in the report); the top salesperson was Carla Ferreira at $4.71M.
- The rank-based podium highlights performance gaps without hard-coding individuals into the report.

## Skills Demonstrated
Power Query data preparation, star-schema modeling, DAX time intelligence and ranking, tooltip UX design and sales performance storytelling.
