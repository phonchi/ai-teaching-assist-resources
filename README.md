# AI 教學助攻課後資源

這個 repo 是「AI 教學助攻：備課與教材設計經驗談」的課後資源頁。投影片裡講了很多概念：agent、NotebookLM、Git、工作區指令檔、Skill、MCP、subagent、把關流程與 insights 回顧。這裡把它們整理成可以直接點開、下載、照做的教學入口。

> 核心原則：先讓教材工作區有規矩，讓 agent 進資料夾就讀得到 `CLAUDE.md` 或 `AGENTS.md`，再用 Git 建立存檔點。不要一開始就追求全自動。

## 先從哪裡開始？

| 你的狀況 | 建議路線 |
|---|---|
| 第一次來，想照順序做 | 先看 [快速開始](docs/00-快速開始.md) |
| 完全不寫程式，只想讓學生能自學 | 先看 [NotebookLM 教學](docs/02-notebooklm.md) |
| 想讓 agent 幫忙改教材，但怕改壞 | 先看 [Git 與 GitHub](docs/04-git-github.md) |
| 想叫 agent 幫你讀檔、改檔、跑指令 | 先看 [Agent CLI 工具](docs/03-agent-cli.md) |
| 想讓 agent 每次都遵守你的教學慣例 | 先看 [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md) |
| 想知道自己怎麼越用越準 | 先看 [回顧用法與 insights](docs/05-工作守則與交辦模板.md#回顧用法與-insights) |
| 已經遇到重複摩擦，想封裝成工具箱 | 先看 [Skill 怎麼和 agent 合作寫](docs/06-skills.md)、[MCP 怎麼接](docs/07-mcp.md) 與 [Subagent 怎麼用](docs/11-subagents.md) |

## 30 分鐘快速上手：先做一輪最小流程

完整分段版請看 [00 快速開始](docs/00-快速開始.md)。主頁先抓最小動線：

1. 建一個測試教材資料夾或 Git repo，放一份可以練習的教材副本。
2. 依你使用的 agent 建立 `CLAUDE.md` 或 `AGENTS.md`，把課程慣例、紅線、反問規則寫進去。
3. 用 Git 或 GitHub Desktop 存第一個版本。改壞時，你有上一版可以回去。
4. 讓 agent 先只讀不改，整理「教材目標、學生卡點、建議修改處、會改哪些檔案」。
5. 再交付本次任務的目標、範圍、格式、限制、驗收標準。
6. 修改後檢查 `git diff`，由老師決定是否 commit / push。
7. 完成後用 `/insights` 或 [回顧 prompt](docs/05-工作守則與交辦模板.md#回顧用法與-insights)，把這次交辦學到的規矩回寫到 `CLAUDE.md` 或 `AGENTS.md`。

## 工具總表

### 零安裝網頁 AI

| 工具 | 入口 | 用途 |
|---|---|---|
| ChatGPT | <https://chatgpt.com/> | 一次性問答、草擬文字、改寫語氣、產生範例 |
| Claude.ai | <https://claude.ai/> | 長文閱讀、教材草稿、規格化交辦、寫作修訂 |
| Gemini | <https://gemini.google.com/> | Google 生態整合、長文件問答、一般對話 |
| NotebookLM | <https://notebooklm.google.com/> | 把講義、PDF、網址變成有來源引用的課程助教 |

### 會動手的 Agent CLI

| 工具 | 入口 | 用途 |
|---|---|---|
| Claude Code | <https://code.claude.com/docs/en/setup> | 讀檔、改檔、跑指令、subagent、Skill、MCP 生態完整 |
| OpenAI Codex CLI | <https://developers.openai.com/codex/cli> | OpenAI 的本機 coding/agent CLI，可用 ChatGPT 帳號或 API key |
| Gemini CLI | <https://github.com/google-gemini/gemini-cli> | Google 官方 Gemini 終端機工具，適合長 context 與 Google 生態使用者 |
| OpenCode | <https://github.com/sst/opencode> | 不綁單一模型供應商的開源 agent CLI |

### 版本控制與 agent 協作

| 工具 | 入口 | 用途 |
|---|---|---|
| Git | <https://git-scm.com/downloads> | 教材的存檔點與時光機，讓 agent 改壞也能回復 |
| GitHub | <https://github.com/> | 讓老師、助教、agent 在同一份修改歷史上協作 |
| GitHub Desktop | <https://desktop.github.com/> | 不熟 terminal 的老師可用圖形介面建立存檔點 |
| GitHub Pages | <https://docs.github.com/en/pages> | 延伸用途：把教材網站自動上線 |

### 進階封裝與整合

| 工具/概念 | 入口 | 用途 |
|---|---|---|
| Claude Code Skills | <https://code.claude.com/docs/en/skills> | 和 agent 合作，把跑順或反覆摩擦的流程封裝成工作手冊 |
| Codex Skills | <https://developers.openai.com/codex/skills> | 在 Codex 裡封裝可觸發的操作流程 |
| MCP | <https://modelcontextprotocol.io/docs/getting-started/intro> | 讓 AI 工具接外部資料與服務的協定介面 |
| Subagent | [subagent 教學](docs/11-subagents.md) | 把大搜尋、審查、對照檢查交給獨立 context 的助理 |
| NotebookLM-py | <https://github.com/teng-lin/notebooklm-py> | 非官方 NotebookLM Python API / CLI / MCP / Skill，適合進階自動化 |
| awesome-agentic-ai-zh | <https://github.com/WenyuChiou/awesome-agentic-ai-zh> | 中文 AI agent 學習地圖與資源庫 |
| Claude Code Workspace Docs | <https://zeuikli.github.io/cc-workspace-docs/> | Claude Code 工作區與設定相關中文文件 |

## 這場投影片對應的資源

| 投影片概念 | 對應教學 |
|---|---|
| 工作守則寫進 `CLAUDE.md` / `AGENTS.md` | [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md) |
| 別給願望，給規格 | [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md) |
| 讓它先反問你 | [工作區指令檔與交辦模板](docs/05-工作守則與交辦模板.md#讓-agent-先反問你) |
| 給目錄，不要全文硬塞 | [NotebookLM 教學](docs/02-notebooklm.md) |
| 快取索引 | [NotebookLM-py 與進階自動化](docs/08-notebooklm-py.md) |
| Agent 會讀檔、改檔、跑程式 | [Agent CLI 工具](docs/03-agent-cli.md) |
| Git 是教材時光機，也是 agent 協作安全網 | [Git 與 GitHub](docs/04-git-github.md) |
| 把反覆摩擦封裝成工具箱 | [Skill 怎麼和 agent 合作寫](docs/06-skills.md) |
| Agent 接外部工具，包含接 NotebookLM | [MCP 怎麼接](docs/07-mcp.md) |
| 請它派分身去查 | [Subagent 怎麼用](docs/11-subagents.md) |
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
