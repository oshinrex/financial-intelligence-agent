# financial-intelligence-agent
Agentic AI system that autonomously examines public equities and crypto assets by dynamically retrieving and reasoning over multiple financial sources, including SEC filings, earnings reports, market news, macro indicators, and congressional trading disclosures.

## Motivation
Financial research involves retrieving information across earnings reports, SEC filings, news, and macro data. This project utilizes an AI agent to replicate parts of that process by dynamically retrieving, reasoning over, and structuring financial information into comprehensive analysis reports.

## What It Does
- **Input:** stock ticker or crypto asset
- Agent dynamically determines what financial data is relevant
- **Retrieves:**
    - SEC filings and earnings data (for equities)
    - Crypto market data and news (for crypto assets)
    - Market news and sentiment signals
    - Congressional trading disclosures (when applicable/relevant)
- Using relevant financial data, uses iterative reasoning to form and test hypotheses about market movements
- **Output:** financial research report in Markdown, structured sections with explanations and supporting evidence

## System Architecture
ReAct-style agent architecture (Reason + Act loop) orchestrated via LangGraph

**ReAct Agent Loop:**
- **Thought:** agent interprets user query and determines what data is needed
- **Action:** agent selects and calls appropriate tools (news, SEC filings, etc.)
- **Observation:** agent processes returned data from tools
- **Iteration:** loop continues until sufficient evidence is gathered
- **Final Answer:** agent synthesizes structured financial research report

## Tools and Data Sources
- SEC EDGAR API (financial filings)
- Market data API (price, volume, sector movement)
- News API / web search
- Congressional trading disclosures (STOCK Act datasets / public filings)
- Crypto market data APIs (for BTC, ETH, etc.)

## Key Features
- Agentic planning and dynamic tool selection
- Multi-step financial reasoning and hypothesis testing
- Supports stock and crypto assets
- Includes congressional trading activity when relevant
- Structured, evidence-based report generation in Markdown

## Output Format
The agent produces a Markdown report, including the following data: 
- **Executive Summary** - one-paragraph synthesis of findings
- **Price Action** — what the asset did and over observed/relevant timeframe
- **Primary Driver(s)** — main factors identified with supporting evidence
- **Market Context** — broader sector/macro conditions
- **Congressional Activity** — any relevant legislator positioning (for equities only)
- **Sentiment Overview** — news tone and volume signals
- **Confidence Score** — '0.0–1.0' representing evidence strength and source quality
- **Sources** — links and citations for retrieved data

## Example
**Input:**
```
Why did NVDA drop today?
```

**Output:**
```markdown
## NVDA — Research Report
**Date:** 2025-06-04 | **Confidence:** 0.74

### Executive Summary
NVDA declined ~3.2% today in a move that appears macro and sector-driven
rather than company-specific. No material negative news was detected at
the individual stock level.

### Primary Driver
Sector-wide semiconductor selloff driven by macro tightening concerns
following stronger-than-expected jobs data, which raised rate-hold
expectations. SOX index down 2.4%.

### Secondary Factor
Mixed sentiment in the AI chip news cycle; no major catalyst but reduced
positive coverage volume versus prior week.

### Market Context
NASDAQ down 1.8% overall. Broad risk-off tone across growth equities.

### Congressional Activity
No significant new positioning detected in recent STOCK Act filings.

### Confidence: 0.74
Evidence is consistent across sources; minor uncertainty due to limited
intraday filing data.
```

## Tech Stack
- Python
- LangGraph (agent orchestration)
- OpenAI API
- FastAPI (backend)
- Financial + news APIs
- SEC EDGAR API

## How to Run
1. Clone repository
2. Install dependencies: `pip install -r requirements.txt`
3. Add API keys to `.env`
4. Run FastAPI server: `uvicorn app.main:app --reload`
5. Query the agent with a ticker or question

## Future Improvements
- Persistent memory with vector database (pgvector/Pinecone)
- Evaluation framework for answer grounding
- Frontend dashboard for interactive exploration
- Portfolio-level analysis across multiple assets
- Real-time market monitoring and alerts
- PDF export of generated reports

*For research and educational purposes only. Not for financial advice.*