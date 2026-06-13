# 06 Skill 怎麼寫

Skill 可以想成「可重複使用的工作手冊」。當你把某個流程跑順，例如「產生 A/B 版小考」或「檢查講義文字」，就可以把步驟、踩過的坑、QA 清單寫成 Skill。

## Skill 適合封裝什麼？

- 固定格式的教案產生。
- 小考與解答版產生流程。
- 講義文字審稿流程。
- 互動教材轉 PDF 的檢查流程。
- 論文或教材資料夾建立快取索引的流程。

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
