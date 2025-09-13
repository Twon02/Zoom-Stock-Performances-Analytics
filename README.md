# ZM Earnings Impact Analysis (2019–2022)

Analyze how **Zoom (ZM)** stock behaves **around quarterly earnings** using a **static snapshot** (no live APIs). Clear steps, reproducible results, and plots after every section.

---

## 1) Overview
- **Goal:** Do earnings drive short‑horizon returns and volatility?
- **Approach:** Daily OHLCV + a small earnings calendar. Compare **±5 trading days** around earnings vs normal days.
- **Why static files?** Reproducible on GitHub. No API breakage. Reviewers can run it as‑is.

---

## 2) Data
- `data/zm_prices.csv` — Kaggle Zoom daily OHLCV (2019-04-18 → 2022-05-20)
- `data/zm_earnings.csv` — curated quarterly earnings (2019‑06‑06 → 2022‑02‑28)  
  Columns: `Date, EPS_Estimate, EPS_Actual, SurprisePct`

> Note: Many tech earnings are **after market close**. We mark the **trading day** that captures the reaction.

---

## 3) What’s inside the notebook
`ZM_Earnings_Impact_Analysis.ipynb` produces a plot or table after each step:
1. **Price trend** (context)  
2. **Daily returns** + **21‑day rolling volatility**  
3. **Earnings flags** (day + ±5d window)  
4. **Mean return**: earnings window vs normal  
5. **Volatility**: distribution & averages  
6. **Event study**: average cumulative path for t = −5 … +5  
7. (Optional) **Welch t‑test** and **OLS** (non‑causal)  
8. **Tableau export**: `tableau/zm_tableau_dataset.csv`

---

## 4) Quick results (from this dataset)
- **Price window used:** 2019-04-18 → 2022-05-20  
- **Earnings events included:** 12
- **Mean daily return (±5d window):** -0.000042  (≈ -0.004%)  
- **Mean daily return (normal):** 0.001551  (≈ 0.155%)  
- **Avg 21‑day volatility (window):** 0.04268  (≈ 4.268%)  
- **Avg 21‑day volatility (normal):** 0.03872  (≈ 3.872%)

**Interpretation**
- Return difference is small (and may be statistically weak).
- **Volatility is higher** around earnings — common for single‑name equities.
- Event‑study line helps you see if the move clusters at **t = 0** or **t = +1** (after‑hours timing).

---

## 5) Repository structure
```
.
├── ZM_Earnings_Impact_Analysis.ipynb
├── data/
│   ├── zm_prices.csv
│   └── zm_earnings.csv
├── outputs/                # auto‑saved by the notebook
│   ├── 01_price_full.png
│   ├── 02_return_distribution.png
│   ├── 03_vol21_with_earnings_days.png
│   ├── 04_avg_return_bar.png
│   ├── 05_vol21_box.png
│   ├── 06_event_study_avg_path.png
│   ├── 07_price_with_markers.png
│   └── 08_executive_snapshot.png
└── tableau/
    └── zm_tableau_dataset.csv
```

---

## 6) How to run (VS Code + venv)
```bash
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows
.venv\Scripts\activate

python -m pip install -U pip wheel setuptools
# minimal
pip install pandas numpy matplotlib
# optional stats
pip install scipy statsmodels

# open the notebook in VS Code, pick the .venv kernel, then: Run All
```

---

## 7) How to read the charts
- **Price with markers:** where earnings sit in the macro trend  
- **Return histogram:** distribution shape / tails  
- **Volatility (21‑day) with markers:** where risk clusters  
- **Mean return bar (window vs normal):** directional difference  
- **Volatility boxplot (window vs normal):** risk uplift  
- **Event study (t = −5…+5):** average reaction path (check **t = +1** for AMC)

---

## 8) Limitations & next steps
- Static snapshot ends 2022-05-20 (not a live feed).  
- No market model: next step is **abnormal returns vs QQQ/SPY**.  
- Daily bars only (no intraday).  
- Split analysis by **SurprisePct** (positive vs negative beats).  
- If extending regression, use **robust SE (e.g., Newey–West)**.

---

## 9) Sources
- Price snapshot: Kaggle (Zoom OHLCV)  
- Earnings dates & EPS: AlphaQuery (compiled into `zm_earnings.csv`)

---

## 10) Contact

**Toan Le**  
- 📧 Email: [nguyenphutoanle@gmail.com](mailto:nguyenphutoanle@gmail.com?subject=ZM%20Earnings%20Analysis%20%F0%9F%93%88)  
- 💼 LinkedIn: https://www.linkedin.com/in/toanle02/  
- 🧑‍💻 GitHub: https://github.com/Twon02  

> Questions about this project? Please open an **Issue** in this repo instead of emailing—this keeps discussion transparent and searchable.

*This project is for educational/portfolio use only — not investment advice.*
