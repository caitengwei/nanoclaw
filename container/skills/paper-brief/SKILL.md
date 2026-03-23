---
name: paper-brief
description: Fetch and summarize a research paper or technical blog post. Produces a structured brief: abstract, key contributions, technical details, and relevance to LLM inference optimization. Use when the user shares a paper URL, arXiv ID, or blog link and wants a structured digest.
---

# /paper-brief — Paper & Blog Digest

Fetch and summarize a research paper or technical blog post.

## Step 1: Identify source

From the user message, extract:
- **URL**: direct link to paper or blog
- **arXiv ID**: e.g., "2501.12345" → fetch `https://arxiv.org/abs/2501.12345`
- **Title + venue**: search if only title is given

If no URL provided, search:
```
WebSearch: "<title> arxiv" or "<title> site:arxiv.org"
```

## Step 2: Fetch content

For arXiv papers:
```
WebFetch: https://arxiv.org/abs/<id>  # for abstract and metadata
WebFetch: https://arxiv.org/html/<id>  # for full text if available
```

For blog posts:
```
agent-browser open <url>
agent-browser snapshot
```

## Step 3: Output structure

```
*论文摘要 — [标题]*

*来源*：[arxiv/blog/venue] [日期]
*作者*：[第一作者 et al.]

*核心贡献*（2-3 条）
• [贡献1]
• [贡献2]

*技术方法*
[3-5 句话描述方法，使用领域术语，无需解释基础概念]

*实验结果*
• [关键 benchmark 结果]
• [对比基线]

*与 LLM 推理的关联*
• [如何影响推理效率、内存、延迟、吞吐]
• [与 vLLM/SGLang/TRT-LLM 的关联（如有）]
• [是否与量化/KV cache/speculative decoding 等方向相关]

*局限性*
• [作者指出的局限 or 推断的局限（标注）]

*跟进建议*
• [是否值得深入阅读，或等待后续工作]
```

## Assumed knowledge

Do not explain: Transformer, Attention, KV Cache, PagedAttention, INT4/INT8/FP8, AWQ, GPTQ, Speculative Decoding, Chunked Prefill, Tensor/Pipeline/Expert Parallelism, MoE.

## Rules

- Technical method section: use domain vocabulary, no hand-holding
- "与 LLM 推理的关联" is the most important section — spend the most effort here
- Distinguish facts (from paper) from inferences (labeled 推断)
- Save to `/workspace/group/papers/<first-author-keyword>-<year>.md` if user says "保存"
