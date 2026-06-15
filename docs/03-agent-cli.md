# 03 Agent 桌面版與 CLI 工具

Agent 是「會動手」的 AI 助手。它不只回答你，還能讀檔、改檔、跑指令、檢查結果。對只用過網頁版 AI 的老師，建議先用 Codex app 或 Claude Code desktop app 這類桌面版入口，熟悉後再進到 CLI。

投影片把 agent 拆成四個部分：

| 部分 | 意思 | 老師要做什麼 |
|---|---|---|
| 腦 | 模型負責推理與判斷 | 選一個可靠工具，不迷信單次輸出 |
| 手 | 工具負責讀檔、改檔、跑程式、查資料 | 先在副本或 Git 存檔點後動工 |
| 規矩 | 工作區指令檔與紅線 | 熟悉基本流程後，請主 agent 草擬課程慣例、格式、個資限制，再由老師確認是否存成 `CLAUDE.md` 或 `AGENTS.md` |
| 迴圈 | 觀察 → 動手 → 驗證 → 修正 | 要求它列計畫、執行、檢查，不只產出漂亮文字 |

## 先知道差別

| 類型 | 代表工具 | 能做什麼 |
|---|---|---|
| 網頁聊天 | ChatGPT、Claude.ai、Gemini | 回答、改寫、草擬 |
| 資料問答 | NotebookLM | 根據你上傳的來源回答 |
| 桌面版 agent | Codex app、Claude Code desktop app | 選本機資料夾、讀檔、改檔、看 diff / review |
| Agent CLI | Claude Code CLI、Codex CLI、Gemini CLI | 進階：用 terminal 跑指令、驗證、整合自動化 |

## 工具入口

| 工具 | 入口 | 適合誰 |
|---|---|---|
| Codex app | <https://developers.openai.com/codex/app> | 已使用 ChatGPT/OpenAI，想用桌面 app 選 project folder、Local 模式、review diff 的人 |
| Claude Code desktop app | <https://code.claude.com/docs/en/overview> | 想用 Claude Code 但不想一開始進 terminal 的人 |
| Claude Code CLI | <https://code.claude.com/docs/en/setup> | 進階：想用 Skill、MCP、subagent，把工作流程長期固定下來的人 |
| Codex CLI | <https://developers.openai.com/codex/cli> | 進階：已熟悉 terminal，想用命令列交辦檔案任務的人 |
| Gemini CLI | <https://github.com/google-gemini/gemini-cli> | 進階：想用 Gemini 長 context 或 Google 生態的人 |

## 安裝前置觀念

桌面版 agent 通常只需要安裝 app、登入帳號、選擇 project folder。CLI 則通常需要：

- Terminal：Windows 可用 PowerShell 或 Windows Terminal；macOS/Linux 用 Terminal。
- Node.js/npm：有些工具用 `npm` 或 `npx` 安裝。
- Git：方便管理教材版本。
- 登入或 API key：依工具不同，可能用網頁登入或 API key。

Node.js 入口：<https://nodejs.org/>

## 新手最小啟動檢查

先選一個工具，不要一次裝滿全部。建議順序：

1. 先用 GitHub Desktop 建立教材副本與第一個 commit。
2. 安裝並登入 Codex app 或 Claude Code desktop app。
3. 在 app 中選剛剛的教材資料夾。
4. 先請工具讀檔，不要改檔。
5. 做過幾次任務後，請主 agent 草擬 `AGENTS.md` 或 `CLAUDE.md`，用來固定長期規矩。

可用這個 prompt 當第一次驗證：

```text
請只閱讀目前資料夾。
先不要修改任何檔案，也不要執行會寫入的指令。
請列出你看到的檔案、這個資料夾可能的用途、以及你不確定的地方。
```

如果工具能正確列出檔案與用途，再進到下一節的交辦範例。

## 三平台提醒

### Windows

