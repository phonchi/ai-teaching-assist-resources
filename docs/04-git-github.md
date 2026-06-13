# 04 Git 與 GitHub

投影片把 Git 比喻成教材的「存檔點」與「時光機」。GitHub 則是把這些存檔放到雲端，讓學生、助教、同事能讀取或協作。

## 工具入口

| 工具 | 入口 | 用途 |
|---|---|---|
| Git | <https://git-scm.com/downloads> | 本機版本控制 |
| GitHub | <https://github.com/> | 雲端 repo、協作、公開資源 |
| GitHub Desktop | <https://desktop.github.com/> | 圖形化操作 GitHub |
| GitHub Pages | <https://docs.github.com/en/pages> | 把 repo 發布成網站 |

## GitHub 最小流程

1. 到 <https://github.com/new> 建立 repo。
2. 勾選 `Add a README file`。
3. 在 README 寫資源頁內容。
4. 按 `Commit changes` 存檔。
5. 複製 repo 連結給學員。

這樣就已經是一個可用的課後資源頁。

## 如果用 GitHub Desktop

1. 安裝 <https://desktop.github.com/>。
2. 登入 GitHub。
3. 選 `File > New repository`。
4. 建立 repo，加入 README。
5. 按 `Publish repository` 上傳到 GitHub。

適合不熟 terminal 的老師或學員。

## 如果用 terminal

```bash
git init
git add README.md docs/
git commit -m "Add teaching assist resources"
git branch -M main
git remote add origin https://github.com/<your-name>/<repo-name>.git
git push -u origin main
```

把 `<your-name>` 與 `<repo-name>` 換成你的 GitHub 帳號與 repo 名稱。

## GitHub Pages 最小發布

1. 進 repo 的 `Settings`。
2. 找到 `Pages`。
3. Source 選 `Deploy from a branch`。
4. Branch 選 `main` 與 `/root`。
5. 儲存後等待 GitHub 產生網址。

如果你的內容只有 README 與 Markdown 文件，GitHub repo 頁面本身通常就夠用；不一定要開 Pages。

## 建議 commit 節奏

每次完成一個小段落就存檔：

```bash
git add .
git commit -m "Add NotebookLM tutorial"
```

不要等到所有檔案都改完才 commit。小存檔比較容易回頭，也比較容易找出哪次改壞。
