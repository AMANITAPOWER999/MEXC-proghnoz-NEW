# Binary Options Trading Bot (ETH/USDT)

## Overview
A trading bot that automates Binary Options trades on the ETH/USDT pair using the Parabolic SAR (PSAR) strategy across multiple timeframes. Includes a real-time web dashboard and optional Telegram integration.

## Architecture

### Backend (Python/Flask)
- **main.py** — Entry point, imports Flask app
- **app.py** — Flask web server, REST API endpoints, bot lifecycle management
- **trading_bot.py** — Core trading logic, Parabolic SAR calculations, strategy loop
- **market_simulator.py** — Simulated market data (used when `USE_SIMULATOR=1`)
- **telegram_notifications.py** — Telegram alerts and message handling
- **telegram_bot_handler.py** — Telegram WebApp setup
- **signal_sender.py** — External webhook/signal sender

### Frontend (Vanilla JS + Bootstrap 5)
- **templates/dashboard.html** — Main monitoring dashboard
- **templates/webapp.html** — Telegram WebApp interface
- **static/css/** — Stylesheets
- **static/js/** — JavaScript files including dashboard.js

### State Persistence
- JSON file: `goldantilopaeth500_state.json` — Stores balance, positions, trade history

## Tech Stack
- **Runtime**: Python 3.11+
- **Package Manager**: uv
- **Web Framework**: Flask + Gunicorn
- **Trading**: CCXT (Ascendex exchange), TA library (Parabolic SAR), Pandas
- **Frontend**: Vanilla JS, Bootstrap 5, Font Awesome
- **Notifications**: Telegram Bot API

## Trading Strategy
- **Timeframes**: 1m, 5m, 15m
- **Entry Signal**: SAR direction aligns across all three timeframes
- **Exit**: Fixed duration (default 10 minutes) — Binary Options model
- **Bet**: Fixed $5 per trade; win = +$4 (80%), loss = -$5 (100%)
- **Modes**: Paper Trading (default) and Live Trading (via Ascendex)

## Running the App
- **Workflow**: `Start application` runs `gunicorn --bind 0.0.0.0:5000 --reuse-port --reload main:app`
- **Port**: 5000

## Environment Variables (Optional)
- `TELEGRAM_BOT_TOKEN` — Telegram bot token for notifications
- `TELEGRAM_CHAT_ID` — Telegram chat/channel ID
- `TELEGRAM_OWNER_ID` — Telegram owner user ID
- `SESSION_SECRET` — Flask session secret (auto-generated if not set)
- `DASHBOARD_PASSWORD` — Optional password to protect dashboard
- `RUN_IN_PAPER` — Set to `0` for live trading (default `1` = paper mode)
- `USE_SIMULATOR` — Set to `1` to use simulated market data

## Deployment
- **Target**: VM (always-running, maintains in-memory state)
- **Run command**: `gunicorn --bind=0.0.0.0:5000 --reuse-port main:app`
