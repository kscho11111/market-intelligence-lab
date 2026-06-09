# market-intelligence-lab

## 1. Project Overview

`market-intelligence-lab` is a financial market data analysis platform designed for real-time market monitoring, short-term pattern detection, range-bound market analysis, and AI/statistical market research.

The project is not intended to be a simple cryptocurrency trading bot.
Its main goal is to build a portfolio-level financial IT project that can be extended to multiple market data sources, including:

* Cryptocurrency market data
* Domestic Korean stock market data
* U.S. stock market data
* External macro/financial data such as exchange rates, oil prices, interest rates, and indices

The initial implementation uses **Upbit WebSocket** because it provides 24-hour real-time market data and is suitable for testing real-time data collection, buffering, feature calculation, API serving, and dashboard visualization.

However, the main long-term target of this project is **stock market data analysis**, especially for domestic and U.S. equity markets.

---

## 2. Project Goals

The main goals of this project are:

1. Build a real-time financial market data pipeline.
2. Design a multi-source market data architecture.
3. Calculate short-term market features from real-time trade and quote data.
4. Visualize real-time market conditions through a React dashboard.
5. Research short-term pattern detection and range-bound market analysis.
6. Extend the platform to domestic and U.S. stock market data.
7. Prepare the project as a portfolio for financial IT and securities industry roles.

---

## 3. Core Research Topics

The main research topics are:

### 3.1 Pattern Analysis

Analyze large amounts of historical and real-time market data to determine whether the current market movement resembles an upward pattern, downward pattern, or neutral pattern.

Possible features include:

* Recent price movement
* Short-term return
* Moving average slope
* Volume change
* Volatility expansion
* Breakout movement
* Similar historical pattern search

---

### 3.2 Range-Bound Market Analysis

Determine whether the current market is moving within a range, approaching the upper or lower bound, or preparing for a breakout or breakdown.

Possible features include:

* Recent high price
* Recent low price
* Current price position
* Range ratio
* Trend slope
* Short-term volatility
* Breakout candidate signal
* Upper/lower bound proximity

Example indicators:

```text
range_ratio = (recent_high - recent_low) / current_price

price_position = (current_price - range_low) / (range_high - range_low)
```

---

### 3.3 Cross-Market Volatility Analysis

Analyze how external financial data affects stock volatility.

Possible external data sources include:

* USD/KRW exchange rate
* U.S. Dollar Index
* WTI crude oil
* Interest rates
* Treasury yields
* KOSPI / KOSDAQ
* S&P 500 / NASDAQ
* Sector ETFs

---

### 3.4 Weekend Crypto Volatility and Monday Stock Market Movement

Analyze whether cryptocurrency market volatility during the weekend has predictive power for Monday stock market return or volatility.

This topic is especially meaningful because U.S. and Korean stock markets are closed during weekends, while cryptocurrency markets remain open.

Possible research questions:

* Does weekend Bitcoin volatility affect Monday stock market volatility?
* Does weekend crypto return predict Monday gap direction?
* Are high-volatility crypto weekends related to Monday risk-off movements?

---

### 3.5 Premarket Data and Regular Session Volatility

Analyze whether U.S. premarket price movement has predictive power for regular session volatility.

Possible targets:

* Regular session opening volatility
* First 30-minute return
* Intraday high-low range
* Gap fill probability
* Closing return
* Volume expansion

This topic can be expanded into a research-oriented project:

> How much predictive power does off-session market information have for regular session price movement and volatility?

---

## 4. Phase Roadmap

After moving to the new project directory, phase numbering starts again from **Phase 1**.

The previous `AI-Stock_Trading` / `AI-Stock-Trading` projects are treated as prototype or legacy experiments.

---

### Phase 1: Multi-Source Real-Time Market Data Pipeline

Phase 1 focuses on building the real-time data pipeline and dashboard architecture.

Main goals:

* Collect real-time market data through WebSocket.
* Process trade and quote data.
* Calculate real-time market features.
* Serve processed data through FastAPI.
* Visualize market status through React.
* Prepare the system for multiple market data sources.

Initial data source:

* Upbit WebSocket

Planned additional data sources:

* Korea Investment & Securities Open API WebSocket for domestic stocks
* Alpaca WebSocket for U.S. stock data
* Optional future support for Polygon/Massive

Important note:

Upbit is used as the first real-time data source because it is available 24 hours a day and is useful for validating real-time data pipelines.
It is not the final main target of the project.

---

### Phase 2: Pattern and Range Detection Research

Phase 2 focuses on the core research logic.

Main topics:

* Short-term pattern analysis
* Range-bound market detection
* Breakout and breakdown candidate detection
* Historical pattern similarity search
* Feature engineering for market condition classification

Possible methods:

