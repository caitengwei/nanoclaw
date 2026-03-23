---
name: macro-scan
description: Run a cross-market macro factor scan: summarize the unified external environment for BTC/crypto, US equities, HK equities, and A-shares into one macro context snapshot. Use when the user wants a big-picture macro read before making position decisions.
---

# /macro-scan — Cross-Market Macro Factor Scan

Generate a unified macro factor snapshot across multiple asset classes.

## Data to gather

Search for current readings on:

1. **USD strength**: DXY level and trend (rising/falling/range)
2. **US rates**: 10Y Treasury yield, recent direction, any Fed commentary
3. **Risk sentiment**: VIX level (fear/complacency), credit spreads if notable
4. **Crypto macro**: BTC dominance, crypto market cap trend, any regulatory news
5. **China macro**: PBOC action, RMB vs USD, any policy signal
6. **Global events**: any major geopolitical or macro events in the past 48h

## Output structure

```
*宏观扫描 — [日期]*

*美元与利率*
• DXY：[数值] [趋势↑↓→]
• 10Y收益率：[数值] [趋势]
• Fed信号：[最新表态 or 无新信号]

*风险偏好*
• VIX：[数值] — [恐慌/正常/贪婪]
• 整体风险偏好：[risk-on / risk-off / 中性]

*加密环境*
• BTC主导率：[百分比] [趋势]
• 市场情绪：[一句话]
• 监管/政策：[如有重大事件]

*中国宏观*
• 人民币：[USD/CNY] [趋势]
• 货币政策：[近期央行动向 or 无变化]
• A股驱动因素：[一句话]

*外部事件*
• [事件1]
• [事件2 or 无重大事件]

*综合判断*
对加密：[宏观环境描述，不做方向判断]
对美股：[宏观环境描述]
对港股/A股：[宏观环境描述]
```

## Rules

- Data only: all numbers must come from search results
- "综合判断" is environment description, not price prediction
- Label any inferred conclusions as 推断
- Save to `/workspace/group/macro-notes.md` if user says "保存" or "更新宏观"
