# Tyne Tunnel Toll Transactions Analysis

Exploratory data analysis and statistical investigation of a year of Tyne Tunnel toll transactions for one individual, using Python and pandas.

![Python](https://img.shields.io/badge/Python-3.x-blue) ![pandas](https://img.shields.io/badge/pandas-data%20analysis-150458) ![SciPy](https://img.shields.io/badge/SciPy-statistics-8CAAE6) ![Jupyter](https://img.shields.io/badge/Jupyter-notebook-F37626)

## Overview

This project takes a raw transaction export and turns it into a clear picture of travel and spending behaviour. It covers the full analytics workflow: profiling the data, cleaning it, creating features, exploring patterns, and testing them statistically.

It was completed as part of a university data analytics workshop on data preprocessing and analytics with Python and pandas.

**Questions explored**
- How does tunnel usage vary by month, day of the week and hour of the day?
- What patterns appear in spending, average toll charges and account top-ups?
- Do journeys differ by direction of travel?
- How consistent is usage over time?
- Are weekday and weekend journeys different, and has the average cost changed?

## Key findings

| Area | Finding |
|---|---|
| Data | 94 transactions: 79 journeys and 15 account top-ups, from 12 March 2024 to 7 March 2025 |
| Weekday pattern | Tuesday and Thursday account for about two thirds of journeys; weekends account for only 3 journeys |
| Direction | Southbound journeys cluster on Tuesday mornings, northbound journeys on Thursday evenings |
| Toll price | The toll rose from £1.98 to £2.16 (+9.1%) in May 2024 |
| Spending | £167.94 spent on tolls against £160 in top-ups, with monthly spend following the number of journeys |
| Consistency | Moderate month-to-month variability (coefficient of variation about 0.47), with quieter summer months and gaps of up to 36 days |
| Statistics | Weekday vs weekend difference is significant (Mann-Whitney U, p < 0.001) |

## Data

The dataset records two types of transaction:
- **Journey**: a toll charge for a tunnel crossing, with direction, vehicle, toll and journey time.
- **Top up**: money added to the account, with a payment reference and balance.

**Data quality findings**
- Most missing values are *structural*: top-ups have no journey details, and journeys have no payment details.
- One column was completely empty and was removed.
- No fully duplicated rows. Some journeys share a posting time (late batch posting), but they are separate journeys and were kept.
- All journey charges matched their toll values, so there were no inconsistent financial amounts.
- Vehicle registrations are personal data, so they were replaced with anonymous labels (Vehicle A, Vehicle B).

> The raw file is not included in this repository because it contains vehicle registration numbers. The anonymised, cleaned data is provided in `data/tollbooth_cleaned.csv`.

## Methods

1. **Data profiling:** structure, data types, missing values, duplicates, outliers and transaction types.
2. **Preprocessing:** date-time conversion, anonymisation, financial consistency checks, and new variables (month, weekday, weekend flag, hour, days since last journey, posting delay).
3. **Exploratory analysis:** usage by month, weekday and hour; spending and top-up patterns; direction of travel; measures of variability (standard deviation, IQR, coefficient of variation).
4. **Statistical investigation:**
   - Mann-Whitney U test for weekday vs weekend frequency (daily counts are skewed, so a t-test is unsuitable)
   - Spearman correlation and trend analysis for changes in expenditure
   - Pearson and Spearman correlation between journey frequency and monthly spend
   - IQR and z-score methods to flag unusually high or low usage periods
   - Chi-square test for direction vs vehicle

## Repository structure

```
.
├── notebooks/
│   └── Tollbooth_Workshop.ipynb    # full analysis with explanations
├── src/
│   └── tollbooth_workshop.py       # the same analysis as a script
├── data/
│   └── tollbooth_cleaned.csv       # cleaned, anonymised data
├── figures/
│   └── tollbooth_workshop_figures.png
└── README.md
```

## How to run

```bash
# 1. clone the repository
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# 2. install the dependencies
pip install pandas numpy matplotlib scipy jupyter

# 3. open the notebook
jupyter notebook notebooks/Tollbooth_Workshop.ipynb
```

Set the `PATH` variable in the first cell to the location of your data file.

## Limitations

- The data covers **one person over about 12 months**, so the results do not generalise.
- Monthly samples are small (2 to 11 journeys), which limits the power of statistical tests.
- Only toll-paying crossings are recorded, so journeys by other routes are not visible.
- Spending is fixed by the toll price, so it adds little beyond the journey count.
- Direction is the only location information: there is no origin, destination or trip purpose.
- Two vehicles are combined, and one stops appearing after October 2024.

## Possible extensions

- Forecast monthly journeys and spending
- Predict when the next top-up will be needed
- Check each journey against the correct tariff, automatically
- Build an interactive dashboard (Streamlit or Plotly)

## Tech stack

Python, pandas, NumPy, SciPy, Matplotlib, Jupyter Notebook

## Author

**[Saheed Oyeniyi Oyetunji]** | Data Science and AI |  | [tunjiassorted@gmail.com]