* Rule-based detection
* Statistical feature analysis
* KNN-based similar pattern search
* Dynamic Time Warping
* Machine learning classification
* Time-series modeling

---

### Phase 3: Cross-Market and Session-Based Analysis

Phase 3 focuses on wider market research.

Main topics:

* Dollar, oil, interest rate, and exchange rate impact on stock volatility
* Weekend cryptocurrency movement and Monday stock market behavior
* U.S. premarket movement and regular session volatility
* External market data integration
* Multi-asset feature analysis

---

### Phase 4: Backtesting, Risk Analysis, and Execution Design

Phase 4 focuses on validating strategy signals and designing trading system architecture.

Main topics:

* Signal performance analysis
* Backtesting
* Risk metrics
* Position sizing
* Paper trading structure
* Execution engine design

Actual order execution will be separated into another repository, such as:

```text
market-execution-engine
```

or

```text
signal-execution-engine
```

This repository will remain focused on market data analysis, AI signal generation, backtesting, and risk analysis.

---

## 5. Data Source Strategy

This project separates data sources by purpose.

### 5.1 Upbit

Purpose:

* Real-time pipeline validation
* 24-hour WebSocket testing
* Short-term pattern and range analysis demo

Use case:

* Real-time trade data
* Trade volume
* BID/ASK ratio
* Trade intensity
* Short-term volatility
* Range-bound candidate detection

---

### 5.2 Domestic Stock Data

Purpose:

* Main stock market data source for the Korean market
* Portfolio relevance for securities and financial IT roles

Candidate platform:

* Korea Investment & Securities Open API

Use case:

* Domestic stock real-time trade data
* Domestic stock quote data
* Stock market monitoring
* Pattern and range detection on Korean equities

---

### 5.3 U.S. Stock Data

Purpose:

* U.S. equity market research
* Premarket and regular session analysis
* Historical pattern research

Candidate platforms:

* Alpaca Market Data API
* Polygon/Massive
* yfinance for historical prototype research

Important note:

Free U.S. stock market data often has limitations.
For example, some platforms provide 15-minute delayed SIP data or exchange-limited real-time data.

Therefore, this project separates:

* Real-time algorithm validation
* Historical research
* Delayed data analysis
* Future paid real-time data integration

---

## 6. System Architecture

The project follows a backend-frontend-Docker structure.

```text
market-intelligence-lab/
│
├─ backend/
│  ├─ app/
│  │  ├─ main.py
│  │  ├─ core/
│  │  ├─ data_sources/
│  │  ├─ processing/
│  │  ├─ features/
│  │  ├─ strategies/
│  │  ├─ api/
│  │  └─ schemas/
│  │
│  ├─ tests/
│  ├─ requirements.txt
│  └─ Dockerfile
│
├─ frontend/
│  ├─ src/
│  │  ├─ api/
│  │  ├─ components/
│  │  ├─ pages/
│  │  ├─ hooks/
│  │  ├─ types/
│  │  ├─ App.tsx
│  │  └─ main.tsx
│  │
│  ├─ package.json
│  ├─ vite.config.ts
│  └─ Dockerfile
│
├─ data/
│  ├─ raw/
│  ├─ realtime/
│  ├─ processed/
│  └─ predictions/
│
├─ logs/
├─ docs/
├─ docker-compose.yml
├─ .env.example
├─ .gitignore
└─ README.md
```

---

## 7. Recommended Backend Structure

```text
backend/app/
├─ core/
│  ├─ config.py
│  └─ logger.py
│
├─ data_sources/
│  ├─ base.py
│  ├─ upbit/
│  │  └─ websocket_collector.py
│  ├─ kis/
│  │  └─ websocket_collector.py
│  ├─ alpaca/
│  │  └─ websocket_collector.py
│  └─ common/
│     └─ normalizer.py
│
├─ processing/
│  ├─ trade_buffer.py
│  ├─ tick_processor.py
│  ├─ candle_builder.py
│  └─ feature_pipeline.py
│
├─ features/
│  ├─ realtime_features.py
│  ├─ range_features.py
│  └─ pattern_features.py
│
├─ strategies/
│  └─ rule_based_signal.py
│
├─ api/
│  └─ routes.py
│
└─ schemas/
   ├─ market.py
   ├─ trade.py
   ├─ quote.py
   └─ candle.py
```

---

## 8. Core Data Models

The system should not depend on a specific exchange or broker.

Instead of using source-specific names such as `UpbitTrade`, the project uses common market data models.

Examples:

```text
MarketTrade
MarketQuote
MarketCandle
MarketSnapshot
```

This makes it possible to process different data sources through the same pipeline.

Example flow:

```text
Upbit trade data
→ normalizer
→ MarketTrade
→ feature pipeline
→ API
→ dashboard
```

```text
Domestic stock trade data
→ normalizer
→ MarketTrade
→ feature pipeline
→ API
→ dashboard
```

