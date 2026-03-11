---
name: vault-insights
description: >
  Use when the user wants to review their consultation history or discover
  patterns. Triggers: "回顧", "洞察", "insights", "我最近問了什麼",
  "review my sessions", "what have I been asking about".
---

# Vault Insights

分析使用者的諮詢歷史，提煉主題模式與成長軌跡。

## 步驟

### 1. 讀取 Sessions

讀取 `Sessions/` 目錄中的所有筆記。

如果 Sessions/ 為空或筆記太少，告知使用者目前累積不足，建議先多幾次諮詢並紀錄。

### 2. 分析模式

從所有 session 紀錄中提煉：
- 最常諮詢的導師
- 最常涉及的主題與框架
- 反覆出現的生活議題（如職涯、人際、財務等）
- 問題類型的變化（從觀念性到應用性？從單一導師到跨導師？）

### 3. 生成 Insight 筆記

在 `Insights/` 建立筆記：

```markdown
---
title: "Insight — {日期}"
date: {YYYY-MM-DD}
sessions_analyzed: {數量}
tags: [insight]
---
# Insight — {日期}

## 主題分佈

{哪些主題被問最多、哪些導師被諮詢最多}

## 反覆出現的議題

{使用者持續關注的生活面向}

## 常用框架

{哪些導師框架被引用最多}

## 觀察與建議

{基於模式的觀察}

## 建議探索

{使用者尚未觸及但可能相關的主題}
```

### 4. 告知使用者

摘要 insight 的重點發現。
