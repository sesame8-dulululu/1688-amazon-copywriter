---
name: "1688-amazon-copywriter"
description: "Use when the user provides a 1688 product link and wants Amazon listing copy generated from that page. Open the product page with Chrome, extract product用途, 目标人群, 使用场景, 长宽高, 重量, and 包装重量, then output four sections: 抓取结果, 标题, 五点描述, and 后台搜索词. If dimensions or weights are not available in page text, inspect detail images for the same information. If still unavailable, mark the field as 未提供. Trigger on requests like 1688链接生成亚马逊文案, 用1688商品链接写Amazon标题五点, 调用1688文案工具, or similar Chinese phrasing."
---

# 1688 Amazon Copywriter

Use this skill for a single 1688 product link at a time. Prioritize output quality over batch throughput.

## Goal

Turn one 1688 product link into a compact Amazon listing draft with fixed output sections:

1. `抓取结果`
2. `标题`
3. `五点描述`
4. `后台搜索词`

## Required workflow

1. Use Chrome to open the 1688 product page.
2. Extract these fields from visible page content first:
   - `产品用途`
   - `目标人群`
   - `使用场景`
   - `长`
   - `宽`
   - `高`
   - `重量`
   - `包装重量`
3. Before checking images, inspect page sections that commonly hold logistics data, such as `包装信息`, `包装参数`, `商品参数`, `产品参数`, shipping panels, and similar packaging or attribute blocks.
4. If `长/宽/高/重量/包装重量` are still not clearly available in page text, continue by inspecting product detail images, parameter images, packaging images, and long description images for the missing values.
5. If a field still cannot be confirmed, return `未提供` for that field. Do not invent dimensions or weights.
6. Generate Amazon copy from the extracted用途, 人群, and 场景 information.

## Extraction rules

- Prefer explicit facts from the page over inference.
- Keep `产品用途`, `目标人群`, and `使用场景` practical and buyer-oriented. If the page implies them indirectly, summarize them in plain Chinese.
- Preserve units when present, such as `cm`, `mm`, `kg`, or `g`.
- If multiple variants appear, use the default or main displayed variant unless the user specifies another one.
- If the page appears incomplete, say so briefly in `抓取结果` rather than silently guessing.
- Do not include screenshots or image dumps in the normal response. Use images only as an internal extraction source when needed, then return text only.

## Output format

Always output these four sections in this exact order.

### 1. 抓取结果

List the extracted fields clearly:

- `产品用途`:
- `目标人群`:
- `使用场景`:
- `长`:
- `宽`:
- `高`:
- `重量`:
- `包装重量`:

### 2. 标题

Generate one Amazon-style title using this rule:

- Structure: `主推关键词 空格 核心卖点 空格 使用场景 空格 规格参数`
- No symbols
- No brand names
- No exaggerated or sensitive wording
- Maximum `195` characters
- Keep it readable, not a keyword pile

### 3. 五点描述

Generate exactly 5 bullets.

Each bullet should:

- emphasize a concrete advantage, pain point solved, or real use case
- stay concise and conversion-oriented
- avoid brand names and sensitive claims
- avoid repeating the title mechanically

### 4. 后台搜索词

Generate one backend search terms line:

- exclude words already used in the title
- include synonyms, long-tail variants, and colloquial search phrases
- aim for broader long-tail coverage
- maximum `250` characters
- no brand names

## Quality bar

- The copy should feel ready for manual review, not like raw notes.
- If source information is weak, be conservative in factual claims and stronger on scenario wording.
- Avoid obvious repetition across the title, bullets, and backend terms.
- When details are sparse, rely on用途, 人群, and 场景 to keep the listing useful.

## Invocation examples

- `用1688-amazon-copywriter处理这个链接：https://detail.1688.com/...`
- `调用1688文案工具，帮我把这个1688商品链接生成亚马逊标题五点和后台词`
- `根据这个1688链接抓信息并输出亚马逊文案`
