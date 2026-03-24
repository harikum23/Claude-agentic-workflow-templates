# Goal Definition Template

## How to Submit a Goal

Use this format for maximum efficiency. Claude will decompose, route, and execute automatically.

```markdown
## GOAL: [One-line description of what you want to achieve]

**Project(s):** [Indian Stock Analyzer | SMA | Both | New]
**Priority:** [P1-Critical | P2-High | P3-Normal]
**Deadline:** [Now | Today | This week | No rush]
**Dependencies/Blockers:** [e.g., "no Anthropic API key yet", "Breeze API token needed"]

### Desired Outputs:
- [ ] Output 1
- [ ] Output 2

### Context:
[Any additional background the agents need]
```

---

## Example Goals

### Example 1: Build a feature
```
GOAL: Add real-time Nifty 50 sector heatmap to Indian Stock Analyzer

Project: Indian Stock Analyzer
Priority: P2-High
Deadline: This week
Blockers: None

Desired Outputs:
- [ ] FastAPI endpoint: GET /api/sectors/heatmap
- [ ] Next.js component: SectorHeatmap
- [ ] PostgreSQL schema for sector weights

Context: Data from Breeze API. NSE sector classification.
```

### Example 2: Market + Risk analysis
```
GOAL: Full analysis of Reliance Industries for potential buy

Project: Indian Stock Analyzer watchlist
Priority: P1-Critical
Deadline: Today

Desired Outputs:
- [ ] Fundamental + F&O snapshot
- [ ] Risk assessment (VaR 1-day, max drawdown)
- [ ] Recommendation: buy/hold/sell with price targets

Context: ICICI Direct account, considering 2% portfolio allocation
```

### Example 3: Multi-project sprint
```
GOAL: Advance both projects this session

Projects: Both
Priority: P2-High
Deadline: Today

Indian Stock Analyzer:
- [ ] Activate Claude API prediction module (#[ACTIVATE] markers)

SMA (US):
- [ ] Add earnings calendar widget
- [ ] Add SPY risk metrics sidebar
```

---

## Goal → Workflow Mapping

| Goal Pattern | Workflow |
|---|---|
| "Build feature X" | WF-1 |
| "Add AI/ML to X" | WF-2 |
| "Analyze Indian stock Y" | WF-3 |
| "Trade plan for US stock Z" | WF-4 |
| "Work on both projects" | WF-5 |
| "Research X then build Y" | WF-6 |
| Custom | Decompose manually using AGENTS_REGISTRY.md routing tree |
