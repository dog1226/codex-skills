---
name: shutdown
description: 收工（shutdown）。對話結束前，把今天的工作存進 GDrive / Obsidian / 本機 git，確保換電腦能無縫接續。當使用者說「收工」、「下班」、「換電腦繼續做」時使用。本質是寫：會在本機 git commit（不 push）、改工作筆記。
---

# 收工（shutdown）

## 做什麼

對話結束前，把今天的工作存進 GDrive / Obsidian / 本機 git，確保換電腦能無縫接續。

**觸發詞：** 收工、下班、換電腦繼續做

## 本質：寫

**會在本機 git commit、會改工作筆記；不推 GitHub。** 這個技能負責「把今天的成果寫進去」，與開工（startup）成對：開工讀出來、收工寫進去，永不重疊。

## 動作

依序執行：

1. **盤點今天做了什麼** — 整理本次對話完成的工作項目與重要決策。
2. **更新 Obsidian 駕駛艙** — 在此專案的 Obsidian 駕駛艙筆記更新「上次做到哪」與「最近更動紀錄」，讓下次開工能直接讀到。
3. **git add + commit（只在本機）** — 把改動 commit 到本機 git。commit message 使用繁體中文，且不要加 Co-Authored-By 行。

## 注意

- ⛔ **不准 `git push`，也不要建議 push 或建立 GitHub repo。** 使用者要求收工只留在本機版控。
- commit 前先 `git status` 確認改動範圍，避免把不該進版控的檔案帶進去。
- GDrive 與 Obsidian 要對得上，換電腦時才能無縫接續。
- 與 startup 互斥：收工才寫，開工只讀。
