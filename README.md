# E-Commerce Transaction Analysis

Analysis of 500,000+ UK-based e-commerce transactions to clean noisy data, segment purchase behaviour, and surface profit and growth insights by product category, geography, and time.

## Problem

The raw dataset had several quality issues that needed to be resolved before any analysis could be trusted:

- Non-numeric characters embedded in product (stock) codes
- Inconsistent date formats (`/` instead of `-`)
- A heavily skewed `Quantity` column with extreme outliers in both directions (large bulk purchases and large returns recorded as negative values)
- Unstructured product descriptions with no category labels

## Approach

### 1. Data cleaning
- Stripped non-numeric characters from `StockCode` using regex
- Standardised `InvoiceDate` formatting and converted to proper datetime
- Removed encoding errors on load

### 2. Outlier handling
Rather than dropping outliers outright — which would have discarded legitimate bulk orders and returns — I used a two-step transformation:

- **Cube root transformation (`np.cbrt`)** to compress the distance between extreme values and the median while preserving the sign (so returns remain distinguishable from purchases)
- **Winsorization** at the 1st and 99th percentile to cap remaining extreme values

I also tested a Yeo-Johnson power transform (via `sklearn.preprocessing.PowerTransformer`) as an alternative and compared distribution shape before settling on cube root, which preserved more of the original spread.

### 3. Transaction segmentation
Built a Z-score on the cleaned quantity column and used `np.select` to classify every transaction into one of four segments:

| Segment           | Condition         |
|-------------------|-------------------|
| Large Purchase    | Z-score ≥ 3       |
| Regular Purchase  | 0 ≤ Z-score < 3   |
| Regular Return    | -3 < Z-score < 0  |
| Large Return      | Z-score ≤ -3      |

### 4. Product categorisation
Built a keyword-matching function to classify ~4,000 unique product descriptions into 6 business categories (Electronics, Household, Children's, Kitchen Appliances, Essentials, Packaging) with no pre-existing category labels in the source data.

### 5. Business metrics
- Revenue and return value per category → category-level profit and % profit contribution
- Order and customer growth tracked monthly (cumulative)
- Sales and customer distribution by country
- Month-over-month sales trend with return-adjusted revenue

### 6. Reusable analysis tooling
Built a `compare_countries` class to generate comparative sales, order, and customer pivot tables and charts for any list of countries without rewriting the underlying logic.

## Key Findings

- The majority of order volume came from **Regular Purchases**, but **Large Purchases** — while far fewer in count — contributed a disproportionately high share of total revenue
- **United Kingdom** dominated both customer count and total sales among all countries
- Clear **seasonal sales peaks** were visible in the November–December period
- Category-level profit analysis revealed that not all high-revenue categories were equally profitable once returns were factored in
- Customer base and order volume showed steady cumulative growth over the observed period

## Tech Stack

`Python` · `Pandas` · `NumPy` · `Seaborn` · `Matplotlib` · `Scikit-learn` (exploratory)

## Techniques Used

Regex cleaning · Cube root transformation · Winsorization · Z-score segmentation · `np.select` conditional logic · Keyword-based text categorisation · Pivot tables · OOP (reusable comparison class) · Time series aggregation

## File

`Project_Ecommerce.ipynb` — full analysis notebook