# AI 教學助攻課後資源

這個 repo 是「AI 教學助攻：備課與教材設計經驗談」的課後資源頁。它假設多數學員只用過 ChatGPT、Claude.ai、NotebookLM 這類網頁版工具，所以先從零安裝或低安裝的流程開始，再慢慢走到 Codex app、Claude Code desktop app、Git、工作區指令檔、Skill、MCP、subagent、把關流程與 insights 回顧。

> 核心原則：先會問、會整理、會存檔，再讓桌面版 agent 只讀教材。熟悉後才讓 agent 小範圍修改，最後再談 CLI、MCP、Skill 或自動化。

## 先分清楚誰要做什麼

這份資源頁會反覆提到 agent、Skill、MCP、subagent。新手不用把它們都當成自己要操作的功能。請先用這個分工理解：

| 對象 | 你需要記得的事 |
|---|---|
| 老師 / 學員 | 說清楚教學目標、提供教材副本、檢查結果、決定是否存檔或發布 |
| 主 agent | 讀檔、列計畫、修改副本、摘要差異；需要時自己安排獨立審查或整理流程 |

所以看到 Skill、MCP、subagent 的技術範例時，不代表每位老師都要自己照著輸入。一般使用者只需要知道：可以對主 agent 說出需求；如果某個功能需要額外設定，第一天先跳過。

## 先從哪裡開始？

