![](asset/logo.png)

# Polymarket Copy Trading Bot

> Automated copy trading bot for Polymarket that mirrors trades from top performers with intelligent position sizing and real-time execution. Version 2.0 employs the fastest transaction detection method, enabling near-instantaneous trade replication with lower latency and reduced API load. The copy trading feature in Version 2.0 delivers outstanding performance and resolves all issues previously encountered with “Cloudflare” and VPNs in older versions.


## Overview

The Polymarket Copy Trading Bot automatically replicates trades from successful Polymarket traders to your wallet. It monitors trader activity 24/7, calculates proportional position sizes based on your capital, and executes matching orders in real-time.

### How It Works

![](asset/howitworks.png)

1. **Select Traders** - Choose top performers from [Polymarket leaderboard](https://polymarket.com/leaderboard) or [Predictfolio](https://predictfolio.com)
2. **Monitor Activity** - Bot continuously watches for new positions opened by selected traders using Polymarket Data API
3. **Calculate Size** - Automatically scales trades based on your balance vs. trader's balance
4. **Execute Orders** - Places matching orders on Polymarket using your wallet
5. **Track Performance** - Maintains complete trade history in MongoDB

## Quick Start

### Prerequisites

- [Node.js](https://nodejs.org/en/download) v18+
- MongoDB database ([MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register) free tier works)
- Polygon wallet with USDC and POL/MATIC for gas
- RPC endpoint ([Infura](https://infura.io) or [Alchemy](https://www.alchemy.com) free tier)

### Installation

#### Clone repository
```bash
git clone https://github.com/Adraylis/polymarket-copy-trading-bot

cd polymarket-copy-trading-bot
```

#### Install dependencies
```bash
npm install
```

##### Configure Environment
```bash
# Copy the example config
cp .env.example .env
```

Edit `.env` with your settings:

```bash
# Traders to copy (find addresses on Polymarket leaderboard)
USER_ADDRESSES = '0x6a72f61820b26b1fe4d956e17b6dc2a1ea3033ee'

# Your trading wallet (the wallet that will execute trades)
PROXY_WALLET = 'your_polygon_wallet_address'
PRIVATE_KEY = 'your_private_key_without_0x_prefix'

# MongoDB (get free database at mongodb.com/cloud/atlas)
# The default link in your .env file is currently functional, but it is recommended that you replace it with your own.
MONGO_URI = 'mongodb+srv://username:password@cluster.mongodb.net/database'

# Polygon RPC (get free key at infura.io or alchemy.com)
# The default link in your .env file is currently functional, but it is recommended that you replace it with your own.
RPC_URL = 'https://polygon-mainnet.infura.io/v3/YOUR_PROJECT_ID'

# Don't change these
CLOB_HTTP_URL = 'https://clob.polymarket.com/'
CLOB_WS_URL = 'wss://ws-subscriptions-clob.polymarket.com/ws'
USDC_CONTRACT_ADDRESS = '0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174'
```

#### Build and start
```bash
npm run build
npm run health-check  # Verify configuration
npm start             # Start trading
```

**📖 For detailed setup instructions, see [Getting Started Guide](./docs/GETTING_STARTED.md)**

## Features

- **Multi-Trader Support** - Track and copy trades from multiple traders simultaneously
- **Smart Position Sizing** - Automatically adjusts trade sizes based on your capital
- **Tiered Multipliers** - Apply different multipliers based on trade size
- **Position Tracking** - Accurately tracks purchases and sells even after balance changes
- **Trade Aggregation** - Combines multiple small trades into larger executable orders
- **Real-time Execution** - Monitors trades every second and executes instantly
- **MongoDB Integration** - Persistent storage of all trades and positions
- **Price Protection** - Built-in slippage checks to avoid unfavorable fills

### Monitoring Method

The bot currently uses the **Polymarket Data API** to monitor trader activity and detect new positions. The monitoring system polls trader positions at configurable intervals (default: 1 second) to ensure timely trade detection and execution.

## Configuration

### Essential Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `USER_ADDRESSES` | Traders to copy (comma-separated) | `'0xABC..., 0xDEF...'` |
| `PROXY_WALLET` | Your Polygon wallet address | `'0x123...'` |
| `PRIVATE_KEY` | Wallet private key (no 0x prefix) | `'abc123...'` |
| `MONGO_URI` | MongoDB connection string | `'mongodb+srv://...'` |
| `RPC_URL` | Polygon RPC endpoint | `'https://polygon...'` |
| `TRADE_MULTIPLIER` | Position size multiplier (default: 1.0) | `2.0` |
| `FETCH_INTERVAL` | Check interval in seconds (default: 1) | `1` |

### Finding Traders

1. Visit [Polymarket Leaderboard](https://polymarket.com/leaderboard)
2. Look for traders with positive P&L, win rate >55%, and active trading history
3. Verify detailed stats on [Predictfolio](https://predictfolio.com)
4. Add wallet addresses to `USER_ADDRESSES`

**📖 For complete configuration guide, see [Quick Start](./docs/QUICK_START.md)**

## Documentation

### Getting Started
- **[🚀 Getting Started Guide](./docs/GETTING_STARTED.md)** - Complete beginner's guide
- **[⚡ Quick Start](./docs/QUICK_START.md)** - Fast setup for experienced users

## License

MIT License - See [LICENSE](LICENSE.md) file for details.


**Disclaimer:** This software is for educational purposes only. Trading involves risk of loss. The developers are not responsible for any financial losses incurred while using this bot.


**Support:** For questions or issues, contact via Discord: `adraylis`