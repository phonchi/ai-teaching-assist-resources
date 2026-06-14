# 07 MCP 怎麼接：讓 agent 讀得到你的工具與資料

MCP 是 Model Context Protocol 的縮寫。簡單說，它是一個讓 AI 工具連接外部資料與服務的標準協定介面。

官方介紹：<https://modelcontextprotocol.io/docs/getting-started/intro>

> 進階提醒：MCP 不是第一天要接的東西，也不是每位老師要自己設定。新手先用 NotebookLM 網頁版、GitHub Desktop、Codex app 或 Claude Code desktop app 完成一輪安全流程；等真的有重複流程，再請主 agent 先評估是否需要接 MCP。

## 用一句話理解

如果 agent 是「會做事的工具」，MCP 就像是幫 agent 接上工具的插座。接上後，AI 才能透過受控的工具介面讀某個資料庫、查某個服務、操作某個工具；真正的安全仍取決於 server、client 權限與你的設定。

在這場投影片脈絡中，MCP 的實用例子是：把 GitHub、Google Drive、Notion、Zotero 這類外部工具接進 agent，讓它不只會聊天，而是能根據你的課程資料做事。NotebookLM 目前先用網頁版或 NotebookLM-py CLI/Skill，不放在 MCP 範例中。

## 常見可以接什麼？

| 類型 | 例子 |
|---|---|
| 本機資料 | 檔案系統、PDF、資料夾、CSV |
| 知識工具 | Notion、Obsidian、Zotero |
| 辦公工具 | Google Drive、Gmail、Calendar、Slack |
| 開發工具 | GitHub、Postgres、瀏覽器、自動化測試 |
| 研究工具 | 文獻庫、筆記庫、研究資料庫 workflow |

## 什麼時候需要 MCP？

老師需要知道「可能需要 MCP」的情境：

- 你想讓 AI 讀取某個固定資料來源。
- 你想讓 AI 在 GitHub、Google Drive、Notion 等工具中操作。
- 你有重複工作流程，不想每次手動複製貼上。

不需要：

- 只是問一個概念。
- 只是整理一份短文。
- 還沒確定這個流程會重複使用。

## 老師實際該怎麼說

一般老師不用自己找 server 或寫設定。可以先對主 agent 說：

```text
我已經把課程資料放在固定資料源，例如 GitHub repo、Google Drive 或 Notion。
我希望之後產生小考或學習指南時，agent 可以查這些資料。
請先評估是否需要 MCP；如果需要，請列出需要設定的項目與安全風險，不要直接連接我的正式資料。
```

## 主 agent 評估 MCP 時會檢查什麼

這一段不是要求老師自己設定。當你請主 agent 評估 MCP 時，它應該先檢查：

1. 要接的是哪個服務，例如 GitHub、Google Drive 或 Notion。
2. 是否有官方或社群成熟的 MCP server。
3. 你的 AI 工具是否支援這個 MCP server。
4. 需要哪些最小必要權限。
5. 是否能先用低風險資料測試。
6. 是否會問、會拒絕危險操作、會回報錯誤。

## NotebookLM 目前不要放在 MCP 範例

本機實測 `notebooklm-py 0.7.1` 時，CLI help 沒有 MCP 群組，也沒有可用的 MCP server console script。因此本 repo 不再把 NotebookLM-py 寫成 MCP server 接法。

NotebookLM 目前建議先保留網頁版路線：

- 零門檻：用 NotebookLM 網頁版上傳講義、問答、產生學習指南。

## 其他可接的 MCP 資源

- MCP 官方文件：<https://modelcontextprotocol.io/docs/getting-started/intro>
- punkpeye awesome-mcp-servers：<https://github.com/punkpeye/awesome-mcp-servers>
- wong2 awesome-mcp-servers：<https://github.com/wong2/awesome-mcp-servers>
- awesome-agentic-ai-zh MCP/Skill catalog：<https://github.com/WenyuChiou/awesome-agentic-ai-zh/blob/main/resources/mcp-skills-catalog.md>

## 安全與權限提醒

- 不要把高權限 token 交給不熟的 MCP server。
- 不要一開始就給整個雲端硬碟或真實課程資料權限。
- 先用測試 notebook，不要直接接學生姓名、學號、成績或可辨識個資。
- 若某個 MCP server 需要登入狀態、cookies 或 token，不能分享、不能 commit。
- 破壞性工具需要確認；教學時應先示範 read-only 問答與 artifact 產生。
- 不要把 HTTP transport 綁到非 localhost，除非你完全理解網路暴露風險。

## 初學者建議

第一天不要急著接 MCP。先把 NotebookLM 網頁版、GitHub Desktop 存檔點、Codex app / Claude Code desktop app 的只讀流程用熟；第二輪再請主 agent 草擬 `CLAUDE.md` / `AGENTS.md`；最後才挑一個「會重複、低風險」且目前真的有可用 server 的流程，請主 agent 評估是否接 MCP。
