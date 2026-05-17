# OZON Automation Workflow

This document defines the fixed automation workflow for the Miaoshou ERP Ozon collection box.

## Schedule

Run once every 48 hours.

## Source

- Platform: Miaoshou ERP web version
- Page: Ozon collection box
- Status filter: unpublished / not listed items

## Processing Rules

1. Open Miaoshou ERP and go to the Ozon collection box.
2. Collect all unpublished 1688 source links.
3. Process links in batches of 2.
4. Do not exceed concurrency 2.
5. Wait a random 3 to 6 seconds between batches.
6. If one item fails, record the error and continue with the remaining items.
7. Do not collect or write product images.

## Copywriting Skill

For every product link, use the `1688-amazon-copywriter` workflow.

The workflow must follow the single-link high-quality extraction rules:

1. Check visible page text first.
2. Inspect packaging, product parameter, logistics, and attribute sections.
3. If dimensions or weights are not available in text, inspect detail images, parameter images, packaging images, and long description images.
4. If a field still cannot be confirmed, write `未提供`.
5. Do not invent dimensions or weights.

## Google Sheet Columns

Use this fixed column order:

1. 日期
2. 商品链接
3. 用途
4. 目标人群
5. 使用场景
6. 长
7. 宽
8. 高
9. 重量
10. 包装重量
11. AI标题
12. 五点描述
13. 后台搜索词

## Target Google Sheet

https://docs.google.com/spreadsheets/d/1T6Yz0A85fS77KOm5KF1PES8yQyCe_DSzY3neike8Yp4/edit

## Completion Report

After every run, report:

- total item count
- success count
- failure count
- Google Sheet link