```text
U.S. stock candle data
→ normalizer
→ MarketCandle
→ research module
→ analysis result
```

---

## 9. Real-Time Features

The following real-time features are planned:

### Price Features

* Current price
* Recent high
* Recent low
* Short-term return
* Moving average
* Price position in recent range

### Volume Features

* Recent trade volume
* Trade count
* Trade amount
* Volume acceleration

### Trade Direction Features

* BID trade count
* ASK trade count
* BID trade amount
* ASK trade amount
* BID/ASK ratio
* Trade intensity

Example:

```text
trade_intensity = bid_trade_amount / ask_trade_amount * 100
```

Interpretation:

```text
Around 100: balanced
Above 100: buy-side dominance
Below 100: sell-side dominance
```

### Volatility Features

* Short-term volatility
* Price range
* Range ratio
* Sudden volatility expansion

### Range-Bound Features

* Recent high
* Recent low
* Range width
* Current price position
* Upper bound proximity
* Lower bound proximity
* Breakout candidate signal
* Breakdown candidate signal

---

## 10. Technology Stack

### Backend

* Python
* FastAPI
* WebSocket client
* pandas
* numpy
* pydantic
* python-dotenv
* loguru
* uvicorn

### Frontend

* React
* TypeScript
* Vite
* Chart library such as Recharts, ECharts, or lightweight-charts

### Infrastructure

* Docker
* Docker Compose
* GitHub
* Virtual environment

---

## 11. Installation

### 11.1 Clone Repository

```bash
git clone git@github.com:<your-github-id>/market-intelligence-lab.git
cd market-intelligence-lab
```

### 11.2 Create Python Virtual Environment

```bash
python -m venv venv
source venv/bin/activate
```

### 11.3 Install Backend Dependencies

```bash
pip install pandas numpy websocket-client fastapi "uvicorn[standard]" python-dotenv pydantic loguru
pip freeze > backend/requirements.txt
```

### 11.4 Install Frontend Dependencies

```bash
cd frontend
npm install
```

---

## 12. Running the Project

### 12.1 Run Backend

```bash
cd backend
uvicorn app.main:app --reload
```

### 12.2 Run Frontend

```bash
cd frontend
npm run dev
```

### 12.3 Run with Docker Compose

```bash
docker compose up --build
```

---

## 13. Environment Variables

Create a `.env` file based on `.env.example`.

Example:

```text
APP_ENV=development
LOG_LEVEL=INFO

UPBIT_MARKET=KRW-BTC

KIS_APP_KEY=
KIS_APP_SECRET=
KIS_ACCOUNT_NO=

ALPACA_API_KEY=
ALPACA_SECRET_KEY=
```

Do not commit actual API keys to GitHub.

---

## 14. GitHub Policy

The following files and directories should not be committed:

```text
venv/
.env
__pycache__/
*.pyc
node_modules/
data/raw/
data/realtime/
data/processed/
logs/
```

Example `.gitignore`:

```gitignore
venv/
.env

__pycache__/
*.pyc

node_modules/
dist/

data/raw/*
data/realtime/*
data/processed/*
data/predictions/*
!data/raw/.gitkeep
!data/realtime/.gitkeep
!data/processed/.gitkeep
!data/predictions/.gitkeep

logs/*
!logs/.gitkeep
```

---

## 15. Portfolio Direction

This project is designed as a financial IT portfolio project.

Key portfolio points:

* Real-time market data collection
* WebSocket-based data pipeline
* Multi-source market data architecture
* Financial feature engineering
* FastAPI backend design
* React dashboard implementation
* Docker-based service structure
* Pattern and range-bound market analysis research
* Expandability to domestic and U.S. stock market data

The project emphasizes financial data engineering and market analysis rather than simple automated trading.

---

## 16. Current Status

Current progress:

* Project direction defined
* New project name selected: `market-intelligence-lab`
* Phase numbering restarted from Phase 1
* Upbit WebSocket test completed
* KRW-BTC real-time trade data successfully received
* Initial real-time feature ideas defined
* Multi-source data strategy defined
* Main research topics selected

---

## 17. Next Steps

Immediate next steps:

1. Create the project directory structure.
2. Initialize Git and connect to GitHub.
3. Implement Upbit WebSocket collector.
4. Define common market data schemas.
5. Implement trade buffer.
6. Implement real-time feature calculator.
7. Build FastAPI endpoints.
8. Create React dashboard layout.
9. Add domestic stock WebSocket collector.
10. Prepare Phase 2 research modules for pattern and range analysis.

---

## 18. Disclaimer

This project is for research, education, and portfolio purposes only.

It does not provide investment advice.
It does not guarantee trading performance.
Actual order execution and automated trading logic will be separated into another repository if needed in the future.

