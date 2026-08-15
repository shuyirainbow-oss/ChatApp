# GitHub 登入與 Push 流程筆記

本專案的 GitHub repository：

```text
https://github.com/shuyirainbow-oss/ChatApp.git
```

目前專案根目錄是 Git repository，會一起管理：

```text
backend/
frontend/
README.md
前後端部署.md
```

`.venv/`、`python.venv/`、`__pycache__/` 與 `.env` 已由 `.gitignore` 排除，請不要手動加入這些檔案。

---

## 1. 第一次登入 GitHub（Git）

在 VS Code Terminal 開啟專案根目錄後，先確認 Git 已安裝：

```bash
git --version
```

設定提交紀錄顯示的名稱與 Email。這是 Git commit 的作者資訊，不是登入密碼：

```bash
git config --global user.name "Shuyirainbow"
git config --global user.email "shuyirainbow@gmail.com"
```

第一次執行 `git push` 時，Git 可能會跳出 GitHub 登入視窗。

1. 選擇 **Sign in with your browser**。
2. 在瀏覽器登入 GitHub 帳號 `shuyirainbow-oss`。
3. 按 **Authorize** 同意 Git Credential Manager 存取 GitHub。
4. 回到 Terminal，等待 push 完成。

登入成功後，Windows 的 Git Credential Manager 會記住授權，之後通常不必重複登入。

> 不要把 GitHub 密碼或 Personal Access Token 寫進程式、README 或 commit。

---

## 2. 第一次將專案推送到 GitHub

若是新的本機專案，於專案根目錄執行：

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/shuyirainbow-oss/ChatApp.git
git push -u origin main
```

本專案已完成以上設定。可用下列指令確認遠端位置：

```bash
git remote -v
```

預期會看到：

```text
origin  https://github.com/shuyirainbow-oss/ChatApp.git (fetch)
origin  https://github.com/shuyirainbow-oss/ChatApp.git (push)
```

---

## 3. 日後修改後的標準 Push 流程

每次修改完成，從專案根目錄執行：

```bash
git status
git add .
git commit -m "描述這次修改"
git push
```

例如修改聊天介面後：

```bash
git add frontend/style.css frontend/script.js
git commit -m "Improve chat interface"
git push
```

`git status` 的用途：

- 修改前：查看哪些檔案被改動。
- `git add` 後：確認準備提交的檔案。
- `git push` 後：應顯示 `working tree clean`，代表本機沒有未提交修改。

---

## 4. 先更新再 Push（多人協作時）

如果曾在 GitHub 網頁或其他電腦修改同一個 repository，先取得最新版本：

```bash
git pull origin main
```

確認沒有衝突後，再執行：

```bash
git add .
git commit -m "描述這次修改"
git push
```

若 Git 顯示衝突，先不要直接刪檔。打開 Git 標示的檔案，保留正確內容、移除衝突符號後，再 `git add`、`git commit`。

---

## 5. 常見問題

### `git is not recognized`

代表 Git 尚未安裝或沒有加入 PATH。安裝 Git for Windows 後，重新開啟 VS Code Terminal，再執行：

```bash
git --version
```

### `remote origin already exists`

代表遠端已設定，不需再次 `git remote add origin`。用以下指令確認：

```bash
git remote -v
```

若遠端網址真的填錯，才修改它：

```bash
git remote set-url origin https://github.com/shuyirainbow-oss/ChatApp.git
```

### `rejected` 或 `fetch first`

代表 GitHub 上有本機沒有的提交。先執行：

```bash
git pull origin main
```

處理完成後再 `git push`。不要隨意使用 `git push --force`，以免覆蓋 GitHub 上的版本。

### 忘記登入或授權失敗

再次執行：

```bash
git push
```

依照跳出的瀏覽器登入流程完成 GitHub 授權。若公司網路或瀏覽器登入受限，可在 GitHub 建立只含必要權限的 Personal Access Token，並在 Git 要求密碼時使用 Token；Token 不可儲存在專案檔案內。

---

## 6. 本專案的後續部署順序

```text
本機測試成功
    ↓
git add / commit / push 到 GitHub
    ↓
Render 連接 GitHub repository
    ↓
部署 backend、frontend，最後再加入資料庫
```

目前只完成 GitHub 程式碼保存；尚未部署 Render。
