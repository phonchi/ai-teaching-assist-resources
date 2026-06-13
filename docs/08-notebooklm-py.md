# 08 NotebookLM-py 與進階自動化

[teng-lin/notebooklm-py](https://github.com/teng-lin/notebooklm-py) 是一個非官方 NotebookLM Python API / CLI / agent skill / MCP server 專案。它可以把 NotebookLM 從網頁操作延伸到程式化、自動化與 agent 整合。

> 注意：這不是 Google 官方 API。NotebookLM 內部機制若改變，這類非官方工具可能失效。初學者先用 NotebookLM 網頁版即可；NotebookLM-py 是熟悉桌面版 agent 與基本安全流程後的進階路線。

## 它適合誰？

- 已經熟悉 NotebookLM 網頁版。
- 想批次查詢 notebook。
- 想從 CLI 或 Python 操作 NotebookLM。
- 想把 NotebookLM 接到 Claude Code、Codex 或其他 agent workflow。
- 想用 MCP server 讓 agent 查 NotebookLM 中的資料。

## 不適合誰？

- 第一次使用 NotebookLM 的學員。
- 不熟 Python、terminal、OAuth 或 CLI 的使用者。
- 要處理學生個資或敏感資料的人。

## 三種主要用法

| 用法 | 適合誰 | 說明 |
|---|---|---|
| CLI | 會用 terminal 的老師或助教 | 在 terminal 中建立 notebook、加 source、問答、產生 artifacts |
| Skill | 使用 Claude Code / Codex 類 agent 的人 | 讓 agent 知道如何用 NotebookLM-py 完成固定流程 |
| MCP server | 想把 NotebookLM 接進 agent 工具的人 | 讓 Claude Code、Claude Desktop、Cursor、Windsurf 等 MCP client 直接呼叫 NotebookLM 工具 |

## 快速入口

CLI 起手：

```bash
uv tool install "notebooklm-py[browser]"
notebooklm login
notebooklm auth check --test --json
```

MCP 起手：

```bash
pip install "notebooklm-py[mcp]"
notebooklm login
notebooklm mcp install claude-code
```

也可用 `uvx` 啟動 MCP server：

```bash
uvx --from "notebooklm-py[mcp]" notebooklm-mcp --help
```

若採用 `uvx`，也可以直接執行 MCP 設定指令：

```bash
uvx --from "notebooklm-py[mcp]" notebooklm mcp install claude-code
```

`uvx` 與自動產生的 MCP 設定都需要電腦上有 `uv`。多 Google 帳號使用者請先確認 NotebookLM-py 的 active profile，避免 agent 接到個人帳號或錯誤課程資料。

更多 MCP 細節請看 [MCP 怎麼接](07-mcp.md#例子用-notebooklm-py-把-notebooklm-接進-agent)。

## 建議學習順序

1. 先完成 [NotebookLM 網頁版教學](02-notebooklm.md)。
2. 建立一個不含敏感資料的測試 notebook。
3. 閱讀 NotebookLM-py README：<https://github.com/teng-lin/notebooklm-py>。
4. 只在測試 notebook 上嘗試 CLI 或 Python。
5. 確認登入、權限、輸出都符合預期後，再考慮接入 Codex app、Claude Code desktop app 或其他 agent。

## 跟投影片「快取索引」的關係

投影片中說的「先把資料做成快取索引」有兩條路：

- 零門檻：直接用 NotebookLM，把來源上傳到 notebook。
- 進階：用自動化工具管理 notebook、批次查詢、接到 agent workflow。

NotebookLM-py 屬於第二條路。它不是必要起點，但適合想把教學資料查詢流程固定下來的人。

例如一個進階教學 workflow 可以是：

```text
NotebookLM notebook 保存講義與考古題
NotebookLM-py MCP 讓 agent 查 notebook
agent 根據查詢結果產生小考草稿
Git 保存這次教材修改
老師人工檢查解答與題目範圍
```

這才是投影片中「給目錄」「快取索引」「agent 做事」「Git 存檔點」合在一起的版本。

## 安全提醒

- 不要用非官方工具處理學生個資或成績。
- 不要把高權限帳號拿來做測試。
- 不要把 OAuth token、cookie、API key commit 到 GitHub。尤其不要 commit `~/.notebooklm/` 或 `storage_state.json`，那裡可能含有 Google session cookies。
- 若用 MCP server，先確認權限範圍與可執行操作。
- 先從 read-only 問答開始，不要第一天就讓 agent 刪 notebook、source 或 note。
