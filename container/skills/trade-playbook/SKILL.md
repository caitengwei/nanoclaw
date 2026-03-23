---
name: trade-playbook
description: Generate a structured trading playbook for a single asset: key price levels, event catalysts, risk factors, and three scenario scripts (base/bull/bear). Use when the user provides a ticker or asset name and wants an analysis framework.
---

# /trade-playbook — Single Asset Trading Playbook

Generate a structured trading playbook for one asset. The user provides the ticker or name; you research and structure it.

## Input parsing

Extract from user message:
- **Asset**: ticker symbol or name (e.g., "BTC", "NVDA", "茅台")
- **Timeframe**: if mentioned (e.g., "本周", "Q2", default: "近期")
- **Context**: any position info the user adds (optional)

## Data to gather

Search for:
1. Current price and recent trend (3-5 day)
2. Key support and resistance levels (from recent charts commentary or analyst notes)
3. Upcoming events: earnings, macro events, product launches, regulatory dates
4. Recent sentiment: analyst ratings, major news

## Output structure

```
*交易剧本 — [Asset] [日期]*

*现价*：[价格] [涨跌% vs 前收]

*关键位*
• 阻力：[价位] — [说明]
• 支撑：[价位] — [说明]
• 关键突破位：[价位]

*催化因子*
• [日期/事件] — [影响评估]
• [日期/事件] — [影响评估]

*风险点*
• [风险1]
• [风险2]

*情景脚本*
基准（概率最高）：[描述价格区间和条件]
乐观：[描述上行条件和目标]
悲观：[描述下行条件和止损参考]

*注*：以上为结构化分析框架，非买卖建议。所有推断已标注，事实来源可查。
```

## Rules

- Clearly separate facts (sourced) from inferences (labeled "推断")
- Never state "建议买入/卖出" — frame as scenarios and levels
- If data is insufficient, note "数据不足，以下为框架性分析"
- Save to `/workspace/group/research/<ticker>.md` if user requests "保存"
