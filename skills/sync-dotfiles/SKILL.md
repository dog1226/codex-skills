---
name: sync-dotfiles
description: 同步設定（sync-dotfiles）。把本機改過的 Codex 設定（全域 AGENTS.md、skills）用 chezmoi 吸回 source 並 push 到 GitHub 私有 repo，之後換電腦能還原。當使用者說「同步設定」、「推設定」、「sync dotfiles」、「同步 dotfiles」、「設定推上去」時使用。本質是寫：會 chezmoi re-add + git push。
---

# 同步設定（sync-dotfiles）

## 做什麼

把本機改過的 Codex 設定吸回 chezmoi source，commit 並 push 到 GitHub，讓設定可跨電腦還原。

**觸發詞：** 同步設定、推設定、sync dotfiles、同步 dotfiles、設定推上去

> 區分：收工（shutdown）= 推「專案」的工作成果到專案 repo；本 skill = 推「設定層」的 Codex 設定到 dotfiles repo。

## 本質：寫

會 `chezmoi re-add` + `git commit` + `git push`。納管範圍只有工作流：`~/.codex/AGENTS.md` 與 `~/.agents/skills/` 底下的 `startup` / `shutdown` / `project-init` / `sync-dotfiles` 等 skill。

## 前提

- 已安裝 chezmoi 與 git，且 dotfiles repo 已用 `chezmoi init` 建好（source 預設在 `~/.local/share/chezmoi`，Windows 為 `%USERPROFILE%\.local\share\chezmoi`）。
- dotfiles repo 必須是 **私有** repo。第一次使用時先問使用者 repo 位置（`<github-user>/dotfiles`），不要猜。
- chezmoi 可能不在 PATH，找不到時問使用者安裝位置，不要自己亂找。

## 動作

依序執行：

1. **chezmoi re-add** — 把本機對納管檔案的改動吸回 source。
2. **檢查 diff** — 在 chezmoi source 目錄跑 `git status -s`，把要 commit 的內容回報。若沒有改動就停下，告知「設定已是最新」。
3. **確認沒有帳密** — 掃一次 diff，看到金鑰、token、密碼類字串就停下，不要 commit。
4. **commit + push** — `git add -A` → `git commit`（訊息用繁體中文、不加 Co-Authored-By）→ `git push`。
5. **回報** — 印出 commit 摘要與遠端 dotfiles repo 已更新。

## 還原（換電腦時，非本 skill 範圍，供參考）

`chezmoi init --apply <github-user>/dotfiles`
