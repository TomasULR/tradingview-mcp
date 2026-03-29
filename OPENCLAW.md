# TradingView MCP × OpenClaw Integration

Use [OpenClaw](https://openclaw.ai) to connect your **tradingview-mcp** AI Trading Intelligence Framework to **Telegram, WhatsApp, Discord**, and 20+ other channels — so you can ask trading questions in plain language from any device.

## What This Enables

After setup, you can send messages like:

| Message | What Happens |
|---------|-------------|
| `AAPL analiz et` | Live price + RSI/MACD/Bollinger + Reddit sentiment combined |
| `BTC 2 yılda en iyi strateji neydi?` | Runs all 6 strategies, returns ranked leaderboard |
| `Bugün piyasalar nasıl?` | S&P500, NASDAQ, BTC/ETH, EUR/USD snapshot |

## Prerequisites

- [OpenClaw](https://openclaw.ai) installed and running (`openclaw doctor` returns healthy)
- A running gateway (Hetzner VPS, local machine, etc.)
- `uv` installed on the same machine as OpenClaw

## Setup (5 Minutes)

You don't need to configure `mcpServers` inside OpenClaw. Instead, we use a lightweight `trading.py` wrapper that acts as a bridge between the OpenClaw agent and the `tradingview-mcp` library.

### 1. Install Dependencies

```bash
# Install uv if you don't have it
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Install tradingview-mcp-server
uv tool install tradingview-mcp-server
```

### 2. Configure Telegram (or other channel)

Create or edit your `~/.openclaw/openclaw.json`:

```json5
{
  channels: {
    telegram: {
      botToken: "YOUR_BOT_TOKEN_HERE",
    },
  },
}
```

### 3. Install the Skill and Tool

This is what tells the agent how to act as a trader.

```bash
mkdir -p ~/.agents/skills/tradingview-mcp ~/.openclaw/tools

# Download the TradingView skill (instructions)
curl -fsSL https://raw.githubusercontent.com/atilaahmettaner/tradingview-mcp/main/openclaw/SKILL.md \
  -o ~/.agents/skills/tradingview-mcp/SKILL.md

# Download the trading execution wrapper (tools)
curl -fsSL https://raw.githubusercontent.com/atilaahmettaner/tradingview-mcp/main/openclaw/trading.py \
  -o ~/.openclaw/tools/trading.py
chmod +x ~/.openclaw/tools/trading.py
```

### 4. Configure Your AI Model

You can use Claude, Gemini, or DeepSeek. We recommend **OpenRouter** for the best tool calling at the lowest price (effectively free using Gemini Flash).

```bash
# Set gateway to local
openclaw config set gateway.mode local

# Ensure main agent is selected
openclaw config set acp.defaultAgent main

# Use Gemini 3 Flash via OpenRouter (or Claude directly)
openclaw config set agents.defaults.model "openrouter/google/gemini-3-flash-preview"

# Setup your OpenRouter API Key
openclaw configure --section model
```

### 5. Restart OpenClaw

```bash
openclaw gateway install
systemctl --user start openclaw-gateway.service
openclaw doctor
```

## Example: Public Telegram Bot (Let Others Use It)

To let other users interact with your trading bot, open the Telegram channel in `~/.openclaw/openclaw.json`:

```json5
{
  channels: {
    telegram: {
      botToken: "YOUR_BOT_TOKEN",
      allowFrom: ["*"],           // Allow all users to DM the bot
      groups: {
        "*": {
          requireMention: true,   // In groups: require @YourBotName mention
        },
      },
    },
  },
}
```

> ⚠️ **Security:** With `allowFrom: ["*"]`, anyone who finds your bot can use it. Each user consumes API tokens. Consider setting an allowlist of specific Telegram user IDs for private use.

## Available Tools (After Integration)

Your OpenClaw agent will have access to all tradingview tools via the wrapper:

### Market Data
- `yahoo_price` — Real-time price for any stock, crypto, ETF, index
- `market_snapshot` — Global market overview (S&P500, NASDAQ, BTC, EUR/USD...)
- `get_prices_bulk` — Multi-symbol price lookup

### Technical Analysis
- `technical_analysis` — 30+ indicators: RSI, MACD, Bollinger, EMA, ATR, ADX...
- `calculate_rsi`, `calculate_macd`, `calculate_bollinger`, `calculate_supertrend`, etc.
- `calculate_atr`, `calculate_donchian_channel`

### Backtesting
- `backtest_strategy` — Run RSI / Bollinger / MACD / EMA Cross / Supertrend / Donchian
  - Supported: `interval="1h"` for hourly, `include_trade_log=True`, `include_equity_curve=True`
- `compare_strategies` — Rank all 6 strategies by Sharpe ratio
- `walk_forward_backtest_strategy` — Overfitting detection with robustness score

### Sentiment & News
- `analyze_sentiment` — Reddit sentiment for any ticker
- `fetch_news_summary` — Latest news from financial RSS feeds

### Screener
- `screener_bullish`, `screener_oversold`, `screener_strong_trend` — TradingView screener
- `egx_stock_screen` — Egyptian Exchange specific screening

## Supported Markets

| Market | Symbols |
|--------|---------|
| US Stocks | AAPL, TSLA, NVDA, MSFT, GOOGL, AMZN |
| Crypto | BTC-USD, ETH-USD, SOL-USD, BNB-USD |
| ETFs | SPY, QQQ, GLD, VTI |
| Indices | ^GSPC (S&P500), ^DJI (Dow), ^IXIC (NASDAQ), ^VIX |
| Turkish | THYAO.IS, SASA.IS, BIMAS.IS, KCHOL.IS |
| Egyptian | COMI.CA, HRHO.CA, EAST.CA |
| FX | EURUSD=X, GBPUSD=X, JPYUSD=X |

## Troubleshooting

**`uvx: command not found`**
```bash
export PATH="$HOME/.local/bin:$PATH"
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
```

**Tools not showing up in OpenClaw**
```bash
openclaw doctor
openclaw gateway restart
```

**Yahoo Finance data fails**
The server uses a direct + proxy fallback. Without a proxy, some symbols may fail due to regional restrictions. Configure `PROXY_*` env vars in the MCP server config.

---

For more, see the [tradingview-mcp README](https://github.com/atilaahmettaner/tradingview-mcp).
