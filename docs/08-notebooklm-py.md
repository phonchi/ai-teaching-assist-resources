# 08 NotebookLM-py 與進階自動化

[teng-lin/notebooklm-py](https://github.com/teng-lin/notebooklm-py) 是一個非官方 NotebookLM Python API / CLI / agent skill 專案。它可以把 NotebookLM 從網頁操作延伸到程式化、自動化與 agent 整合。

> 注意：這不是 Google 官方 API。NotebookLM 內部機制若改變，這類非官方工具可能失效。初學者先用 NotebookLM 網頁版即可；NotebookLM-py 是熟悉桌面版 agent 與基本安全流程後才評估的進階路線。

## 它適合誰？

- 已經熟悉 NotebookLM 網頁版。
- 已經有會重複的 NotebookLM 查詢流程。
- 願意處理 CLI、Python、登入與權限等設定細節。
- 想把 NotebookLM 接到 Claude Code、Codex 或其他 agent workflow。

## 不適合誰？

- 第一次使用 NotebookLM 的學員。
- 不熟 Python、terminal、OAuth 或 CLI 的使用者。
- 要處理學生個資或敏感資料的人。

## 兩種主要用法

| 用法 | 適合誰 | 說明 |
|---|---|---|
| CLI | 熟悉 terminal 後再用 | 在 terminal 中建立 notebook、加 source、問答、產生 artifacts |
| Skill | 主 agent 草擬、老師審內容 | 讓 agent 知道如何用 NotebookLM-py 完成固定流程 |

## 老師實際該怎麼說

一般老師不用從這一頁開始下指令。可以先對主 agent 說：

```text
我已經熟悉 NotebookLM 網頁版，想把某個測試 notebook 接進教材產生流程。
請先評估 NotebookLM-py 是否適合，列出需要設定的項目、權限風險、以及替代方案。
不要直接連正式課程資料。
```

## 進階 CLI 設定參考

這段是主 agent 評估 NotebookLM-py 後才看的技術參考，不是要求本場演講的聽眾照著輸入。老師的工作是先確認目標、測試資料與權限風險。

CLI 起手：

```bash
uv tool install "notebooklm-py[browser]"
notebooklm login
notebooklm auth check --test --json
```

多 Google 帳號使用者請先確認 NotebookLM-py 的 active profile，避免 agent 接到個人帳號或錯誤課程資料。

目前本機實測 `notebooklm-py 0.7.1` 沒有 MCP 子命令或 MCP server 可執行入口；所以這頁不再提供 NotebookLM-py MCP 設定。

## 建議導入順序

1. 先完成 [NotebookLM 網頁版教學](02-notebooklm.md)。
2. 建立一個不含敏感資料的測試 notebook。
3. 請主 agent 評估是否真的需要 NotebookLM-py。
4. 若需要，再閱讀 NotebookLM-py README：<https://github.com/teng-lin/notebooklm-py>。
5. 只在測試 notebook 上嘗試 CLI 或 Python。
6. 確認登入、權限、輸出都符合預期後，再考慮如何讓 Codex app、Claude Code desktop app 或其他 agent 協助使用 CLI 結果。

## 跟投影片「快取索引」的關係

投影片中說的「先把資料做成快取索引」有兩條路：

- 零門檻：直接用 NotebookLM，把來源上傳到 notebook。
- 進階：用自動化工具管理 notebook、批次查詢、接到 agent workflow。

NotebookLM-py 屬於第二條路。它不是必要起點，但適合想把教學資料查詢流程固定下來的人。

例如一個進階教學 workflow 可以是：

```text
NotebookLM notebook 保存講義與考古題
NotebookLM-py CLI 產生或查詢測試 notebook 的結果
agent 根據查詢結果產生小考草稿
Git 保存這次教材修改
老師人工檢查解答與題目範圍
```

這才是投影片中「給目錄」「快取索引」「agent 做事」「Git 存檔點」合在一起的版本。

## 安全提醒

- 不要用非官方工具處理學生個資或成績。
- 不要把高權限帳號拿來做測試。
- 不要把 OAuth token、cookie、API key commit 到 GitHub。尤其不要 commit `~/.notebooklm/` 或 `storage_state.json`，那裡可能含有 Google session cookies。
- 先從 read-only 問答開始，不要一開始就讓 agent 刪 notebook、source 或 note。
