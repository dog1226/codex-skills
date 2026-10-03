# codex-skills

個人的 Codex 工作流技能與全域規則，從 Claude Code 版本轉換而來。

## 內容

| 項目 | 用途 | 換電腦後能不能直接用 |
|---|---|---|
| `AGENTS.md` | 全域規則：個人偏好（繁體中文、完成率回報、畫圖說明）加 12 條開發規則 | ✅ |
| `skills/startup` | 開工：讀 Obsidian 駕駛艙回到上次進度，唯讀 | 需要 Obsidian 筆記 |
| `skills/shutdown` | 收工：更新駕駛艙、本機 git commit，不 push | 需要 Obsidian 筆記 |
| `skills/project-init` | 新專案起手式：AGENTS.md、git、.gitignore、Obsidian 資料夾 | ✅ |
| `skills/sync-dotfiles` | 用 chezmoi 把 Codex 設定備份到私有 repo | 需要 chezmoi |
| `skills/to-obsidian` | 把網站報告整理成 5W1H 的 Obsidian 筆記，只能 `$to-obsidian` 叫用 | 需要 Python 3 |

## 安裝

```
repo
├── AGENTS.md          ──copy──►  ~/.codex/AGENTS.md
└── skills/<name>/     ──copy──►  ~/.agents/skills/<name>/
```

PowerShell（Windows）：

```powershell
git clone https://github.com/<github-user>/codex-skills.git
cd codex-skills
New-Item -ItemType Directory -Force "$HOME\.agents\skills", "$HOME\.codex" | Out-Null
Copy-Item skills\* "$HOME\.agents\skills\" -Recurse -Force
Copy-Item AGENTS.md "$HOME\.codex\AGENTS.md"
```

- 技能位置 `~/.agents/skills` 是 Codex 官方文件列出的使用者層級位置。
- 全域 `~/.codex/AGENTS.md` 這個路徑**沒有**在技能文件裡確認過，安裝後請在 Codex 問一句「你讀到哪些全域規則？」確認有生效。
- 技能叫用：輸入 `$startup`、`$shutdown` 等，或直接說觸發詞（如「開工」）。`to-obsidian` 只接受 `$to-obsidian`。

## 要先改的地方

- `skills/sync-dotfiles/SKILL.md`：第一次執行時 Codex 會問你的 dotfiles repo 位置，必須是私有 repo。
- `startup`、`shutdown`：說明的是「Obsidian 駕駛艙」工作流，另一台電腦要先有對應的 Obsidian 筆記。

## 與 Claude Code 版本的差異

| 項目 | Claude Code | Codex |
|---|---|---|
| 全域規則檔 | `~/.claude/CLAUDE.md` | `~/.codex/AGENTS.md` |
| 技能位置 | `~/.claude/skills` | `~/.agents/skills` |
| 叫用 | `/skill-name` | `$skill-name` |
| 禁止自動觸發 | frontmatter `disable-model-invocation: true` | `agents/openai.yaml` 的 `policy.allow_implicit_invocation: false` |

此轉換尚未在 Codex 上實測。若發現技能沒被載入，先確認資料夾位置，再檢查 `SKILL.md` 開頭的 `name` 與 `description`。
