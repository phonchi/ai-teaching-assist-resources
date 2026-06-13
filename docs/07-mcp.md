# 07 MCP 怎麼接：讓 agent 讀得到你的工具與資料

MCP 是 Model Context Protocol 的縮寫。簡單說，它是一個讓 AI 工具連接外部資料與服務的標準協定介面。

官方介紹：<https://modelcontextprotocol.io/docs/getting-started/intro>

## 用一句話理解

如果 agent 是「會做事的助教」，MCP 就像是幫助教接上工具的插座。接上後，AI 才能透過受控的工具介面讀某個資料庫、查某個服務、操作某個工具；真正的安全仍取決於 server、client 權限與你的設定。

在這場投影片脈絡中，MCP 的實用例子是：把 NotebookLM、GitHub、Google Drive、Notion、Zotero 這類外部工具接進 agent，讓它不只會聊天，而是能根據你的課程資料做事。

## 常見可以接什麼？

| 類型 | 例子 |
|---|---|
| 本機資料 | 檔案系統、PDF、資料夾、CSV |
| 知識工具 | NotebookLM、Notion、Obsidian、Zotero |
| 辦公工具 | Google Drive、Gmail、Calendar、Slack |
| 開發工具 | GitHub、Postgres、瀏覽器、自動化測試 |
| 研究工具 | 文獻庫、筆記庫、NotebookLM research workflow |

## 什麼時候需要 MCP？

需要：

- 你想讓 AI 讀取某個固定資料來源。
- 你想讓 AI 在 NotebookLM、GitHub、Google Drive 等工具中操作。
- 你有重複工作流程，不想每次手動複製貼上。

不需要：

- 只是問一個概念。
- 只是整理一份短文。
- 還沒確定這個流程會重複使用。

## 概念流程

1. 找到你要接的服務，例如 NotebookLM 或 GitHub。
2. 找現成 MCP server，優先用官方或社群成熟專案。
3. 在你的 AI 工具中註冊 MCP server。
4. 給予最小必要權限。
5. 用低風險資料測試。
6. 確認它會問、會拒絕危險操作、會回報錯誤。

## 例子：用 NotebookLM-py 把 NotebookLM 接進 agent