- 新手可先安裝 [Git for Windows](https://git-scm.com/download/win) 與 [GitHub Desktop](https://desktop.github.com/)。
- 若常跑 CLI 工具，建議使用 Windows Terminal。
- 需要 Linux 環境時再考慮 WSL，不要一開始就把所有工具都裝滿。

### macOS

- 可用內建 Terminal。
- 常見安裝方式會用 `npm` 或 Homebrew。
- 若不熟 Homebrew，先照官方文件走，不要混用太多部落格指令。

### Linux

- 使用系統套件管理器安裝 Git、Node.js。
- 注意不同 distribution 的套件版本可能偏舊。

## 桌面版第一次交辦範例

在一個只有測試資料的資料夾中啟動 agent，先做低風險任務：

```text
請先只讀取這個資料夾，不要修改任何檔案，也不要執行會寫入的指令。

請用三段回報：
1. 這份教材看起來在教什麼
2. 學生可能卡在哪裡
3. 如果要改善，你會建議改哪些檔案與原因
```

確認它讀對之後，再交辦修改：

```text
請只新增一段「快速開始」到 README。
修改前先列出你打算改哪個檔案與改動重點。
```

## 教師任務的標準流程

### 1. 先存檔或建立副本

如果教材已經在 Git repo 中，先確認乾淨狀態：

```bash
git status
```

如果還沒有 Git，至少先複製一份教材資料夾，不要在唯一版本上練習。新手可以先用 GitHub Desktop，不必一開始就學 terminal 指令。

### 2. 熟悉後再建立指令檔

做過幾次「只讀、列計畫、小修改、看 diff」後，請主 agent 根據實際合作摩擦草擬 `CLAUDE.md` 或 `AGENTS.md`；老師確認內容後再存檔。本次任務 prompt 只補目標、範圍與驗收標準。

### 3. 交規格，不交願望

```text
目標：請幫我改一份微積分講義，讓偏導數的幾何直觀更清楚。
範圍：只改第 2 節，不新增未教過的定理。
格式：保留原本 Markdown 結構與 LaTeX 數學式。
限制：不要碰學生資料；不要改其他章節。
驗收標準：學生能看出偏導數是固定另一個變數時的切線斜率。

動工前先反問我最多 3 個問題。
```

### 4. 先列計畫再改檔

要求 agent 先回報：

- 會讀哪些檔案。
- 會改哪些檔案。
- 每個檔案改什麼。
- 如何檢查結果。

### 5. 修改後要看 diff

如果是 Git repo：

```bash
git diff
```

請 agent 也用人話整理 diff：

```text
請用老師看得懂的方式摘要這次 git diff：
1. 哪些教學說法被改了？
2. 哪些數學式被改了？
3. 哪些地方需要我人工確認？
```

### 6. 驗證後才 commit / push

對應投影片的「觀察 → 動手 → 驗證 → 循環」：

新手優先用 GitHub Desktop 的 `Commit` 與 `Push origin`。熟悉 terminal 後，才把下面指令當參考：

```bash
git add .
git commit -m "Clarify partial derivative handout"
git push
```

`push` 是把已確認的修改同步給共同歷史，不是讓 agent 自己任意發布。

## 使用原則

- 一開始只在副本資料夾練習。
- 第一輪先用單次 prompt；熟悉後再請主 agent 把長期規矩整理成 `CLAUDE.md` / `AGENTS.md` 草稿。
- 修改超過 3 個檔案前，要求它先列計畫。
- 要求它跑驗證，不要只相信它說完成。
- 重要教材、解答、成績一定人工檢查。
- 讓 agent 改教材前，先建立 Git 存檔點。
- 讓 agent 說明 `git diff`，但最後由老師決定是否 commit。

## 什麼時候不要用 agent？

- 你只要問一句定義。
- 你不想讓工具碰本機檔案。
- 你正在處理學生個資或成績原始檔。
- 你不清楚它會改哪些檔案。