| 你的狀況 | 建議路線 |
|---|---|
| 第一次來，想照順序做 | 先看 [快速開始](docs/00-快速開始.md) |
| 完全不寫程式，只想讓學生能自學 | 先看 [NotebookLM 教學](docs/02-notebooklm.md) |
| 想從網頁版過渡到會讀檔的 agent | 先看 [Agent 桌面版與 CLI 工具](docs/03-agent-cli.md) |
| 想讓 agent 幫忙改教材，但怕改壞 | 先看 [Git 與 GitHub](docs/04-git-github.md) |
| 想讓 agent 每次都遵守你的教學慣例 | 熟悉基本任務後看 [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md) |
| 想知道自己怎麼越用越準 | 先看 [回顧用法與 insights](docs/05-工作守則與交辦模板.md#回顧用法與-insights) |
| 已經遇到重複摩擦，想讓流程固定下來 | 先請主 agent 幫你整理流程，再看 [Skill 怎麼和 agent 合作寫](docs/06-skills.md)、[MCP 怎麼接](docs/07-mcp.md) 與 [Subagent 怎麼用](docs/11-subagents.md) |

## 30 分鐘快速上手：先做一輪最小流程

完整分段版請看 [00 快速開始](docs/00-快速開始.md)。主頁先抓最小動線：

1. 用 ChatGPT、Claude.ai 或 NotebookLM 網頁版，先整理一份教材或產生 3-5 題練習題。
2. 用 GitHub Desktop 建立教材副本與第一個 commit。這是改壞時能回去的存檔點。
3. 安裝或開啟 [Codex app](https://developers.openai.com/codex/app) 或 [Claude Code desktop app](https://code.claude.com/docs/en/overview)。
4. 在桌面版 agent 中選教材資料夾，先交辦「只讀、整理、列計畫」，不要改檔。
5. 確認它讀對後，才讓它小範圍修改一份副本，例如 README 或一小段講義。
6. 用 GitHub Desktop 或 agent app 的 diff / review 畫面檢查修改，由老師決定是否 commit / push。
7. 跑過幾次後，請主 agent 把常見摩擦整理成 `AGENTS.md` / `CLAUDE.md` 草稿，或用 `/insights` 回顧可改進的交辦習慣；老師只負責確認哪些規矩真的要留下。

## 工具總表

### 零安裝網頁 AI

| 工具 | 入口 | 用途 |
|---|---|---|
| ChatGPT | <https://chatgpt.com/> | 一次性問答、草擬文字、改寫語氣、產生範例 |
| Claude.ai | <https://claude.ai/> | 長文閱讀、教材草稿、規格化交辦、寫作修訂 |
| Gemini | <https://gemini.google.com/> | Google 生態整合、長文件問答、一般對話 |
| NotebookLM | <https://notebooklm.google.com/> | 把講義、PDF、網址變成有來源引用的課程問答工具 |

### 會讀檔與改檔的桌面 agent

| 工具 | 入口 | 用途 |
|---|---|---|
| Codex app | <https://developers.openai.com/codex/app> | OpenAI 的桌面 agent 入口，可選本機 project folder、Local 模式、review diff 與使用 Git 功能 |
| Claude Code desktop app | <https://code.claude.com/docs/en/overview> | Claude Code 的桌面入口，不熟 terminal 也能視覺化 review diff、開多個 session |
| Claude Code CLI | <https://code.claude.com/docs/en/setup> | 進階：讀檔、改檔、跑指令、subagent、Skill、MCP 生態完整 |
| Codex CLI | <https://developers.openai.com/codex/cli> | 進階：偏好 terminal、想用命令列交辦檔案任務的人 |
| Gemini CLI | <https://github.com/google-gemini/gemini-cli> | 進階：Google 官方 Gemini 終端機工具，適合長 context 與 Google 生態使用者 |

### 版本控制與 agent 協作

| 工具 | 入口 | 用途 |
|---|---|---|
| Git | <https://git-scm.com/downloads> | 教材的存檔點與時光機，讓 agent 改壞也能回復 |
| GitHub | <https://github.com/> | 讓老師與 agent 在同一份修改歷史上協作 |
| GitHub Desktop | <https://desktop.github.com/> | 不熟 terminal 的老師可用圖形介面建立存檔點 |
| GitHub Pages | <https://docs.github.com/en/pages> | 延伸用途：把教材網站自動上線 |

### 進階封裝與整合

| 工具/概念 | 入口 | 用途 |
|---|---|---|
| Claude Code Skills | <https://code.claude.com/docs/en/skills> | 進階：讓 agent 把固定流程封裝成工作手冊 |
| Codex Skills | <https://developers.openai.com/codex/skills> | 進階：在 Codex 裡封裝可觸發的操作流程 |
| MCP | <https://modelcontextprotocol.io/docs/getting-started/intro> | 進階：把外部資料與服務接進 agent；第一天先不用設定 |
| Subagent | [subagent 教學](docs/11-subagents.md) | 進階：主 agent 需要大量搜尋、審查、對照時可安排獨立 context |
| NotebookLM-py | <https://github.com/teng-lin/notebooklm-py> | 非官方 NotebookLM Python API / CLI / Skill，適合進階自動化 |
| awesome-agentic-ai-zh | <https://github.com/WenyuChiou/awesome-agentic-ai-zh> | 中文 AI agent 學習地圖與資源庫 |
| Claude Code Workspace Docs | <https://zeuikli.github.io/cc-workspace-docs/> | Claude Code 工作區與設定相關中文文件 |

## 這場投影片對應的資源

| 投影片概念 | 對應教學 |
|---|---|
| 從 Chat 到 Agent，不要跳太快 | [快速開始](docs/00-快速開始.md)、[Agent 桌面版與 CLI 工具](docs/03-agent-cli.md) |
| 工作守則寫進 `CLAUDE.md` / `AGENTS.md` | 熟悉幾次任務後看 [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md) |
| 別給願望，給規格 | [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md) |
| 讓它先反問你 | [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md#讓-agent-先反問你) |
| 給目錄，不要全文硬塞 | [NotebookLM 教學](docs/02-notebooklm.md) |
| 快取索引 | [NotebookLM-py 與進階自動化](docs/08-notebooklm-py.md) |
| Agent 會讀檔、改檔、跑程式 | [Agent 桌面版與 CLI 工具](docs/03-agent-cli.md) |
| Git 是教材時光機，也是 agent 協作安全網 | [Git 與 GitHub](docs/04-git-github.md) |
| 把反覆摩擦封裝成工具箱 | 請主 agent 先整理流程，再看 [Skill 怎麼和 agent 合作寫](docs/06-skills.md) |
| Agent 接外部工具 | 先知道可以這樣做；設定細節見 [MCP 怎麼接](docs/07-mcp.md)。NotebookLM 目前先走網頁版或 NotebookLM-py CLI/Skill |
| 需要獨立審查或大量查找 | 對主 agent 提需求，細節見 [Subagent 怎麼用](docs/11-subagents.md) |
| 漂亮不等於正確 | [把關與安全](docs/09-把關與安全.md) |
| `/insights` 與精進迴圈 | [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md#回顧用法與-insights) |
| 投影片與公開範例 | [投影片與延伸資源](docs/10-投影片與延伸資源.md) |

## 重要安全提醒

- 不要上傳學生姓名、學號、成績、聯絡方式或可辨識個資。
- 不要把未授權分享的教材、書籍 PDF、學生作業公開放到 GitHub。
- AI 產生的答案、解答、反例、引用都要人工抽查。
- 對關鍵內容，不要只問「這樣對嗎？」請改問「請挑出錯誤、反例、缺漏與需要人工確認的地方」。

## License

本 repo 內容以 MIT License 釋出。若你放入課程講義、投影片或截圖，請另外確認那些素材本身的授權。
