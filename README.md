# Obsidian Mentor Vault

一個 Obsidian vault + AI agent 工作流。你提供導師的原始內容（書、Podcast、文章），agent 自動整理成結構化筆記。之後你可以隨時提問，agent 依據導師的真實思想框架，從整理好的資料中取材回答。

## 設計理念

- **真實性優先** — 回答基於導師的實際著作，附出處連結，絕不編造
- **分層回答** — 事實、推論、延伸三層清楚區分，你自行判斷採信程度
- **結構化取材** — 先定位來源，再讀摘要與原文，最後才組織回答

## 快速開始

### 環境需求

- [Obsidian](https://obsidian.md/)
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 或 [Codex CLI](https://github.com/openai/codex)（擇一）

### 步驟

1. Clone repo，用 Obsidian 打開
2. 在 vault 目錄下啟動 agent，貼上書籍內容並說「處理這個章節」
3. Agent 自動建立導師資料、主題索引、摘要與原文引述
4. 直接向 agent 提問，例如「Naval 怎麼看財富？」

## Vault 結構

```
Mentors/
    {mentor-slug}/
        mentor-profile.md       # 導師身份、框架、資料清單
        {source-slug}/          # 每個來源（書/Podcast/文章集）
            index.md            # 主題地圖 + 關鍵詞
            summaries/          # AI 生成的主題摘要
            sources/            # 精選引述與原文
Sessions/                       # 對話紀錄
Insights/                       # 定期回顧
```

## Skills

內建兩個 agent skill：

### add-mentor-content

處理原始內容，自動生成：
- `sources/` — 完整原文，供精確引用
- `summaries/` — 結構化摘要（核心論點、關鍵觀點、例子、實踐建議）
- 更新 `index.md` 主題索引

### vault-insights

- 對話結束後說「紀錄」，agent 將重點統整存入 `Sessions/`
- 累積紀錄後，分析諮詢歷史，找出反覆關注的議題與變化趨勢

## 回答的三個層次

- **事實層** — 導師的原話與觀點，附出處連結
- **推論層** — 基於導師框架分析你的具體情境
- **延伸層** — 超出導師範圍的補充，標記為 AI 判斷

## 範例導師

Repo 包含 [Naval Ravikant](https://www.navalmanack.com/) 的架構作為範例。*The Almanack of Naval Ravikant* 由 Eric Jorgenson 編撰，全書免費公開於 [navalmanack.com](https://www.navalmanack.com/)。

由於版權考量，repo 不包含書籍內容。你可以自行取得書籍後，用 agent 生成。

## 新增導師

告訴 agent「新增導師」並提供名稱，agent 會建立資料夾結構。再提供內容即可。

## Agent 支援

| Agent | 指令檔 | Skills 路徑 |
|-------|--------|------------|
| Claude Code | `CLAUDE.md` | `.claude/skills/` |
| Codex CLI | `AGENTS.md` | `.agents/skills/` |

## 授權

Vault 架構與工作流為開源。導師的書籍內容受各自版權保護，不包含在 repo 中。
