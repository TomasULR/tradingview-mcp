# Changelog

All notable changes to this project will be documented in this file.

## [0.5.0] - 2026-03-29

### Added
- **Real-Time Market Sentiment (Agent-Reach Integration)**: Integrated Reddit JSON API to track symbol sentiment across finance communities (`market_sentiment`).
- **Live Financial News RSS**: Added `fetch_news` service via `feedparser` to track real-time headlines across Reuters, CoinDesk, and CoinTelegraph (`financial_news`).
- **Combined Analysis Power Tool**: The new `combined_analysis` tool merges TradingView technicals, Reddit sentiment, and live news into a single confluence analysis (signals agree/conflict, confidence score, full recommendation).
- Added `feedparser` dependency to `pyproject.toml`.

## [0.4.0] - 2026-03-29

### Added
- **EGX (Egyptian Exchange) Full Support**: Complete trading infrastructure for the Egyptian Stock Market.
  - `egx_market_overview`: Top gainers, losers, most active stocks, and market breadth stats (advancing/declining/unchanged).
  - `egx_sector_scan`: Scan across 18 EGX sectors (banks, real_estate, healthcare_and_pharma, technology, etc.).
  - `egx_stock_screener`: Cross-sectional ranking with auto trade plan generation.
  - `egx_trade_plan`: Single-stock detailed trade setup (entry, stop-loss, targets, R:R).
  - `egx_fibonacci_retracement`: Fibonacci retracement + extension levels with golden pocket detection.
  - 6 EGX indices: EGX30, EGX70, EGX100, SHARIAH33, EGX35LV, TAMAYUZ (200+ symbols).
- **3-Layer Stock Decision Engine**:
  - Layer A: 100-point stock ranking model (trend, momentum, risk, fundamentals).
  - Layer B: Trade setup engine (entry points, stop-loss, targets, support/resistance, R:R).
  - Layer C: Trade quality scoring (structure, risk/reward, volume, liquidity).
- **Liquidity-Aware Scoring**: Hard grade caps prevent illiquid stocks from ever receiving "Strong" or "Elite" grades.
- **23 Technical Indicators**: Expanded from 5 → 23: CCI, Williams %R, Awesome Oscillator, Momentum, Parabolic SAR, Ichimoku, Stoch RSI, ADX +DI/-DI, Hull MA, VWMA, Ultimate Oscillator, full EMA/SMA suites.
- **Multi-Timeframe Alignment**: Weekly→Daily→4H→1H→15m bias analysis with timeframe-specific advice.

### Fixed
- Hardcoded `"crypto"` market type in `_fetch_multi_changes`, `_fetch_multi_timeframe_patterns`, and `screener_provider` — now dynamically resolved per exchange (egypt, turkey, america, etc.).
- `volume_confirmation_analysis` was appending `"USDT"` to stock symbols — now exchange-aware with proper `EGX:SYMBOL` formatting.

### Changed
- MCP server name updated to "TradingView Multi-Market Screener".
- All tool descriptions updated to reference both crypto and stock exchanges.
- Added `is_stock_exchange()`, `get_market_type()`, and `STOCK_EXCHANGES` helpers to `validators.py`.

## [0.3.0] - 2026-03-24

### Added
- **Docker Support**: Official Dockerfile and docker-compose.yml for easy 1-click self-hosting.
- **PyPI Release**: Added proper metadata and structuring for PyPI distribution (`pip install tradingview-mcp`).

## [0.2.0] - 2026-03-24

### Added
- **Multi-Agent Trading Framework**: Introduced `multi_agent_analysis` MCP tool.
  - **Technical Analyst Agent**: Analyzes RSI, MACD, and Bollinger Bands.
  - **Sentiment Analyst Agent**: Calculates momentum and produces a sentiment score.
  - **Risk Manager Agent**: Evaluates volatility (BBW) and mean reversion risk.
- **Debate System**: Agents combine their scores to provide a single, logical Framework Decision (Strong Buy, Buy, Hold, Sell, Strong Sell) with confidence levels.

### Changed
- Repositioned the project from a "screener" to an "AI Trading Intelligence Framework".
- Updated `README.md` to reflect the new architecture.

## [0.1.0] - Initial Release
- Basic MCP Server setup.
- Bollinger Band squeeze detection.
- Consecutive candle pattern detection.
- Real-time market screening (gainers, losers).
