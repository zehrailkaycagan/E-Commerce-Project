## E‑Commerce Purchases – Exploratory Data Analysis (EDA)

This repository contains a compact, well-documented exploratory analysis of the E‑Commerce Purchases dataset using a Jupyter Notebook. It demonstrates practical pandas workflows for data loading, inspection, filtering, string processing, and summarization that are commonly used in analytics, data quality checks, and ad‑hoc investigations.

### Contents
- Notebook: `ECommercePurchases.ipynb`
- Data: `ECommercePurchasesData` folder (CSV file read as "Ecommerce Purchases")
- Documentation: `README.md` (this file)

## Getting Started
The steps below target Windows/PowerShell. Adapt paths if needed.

```powershell
# 1) Create and activate virtual environment (recommended)
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# 2) Install minimal dependencies
pip install pandas jupyter

# 3) Launch Jupyter
jupyter notebook
```

Open `ECommercePurchases.ipynb` in the browser and run the cells in order.

## Notebook Overview
The notebook walks through the following:
- Load CSV with pandas and preview head/tail samples
- Inspect schema and metadata: `dtypes`, `columns`, `info()`
- Check missingness via `isnull().sum()`
- Basic descriptive stats on Purchase Price (min, max, mean)
- Conditional filtering (by language, card provider, price thresholds)
- String operations (substring search on job titles, extracting email domains)
- Targeted record lookups (by IP or credit card number)

## Highlights and Key Findings
- Dataset size: 10,000 rows × 14 columns
- Null values: none across all columns
- Purchase Price
  - Max: 99.99
  - Min: 0.00
  - Mean: ≈ 50.35
- AM/PM distribution
  - PM: 5,068
  - AM: 4,932
- Language filter
  - French (`Language == 'fr'`): 1,097 rows
- Engineering roles ("engineer" substring in `Job`): 531 rows
- Top email domains (top 5)
  - hotmail.com: 1,638
  - yahoo.com: 1,616
  - gmail.com: 1,605
  - smith.com: 42
  - williams.com: 37
- Mastercard and Purchase Price > 50: 405 rows
- Credit cards expiring in year '20' (MM/YY): 988 rows
- Examples
  - IP `132.207.160.22` → email `amymiller@morales-harrison.com`
  - Credit card `4664825258997302` → email `bberry@wright.net`

## Reproducible Query Examples (pandas)
```python
# French-speaking customers
fr_df = data[data['Language'] == 'fr']

# Roles containing 'engineer' (case-insensitive)
eng_df = data[data['Job'].str.contains('engineer', case=False)]

# Mastercard users with Purchase Price > 50
mc_gt50 = data[(data['CC Provider'] == 'Mastercard') & (data['Purchase Price'] > 50)]

# Credit cards expiring in year '20' (format: MM/YY)
exp20 = data[data['CC Exp Date'].apply(lambda x: x[3:] == '20')]

# Top 5 email domains
domain_counts = data['Email'].apply(lambda x: x.split('@')[1]).value_counts().head()
```

## Project Structure
- `ECommercePurchases.ipynb`: Main analysis notebook
- `ECommercePurchasesData/`: Source data directory
- `README.md`: Project documentation

## Data Ethics and Privacy
This dataset is for educational and illustrative purposes only. When dealing with similar fields in production (e.g., emails, IP addresses, payment details), ensure strict compliance with applicable regulations (e.g., GDPR, CCPA) and internal security policies. Avoid storing or sharing sensitive information.

## Environment
- Python ≥ 3.10
- pandas
- Jupyter Notebook

## Contributing
Contributions are welcome. Feel free to open an issue to propose enhancements or submit a pull request with improvements (tests, clearer explanations, performance tips, additional analyses).

## License
This project is released under the MIT License. You may add a `LICENSE` file for the full text.
