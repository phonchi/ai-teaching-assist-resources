# 08 NotebookLM-py 與進階自動化

[teng-lin/notebooklm-py](https://github.com/teng-lin/notebooklm-py) 是一個非官方 NotebookLM Python API / CLI / agent skill / MCP server 專案。它可以把 NotebookLM 從網頁操作延伸到程式化、自動化與 agent 整合。

> 注意：這不是 Google 官方 API。NotebookLM 內部機制若改變，這類非官方工具可能失效。初學者先用 NotebookLM 網頁版即可。

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

## 可能用途

| 用途 | 說明 |
|---|---|
| CLI 查詢 | 在 terminal 中查 NotebookLM 內容 |
| Python API | 寫腳本自動化 NotebookLM 查詢 |
| Agent skill | 讓 agent 用固定流程查 NotebookLM |
| MCP server | 讓支援 MCP 的 AI 工具把 NotebookLM 當外部資料來源 |

## 建議學習順序

1. 先完成 [NotebookLM 網頁版教學](02-notebooklm.md)。
2. 建立一個不含敏感資料的測試 notebook。
3. 閱讀 NotebookLM-py README：<https://github.com/teng-lin/notebooklm-py>。
4. 只在測試 notebook 上嘗試 CLI 或 Python。
5. 確認登入、權限、輸出都符合預期後，再考慮接入 agent。

## 跟投影片「快取索引」的關係

投影片中說的「先把資料做成快取索引」有兩條路：

- 零門檻：直接用 NotebookLM，把來源上傳到 notebook。
- 進階：用自動化工具管理 notebook、批次查詢、接到 agent workflow。

NotebookLM-py 屬於第二條路。它不是必要起點，但適合想把教學資料查詢流程固定下來的人。

## 安全提醒

- 不要用非官方工具處理學生個資或成績。
- 不要把高權限帳號拿來做測試。
- 不要把 OAuth token、cookie、API key commit 到 GitHub。
- 若用 MCP server，先確認權限範圍與可執行操作。
