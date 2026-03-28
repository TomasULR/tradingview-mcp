# 📈 AI Trading Intelligence Framework (MCP Server)

A powerful, multi-agent Model Context Protocol (MCP) server that transforms Claude (or any MCP client) into an autonomous financial analysis firm. By deploying specialized AI agents—Technical Analyst, Sentiment Analyst, and Risk Manager—the framework collaboratively evaluates real-time market conditions and delivers consensus-driven trading decisions.

**Now with real-time Reddit sentiment analysis + live financial news integration.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![MCP Ready](https://img.shields.io/badge/MCP-Ready-brightgreen)](https://modelcontextprotocol.com/)
[![Version](https://img.shields.io/badge/version-v0.5.0-blue)](https://github.com/atilaahmettaner/tradingview-mcp/releases)
[![GitHub Sponsors](https://img.shields.io/badge/Sponsor-❤️-pink?logo=github-sponsors)](https://github.com/sponsors/atilaahmettaner)
[![PyPI](https://img.shields.io/badge/PyPI-tradingview--mcp--server-orange)](https://pypi.org/project/tradingview-mcp-server/)

> **⭐ If this tool improves your workflow, please star the repo and consider [sponsoring](https://github.com/sponsors/atilaahmettaner) — it helps keep the project maintained and growing!**

---

## 🤖 The Multi-Agent Architecture

Unlike basic screeners, this framework decomposes complex trading tasks into specialized roles to ensure robust, scalable decision-making:

1. **🛠️ Technical Analyst Agent**: Evaluates intrinsic price action using Bollinger Bands (proprietary rating from -3 to +3), RSI, and MACD.
2. **🌊 Sentiment & Momentum Analyst**: Analyzes recent price momentum, MACD crossovers, and RSI trends to gauge short-term market mood.
3. **🛡️ Risk Manager**: Continuously evaluates portfolio risk by assessing market volatility (Bollinger Band Width) and mean reversion risk against major moving averages (SMA20, EMA200).

*Agents debate their findings in real-time to output a single logical framework decision: `STRONG BUY`, `BUY`, `HOLD`, `SELL`, or `STRONG SELL` with calculated confidence levels.*

---

## 🎥 Framework Demo
> **Quick 19-second demo showing the underlying data retrieval in action**

https://github-production-user-asset-6210df.s3.amazonaws.com/67838093/478689497-4a605d98-43e8-49a6-8d3a-559315f6c01d.mp4

## ✨ Why this Framework? (vs Traditional Setups)

| Feature | `tradingview-mcp` | Traditional Trading Agents | Bloomberg Terminal |
|---------|--------------------|----------------------------|--------------------|
| **Setup Time** | 5 minutes | Hours (Docker, Conda...) | Weeks (Contracts) |
| **Cost** | Free (Open Source) | Free | $30k+/year |
| **Market Data** | Live / Real-Time | Historical / Delayed | Live |
| **API Keys Needed** | **None** | Multiple (OpenAI, AlphaVantage) | N/A |
| **Architecture** | MCP integrated Agents | Complex Graph Networks | Proprietary UI |

---

## 🚀 Quick Start (5-Minute Setup)

### Option 1: Docker (Fastest)

Run the framework immediately on port 8080:
```bash
docker run -p 8080:8000 atilaahmet/tradingview-mcp:latest
```

**Claude Desktop Configuration:**
```json
{
  "mcpServers": {
    "tradingview-mcp": {
      "command": "curl",
      "args": ["-s", "http://localhost:8080/sse"]
    }
  }
}
```
*(For Cursor/Windsurf, just use the SSE URL: `http://localhost:8080/sse`)*

### Option 2: Python / PyPI

Install the package directly:
```bash
uv tool install tradingview-mcp-server
# or standard pip:
pip install tradingview-mcp-server
```

**Claude Desktop Configuration:**
```json
{
  "mcpServers": {
    "tradingview-mcp": {
      "command": "tradingview-mcp",
      "args": []
    }
  }
}
```

### Option 3: Direct Git Execution (No Installation)

1. **Install UV Package Manager:**
   ```bash
   brew install uv  # macOS
   curl -LsSf https://astral.sh/uv/install.sh | sh  # Linux
   ```

2. **Claude Desktop Configuration:**
   ```json

   {
     "mcpServers": {
       "tradingview-mcp": {
         "command": "uv",
         "args": [
           "tool", "run", "--from",
           "git+https://github.com/atilaahmettaner/tradingview-mcp.git",
           "tradingview-mcp"
         ]
       }
     }
   }
   ```

3. **Restart Claude Desktop** - The framework is now loaded and your AI Analyst firm is ready!

📋 **For detailed Windows or Manual Local Installation instructions, see [INSTALLATION.md](INSTALLATION.md)**

---

## 🛠️ Framework Capabilities

### 🧠 Multi-Agent Analysis
| Tool | Description | Example Usage |
|------|-------------|---------------|
| `multi_agent_analysis` | Runs the full 3-agent debate for a final trading decision | "Run a multi-agent analysis on BTC on Binance" |
| `coin_analysis` | Raw deep-dive for manual technical analysis | "Analyze IBM stock on NYSE with technical indicators" |
| `combined_analysis` | **NEW** ⚡ Technical + Reddit Sentiment + Live News confluence | "Full analysis on AAPL with news and sentiment" |

### 📡 Sentiment & News *(New in v0.5.0)*
| Tool | Description | Example Usage |
|------|-------------|---------------|
| `market_sentiment` | Real-time Reddit sentiment across r/wallstreetbets, r/stocks, r/CryptoCurrency | "What's Reddit saying about ETH right now?" |
| `financial_news` | Live headlines from Reuters, CoinDesk, CoinTelegraph via RSS | "Get the latest crypto news" |

### 📈 Real-Time Market Screening
| Tool | Description | Example Usage |
|------|-------------|---------------|
| `top_gainers` | Find highest performing assets | "Top crypto gainers in 15m" |
| `top_losers` | Find biggest declining assets | "Worst performing stocks today" |
| `bollinger_scan` | Find assets with tight Bollinger Bands (breakout prep) | "Coins ready for breakout" |
| `rating_filter` | Filter by Bollinger Band rating (-3 to +3) | "Strong buy signals (rating +2)" |
| `volume_breakout_scanner` | Detect unusual volume with price confirmation | "Volume breakout on NASDAQ" |

### 🕯️ Pattern Recognition  
| Tool | Description | Example Usage |
|------|-------------|---------------|
| `consecutive_candles_scan` | Find consecutive bullish/bearish patterns | "Scan for 3+ consecutive green candles" |
| `advanced_candle_pattern` | Multi-timeframe pattern analysis | "Complex pattern detection" |

### 🇪🇬 Egyptian Exchange (EGX)
| Tool | Description |
|------|-------------|
| `egx_market_overview` | Full market breadth, top movers, sector summary |
| `egx_sector_scan` | Analyze all 18 EGX sectors |
| `egx_index_analysis` | EGX30 / EGX70 / EGX100 index tracking |
| `egx_fibonacci_retracement` | Fib levels with golden pocket detection |

---

## 📝 Talk to Your AI Like a Portfolio Manager

**Run the Agent Debate:**
```text
"Run a multi-agent analysis on ETH with a 4h timeframe on KuCoin and tell me the final decision"
"Deploy the analyst team to check AAPL stock. I need the Technical, Sentiment, and Risk breakdown."
```

**Advanced Market Queries:**
```text
"Show me the top 10 crypto gainers on Binance in the last 15 minutes that have a low risk profile"
"Which Turkish stocks (BIST) are down more than 5% today?"
"Find crypto coins with a Bollinger Band squeeze (BBW < 0.05) ready to break out"
```

---

## 🏢 Supported Markets & Exchanges

### 💰 Cryptocurrency
Supports global leaders: **KuCoin** (Primary), **Binance**, **Bybit**, **Bitget**, **OKX**, **Coinbase**, **Gate.io**, **Huobi**, **Bitfinex**.

### 📊 Traditional Markets
Supports standard equities: **NASDAQ** (Tech), **NYSE** (Traditional), **BIST** (Turkey).

*Timeframes: `5m`, `15m`, `1h`, `4h`, `1D`, `1W`, `1M`*

---

## 🚨 Troubleshooting

**1. "No data found" errors / Empty Arrays:**
- Try different exchanges (KuCoin usually works best for Crypto).
- Standardise timeframes (15m, 1h, 1D).
- You may have hit TradingView's rate limits. Wait 5-10 minutes.

**2. Claude Desktop not detecting the server:**
- Restart Claude Desktop after adding configuration.
- Check that UV is installed: `uv --version`.
- Verify the configuration JSON syntax.

---

## 🤝 Contributing & Development

We welcome contributions from researchers, traders, and engineers to expand our analytical models!

```bash
git clone https://github.com/atilaahmettaner/tradingview-mcp.git
cd tradingview-mcp
uv sync

# Run with MCP Inspector for debugging
uv run mcp dev src/tradingview_mcp/server.py
```

- **Ideas:** Implementing more advanced Risk models, integrating alternative data (News APIs) for the Sentiment Analyst, backtesting capabilities.

---

## 💖 Support the Project

This project is **free and open source**, maintained in personal time. If it saves you hours of work or improves your trading workflow, please consider sponsoring:

<a href="https://github.com/sponsors/atilaahmettaner">
  <img src="https://img.shields.io/badge/Sponsor-%E2%9D%A4-pink?logo=github-sponsors&style=for-the-badge" alt="Sponsor atilaahmettaner" height="32"/>
</a>

**Why sponsor?**
- 🔄 Keeps new exchanges, indicators, and tools coming
- 🐛 Faster bug fixes and platform compatibility updates
- 📖 Better documentation and examples
- 🌍 Support for more global markets (BSE, TSX, ASX, etc.)

### ⭐ Free Ways to Help
- **Star the repo** — helps others discover it
- **Share on Twitter/X or Reddit** — tag us so we can RT
- **Open an Issue** — bugs and feature requests are always welcome
- **Submit a PR** — all skill levels welcome

---

## 📄 License & Disclaimer
This project is licensed under the **MIT License**.
* **Report bugs**: [GitHub Issues](https://github.com/atilaahmettaner/tradingview-mcp/issues)
* **Disclaimer**: This framework is designed for research and educational purposes. It is *not* intended as financial, investment, or trading advice. Always do your own research.

---
*Empowering intelligent trading decisions through multi-agent market analysis.*
