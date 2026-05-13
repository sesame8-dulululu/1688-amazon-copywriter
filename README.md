# 1688 Amazon Copywriter

Reusable prompt and skill package for turning a single 1688 product link into Amazon listing copy.

## Included versions

- `codex/SKILL.md`: Codex skill version
- `manus/1688-amazon-copywriter.md`: generic Markdown version for Manus or other AI tools

## What it does

Given one 1688 product URL, this workflow:

1. extracts product usage, audience, scenarios, size, weight, and package weight
2. checks page text first, then packaging or parameter sections, then detail images if needed
3. returns four fixed sections:
   - `抓取结果`
   - `标题`
   - `五点描述`
   - `后台搜索词`

## Privacy

This repository is intended to be stored in a private GitHub repository if you do not want others to view it.

## Suggested repo name

`1688-amazon-copywriter`
