# 06 Skill 怎麼寫

Skill 可以想成「可重複使用的工作手冊」。當你把某個流程跑順，例如「產生 A/B 版小考」或「檢查講義文字」，就可以把步驟、踩過的坑、QA 清單寫成 Skill。

投影片中的說法是：把跑順的流程變成「實驗室手冊」。以後遇到同類任務，agent 不必每次重新理解你的偏好，而是直接套用這份手冊。

## Skill 適合封裝什麼？

| 投影片中的工具箱 | 可以寫成的 Skill | 內容應包含 |
|---|---|---|
| 做投影片 | `teaching-slides` | 從規格產生投影片大綱、視覺檢查、講稿檢查 |
| 互動投影片轉 PDF | `interactive-slides-pdf` | 動畫截圖、書籤、PDF 可讀性、課後版本 QA |
| 參考資料快取索引 | `document-cache-index` | PDF 抽文字、quick notes、索引、全文引用規則 |
| 新工具產生器 | `teaching-tool-creator` | 先問需求、產生工作手冊、附測試與安全檢查 |
| 寫作審稿 | `teaching-writing-review` | 講義語氣、概念順序、學生誤解點、具體改寫 |
| 小考與解答版 | `teaching-quiz-review` | A/B 版對應、解答驗算、難度一致、人工檢查提醒 |

不適合封裝只做一次的任務。

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

先寫一個「教學工作守則」Skill，不要一開始就寫複雜自動化：

```markdown
---
name: teaching-assistant-rules
description: Use when helping prepare course material, quizzes, lecture notes, or student-facing resources.
---

# Teaching Assistant Rules

Always use Traditional Chinese.
Before editing more than 3 files, present a short plan.
For quizzes and answer keys, check correctness before polishing prose.
Do not handle student personal data or grades.
When requirements are unclear, ask up to 3 concrete questions before starting.
```

## Skill 跟工作守則的差別

| 類型 | 適合放什麼 |
|---|---|
| 工作守則 | 你每次都希望 AI 遵守的偏好與紅線 |
| Skill | 某一類任務的標準流程、模板、檢查表 |

可以先寫工作守則，等某個流程常常重複，再升級成 Skill。
