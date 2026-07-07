# GeoPulse Intelligence — Commodities & Currency Markets

**Applied Data Analytics and Market Research Assignment**
Author: Vaibhav Malhotra

An end-to-end analysis linking 80+ years of commodity price history (Brent Oil, Gold, Silver) with SWIFT's Global Currency Tracker, connecting the observed market patterns to real 2025–2026 global events (the Iran–Hormuz crisis, BRICS de-dollarisation, gold accumulation, and tariff/sanctions activity).

---

## 📁 Project Structure

```
geopulse-intelligence/
├── README.md                              # This file
├── requirements.txt                       # Python dependencies
├── geopulseintelligence-notebook.ipynb    # Main analysis notebook (run top to bottom)
│
├── data/                                  # Input datasets
│   ├── Brent_Oil.csv
│   ├── silver_100_years.csv
│   ├── Gold_100years.csv
│   └── swift_currency_tracker_all_reports.csv
│
├── reports/                               # Written deliverables
│   ├── DSB_assignment.docx                # Original assignment brief
│   ├── DSB_GeoPulse_Intelligence_VaibhavMalhotra.docx   # Part I answers (Q1–Q30)
│   ├── Part_II_Market_Research_Component.docx           # Part II answers (event research)
│   └── Bonus_Analytics_Section.docx       # Bonus B1–B6 answers
│
└── outputs/                               # Generated on notebook run
    ├── DSB_Cleaned_Datasets.xlsx          # Cleaned data + summary tables workbook
    ├── fig1_brent_oil_trend.png … fig7_dashboard.png
    ├── figB1_annual_pct_change.png … figB6_gold_forecast.png
    └── GeoPulse_Intelligence_Outputs.zip  # All figures + workbook, zipped
```

---

## 🧭 Project Overview

| Item | Description |
|---|---|
| **Objective** | Produce evidence-based insights on commodity and global currency markets, then connect observed patterns to real-world macro/geopolitical events. |
| **Part I** | Data Analytics — cleaning, descriptive statistics, trend visualisation, currency-tracker analysis, and comparisons (30 questions). |
| **Part II** | Market Research — event identification and linkage between global events and market data (16 questions). |
| **Bonus** | Percentage change, correlation, heat map, scatter plot, moving averages, and a simple linear forecast (B1–B6). |
| **Output** | A written report, a cleaned Excel workbook, and 15+ labelled charts/dashboards. |

---

## 📊 Datasets

| File | Coverage | Rows | Description |
|---|---|---|---|
| `Brent_Oil.csv` | Jan 1946 – Mar 2026 | 963 | Monthly Brent crude oil price (USD/barrel) |
| `Gold_100years.csv` | Jan 1915 – Apr 2026 | 1,336 | Monthly gold price (USD/oz) |
| `silver_100_years.csv` | Jan 1915 – Apr 2026 | 1,336 | Monthly silver price (USD/oz) |
| `swift_currency_tracker_all_reports.csv` | Jan 2026 – Apr 2026 | 330 | SWIFT Global Currency Tracker: global payment share, trade finance share, offshore RMB economy share, FX spot rankings |

All four datasets were checked for missing values and duplicate dates — none were found. Date columns were parsed into proper datetime types with derived `Month`/`Year` fields for the three commodity series.

---

## 🔍 Key Findings (Summary)

- **Oil is the most event-sensitive market.** Brent Oil jumped **+52% in one month** (Feb → Mar 2026, $67.66 → $102.86) following the Iran–Hormuz Strait disruption — the sharpest short-term move of any asset in the dataset.
- **Gold is at a structural, multi-decade high**, trading at **1,085% above its long-term average** ($4,712.89 vs. $397.55), driven by central-bank/BRICS gold accumulation and safe-haven demand.
- **Silver led gold by one month** (peaking in Jan 2026 vs. Feb 2026 for gold), suggesting an industrial-demand-driven rally (EVs, solar, defence electronics) that preceded the geopolitical safe-haven spike.
- **Gold and Silver are very tightly correlated** (r = 0.95); Oil correlates only moderately with both (r ≈ 0.46–0.51), meaning oil offers more diversification benefit than a gold/silver pairing.
- **USD still dominates global payments** at **51.14%** (58.50% ex-Eurozone), and its share *rose* into the Hormuz crisis — a classic "flight to safety" effect.
- **CNY punches above its weight in trade finance** (rank #2, 8.04%) despite a modest global payments share (rank #5, 3.10%), and **75.23% of all offshore RMB activity runs through Hong Kong**, a notable concentration risk.

Full findings, charts, and event-linked commentary are in `reports/`.

---

## ⚙️ How to Run

### Option 1 — Kaggle (recommended, zero setup)
1. Upload the four CSVs in `data/` as a Kaggle Dataset ("+ Add Data").
2. Open `geopulseintelligence-notebook.ipynb` in a Kaggle Notebook.
3. Click **Run All**. The notebook auto-detects the dataset path under `/kaggle/input/`.
4. Use the final cell to download all outputs as a single ZIP.

### Option 2 — Local / Jupyter
```bash
# 1. Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Place the 4 CSVs inside a "data/" folder next to the notebook
mkdir -p data
# copy Brent_Oil.csv, Gold_100years.csv, silver_100_years.csv,
# swift_currency_tracker_all_reports.csv into data/

# 4. Launch and run
jupyter notebook geopulseintelligence-notebook.ipynb
# Run All Cells
```

Outputs (charts + cleaned workbook + ZIP) are written to `outputs/` automatically — no path editing required in either environment, since the notebook searches `/kaggle/input`, `data/`, and `.` for the CSVs.

---

## 🛠️ Methodology Notes

- **Cleaning:** dates parsed to `datetime64`, `Month`/`Year` columns derived; no imputation was needed as there were no missing values.
- **Correlation (B2/B3):** Pearson correlation on **annual average** prices, to avoid short-term noise dominating the relationship.
- **Moving averages (B5):** 12-month and 60-month (5-year) rolling means applied to Brent Oil to separate cyclical noise from structural trend.
- **Forecast (B6):** simple linear regression fitted on Gold prices from Jan 2010 onward, extrapolated 12 months. **This is a naive statistical estimate, not a financial prediction** — it does not account for geopolitics, policy, or sentiment, and is explicitly flagged as such in the report.

---

## 📦 Requirements

See [`requirements.txt`](requirements.txt). Core stack: `pandas`, `numpy`, `matplotlib`, `openpyxl` (Excel export), run inside `jupyter`/`ipython`.

---

## ⚠️ Disclaimer

This project is an educational/analytical exercise. Charts and the linear forecast are estimates derived from historical data only and **do not constitute financial or investment advice**. Market events referenced (Iran–Hormuz crisis, BRICS activity, tariffs) are drawn from the supplied source reports for the purpose of this assignment and should be independently verified before use in any real decision-making context.
