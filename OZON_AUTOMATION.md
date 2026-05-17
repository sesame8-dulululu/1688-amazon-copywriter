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
3. Extract the 1688 source ID from each product link.
   - Example: `http://detail.1688.com/offer/958618745268.html`
   - Source ID: `958618745268`
4. Before processing, read the target Google Sheet and build a processed ID set from rows where `处理状态` is `成功`.
5. If a source ID already exists in the processed ID set, skip it and do not add it to the processing queue.
6. If a source ID exists with `处理状态` as `失败`, retry it only when `重试次数` is less than 2.
7. Process remaining links in batches of 2.
8. Do not exceed concurrency 2.
9. Wait a random 3 to 6 seconds between batches.
10. If one item fails, record the error and continue with the remaining items.
11. Do not collect or write product images.

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
2. 货源ID
3. 商品链接
4. 用途
5. 目标人群
6. 使用场景
7. 长
8. 宽
9. 高
10. 重量
11. 包装重量
12. AI标题
13. 五点描述
14. 后台搜索词
15. 处理状态
16. 处理时间
17. 错误信息
18. 重试次数

## Deduplication Rules

Use `货源ID` as the deduplication key.

Before every run:

1. Read all existing rows in the Google Sheet.
2. Build a set of source IDs where `处理状态` is `成功`.
3. Skip any ERP item whose source ID is already in that success set.
4. For failed rows, retry only if `重试次数` is less than 2.
5. Mark items as `处理中` before processing when possible.
6. Mark successful items as `成功`.
7. Mark failed items as `失败`, fill `错误信息`, and increment `重试次数`.

## Target Google Sheet

https://docs.google.com/spreadsheets/d/1T6Yz0A85fS77KOm5KF1PES8yQyCe_DSzY3neike8Yp4/edit

## Completion Report

After every run, report:

- total item count
- success count
- failure count
- Google Sheet link
