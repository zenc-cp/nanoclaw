---
name: crypto-dca-monitor
description: Crypto DCA (Dollar Cost Averaging) trading monitor and manager for NanoClaw. Monitors trading status, auto-restarts DCA bot, reports portfolio P&L, and manages earning strategies via ClawWork Cloud API. Triggers on "check trading", "dca status", "portfolio", "trading report", "start trading", "stop trading".
---

# Crypto DCA Trading Monitor

Automated crypto DCA trading management via ClawWork Cloud API.

> Compatibility: NanoClaw v1.0.0+

## Features

| Action | Endpoint | Description |
|--------|----------|-------------|
| Check Status | GET /dca/status | Get current DCA bot status, trades, errors |
| Start DCA | POST /dca/start | Start the DCA trading bot |
| Stop DCA | POST /dca/stop | Stop the DCA trading bot |
| Dashboard | GET /dashboard | Overall system dashboard |
| Health Check | GET /health | API health check |

## Configuration

### API Endpoint

```
API_BASE=https://clawwork-cloud-api-sg.onrender.com
```

### Trading Parameters (Current)

- Exchange: Binance
- DCA Pairs: BTC/USDT, ETH/USDT
- DCA Amount: $11 USDT per trade
- DCA Interval: 24 hours
- Region: Singapore (Render)

## Quick Start

### 1. Check Trading Status

```bash
curl https://clawwork-cloud-api-sg.onrender.com/dca/status
```

Key fields to monitor:
- `is_running`: Whether DCA bot is active
- `api_configured`: Whether Binance API keys are set
- `total_dca_trades`: Number of completed trades
- `total_spent_usdt`: Total USDT invested
- `total_bought`: Crypto accumulated
- `recent_errors`: Any errors to address

### 2. Auto-Monitor (Scheduled Task)

```
schedule_task(
  prompt: "Check DCA status at https://clawwork-cloud-api-sg.onrender.com/dca/status. If is_running is false and api_configured is true, start it via POST /dca/start. Report status summary.",
  schedule_type: "cron",
  schedule_value: "*/30 * * * *"
)
```

### 3. Daily Portfolio Report

```
schedule_task(
  prompt: "Generate daily portfolio report. GET /dca/status, calculate total value based on current prices, report P&L to user.",
  schedule_type: "cron",
  schedule_value: "0 1 * * *"
)
```

## Known Issues

- **Binance 451 Error**: Geo-restriction from certain IP ranges. SG region helps but may still occur.
- **NOTIONAL Filter**: Minimum order amount not met. Increase dca_amount_usdt if triggered.
- **API Key Permissions**: Ensure Binance API key has spot trading permissions and IP whitelist includes Render SG IPs.

## Error Handling

1. If `recent_errors` contains "451" -> Geo-restriction, report to user
2. If `recent_errors` contains "NOTIONAL" -> Increase trade amount
3. If `recent_errors` contains "Invalid API-key" -> API key needs reconfiguration
4. If `is_running` is false -> Auto-restart via POST /dca/start

## Trading Log

Maintain a trading log at `/workspace/group/trading-log.md` with:
- Date/time of each trade
- Pair, amount, price
- Running total invested
- Running total accumulated
- Estimated P&L
