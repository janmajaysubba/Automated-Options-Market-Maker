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

# Repo Structure

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

# Requirements

 ## 1. **Python Libraries:**
    
   - numpy
   - pandas
   - yfinance
   - ib_insync
   - python-dotenv

   Install dependencies:

```bash
pip install numpy pandas yfinance ib_insync python-dotenv
```

## 2. **Environment Setup**

   Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
```
   
   Set up environment variables in a ".env" file to configure IBKR connection and market maker parameters in the same directory as the other modules. 

```bash
# IBKR connection
IB_TARGET=tws-paper        # tws-paper | tws-live | gw-paper | gw-live
IB_CLIENT_ID=101           # arbitrary int; must be unique per session
IB_MARKET_DATA_TYPE=3      # 3=delayed (default, free), 1=live (requires subscription)
IB_HOST=127.0.0.1          # local TWS/Gateway host
# IB_PORT=7497             # override if you changed the default paper port

# Market maker parameters
MM_TICKER=SPY              # underlying ticker
MM_EXPIRY=2025-10-08       # options expiry (YYYY-MM-DD)
MM_BAND=0.95,1.05          # relative strike band for quoting
MM_QTY=1                   # quote size (contracts)

```

   *Important:*
   
   *The script has default values for most MM_* parameters (MM_TICKER, MM_BAND, MM_QTY). However, MM_EXPIRY must always be set manually in .env to a valid option expiry date (YYYY-MM-DD). Be extra careful to use an expiry that actually exists in IBKR — otherwise, the program will not function correctly.*

## 3. **IBKR API Access**
   
   - Requires a funded IBKR Pro account (IBKR Lite accounts do not support API access).
   - Once funded, you’ll also get a linked Paper Trading account with API access.
   - For setup instructions (TWS/Gateway, enabling API, ports, etc.), please see the official IBKR API documentation.

 
