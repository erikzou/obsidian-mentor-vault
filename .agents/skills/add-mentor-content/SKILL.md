---
name: add-mentor-content
description: >
  Use when adding content to the mentor vault: pasting book chapters, podcast
  transcripts, articles, or saying "新增內容", "處理這個章節", "add this content".
  Also for creating new mentors or source collections.
---

# Add Mentor Content

將使用者提供的原始內容（書籍章節、Podcast 逐字稿、文章）處理成結構化的 source + summary。

寫入任何 `.md` 檔案前，確保 Obsidian 語法正確（wikilinks、callouts、properties）。

## 步驟

### 1. 判斷來源資訊

確認以下資訊（不確定時詢問使用者）：
- **導師**：屬於哪位導師？（如果是新導師，先建立目錄和 mentor-profile.md）
- **來源**：屬於哪本書 / 哪集 Podcast / 文章集？
- **主題**：這段內容對應 index.md 中的哪個主題？（如果是新主題，需要新增 index 條目）

### 2. 儲存原文到 sources/（必須先完成，再寫 summary）

建立 `sources/{topic-slug}-src.md`：

```markdown
---
title: "{主題名稱} — Source"
source: {來源名稱}
mentor: {mentor-slug}
---
# {主題名稱}

原文章節：[[{原始檔名}#^{chapter-anchor}]]

## {段落標題 1}

{完整原文段落}

^{block-id}

## {段落標題 2}

{完整原文段落}

^{block-id}
```

**Source 規則：**
- 預設保留完整原文，不做刪減或改寫
- 用 `##` heading 標記段落錨點（繁中），作為 wikilink 目標
- 每段落末尾加 `^block-id`（block anchor），供外部精確引用
- 保留原文語言（通常是英文），不翻譯
- 頂部加 `原文章節` 連結，指向原始書檔的章節 anchor
- 若原始書檔有目錄（TOC）造成重複 heading，需在內容章節 heading 後加 `^ch{N}-{NN}` anchor 繞開

**降級：若觸發 content filtering**（API 拒絕大量逐字複製），改為精選引述模式：
- 每個主題精選 5-8 段，每段 1-3 句
- 其餘規則不變

### 3. 生成摘要到 summaries/

建立 `summaries/{topic-slug}-sum.md`（**必須在 source 寫完之後**）：

```markdown
---
title: "{主題名稱}"
source: {來源名稱}
mentor: {mentor-slug}
tags: [{相關標籤}]
---
# {主題名稱}

原文引述：[[{topic-slug}-src]]

## 核心論點

{2-3 句導師的主要論點，包含推導過程（為什麼），不只結論}

## 關鍵觀點

- {觀點 1：導師的具體建議或推理}
- {觀點 2}
- {觀點 3}

## 例子與故事

- {導師用來說明觀點的案例概要}

## 實踐建議

- {可操作的行動指引}

## 相關主題

- [[{related-topic-slug}]] — {關聯說明}
```

### Token 預算

| 來源類型 | 目標長度 |
|---------|---------|
| 書籍主題 | 1000-2000 tokens |
| Podcast 段落 | 800-1500 tokens |
| 文章 | 500-1000 tokens |

### Summary 原則

**必須包含**：
- 論點的推導過程（不只結論，要有「為什麼」）
- 導師的具體建議
- 例子與故事概要
- 與其他主題的關聯
- 導師的推理邏輯

**不應包含**：
- 純標題列表（那是 index 的工作）
- AI 自己的詮釋（summary 只呈現導師原意）
- 任何引述（英文原文引述屬於 sources 層，summary 絕對不引述）
  - 原因：agent 生成引述時容易幻覺，寫出原文中不存在的句子
  - sources 已有精選引述，summary 只需分析與消化

### 4. 更新 index.md

在對應來源的 `index.md` 表格中加入新條目：

```markdown
| {主題名稱} | {關鍵詞，中英文混合} | [[{topic-slug}]] |
```

### 5. 更新 mentor-profile.md（如有新洞見）

處理完一批來源後，檢視 `mentor-profile.md` 是否需要更新：
- **核心框架**：書中是否強調了尚未列入的框架？
- **關鍵術語表**：是否有新術語或現有定義需要修正？

初版可先用通識填寫，但每次處理來源後應對照原文審視並補充。

### 6. 確認

告知使用者已建立的檔案，並提示可以開始提問。
