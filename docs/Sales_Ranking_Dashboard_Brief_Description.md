# Sales & Salesperson Ranking Analysis Dashboard — Project Description

**Tool:** Microsoft Power BI | **Type:** Sales Analytics Portfolio Project

## Overview
The Sales & Salesperson Ranking Analysis Dashboard turns an operational sales report into a normalized star-schema model and a five-page Power BI dashboard covering revenue, orders, achievement against target and salesperson performance from 2019 to 2021.

## What It Does
- Cleans the raw sales workbook in Power Query: promotes headers, skips preamble rows, filters blank product keys, deduplicates dimensions and standardizes supervisor names.
- Unpivots the monthly budget workbook into a tidy `Target` table and joins product-group and salesperson photo URLs from a separate workbook.
- Models `Sales` as the fact table with `dProducts`, `dSalesperson`, `dcalendar` and `Target` as supporting tables.
- Builds DAX measures for Revenue, Orders, ATP, Target, achievement percentage, contribution percentage and a dynamic `RANKX` salesperson rank.
- Delivers a Home page, an analytical Sales page, two hidden tooltip pages and a Sales Person Ranking page with podium cards and a Top-3 table.

## Data Model
A star schema with a 260,096-row sales fact table, 798 products, 12 salespeople, 241 monthly target rows and a DAX calendar table, driven by eight DAX measures.

## Key Findings
- $17.9M revenue analyzed across 52,560 orders over three years, finishing at 103.7% of target.
- Wheat Flour was the top revenue product group at $4.47M; Food made up 90.21% of orders.
- Channel revenue split: Online 48.56% (~$9M), Distributor 34.05% (~$6M), Retail 17.39% (~$3M).
- Revenue peaked in late 2020 (Q3–Q4), with October 2020 the strongest individual month, before declining in early 2021.
- The rank-based podium highlights performance gaps without hard-coding individuals into the report.

## Skills Demonstrated
Power Query data preparation, star-schema modeling, DAX time intelligence and ranking, tooltip UX design and sales performance storytelling.
