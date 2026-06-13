# 06 Skill 怎麼和 agent 合作寫

Skill 可以想成「可重複使用的工作手冊」。重點不是老師自己從零寫一份工程文件，而是你和 agent 合作幾次後，把已經跑順、或反覆卡住的流程整理成 Skill 草稿，再由老師審查。

投影片中的說法是：把跑順的流程變成「實驗室手冊」。以後遇到同類任務，agent 不必每次重新理解你的偏好，而是直接套用這份手冊。

## 什麼時候該寫 Skill？

不要第一天就寫 Skill。先用 `CLAUDE.md` / `AGENTS.md` 固定全域規矩，再在對話中觀察摩擦。適合封裝的時機：

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

概念相同：把可重複流程寫成清楚的 instructions，讓 Codex 在相關任務自動載入。

## 寫 Skill 的原則

- 請 agent 先根據最近一次成功任務產生 Skill 草稿，老師再審。
- `description` 要寫「什麼情境使用」，不要只寫功能名稱。
- Workflow 要可執行，不要寫抽象口號。
- 把「不要做什麼」寫清楚，例如不碰學生個資。
- 對關鍵產出加入 QA 清單。
- 如果有固定檔案格式，放到 `templates/`。
- 如果有固定檢查程式，放到 `scripts/`。
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

當一次合作出現明顯摩擦時，可以直接對 agent 說：

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

Agent 可能整理出這樣的 `SKILL.md` 草稿：

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

老師審過草稿後，再決定是否安裝成真正 Skill。

## Skill 跟工作守則的差別

| 類型 | 適合放什麼 |
|---|---|
| `CLAUDE.md` / `AGENTS.md` | 這個教材工作區每次都要遵守的偏好與紅線 |
| Skill | 某一類任務才需要的標準流程、模板、檢查表 |

先把全域規矩寫進 `CLAUDE.md` / `AGENTS.md`。等某個任務反覆出現摩擦，再請 agent 幫你封裝成 Skill 草稿。
