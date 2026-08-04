# Cross-Country Used Car Depreciation: Germany vs. the Netherlands

**Summary:** Age matters about the same in both countries (~3%/year). Mileage doesn't — Dutch buyers punish high-mileage cars **3x harder** than German buyers do. Same car, same age, wildly different price penalty depending on which side of the border you're selling it.

**[Full paper (PDF)](FINAL-PAPER/cross-country-differences.pdf)** - 4,862 listings, OLS regression, methodology and full results

---

## The question

Everyone knows used cars lose value as they age and rack up mileage. What's less obvious is whether *how much* they lose depends on which country you're selling in. This project scrapes real listings from Germany and the Netherlands to find out.

## Actions

- Scraped **4,862 listings** (2,441 DE / 2,421 NL) from Mobile.de via an Apify actor
- Cleaned and harmonized the data — standardized fuel types, filtered implausible outliers (e.g. a 12-year-old car with 20,000 km), restricted to a sane price/age/mileage range
- Built an **OLS regression** on log price, with country interaction terms to test whether age and mileage are valued differently depending on market
- Did all of it in Python (pandas, statsmodels) in Jupyter/VS Code

## Findings

| | Germany | Netherlands |
|---|---|---|
| Price drop per extra year of age | -2.8% | -3.1% |
| Price drop per +10% mileage | -0.83% | **-2.91%** |

The model explains 41.5% of price variation (R² = 0.415, p < 0.001). Age depreciation is basically the same everywhere — but mileage sensitivity is night and day. My best guess as to why: Dutch buyers face higher ongoing usage costs (taxes, fuel), so mileage reads as a stronger signal of total cost of ownership, not just wear and tear. Germany's bigger, more liquid market may also just dilute how much any single factor matters.

Also, as a side note: manual transmission cars trade at a huge discount (-50%) in this sample, and electric cars are actually *cheaper* than equivalent petrol cars (-11%) — diesel still commands a premium (+9.7%).

## Repo structure

```
├── FINAL PAPER/        # Folder containing the final paper
├── notebooks/          # data cleaning, variable construction, regression
├── Jupyter exports/    # html exports of notebooks
├── Research Paper.gdoc # project writing file
├── README.md           
└── other files         # Jupyter  notebooks, data sets …
```

## Caveats

No brand/model/condition data, so there's real risk of omitted variable bias — a beat-up BMW and a pristine BMW of the same age/mileage are treated identically here. Also single-platform, single-point-in-time data, so treat this as a cross-sectional snapshot, not a true depreciation curve over time.

## Why I built this

A statistics/econometrics exercise, ended up being a genuinely interesting look at how national market structure shapes pricing - which is basically a valuation/risk question wearing a car-shopping costume.
