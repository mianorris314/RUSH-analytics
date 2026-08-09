# RUSH Analytics

The code notebook covers sales analysis for RUSH, a global sportswear and footwear brand. This project was completed as the final project for GENBUS 885.

**Author:** Mia Norris

## Project Overview

The VP of US Sales requested an analysis of raw sales data to identify trends and growth opportunities, along with answers to four specific business questions. The source data was cleaned and inspected before it was analyzed and used to answer the questions.

## Data Sources

Three raw tables, loaded from CSV:
- `TABLE_SALES_885.csv`
- `TABLE_RETAILER_885.csv`
- `TABLE_PRODUCTS_885.csv` (pipe delimited)

## How to Run

1. Open `GENBUS885_Final_Norris_M.ipynb` in Google Colab.
2. Run the first cell to import libraries.
3. Run the upload cell and select all three CSV files when prompted.
4. Run all remaining cells in order.

## Data Quality Issues Addressed

| Issue | Location | Resolution |
|---|---|---|
| Placeholder price of 99999 | `PRICE_PER_UNIT`, 1 row | Replaced with product median|
| Two nulls | `PRICE_PER_UNIT` | Filled with product median |
| `***` instead of a number | `UNITS_SOLD`, 2 rows | Coerced to NaN and dropped |
| "Ootlet" misspelling | `SALES_METHOD`, 20 rows | Corrected to "Outlet" |
| 4 non-unique retailer IDs | `RETAILER_ID`, 8 rows | Kept occurrence as duplicates were inflating the merge by 623 rows |
| Orphaned `RETAILER_ID` 999999999 | 1 sales row | Documented, not altered |
| `INVOICE_DATE` was stored as a string | `INVOICE_DATE` in sales_df | The column was cast to a datetime |
| `UNITS_SOLD` incorrect datatype | `UNITS_SOLD` in sales_df | The column was cast to an integer |

## Business Questions

| # | Question | Answer |
|---|---|---|
| 1 | Highest-selling product category in 2021 | Men's Street Footwear — $22,672,800 (493,753 units) |
| 2 | Top state for women's products in 2021 | Maine — $2,176,301 |
| 3 | Top state for men's products in 2021 | Delaware — $2,334,300 |
| 4 | Retailer with most units purchased | Foot Locker in 2021 (1,097,410) / Amazon in 2020 (317,930) |

## Key Findings

- Revenue and unit volume both peak around July and December in both years.
- Online pulled ahead of Outlet and In-store from June 2021 onward.
- The Northeast leads at $38.8M in revenue while the South trails at $10.3M.
- Foot Locker went from no recorded sales in 2020 to 1.1 million units in 2021, becoming the #1 retailer.
- Amazon is the only retailer whose volume declined year over year.
- Average operating margin sits between 0.40 and 0.45 across all six product categories, so product mix has little effect on profitability.

## Known Limitations

- Four retailer IDs appear twice in the source data with conflicting retailer names or cities. I kept the first occurance of the retailer to preserve the sales totals. This means that the city and region for these transactions may be incorrect.
- One order references a retailer ID with no matching record, so it is excluded from all location-based groupings.
