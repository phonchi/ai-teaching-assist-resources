# 07 MCP 怎麼接

MCP 是 Model Context Protocol 的縮寫。簡單說，它是一個讓 AI 工具連接外部資料與服務的標準接口。

官方介紹：<https://modelcontextprotocol.io/docs/getting-started/intro>

## 用一句話理解

如果 agent 是「會做事的助教」，MCP 就像是幫助教接上工具的插座。接上後，AI 才能安全地讀某個資料庫、查某個服務、操作某個工具。

## 常見可以接什麼？

| 類型 | 例子 |
|---|---|
| 本機資料 | 檔案系統、PDF、資料夾、CSV |
| 知識工具 | Notion、Obsidian、Zotero |
| 辦公工具 | Google Drive、Gmail、Calendar、Slack |
| 開發工具 | GitHub、Postgres、瀏覽器、自動化測試 |
| 研究工具 | 文獻庫、筆記庫、NotebookLM 相關工具 |

## 什麼時候需要 MCP？

需要：

- 你想讓 AI 讀取某個固定資料來源。
- 你想讓 AI 在 Notion、GitHub、Google Drive 等工具中操作。
- 你有重複工作流程，不想每次手動複製貼上。

不需要：

- 只是問一個概念。
- 只是整理一份短文。
- 還沒確定這個流程會重複使用。

## 概念流程

1. 找到你要接的服務，例如 GitHub 或 Google Drive。
2. 找現成 MCP server，優先用官方或社群成熟專案。
3. 在你的 AI 工具中註冊 MCP server。
4. 給予最小必要權限。
5. 用低風險資料測試。
6. 確認它會問、會拒絕危險操作、會回報錯誤。

## 重要安全原則

- 不要把高權限 token 交給不熟的 MCP server。
- 不要一開始就給整個雲端硬碟權限。
- 先用測試資料夾，不要直接接真實學生資料。
- 若工具要寫入或刪除資料，先要求 AI 列計畫並等待確認。

## 找 MCP server 的資源

- MCP 官方文件：<https://modelcontextprotocol.io/docs/getting-started/intro>
- awesome-mcp-servers：<https://github.com/punkpeye/awesome-mcp-servers>
- awesome-mcp-servers：<https://github.com/wong2/awesome-mcp-servers>
- awesome-agentic-ai-zh MCP/Skill catalog：<https://github.com/WenyuChiou/awesome-agentic-ai-zh/blob/main/resources/mcp-skills-catalog.md>

## 教師常見應用

| 情境 | 可能接法 |
|---|---|
| 課程資料都在 Google Drive | 接 Drive 類 MCP，讓 AI 查找指定資料夾 |
| 教材放 GitHub | 接 GitHub MCP 或直接用 CLI agent 操作 repo |
| 研究筆記在 Zotero/Obsidian | 接文獻與筆記工具，做摘要與 cross-reference |
| 每週公告與信件 | 接 Gmail/Calendar 類工具，但要注意學生個資 |

## 初學者建議

第一天不要急著接 MCP。先把工作守則與 NotebookLM 用熟，再挑一個「會重複、低風險」的流程接 MCP。
