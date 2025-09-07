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

3. Weekly Reports & Updates:
   - Summaries of PnL, exposures, and inventory snapshots under /reports


