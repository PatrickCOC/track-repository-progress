# Track Repository Progress

將一組已授權 GitHub repositories 整理成一致、可追蹤的工作進度報告，並可在使用者明確要求後更新 Google Sheets。

這個 repository 包含可安裝的 ChatGPT／Codex Skill。Skill 不會自動取得 GitHub 或 Google Drive 權限，也不會自行擴大 repository 範圍。

## 功能

- 只分析使用者明確授權的 repositories
- 整理開始日期、目前階段、最近活動、已完成工作、下一步與風險
- 區分「已有證據」與「推斷」，避免把 README 計劃當成已完成工作
- 為每個進度判斷附上信心程度
- 產生 Markdown 摘要或 Google Sheets 相容表格
- 只有在使用者明確要求時才寫入 Google Sheets

## Repository 結構

```text
track-repository-progress/
├── README.md
└── skill/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── output-schema.md
        └── status-model.md
```

## 安裝

### ChatGPT Skills

1. 下載這個 repository：

   ```bash
   git clone https://github.com/PatrickCOC/track-repository-progress.git
   ```

2. 將 `skill` 資料夾壓縮成 ZIP。ZIP 的最上層必須直接看見 `SKILL.md`，不要多包一層 `skill/`。
3. 在 ChatGPT 的 **Skills** 頁面選擇新增／上傳 Skill，然後上傳該 ZIP。
4. 連接 GitHub；如要更新試算表，再連接 Google Drive。

### Codex 本機安裝

將 `skill` 資料夾複製至個人 skills 目錄，並命名為 `track-repository-progress`：

```text
<Codex skills directory>/track-repository-progress/SKILL.md
```

重新開啟一個工作階段後，即可用 `@track-repository-progress` 明確呼叫。實際個人 skills 目錄視你的 Codex 安裝方式而定。

## 使用方法

第一次使用時，請提供 repository allowlist。例如：

```text
使用 @track-repository-progress，只檢查以下 repositories：
- PatrickCOC/readbar
- PatrickCOC/game_price_comparison
- PatrickCOC/touch_fish

先產生報告，不要更新 Google Sheet。
```

常用指令：

```text
整理這些 repo 的開始日期、目前階段、最近進度、風險和下一步。
```

```text
比較這星期與上星期的 repository 進度，標示停滯項目。
```

```text
先預覽將會寫入的資料，得到我確認後才更新 Repository Progress Google Sheet。
```

## 建議 Google Sheet 欄位

| 欄位 | 用途 |
|---|---|
| Repository | `owner/name` |
| Project | 顯示名稱 |
| Start Date | 開始日期及判定依據 |
| Stage | Planning／Prototype／MVP／Beta／Production／Paused／Closed |
| Progress | 0–100 的保守估算 |
| Last Activity | 最近有證據的活動日期 |
| Completed | 已完成成果摘要 |
| Next Step | 最接近可執行的下一步 |
| Risks | 阻礙、成本或依賴 |
| Confidence | High／Medium／Low |
| Evidence | commit、PR、release 或文件連結 |
| Updated At | 報告產生時間 |

## 安全與限制

- Allowlist 以外的 repository 不會被探索或加入報告。
- Skill 預設只讀；更新 Sheet、建立 issue、修改 repo 等操作必須由使用者明確要求。
- 私有 repository 仍受已連接 GitHub 帳戶權限限制。
- Progress 是有依據的估算，不等同工時完成百分比。
- Commit 數量只代表活動，不代表品質或商業完成度。

