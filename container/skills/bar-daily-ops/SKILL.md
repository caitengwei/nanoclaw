---
name: bar-daily-ops
description: Generate a structured weekly bar operations report covering revenue, SKU performance, customer spend, time-period breakdown, and anomaly flags. Data comes from 银豹 (POS system web interface) via agent-browser, and optionally from 金山云文档. Use when the user asks for a weekly report, operations summary, or business review.
---

# /bar-daily-ops — Bar Weekly Operations Report

Generate a structured weekly operations report. Use agent-browser to fetch data from 银豹 POS web interface.

## Step 1: Data collection

### From 银豹 POS (primary source)

Open the POS dashboard:
```bash
agent-browser open https://pos.yinbao.com  # adjust URL if different
```

Navigate to the reports section and extract:
- **Revenue**: total sales for the reporting period
- **SKU breakdown**: top 10 selling items by quantity and revenue
- **Customer spend**: average transaction value
- **Time-period breakdown**: revenue by time slot (happy hour, evening, late night)
- **Payment methods**: cash vs card vs digital

If login is required, check `/workspace/group/auth.json` for saved session:
```bash
agent-browser state load /workspace/group/auth.json
```

If no saved session, pause and ask the user to log in manually, then save state:
```bash
agent-browser state save /workspace/group/auth.json
```

### From 金山云文档 (if user provides link)

If user includes a 金山云文档 link:
```bash
agent-browser open <provided_url>
agent-browser snapshot -i
# extract relevant table data
```

## Step 2: Report structure

Format the report as:

```
*经营周报 — [开始日期] 至 [结束日期]*

*营收*
• 总营收：¥[金额]
• 环比：[+/-X%] vs 上周
• 目标完成率：[X%]（如有目标）

*SKU 表现*
• Top 3 品类：[品类] ¥[营收] / [数量]
• Top 3 单品：[商品名] x[数量]
• 滞销项：[商品名]（如有）

*客单价*
• 平均客单：¥[金额]
• 环比：[+/-X%]

*时段分布*
• 最佳时段：[时间段] ¥[营收]（占比 X%）
• 最差时段：[时间段] ¥[营收]

*异常项*
• [如退款异常、高折扣、库存不足等，否则写"无异常"]

*建议关注*
• [1-2 条基于数据的运营观察，不做主观评价]
```

## Rules

- Numbers must come directly from the POS system — do not estimate
- If data is unavailable for a field, write "数据暂缺"
- "建议关注" is data-driven observation only, not marketing advice
- Save report to `/workspace/group/ops/YYYY-MM-DD.md` (report end date)
- After saving, confirm: "周报已保存到 ops/[filename].md"
