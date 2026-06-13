# 03 Agent CLI 工具

Agent CLI 是「會動手」的 AI 助手。它不只回答你，還能讀檔、改檔、跑指令、檢查結果。投影片中的「會做事的助手」主要指這類工具。

## 先知道差別

| 類型 | 代表工具 | 能做什麼 |
|---|---|---|
| 網頁聊天 | ChatGPT、Claude.ai、Gemini | 回答、改寫、草擬 |
| 資料問答 | NotebookLM | 根據你上傳的來源回答 |
| Agent CLI | Claude Code、Codex CLI、Gemini CLI | 讀檔、改檔、跑程式、驗證 |

## 工具入口

| 工具 | 入口 | 適合誰 |
|---|---|---|
| Claude Code | <https://code.claude.com/docs/en/setup> | 想用 Skill、MCP、subagent，把工作流程長期固定下來的人 |
| OpenAI Codex CLI | <https://developers.openai.com/codex/cli> | 已使用 ChatGPT/OpenAI，想在終端機交辦檔案任務的人 |
| Gemini CLI | <https://github.com/google-gemini/gemini-cli> | 想用 Gemini 長 context 或 Google 生態的人 |
| OpenCode | <https://github.com/sst/opencode> | 想使用開源、可換模型的 CLI agent 的人 |

## 安裝前置觀念

大多數 CLI agent 都需要：

- Terminal：Windows 可用 PowerShell 或 Windows Terminal；macOS/Linux 用 Terminal。
- Node.js/npm：有些工具用 `npm` 或 `npx` 安裝。
- Git：方便管理教材版本。
- 登入或 API key：依工具不同，可能用網頁登入或 API key。

Node.js 入口：<https://nodejs.org/>

## 三平台提醒

### Windows

- 新手可先安裝 [Git for Windows](https://git-scm.com/download/win) 與 [GitHub Desktop](https://desktop.github.com/)。
- 若常跑 CLI 工具，建議使用 Windows Terminal。
- 需要 Linux 環境時再考慮 WSL，不要第一天就把所有工具都裝滿。

### macOS

- 可用內建 Terminal。
- 常見安裝方式會用 `npm` 或 Homebrew。
- 若不熟 Homebrew，先照官方文件走，不要混用太多部落格指令。

### Linux

- 使用系統套件管理器安裝 Git、Node.js。
- 注意不同 distribution 的套件版本可能偏舊。

## 第一次交辦範例

在一個只有測試資料的資料夾中啟動 agent，先做低風險任務：

```text
請閱讀這個資料夾中的 README 與 docs。
先不要修改檔案。
請整理：
1. 這個 repo 的用途
2. 目前有哪些文件
3. 哪些地方對新手最難懂
```

確認它讀對之後，再交辦修改：

```text
請新增一段「快速開始」到 README。
修改前先列出你打算改哪個檔案與改動重點。
```

## 使用原則

- 一開始只在副本資料夾練習。
- 修改超過 3 個檔案前，要求它先列計畫。
- 要求它跑驗證，不要只相信它說完成。
- 重要教材、解答、成績一定人工檢查。

## 什麼時候不要用 CLI agent？

- 你只要問一句定義。
- 你不想讓工具碰本機檔案。
- 你正在處理學生個資或成績原始檔。
- 你不清楚它會改哪些檔案。
