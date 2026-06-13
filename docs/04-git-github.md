# 04 Git 與 GitHub：教材的存檔點與 agent 協作安全網

投影片裡的 Git 不是只為了「把 README 放上 GitHub」。它真正解決的是老師開始讓 agent 動手改教材後的安全問題：

- agent 改壞了，怎麼回到上一版？
- 助教和老師同時改，怎麼避免互相覆蓋？
- 網站或講義出問題，怎麼知道是哪一次修改造成的？
- 一學期改了很多次，怎麼留下教材修改日誌？

Git 就是教材的「存檔點」與「時光機」；GitHub 則讓這份修改歷史可以被老師、助教、agent 共同使用。

## 工具入口

| 工具 | 入口 | 在這場投影片中的角色 |
|---|---|---|
| Git | <https://git-scm.com/downloads> | 本機版本控制：每次修改都能存檔、比較、回復 |
| GitHub | <https://github.com/> | 雲端協作：老師、助教、agent 共用同一份修改歷史 |
| GitHub Desktop | <https://desktop.github.com/> | 圖形介面：不熟 terminal 也能 commit、push、看差異 |
| GitHub Pages | <https://docs.github.com/en/pages> | 延伸用途：教材網站可從 GitHub 自動上線 |

## 投影片中的版本控制流程

傳統做法是手動上傳檔案，覆蓋舊版。問題是：

- 改壞了難救回。
- 助教同時改會互相覆蓋。
- 出問題時不知道是哪一次修改造成的。

版本控制流程改成：

```text
你說「把這章更新推上去」
修改前先建立乾淨起點
agent 修改教材
Git 建立存檔點
GitHub 保存修改歷史
網站或資源頁自動更新
```

每一次修改都留下紀錄，等於自動產生一份「教材修改日誌」。

## 三個核心價值

| 投影片用語 | 白話意思 | 教學情境 |
|---|---|---|
| 可協作 | 多人接力，不互相覆蓋 | 老師、助教、agent 都能在同一份教材上工作 |
| 可追溯 | 能找出哪次修改造成問題 | 學生回報講義錯誤時，可以查是哪次改壞 |
| 可回溯 | 能回到上一個好版本 | agent 改壞排版或公式時，可以復原 |

## 和 agent 協作的安全流程

### 1. 先建立乾淨起點

在開始交給 agent 修改前，先存一版：

```bash
git status
git add .
git commit -m "Save clean course material before agent edits"
```

這個 commit 就是「改壞也回得去」的起點。

### 2. 讓 agent 先列計畫

交辦時不要直接說「幫我改講義」。改成：

```text
請先閱讀這份講義與 README。
先不要修改檔案。
請列出你打算修改哪些檔案、每個檔案要改什麼、以及要如何檢查結果。
```

### 3. 修改後先看差異

Agent 改完後，不要直接上傳。先看差異：

```bash
git diff
```

如果用 GitHub Desktop，就看 `Changes` 畫面。

### 4. 檢查後再存檔

確認內容合理後再 commit：

```bash
git add .
git commit -m "Revise chain rule handout with agent"
```

Commit 訊息請寫「這次改了什麼」，不要只寫 `update`。

### 5. 推送到 GitHub

```bash
git push
```

這一步不是單純「放上 GitHub」，而是把這次教材修改同步到共同歷史，方便助教接手、網站部署、日後追查。

## 如果 agent 改壞了怎麼辦？

先看有哪些檔案被改：

```bash
git status
```

看具體差異：

```bash
git diff
```

如果還沒 commit，可以請 agent 根據 `git diff` 修正，或人工只保留好的部分。若已經 commit，先不要慌，Git 的重點就是每個存檔點都還在。新手建議先不要自行刪歷史，請有經驗的人協助回復到指定 commit。

## GitHub Pages 是延伸，不是主軸

GitHub Pages 可以把教材網站自動上線，對應投影片中的「改完自動上線，學生即刻看到最新版」。

但這是版本控制之後的延伸。先有 Git 的存檔點與修改歷史，才有安全的自動上線。

最小發布流程：

1. 進 repo 的 `Settings`。
2. 找到 `Pages`。
3. Source 選 `Deploy from a branch`。
4. Branch 選 `main` 與 `/ (root)`。
5. 儲存後等待 GitHub 產生網址。

Pages 需要 repo 裡有可發布的首頁，例如 `README.md`、`index.html`，或之後再接靜態網站工具。新手先確認 Git 修改歷史乾淨，再處理自動上線。

## 給老師的日常口令

可以直接對 agent 說：

```text
請先檢查 git status。
如果工作區不乾淨，先告訴我有哪些尚未存檔的修改。
接著閱讀講義，提出修改計畫。
修改後請列出 git diff 摘要與需要我人工確認的地方。
不要自行 push，等我確認。
```

這樣 Git 就不是工程師專用工具，而是老師放心和 agent 協作的安全網。
