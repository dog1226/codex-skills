# codex-skills

這是 **dog1226 個人的** Codex 全域規則與工作流技能，從他自己的 Claude Code 設定轉換而來。

> ⚠️ **這些是別人的偏好，不是通用設定。**
> 裝了之後，你的 Codex 會改變行為（例如一律用繁體中文回答、每次回報完成率百分比、commit 不加共同作者）。
> 安裝前請先看過完整內容，確認每一項你都想要，再決定要不要裝。

## 給 Codex 的安裝指示（推薦）

把下面這段貼給你的 Codex，讓它帶你確認後再安裝：

```text
請幫我安裝 https://github.com/dog1226/codex-skills 這個 repo，照這個順序，每一步都等我回答再繼續：
1. 直接執行 git clone https://github.com/dog1226/codex-skills.git 到暫存資料夾。不要上網搜尋這個 repo：
   網路上有名稱相同、但擁有者不同的 repo（例如 arumaekawa/codex-skills），擁有者必須是 dog1226。
2. 把將要安裝的每個檔案「完整內容」顯示給我看（AGENTS.md 和 skills 底下每個 SKILL.md），並用白話告訴我：
   這些是別人的個人偏好，安裝後你（Codex）的行為會有哪些改變。
3. 檢查 ~/.codex/AGENTS.md 和 ~/.agents/skills/ 是否已有同名檔案。有的話先備份，再問我要「附加」、「取代」還是「跳過」，不要自己決定。
4. 等我明確說「確認安裝」才複製檔案，不要提前動手。
5. 裝完告訴我複製了哪些檔案、放在哪裡，以及怎麼移除。
```

## 內容

| 項目 | 用途 | 要先知道的 |
|---|---|---|
| `AGENTS.md` | 全域規則：個人偏好（繁體中文、完成率回報、畫圖說明、commit 習慣）加 12 條開發規則 | 會影響 Codex 所有回答，裝之前一定要看 |
| `skills/startup` | 開工：讀 Obsidian「駕駛艙」筆記回到上次進度，唯讀 | 需要有 Obsidian 筆記，沒有就用不到 |
| `skills/shutdown` | 收工：更新駕駛艙、本機 git commit，不 push | 同上；會 commit |
| `skills/project-init` | 新專案起手式：AGENTS.md、git、.gitignore、Obsidian 資料夾、GitHub 私有 repo、三處同步對照表 | 流程是作者個人的，會建 GitHub repo |
| `skills/sync-dotfiles` | 用 chezmoi 把 Codex 設定備份到私有 repo | 需要 chezmoi，且 repo 必須是私有 |
| `skills/to-obsidian` | 把網站報告整理成 5W1H 的 Obsidian 筆記 | 需要 Python 3；只能用 `$to-obsidian` 叫用 |

## 手動安裝

```
repo
├── AGENTS.md          ──copy──►  ~/.codex/AGENTS.md
└── skills/<name>/     ──copy──►  ~/.agents/skills/<name>/
```

先檢查有沒有同名檔案，**有的話不要直接複製**，會被蓋掉：

```powershell
Test-Path "$HOME\.codex\AGENTS.md"          # True 代表你已經有自己的全域規則
Get-ChildItem "$HOME\.agents\skills"        # 看有沒有同名技能
```

沒有同名才安裝：

```powershell
git clone https://github.com/dog1226/codex-skills.git
cd codex-skills
New-Item -ItemType Directory -Force "$HOME\.agents\skills", "$HOME\.codex" | Out-Null
Copy-Item skills\* "$HOME\.agents\skills\" -Recurse
Copy-Item AGENTS.md "$HOME\.codex\AGENTS.md"
```

已經有 `AGENTS.md` 的話，先備份，再用 `Add-Content` 把內容附加在後面，或只挑你要的幾條貼進去。

## 移除

刪掉 `~/.agents/skills/` 底下上表列出的資料夾，以及（如果你是整份複製的）`~/.codex/AGENTS.md`，重開 Codex。

## 使用

- 叫用：輸入 `$startup`、`$shutdown` 等，或直接說觸發詞（如「開工」）。
- `to-obsidian` 只接受 `$to-obsidian`，不會自動觸發。

## 與 Claude Code 版本的差異

| 項目 | Claude Code | Codex |
|---|---|---|
| 全域規則檔 | `~/.claude/CLAUDE.md` | `~/.codex/AGENTS.md` |
| 技能位置 | `~/.claude/skills` | `~/.agents/skills` |
| 叫用 | `/skill-name` | `$skill-name` |
| 禁止自動觸發 | frontmatter `disable-model-invocation: true` | `agents/openai.yaml` 的 `policy.allow_implicit_invocation: false` |

## 測試狀況（2026-10-03，Codex CLI 0.160.0，Windows）

| 項目 | 結果 |
|---|---|
| 全域規則 `~/.codex/AGENTS.md` 有被讀到 | ✅ |
| 4 個工作流技能出現在技能清單 | ✅ |
| `$to-obsidian` 明確叫用可載入、不會自動觸發 | ✅ |
| 說「開工」會自動套用 startup | ✅ |
| 技能完整流程（讀 Obsidian、commit 等）跑完一遍 | ⚠️ 未驗證。非互動模式下 Codex 會擋下所有 shell 指令，要在桌面版互動確認 |
