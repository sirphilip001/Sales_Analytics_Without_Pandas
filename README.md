# Tech Hub Kenya — September Sales Analysis

## Project overview

This project analyzes Tech Hub Kenya’s September sales. The notebook uses Python’s standard library for its main analysis and pandas to independently verify the headline results.

## Project files

- `sales_analysis.ipynb` — analysis, cleaning, calculations, and pandas verification
- `data/electronics_sales.csv` — source sales data
- `output/sales_report.txt` — generated text report
- `requirements.txt` — pandas dependency for verification

## How to run

1. Open `sales_analysis.ipynb` in VS Code.
2. Select the project’s `.venv` Python kernel.
3. Run all notebook cells from top to bottom.

To install the verification dependency in the environment:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

The notebook reads the CSV from `data/electronics_sales.csv` and writes the report to `output/sales_report.txt`.

## Data cleaning rules

The source file contains 50 sales rows. The notebook keeps a record of skipped rows and the reason each one was skipped.

- Leading and trailing whitespace is removed from values before parsing.
- Blank values and the text values `N/A`, `NA`, `NONE`, and `NULL` are treated as missing.
- The quantity value `two` is interpreted as 2.
- Commas are removed from prices when they are used as thousands separators, such as `38,999`.
- A leading `KES` label is removed from prices, such as `KES 18999`.
- Rows with a missing or unparseable quantity or unit price are skipped.
- Rows with non-positive quantities or prices are skipped.
- Fractional quantities are skipped because sales quantities are assumed to represent whole items.

Three rows were skipped: S-3030, S-3035, and S-3039. The analysis uses the remaining 47 rows.

## Assumptions and calculation choices

- Revenue per sale is `quantity × unit price`.
- The high-value threshold is inclusive: a sale qualifies when its revenue is at least KES 50,000.
- Product ranking is sorted by revenue from highest to lowest. If revenues tie, product names are sorted alphabetically.
- Mean, median, minimum, and maximum are calculated from the revenue of each included transaction.
- The pandas verification applies the same cleaning rules as the standard-library analysis.

## Results

- Total revenue: **KES 1,317,210.00**
- Included sales: **47**; skipped sales: **3**
- Top three products by revenue:
  1. HP 15 Laptop — KES 389,994.00
  2. Hisense 43in Smart TV — KES 272,993.00
  3. Lenovo Tab M10 — KES 199,992.00
- High-value sales at or above KES 50,000: **5**
- Mean transaction revenue: **KES 28,025.74**
- Median transaction revenue: **KES 10,998.00**
- Minimum transaction revenue: **KES 1,499.00**
- Maximum transaction revenue: **KES 259,996.00**

The notebook’s pandas verification reports `MATCH` for total revenue, product revenue, the top three products, and mean/median transaction revenue.