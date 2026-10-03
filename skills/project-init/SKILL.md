---
name: project-init
description: 專案初始化（project-init）。新專案的標準起手式，把 AGENTS.md、git、GitHub 私有 repo、Obsidian 資料夾、三處同步對照表一次建好。當使用者說「初始化專案」、「新專案」、「開新專案」、「建專案」時使用。本質是寫：會建檔、git init、開 GitHub repo、改對照表。
---

# 專案初始化（project-init）

## 做什麼

新專案的標準起手式，把專案在三個家（GDrive / Obsidian / GitHub）都設好，確保之後開工（startup）／收工（shutdown）能順利接續。

**觸發詞：** 初始化專案、新專案、開新專案、建專案

## 本質：寫

**會建檔、git init、開 GitHub repo、改三處對照表。** 與開工成對的「建立階段」，做完後此專案才能進入日常的開工讀／收工寫循環。

## 動作

依序執行，每一步完成後回報再進行下一步：

1. **建 AGENTS.md** — 在專案根目錄建立 AGENTS.md（可從全域 AGENTS.md（~/.codex/AGENTS.md）帶入 12 條規則與個人偏好）。
2. **git init + 建 .gitignore** — 初始化 git，並依專案語言/框架建立合適的 .gitignore。
3. **開 GitHub 私有 repo** — （使用者說「只做本機 git」就跳過此步）建立同名私有 repo 並設為遠端 origin（用 `gh repo create`）。
4. **建 Obsidian 對應資料夾** — 在 Obsidian vault 中建立此專案對應的工作筆記資料夾（含「駕駛艙」筆記）。
5. **回填三處同步對照表** — 在 GDrive / Obsidian / GitHub 三處的同步對照表登記此專案，確保三個家彼此對得上。

## 注意

- 完成後輸出一份對照表，列出每一步的產出位置（repo URL、Obsidian 資料夾、對照表項目）。
- commit message 使用繁體中文，且不要加 Co-Authored-By 行。
- 與 startup / shutdown 屬同一套工作流：初始化建立、開工讀、收工寫。
