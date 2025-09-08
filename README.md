# Automated-Options-Market-Maker

This repository extends my Options Market Maker Demo and runs it in an IBKR Paper Trading environment.
The base repo explains the core logic (CRR pricing, IV solver, inventory‑aware quoting, risk, hedging).

Here, the focus is on: 
- IBKR Paper Trading integration
- Weekly performance updates 
- Iteratively improving each component toward a more robust market-making system

# What's New In This Repo

1. IBKR Execution Path:
   - ib_connector.py → TWS/Gateway session management (paper).
   - ibkr_adapter.py → Thin wrapper to place/modify/cancel and receive fills.

2. Paper‑Trading Loop:
   - mm_loop_ibkr.py → builds quotes from yfinance chains (IBKR market data to be added later once the system is more stable), routes orders to IBKR Paper, consumes fills, and updates risk
   - *Note: Market data comes from `yfinance` for now; an IBKR data subscription is not required to run this repo.* 

3. Weekly Reports & Updates:
   - Summaries of PnL, exposures, and inventory snapshots under reports/

## Repo Structure

- pricer.py # (from base demo)
- iv_solver.py # (from base demo)
- live_data.py # yfinance options chain/spot (for now)
- batch_surface.py # Batch IV calculation
- mm_quote.py # Inventory-aware quoting
- risk_tracker.py # RiskBook: delta/vega exposures
- mm_vega.py # Vega hedge sizing
- ib_connector.py # TWS/Gateway session management (paper)
- ibkr_adapter.py # Thin wrapper for IBKR orders/fills
- mm_loop_ibkr.py # Event loop: yfinance → quotes → IBKR orders → fills → risk management

## Requirements

# Python Libraries: 
- numpy
- pandas
- yfinance
- ib_insync
- python-dotenv

Install dependencies:

```bash
pip install numpy pandas yfinance ib_insync python-dotenv
```

# IBKR API Access

- Requires a funded IBKR Pro account (IBKR Lite accounts do not support API access).
- Once funded, you’ll also get a linked Paper Trading account with API access.
- For setup instructions (TWS/Gateway, enabling API, ports, etc.), please see the official IBKR API documentation.

