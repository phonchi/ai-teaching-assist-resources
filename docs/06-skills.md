# 06 Skill 怎麼和 agent 合作寫

Skill 可以想成「可重複使用的工作手冊」。重點不是老師自己從零寫一份工程文件，而是你和主 agent 合作幾次後，請主 agent 把已經跑順、或反覆卡住的流程整理成 Skill 草稿，再由老師審查內容。是否安裝成真正 Skill，等熟悉基本流程後再處理。

> 進階提醒：Skill 不是第一天要做的事，也不是每位老師要手寫的檔案。老師只需要指出「哪個流程一直卡住」；主 agent 可以先整理草稿，是否安裝等熟悉後再決定。

投影片中的說法是：把跑順的流程變成「實驗室手冊」。以後遇到同類任務，agent 不必每次重新理解你的偏好，而是直接套用這份手冊。

## 什麼時候該寫 Skill？

不要第一天就寫 Skill。先用單次 prompt 與桌面版 agent 跑幾次安全任務，再請主 agent 幫你整理 `CLAUDE.md` / `AGENTS.md` 草稿固定全域規矩，最後才考慮把反覆摩擦的流程封裝成 Skill。適合封裝的時機：

- 同一類任務已經做了 2-3 次，例如 A/B 版小考、講義審查、互動教材轉 PDF。
- 對話中一直出現摩擦，例如 agent 忘記先問、改太多檔、漏驗算、A/B 版難度不一致。
- 某個流程有固定步驟、固定檢查表、固定踩坑。
- `/insights` 或回顧 prompt 明確指出「這段流程可以固定下來」。
- 你希望下次不用再口頭重教同一套流程。

## Skill 適合封裝什麼？

| 投影片中的工具箱 | 可以寫成的 Skill | 內容應包含 |
|---|---|---|
| 做投影片 | `teaching-slides` | 從規格產生投影片大綱、視覺檢查、講稿檢查 |
| 互動投影片轉 PDF | `interactive-slides-pdf` | 動畫截圖、書籤、PDF 可讀性、課後版本 QA |
| 參考資料快取索引 | `document-cache-index` | PDF 抽文字、quick notes、索引、全文引用規則 |
| 新工具產生器 | `teaching-tool-creator` | 先問需求、產生工作手冊、附測試與安全檢查 |
| 寫作審稿 | `teaching-writing-review` | 講義語氣、概念順序、學生誤解點、具體改寫 |
| 小考與解答版 | `teaching-quiz-review` | A/B 版對應、解答驗算、難度一致、人工檢查提醒 |

不適合封裝只做一次的任務，也不適合拿來放所有通用偏好；通用偏好應放在 `CLAUDE.md` / `AGENTS.md`。

## Claude Code Skill 入口

官方文件：<https://code.claude.com/docs/en/skills>

下面是 Skill 草稿的結構示意，不是要求老師現場手寫。

典型結構：

```text
my-teaching-skill/
  SKILL.md
  scripts/
  templates/
```

最小 `SKILL.md` 範例：

```markdown
---
name: teaching-quiz-review
description: Use when reviewing quiz questions, answer keys, or multi-version exam drafts for a course.
---

# Teaching Quiz Review

## Workflow

1. Read the quiz questions and answer key.
2. Check whether every question has a clear learning target.
3. Verify calculations and answer choices.
4. Compare A/B versions for matching difficulty.
5. Report issues first, then suggest exact rewrites.

## Safety

- Do not process student names, IDs, grades, or private records.
- If a claim depends on a textbook or handout, say what source must be checked.
- Never say the quiz is correct without verification evidence.
```

## Codex Skill 入口

官方文件：<https://developers.openai.com/codex/skills>

概念相同：把可重複流程寫成清楚的 instructions，讓 Codex 在相關任務自動載入。一般老師只需要確認「這份流程是不是符合我的教學習慣」。

## 老師審 Skill 草稿的重點

- 請主 agent 先根據最近一次成功任務產生 Skill 草稿，老師再審。
- `description` 要寫「什麼情境使用」，不要只寫功能名稱。
- Workflow 要可執行，不要寫抽象口號。
- 把「不要做什麼」寫清楚，例如不碰學生個資。
- 對關鍵產出加入 QA 清單。
- 如果有固定檔案格式，之後可以放到 `templates/`。
- 如果有固定檢查程式，之後可以放到 `scripts/`。
- 如果流程會修改教材，要求先檢查 Git 狀態並在完成後摘要 diff。

## 一個比較貼近投影片的 Skill 範例

```markdown
---
name: course-material-agent-review
description: Use when an agent helps revise lecture notes, quizzes, answer keys, or course websites.
---

# Course Material Agent Review

## Workflow

1. Check whether the work is in a copy or a Git repo with a clean save point.
2. Read the teacher's goal, scope, format, constraints, examples, and acceptance criteria.
3. If requirements are unclear, ask up to 3 concrete questions before editing.
4. Present a short edit plan before changing files.
5. After editing, summarize the content changes and the files changed.
6. For math, answers, dates, links, and student-facing claims, list what the teacher must verify.

## Safety

- Do not process student names, IDs, grades, or private records.
- Do not push or publish without explicit teacher confirmation.
- Do not say the material is correct without verification evidence.
```

## 教學 Skill 起手題

當一次合作出現明顯摩擦時，老師可以直接對主 agent 說：

```text
我們剛剛處理 A/B 版小考時，反覆卡在難度對應、答案驗算、以及修改前沒有先列計畫。
請根據這次合作，幫我整理一份 Skill 草稿。
請包含：
1. 什麼情境會觸發這個 Skill
2. 每次要照做的 workflow
3. 常見踩坑
4. QA 檢查清單
5. 不可碰的紅線
先輸出草稿，不要直接安裝。
```

主 agent 可能整理出這樣的 `SKILL.md` 草稿。這是草稿範例，不是老師必須手寫的內容：

```markdown
---
name: teaching-quiz-version-review
description: Use when creating or reviewing A/B quiz versions, answer keys, or practice questions for a course.
---

# Teaching Quiz Version Review

## Workflow

1. Read the teacher's target chapters, question count, allowed formats, and time limit.
2. Ask up to 3 clarifying questions before drafting if difficulty, format, or answer-key requirements are unclear.
3. Draft A/B versions with matched learning targets and similar difficulty.
4. Verify every answer key before polishing wording.
5. Report possible ambiguity, over-scope content, and items the teacher must manually check.

## Safety

- Do not handle student names, IDs, grades, or private records.
- Do not claim the answer key is correct without showing verification evidence.
- Do not publish or push files without explicit teacher confirmation.
```

老師審過草稿後，再決定是否要安裝成真正 Skill；第一天只要保留草稿即可。

## Skill 跟工作守則的差別

| 類型 | 適合放什麼 |
|---|---|
| `CLAUDE.md` / `AGENTS.md` | 這個教材工作區每次都要遵守的偏好與紅線 |
| Skill | 某一類任務才需要的標準流程、模板、檢查表 |

先請主 agent 草擬 `CLAUDE.md` / `AGENTS.md`，固定全域規矩。等某個任務反覆出現摩擦，再請主 agent 整理 Skill 草稿；是否安裝等熟悉後再決定。
