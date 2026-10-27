# Stock Market Predictor

A Jupyter notebook project that pulls historical S&P 500 data and explores whether past price behaviour can be used to predict future movements.

> **Status:** work in progress. This is a learning project, not financial advice.

## What it does

- Downloads the full price history for the S&P 500 index (`^GSPC`) from Yahoo Finance using `yfinance`
- Loads and cleans the data with `pandas`
- Plots the closing price over time with `matplotlib`
- Builds and evaluates a prediction model with `scikit-learn` *(update this line as the model develops)*

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

## Notes

- Data comes from Yahoo Finance via `yfinance`. If a download fails, it's usually rate limiting or a change on Yahoo's side rather than a bug in the notebook.
- Index tickers on Yahoo use a caret, so the S&P 500 is `^GSPC`, not `GSPC`.
- `yfinance` currently prints some pandas deprecation warnings. These come from the library itself and don't affect the results.

## Roadmap

- [ ] Add feature engineering (returns, moving averages, etc.)
- [ ] Train and evaluate a baseline model
- [ ] Compare against a simple "no change" benchmark
- [ ] Document results and limitations

## Disclaimer

This project is for educational purposes only. Nothing here is financial advice, and past performance does not guarantee future results.
