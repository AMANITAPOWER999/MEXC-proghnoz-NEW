---
title: MEXC Prognoz
emoji: 📈
colorFrom: blue
colorTo: indigo
sdk: docker
pinned: false
app_port: 7860
---

# MEXC ETH/USDT Signal Bot

SAR-based trading signal system for MEXC Event Futures ETH/USDT.

## Environment Variables (Secrets)

Set these in the Space settings:

| Variable | Description |
|----------|-------------|
| `MEXC_API_KEY` | MEXC API Key |
| `MEXC_SECRET` | MEXC Secret Key |
| `RUN_IN_PAPER` | Set to `1` for paper mode (default) |
| `SESSION_SECRET` | Random string for Flask sessions |
