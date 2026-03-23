---
name: repo-watch
description: Check tracked open-source repositories for recent activity: new releases, significant PRs merged, notable issues opened. Reads target repos from /workspace/group/watch-list.md. Use when the user asks for a repo update, weekly tech digest, or "what's new in SGLang/vLLM".
---

# /repo-watch — Open Source Repo Activity Tracker

Check recent activity for tracked repositories. Target repos are stored in `/workspace/group/watch-list.md`.

## Step 1: Load watch list

Read the watch list:
```bash
cat /workspace/group/watch-list.md 2>/dev/null || echo "No watch-list.md found"
```

If the file doesn't exist, ask the user which repos to track and create the file:
```
# Watch List

## Repos
- vllm-project/vllm
- sgl-project/sglang
- NVIDIA/TensorRT-LLM
```

The user can also override repos directly in their message (e.g., "看一下 sglang 最近").

## Step 2: Fetch recent activity

For each repo in the watch list, use WebFetch or WebSearch:

**Releases** (last 14 days):
```
WebSearch: "site:github.com/<owner>/<repo> release"
or WebFetch: https://api.github.com/repos/<owner>/<repo>/releases?per_page=3
```

**Merged PRs** (significant ones):
```
WebFetch: https://api.github.com/repos/<owner>/<repo>/pulls?state=closed&per_page=10&sort=updated
```
Filter for PRs merged in the last 7 days. Focus on PRs with large diffs or important labels (perf, feature, breaking).

**Issues** (newly opened, high engagement):
```
WebFetch: https://api.github.com/repos/<owner>/<repo>/issues?state=open&per_page=10&sort=created
```

## Step 3: Output structure

For each repo with activity:

```
*[repo名] — 近期动态*

*Release*
• [版本号] [日期] — [核心变化 1 句话]

*重要 PR*（已合并）
• #[编号] [标题] — [影响评估]
• #[编号] [标题] — [影响评估]

*值得关注的 Issue*
• #[编号] [标题] — [问题类型: 性能/bug/feature]
```

If no significant activity: "本周无重大变化"

## Step 4: Inference labeling

- State PR content as **事实** if you read the PR description/diff directly
- Mark your assessment of impact as **推断**
- If you cannot verify a detail, write "需确认"

## Step 5: Save

After the report, ask: "是否保存到 competitive/ 目录？"
If yes, save to `/workspace/group/competitive/<repo-name>-YYYY-MM-DD.md`
