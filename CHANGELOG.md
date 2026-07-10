# Changelog

本專案的所有重大變更記錄於此（格式參考 [Keep a Changelog](https://keepachangelog.com/zh-TW/1.0.0/)）。

## [1.1.3] - 2026-07-10

### Changed
- SKILL.md 補上 repo 絕對路徑（`~/Github/Projects/claude-notify-sounds/`）：從任意資料夾觸發時不用再猜 install.sh 在哪。
- 預設音效表格加註「僅為出廠預設，實際以 `~/.config/claude-notify-sounds/env` 為準」：避免使用者已客製音效時，照表格回答出錯誤資訊。

## [1.1.2] - 2026-07-10

### Changed
- **觸發詞精簡為「claude通知音效」**：移除「裝 Claude 音效 / 設定 Claude 音效 / claude sounds / 移除 Claude 音效」等別名，統一成單一觸發詞。動機：使用者全面收斂各 skill 觸發語、降低記憶負擔。功能與安裝流程完全不變（安裝／設定／移除仍在同一 skill 內）。

## [1.1.1] - 2026-07-09

### Changed
- 預設音效調整：完工（Stop）從 `Glass` 改為 **`Funk`**、需要你回應（Notification）從 `Funk` 改為 **`Morse`**。兩者辨識度更高、彼此更不易混淆，避免同一輪結束時聽起來像同一種音。僅調整 `config.example.env` 的預設值，既有安裝者的個人設定檔（`~/.config/claude-notify-sounds/env`）不受影響。

## [1.1.0] - 2026-06-30

### Removed
- 移除「**每次跑 bash**」時機（`PreToolUse(Bash)` hook、`notify-bash.sh`、`NOTIFY_BASH_*` 設定）。每跑一次指令就響太吵，且純音效情境下用處不大。現在只保留 **Stop（換你了）** 與 **Notification（需要你回應）** 兩個時機。

### Changed
- `install.sh` 改為只合併兩個 hook；文件 / 設定範本同步更新。
- `uninstall.sh` 仍會清掉舊版裝過的 `PreToolUse` bash hook（向後相容）。

## [1.0.1] - 2026-06-30

### Changed
- 文件用詞：Stop hook 的時機從「回答完畢」正名為「**換你了（這輪結束）**」，更貼近 Stop 的真實語意（主對話這輪做完、把控制權交還給你，含我用文字反問你的情況），避免被誤解成字面「答完一段話」。
- 純文件 / 註解調整，**行為與設定變數（`NOTIFY_DONE_*`）皆未變**，不影響既有安裝。

## [1.0.0] - 2026-06-29

### Added
- 初版發布。[claude-notify-hooks](https://github.com/chensoo8911/claude-notify-hooks) 的「純音效」精簡分支。
- `PreToolUse(Bash)` hook：每次跑 bash 播音效（預設 Frog）。
- `Stop` hook：回答完畢播音效（預設 Glass），含 `stop_hook_active` 連續觸發防護。
- `Notification` hook：需要你回應 / 批准時播音效（預設 Funk）。
- 三個 hook 一律**同步**播放、不掛 async（async 會在 afplay 播完前被收掉 → 聽不到）。
- `install.sh` / `uninstall.sh`：依賴檢查、symlink 到 `~/.claude/skills/`、用 `jq` 安全合併 / 移除 settings.json hook、idempotent。
- `config.example.env`：三個時機各自的開關 / 音效，改完即時生效。
- `SKILL.md`：可讓 Claude 使用者一句話觸發安裝。
- 僅支援 macOS。
