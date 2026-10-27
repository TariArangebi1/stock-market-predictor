# Stock Market Predictor

A Jupyter notebook project that pulls historical S&P 500 data and tests whether past price behaviour can be used to predict future movements.

> **Status:** work in progress. This is a learning project, not financial advice.

## What's been done so far

1. **Downloaded the data:** full S&P 500 (`^GSPC`) price history from Yahoo Finance using `yfinance`
2. **Cleaned and visualised it:** removed unneeded columns, plotted the closing price over time
3. **Set up the ML target:** whether the market closes higher the next day (1) or not (0)
4. **Trained an initial model** with `scikit-learn`
5. **Evaluated the errors** to see where the model was going wrong
6. **Built a backtest:** a way to test the model on past data it hasn't seen, so results aren't flattered by training on the answers
7. **Improved the model with extra predictors:** rolling-average ratios and recent-trend counts over several time horizons (2, 5, 60, 250 and 1000 days), using a random forest that only predicts "up" when it is at least 60% confident. Backtest precision rose from 0.53 to **0.575**. The market rises on about 53.7% of days, so that is the baseline to beat

## Tech stack

- Python 3.13
- JupyterLab
- pandas
- yfinance
- scikit-learn
- matplotlib

## Getting started

**1. Clone the repo**

```
git clone https://github.com/TariArangebi1/stock-market-predictor.git
cd stock-market-predictor
```

**2. Create and activate a virtual environment**

```
py -3.13 -m venv jupyter-env
jupyter-env\Scripts\activate
```

On macOS/Linux, use `python3 -m venv jupyter-env` and `source jupyter-env/bin/activate`.

**3. Install dependencies**

```
pip install -r requirements.txt
```

**4. Launch JupyterLab**

```
jupyter lab
```

Then open `stock_market_predictor.ipynb`.

## Project structure

```
.
├── stock_market_predictor.ipynb   # main notebook
├── requirements.txt               # Python dependencies
├── .gitignore
└── README.md
```

## Ideas for improving the model

I plan to extend this project and keep pushing the accuracy up. Ideas so far:

### 1. News and article data
Price alone ignores what's happening in the world. Adding signals from news articles (for example, sentiment scores or counts of events like tariffs, sanctions or disruptions) could give the model information that price history can't.

This links to **SupplySphere**, a supply-chain disruption prediction concept I developed during my Microsoft work experience. SupplySphere tracks things like trade policy and tariffs, geopolitical conflict, sanctions, extreme weather, cyber threats and economic instability, using sources such as UN Comtrade, World Bank Open Data, OFAC and NOAA. Many of those same signals move markets, so some could be reused here as extra predictors, such as tariff changes, PMI, inflation and interest rates.

### 2. More frequent / real-time data
Daily data limits how much the model can learn. Higher-frequency data (hourly, or roughly 12-hourly) would give more rows and let the model react faster. `yfinance` supports intraday intervals, though only for a limited look-back window, so a proper real-time source may be needed later.

### 3. Better evaluation
- The model's 0.575 precision beats the 0.537 "always predict up" baseline by only a few points, so check whether the gap holds up on different time periods
- Look at accuracy and recall as well as precision, since precision only covers the ~885 days (out of ~5,800) where the model calls "up"
- Tune the 0.6 confidence threshold and the model settings, using a validation period that is separate from the final backtest
- Try other models

### 4. Turn it into a portfolio platform
Link this with my JavaScript work, including **Dangerfy** (a staged-alert escalation logic simulator), to build a web front end for viewing predictions, backtest results and alerts in one place. Dangerfy needs finishing first.

## Roadmap

- [x] Download and clean S&P 500 data
- [x] Visualise the data
- [x] Set up the prediction target
- [x] Train an initial model
- [x] Evaluate errors
- [x] Build a backtest
- [x] Add extra predictors (precision 0.575)
- [ ] Add news / article-based features
- [ ] Explore higher-frequency or real-time data
- [x] Compare against a naive benchmark (up days are 53.7% of the total)
- [ ] Build a front-end dashboard

## Notes

- Index tickers on Yahoo use a caret, so the S&P 500 is `^GSPC`, not `GSPC`.
- If a `yfinance` download fails, it's usually rate limiting or a change on Yahoo's side rather than a bug in the notebook.
- `yfinance` currently prints some pandas deprecation warnings. These come from the library itself and don't affect the results.

## Disclaimer

This project is for educational purposes only. Nothing here is financial advice, and past performance does not guarantee future results.
