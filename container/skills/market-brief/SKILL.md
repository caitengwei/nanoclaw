---
name: market-brief
description: Generate a structured daily or weekly market summary covering BTC/ETH, US equities (SPX/NDX/TSLA/NVDA), HSI, A-shares (CSI300/SH), and macro context. Use when the user asks for a market update, morning brief, or weekly recap.
---

# /market-brief — Market Summary

Generate a structured market summary. Adapt scope based on user request (daily vs. weekly).

## Data to gather

Use WebSearch or WebFetch to collect:

1. **Crypto**: BTC and ETH price, 24h change, key level context
2. **US equities**: SPX, NDX, and 2-3 notable movers (TSLA, NVDA, etc.)
3. **HK/China**: HSI, CSI300 or Shanghai Composite
4. **Macro context**: DXY trend, 10Y yield direction, any major macro event

For each, search: `"<asset> price today"` or `"<asset> market recap"`.

## Output structure

Format the response as:

```
*市场摘要 — [日期]*

*宏观环境*
• [DXY/利率/地缘 1 句话]

*加密*
• BTC [价格] [涨跌%] — [关键位说明]
• ETH [价格] [涨跌%]

*美股*
• SPX [点位] [涨跌%]
• NDX [点位] [涨跌%]
• [个股] [涨跌%] — [简短原因]

*港股/A股*
• HSI [点位] [涨跌%]
• CSI300 [点位] [涨跌%]

*本周/今日关键催化*
• [事件1]
• [事件2]

*需关注*
• [风险点或待跟踪]
```

## Rules

- Facts only: prices and % changes must be verifiable from search results
- Mark uncertain items: if data is unavailable, write "数据暂缺"
- Keep the whole summary under 300 characters per section
- Do not interpret or predict — describe what happened, not what will happen
- Save a copy to `/workspace/group/macro-notes.md` if user requests "保存" or "记录"
