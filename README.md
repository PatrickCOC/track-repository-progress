# Track Repository Progress

[繁體中文](#繁體中文) | [English](#english)

## 繁體中文

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

### 其他 AI Agent

這個 Skill 採用開放的 Agent Skills 結構。將完整 `skill` 資料夾複製到對應位置，並保留 `SKILL.md`、`references/` 和 `agents/` 的相對結構。

| Agent | Project-level | User-level |
|---|---|---|
| 通用 Agent Skills | `.agents/skills/track-repository-progress/` | `~/.agents/skills/track-repository-progress/` |
| Claude Code | `.claude/skills/track-repository-progress/` | `~/.claude/skills/track-repository-progress/` |
| Cursor | `.cursor/skills/track-repository-progress/` 或 `.agents/skills/track-repository-progress/` | `~/.cursor/skills/track-repository-progress/` 或 `~/.agents/skills/track-repository-progress/` |
| GitHub Copilot／VS Code | `.github/skills/track-repository-progress/` 或 `.agents/skills/track-repository-progress/` | `~/.copilot/skills/track-repository-progress/` 或 `~/.agents/skills/track-repository-progress/` |

安裝後，確認以下檔案存在：

```text
<agent skills directory>/track-repository-progress/SKILL.md
```

- **Claude Code**：輸入 `/track-repository-progress`，或直接要求 Claude 整理已授權 repositories。
- **Cursor**：在 Agent chat 輸入 `/` 並選擇這個 Skill；Cursor 亦可按描述自動使用它。
- **GitHub Copilot／VS Code**：在 Agent chat 以 `/track-repository-progress` 呼叫，或提出符合描述的 repository progress 任務。
- **其他兼容 Agent Skills 的工具**：使用 `.agents/skills/` 作為最通用位置；實際發現位置仍以該工具文件為準。
- **未支援 Agent Skills 的 agent**：將 `SKILL.md` 加入 agent 的 system instructions，並在需要時一併提供 `references/status-model.md` 和 `references/output-schema.md`。這種方式不會自動觸發，也不會自動提供 GitHub 或 Google Drive 權限。

## 使用方法

第一次使用時，請提供 repository allowlist。例如：

```text
使用 @track-repository-progress，只檢查以下 repositories：
- example-org/browser-tool
- example-org/product-catalog
- example-org/team-dashboard

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

---

## English

Turn an explicit allowlist of GitHub repositories into a consistent, trackable project progress report. The skill can also update Google Sheets when the user explicitly requests it.

This repository contains an installable ChatGPT/Codex skill. Installing the skill does not automatically grant access to GitHub or Google Drive, and the skill never expands the repository scope on its own.

## Features

- Analyze only repositories explicitly authorized by the user
- Track start dates, current stages, recent activity, completed work, next steps, and risks
- Separate verified evidence from inference, preventing roadmap plans from being reported as completed work
- Attach a confidence level to each progress assessment
- Produce Markdown summaries or Google Sheets-compatible records
- Write to Google Sheets only when explicitly requested

## Repository Structure

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

## Installation

### ChatGPT Skills

1. Download this repository:

   ```bash
   git clone https://github.com/PatrickCOC/track-repository-progress.git
   ```

2. Create a ZIP archive from the contents of the `skill` directory. `SKILL.md` must be visible at the top level of the ZIP; do not wrap it in an additional `skill/` directory.
3. Open the **Skills** page in ChatGPT, choose the add/upload option, and upload the ZIP.
4. Connect GitHub. Connect Google Drive as well if you want the skill to update a spreadsheet.

### Local Codex Installation

Copy the `skill` directory into your personal skills directory and name it `track-repository-progress`:

```text
<Codex skills directory>/track-repository-progress/SKILL.md
```

Open a new session, then invoke it explicitly with `@track-repository-progress`. The exact personal skills directory depends on how Codex was installed.

### Other AI Agents

This skill follows the open Agent Skills directory structure. Copy the complete `skill` directory to the location supported by your agent, preserving the relative structure of `SKILL.md`, `references/`, and `agents/`.

| Agent | Project-level | User-level |
|---|---|---|
| Generic Agent Skills | `.agents/skills/track-repository-progress/` | `~/.agents/skills/track-repository-progress/` |
| Claude Code | `.claude/skills/track-repository-progress/` | `~/.claude/skills/track-repository-progress/` |
| Cursor | `.cursor/skills/track-repository-progress/` or `.agents/skills/track-repository-progress/` | `~/.cursor/skills/track-repository-progress/` or `~/.agents/skills/track-repository-progress/` |
| GitHub Copilot / VS Code | `.github/skills/track-repository-progress/` or `.agents/skills/track-repository-progress/` | `~/.copilot/skills/track-repository-progress/` or `~/.agents/skills/track-repository-progress/` |

After copying the directory, verify that this file exists:

```text
<agent skills directory>/track-repository-progress/SKILL.md
```

- **Claude Code:** enter `/track-repository-progress`, or ask Claude to summarize progress for an explicit repository allowlist.
- **Cursor:** type `/` in Agent chat and select the skill. Cursor may also select it automatically when the request matches its description.
- **GitHub Copilot / VS Code:** invoke `/track-repository-progress` in Agent chat, or ask for a repository progress task that matches the skill description.
- **Other Agent Skills-compatible tools:** prefer `.agents/skills/` as the portable location, but confirm the discovery path in that tool's documentation.
- **Agents without Agent Skills support:** add `SKILL.md` to the agent's system instructions and provide `references/status-model.md` and `references/output-schema.md` when needed. This fallback does not provide automatic triggering or GitHub/Google Drive access.

## Usage

Provide a repository allowlist the first time you use the skill. For example:

```text
Use @track-repository-progress and inspect only these repositories:
- example-org/browser-tool
- example-org/product-catalog
- example-org/team-dashboard

Generate a report first. Do not update Google Sheets.
```

Common prompts:

```text
Summarize the start date, current stage, recent progress, risks, and next step for each repository.
```

```text
Compare this week's repository progress with last week's and flag stalled projects.
```

```text
Preview the proposed changes first. Update the Repository Progress Google Sheet only after I confirm them.
```

## Recommended Google Sheet Columns

| Column | Purpose |
|---|---|
| Repository | Exact `owner/name` identifier |
| Project | Human-readable project name |
| Start Date | Start date and the evidence used to determine it |
| Stage | Planning / Prototype / MVP / Beta / Production / Paused / Closed |
| Progress | Conservative estimate from 0 to 100 |
| Last Activity | Date of the latest meaningful evidence |
| Completed | Summary of verified deliverables |
| Next Step | Closest actionable next step |
| Risks | Current blockers, costs, or dependencies |
| Confidence | High / Medium / Low |
| Evidence | Commit, pull request, release, or document links |
| Updated At | Report generation time |

## Safety and Limitations

- Repositories outside the allowlist are never explored or added to the report.
- The skill is read-only by default. Updating a sheet, creating an issue, or modifying a repository requires an explicit user request.
- Access to private repositories remains limited by the connected GitHub account's permissions.
- Progress is an evidence-based estimate, not a percentage of engineering hours completed.
- Commit volume indicates activity, not quality or commercial readiness.