[teng-lin/notebooklm-py](https://github.com/teng-lin/notebooklm-py) 是非官方 NotebookLM Python API / CLI / Skill / MCP server。它的 [MCP guide](https://github.com/teng-lin/notebooklm-py/blob/main/docs/mcp-guide.md) 說明，NotebookLM-py 的 MCP server 可以把 NotebookLM 暴露給 Claude Desktop、Claude Code、Cursor、Windsurf 等 MCP client。

它適合的情境：

- 你已經有 NotebookLM notebook，想讓 agent 直接查詢其中資料。
- 你想讓 agent 管理 notebooks / sources / notes。
- 你想讓 agent 產生並下載 Audio Overview、quiz、flashcards、mind map、slide deck 等 artifacts。
- 你想把 NotebookLM 納入可重複的教學工作流，而不是每次手動開網頁操作。

不適合的情境：

- 第一次接觸 NotebookLM。
- 還不熟 terminal、Python、OAuth 或 MCP。
- notebook 裡有學生個資、成績、未授權教材。

## NotebookLM-py MCP 最小流程

> 注意：NotebookLM-py 是非官方工具，使用未公開 Google API，可能因 Google 改動而失效。它的 MCP server 目前也是 experimental / preview，工具名稱、參數與輸出格式可能在版本間改變。請先用測試 notebook。

先確認你有 Python 環境與 `uv`。如果使用下面的 `uvx` 或自動寫入 MCP block，電腦上需要可執行的 `uv`。

### 1. 安裝 MCP extra

```bash
pip install "notebooklm-py[mcp]"
```

或不先安裝、直接用 `uvx` 從 PyPI 啟動：

```bash
uvx --from "notebooklm-py[mcp]" notebooklm-mcp --help
```

如果還沒有 `uv`，先看 uv 官方安裝說明：<https://docs.astral.sh/uv/getting-started/installation/>

### 2. 先登入 NotebookLM

MCP server 會重用 CLI 儲存的登入憑證，不會自己登入：

```bash
notebooklm login
```

如果使用 `uvx`：

```bash
uvx --from "notebooklm-py[mcp]" notebooklm login
```

多 Google 帳號的人要特別小心：NotebookLM-py 會把憑證存在 `~/.notebooklm/` 的 profile 中，MCP server 啟動時綁定目前 active profile。若你同時有個人帳號與學校帳號，請先確認 active profile，不要讓 agent 接到錯帳號的 notebook。

### 3. 寫入 MCP client 設定

NotebookLM-py 提供自動設定指令：

```bash
notebooklm mcp install claude-code
```

如果你採用 `uvx` 路線，也可以用同樣方式執行安裝指令：

```bash
uvx --from "notebooklm-py[mcp]" notebooklm mcp install claude-code
```

也可改成：

```bash
notebooklm mcp install claude-desktop
notebooklm mcp install cursor
notebooklm mcp install windsurf
```

它會寫入類似下面的 MCP server block：

```json
{
  "mcpServers": {
    "notebooklm": {
      "command": "uvx",
      "args": ["--from", "notebooklm-py[mcp]", "notebooklm-mcp"]
    }
  }
}
```

設定後要重啟 MCP client，工具才會出現。

## NotebookLM MCP 可以做什麼？

NotebookLM-py MCP guide 目前列出 25 個工具，範圍包括：

| 類型 | 工具能力 |
|---|---|
| Notebooks | 建立、列出、描述、改名、刪除 notebook |
| Sources | 加入 URL、文字、檔案、Google Drive、YouTube source；等待處理完成；讀 source 內容 |
| Chat | 對指定 notebook 問問題 |
| Notes | 建立、列出、更新、刪除 note |
| Artifacts | 產生與下載 audio、video、slide deck、quiz、flashcards、infographic、data table、mind map、report |
| Research | 啟動 web/Drive research，查詢狀態並匯入結果 |

這和投影片中的分工剛好互補：

- NotebookLM 網頁版：適合老師或學生直接讀與答。
- Agent + NotebookLM MCP：適合把 NotebookLM 放進更大的工作流，例如「查課程資料 → 產生學習指南 → 存到 repo → 交給老師審」。

## 其他可接的 MCP 資源

- MCP 官方文件：<https://modelcontextprotocol.io/docs/getting-started/intro>
- NotebookLM-py MCP guide：<https://github.com/teng-lin/notebooklm-py/blob/main/docs/mcp-guide.md>
- punkpeye awesome-mcp-servers：<https://github.com/punkpeye/awesome-mcp-servers>
- wong2 awesome-mcp-servers：<https://github.com/wong2/awesome-mcp-servers>
- awesome-agentic-ai-zh MCP/Skill catalog：<https://github.com/WenyuChiou/awesome-agentic-ai-zh/blob/main/resources/mcp-skills-catalog.md>

## 安全與權限提醒

- 不要把高權限 token 交給不熟的 MCP server。
- 不要一開始就給整個雲端硬碟或真實課程資料權限。
- 先用測試 notebook，不要直接接學生姓名、學號、成績或可辨識個資。
- NotebookLM-py 的登入狀態會存成本機檔案，例如 `~/.notebooklm/profiles/<profile>/storage_state.json`。這是 Google session cookies，不能分享、不能 commit。若不小心外洩，請刪除 `~/.notebooklm/`、重新登入，並到 Google Security Settings 撤銷可疑存取。
- `notebook_delete`、`source_delete`、`note_delete` 這類破壞性工具需要確認；教學時應先示範 read-only 問答與 artifact 產生。
- 不要把 HTTP transport 綁到非 localhost，也不要設定 `NOTEBOOKLM_MCP_ALLOW_EXTERNAL_BIND=1`，除非你完全理解網路暴露風險。
- 如果出現 `AUTH` 錯誤，先在 terminal 跑 `notebooklm login`，再重啟 client。
- 如果 client 看不到工具，確認 `notebooklm mcp install ...` 有寫入設定，並重啟 client。

## 初學者建議

第一天不要急著接 MCP。先把工作守則與 NotebookLM 網頁版用熟，再挑一個「會重複、低風險」的流程接 MCP。NotebookLM-py MCP 是進階路線，不是零門檻第一步。
