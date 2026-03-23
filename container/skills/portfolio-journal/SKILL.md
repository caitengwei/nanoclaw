---
name: portfolio-journal
description: Record a position review or trade debrief into the journal. Structures the user's input into a standardized entry covering entry rationale, outcome, execution deviation, and lesson. Use when the user wants to log a trade, record a post-mortem, or update their position record.
---

# /portfolio-journal — Position Review & Journal

Help the user record a structured position review or trade debrief.

## Input parsing

The user provides position details in natural language. Extract:
- **Asset**: ticker or name
- **Direction**: long / short / flat
- **Entry / exit**: price levels and dates (if provided)
- **P&L**: if mentioned
- **Narrative**: user's explanation of what happened

If any field is missing, ask a single clarifying question before writing the entry.

## Output structure

Write the journal entry in this format, then save it:

```
## [Asset] — [日期]

*方向*：[多/空/平]
*建仓价*：[价格] | *离场价*：[价格 or 持仓中]
*盈亏*：[金额 or 百分比 or 未知]

*入场逻辑*
[用户描述的建仓理由，1-3 句]

*执行偏差*
[实际执行与计划的差异，若无则写"与计划一致"]

*结果评估*
[事实性描述：什么发生了，对比入场假设]

*教训*
[一句话核心收获]
```

## Saving

Always save the entry to `/workspace/group/journal/YYYY-MM.md` (use current month).
- If the file exists, append to the end
- If the file does not exist, create it with a header `# Journal — YYYY-MM`

After saving, confirm: "已记录到 journal/[YYYY-MM].md"

## Rules

- Do not add interpretation beyond what the user provided
- Execution deviation is the most important field — prompt the user if they skip it
- Keep entries factual; mark any inferences as 推断
