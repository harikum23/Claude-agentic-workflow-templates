# Agent Registry — Full Routing Matrix

## How to Use This File
For any task, find the best-match agent by domain. When a task spans multiple rows, split it and assign each part to its owner agent.

---

## 1. expert-engineer
**Subagent type:** `expert-engineer`
**Invoke:** `/expert-engineer`

**Route here when:**
- Writing or reviewing production code (Python, FastAPI, Next.js, React, Java, Spring Boot)
- System design, API design, database schema
- Docker/infra configuration
- Debugging build errors, runtime errors
- Code refactoring, architecture decisions
- Integration between services

**Do NOT route here for:**
- Pure ML model work → ai-engineer
- Pure market analysis → market-researcher / india-market-researcher
- Data pipeline analysis → expert-data-engineer

---

## 2. ai-engineer
**Subagent type:** `ai-engineer`
**Invoke:** `/ai-engineer`

**Route here when:**
- Building ML/DL models (training, evaluation, deployment)
- NLP pipelines, embeddings, RAG systems
- Feature engineering for prediction models
- MLOps: model versioning, serving, monitoring
- Activating `# [ACTIVATE]` Claude API markers in Indian Stock Analyzer
- Designing AI-powered prediction modules

**Do NOT route here for:**
- Raw data analysis without model → expert-data-engineer
- Frontend integration of AI output → expert-engineer

---

## 3. expert-data-engineer
**Subagent type:** `expert-data-engineer`
**Invoke:** `/expert-data-engineer`

**Route here when:**
- EDA on stock/financial data
- Statistical analysis, hypothesis testing
- SQL query optimization (TimescaleDB, PostgreSQL)
- Building dashboards or BI views
- Data pipeline design (ingestion, transformation, storage)
- Feature analysis and selection (pre-ML)
- Backtesting data preparation

**Do NOT route here for:**
- Model training → ai-engineer
- API/backend code → expert-engineer

---

## 4. india-market-researcher
**Subagent type:** `india-market-researcher`
**Invoke:** `/india-market-researcher`

**Route here when:**
- NSE/BSE equity research (fundamentals, technicals)
- SEBI/RBI policy impact analysis
- Nifty/Sensex macro outlook
- F&O strategy design for Indian markets
- Sector rotation in India (IT, Banking, Pharma, Auto, FMCG)
- Breeze API data interpretation
- Identifying stocks for Indian Stock Analyzer watchlist

---

## 5. market-researcher
**Subagent type:** `market-researcher`
**Invoke:** `/market-researcher`

**Route here when:**
- US equity research (NYSE/NASDAQ)
- Fed policy, macro economic analysis (US)
- Technical analysis, chart patterns
- Earnings analysis, sector rotation (US)
- Stock screening for SMA project
- Quantitative signals for US prediction models

---

## 6. market-risk-analyzer
**Subagent type:** `market-risk-analyzer`
**Invoke:** `/market-risk-analyzer`

**Route here when:**
- VaR/CVaR calculation for any portfolio
- Stress testing, drawdown analysis
- Hedging strategy design
- India VIX interpretation, FII flow risk
- US yield curve risk, options Greeks risk
- Risk-adjusted return analysis
- Promoter pledge risk (Indian stocks)

**Best used in parallel with:** india-market-researcher OR market-researcher

---

## 7. us-expert-trader
**Subagent type:** `us-expert-trader`
**Invoke:** `/us-expert-trader`

**Route here when:**
- Trade execution strategy and sizing
- Options strategies: spreads, earnings plays, IV analysis
- Order flow, VWAP/tape reading
- Intraday or swing trading plan
- Algorithmic execution design (TWAP/VWAP/IS/POV)
- Building systematic trading logic for SMA project

---

## Routing Decision Tree

```
Task received
├── Is it code/engineering? → expert-engineer
│   └── Does it involve ML/AI models? → ai-engineer (+ expert-engineer for integration)
│   └── Does it involve data analysis first? → expert-data-engineer → ai-engineer → expert-engineer
├── Is it market analysis?
│   ├── Indian market? → india-market-researcher (+ market-risk-analyzer in parallel)
│   └── US market? → market-researcher (+ market-risk-analyzer in parallel)
│       └── Need trade plan? → us-expert-trader (after research)
└── Multi-domain? → Decompose → assign each sub-task → run in parallel
```

---

## Agent Compatibility Matrix (for parallel execution)

| | expert-engineer | ai-engineer | expert-data-engineer | india-market-researcher | market-researcher | market-risk-analyzer | us-expert-trader |
|---|---|---|---|---|---|---|---|
| **expert-engineer** | — | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel |
| **ai-engineer** | sequential* | — | sequential* | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel |
| **expert-data-engineer** | sequential* | sequential* | — | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel |
| **india-market-researcher** | ✓ parallel | ✓ parallel | ✓ parallel | — | ✓ parallel | ✓ parallel | N/A |
| **market-researcher** | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel | — | ✓ parallel | sequential* |
| **market-risk-analyzer** | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel | ✓ parallel | — | sequential* |

*sequential = data-engineer feeds ai-engineer feeds expert-engineer (pipeline); market-researcher feeds us-expert-trader
