# Output Schema

## Portfolio Summary

Include:

- reporting date and timezone;
- repositories reviewed;
- active, quiet, stale, paused and closed counts;
- strongest recent progress;
- most important shared risk;
- recommended portfolio-level focus.

## Repository Record

Use these fields in this order:

| Field | Required content |
|---|---|
| Repository | Exact `owner/name` |
| Project | Human-readable project name |
| Start Date | Absolute date plus basis |
| Stage | One stage from the status model |
| Activity | Active, Quiet, Stale, Paused or Closed |
| Progress | Conservative percentage or `Not estimable` |
| Last Activity | Date of latest meaningful evidence |
| Completed | Verified deliverables, not plans |
| Next Step | One to three concrete actions |
| Risks | Relevant current risks |
| Confidence | High, Medium or Low, with a short reason |
| Evidence | Direct URLs, commit IDs, PRs, releases or file paths |
| Updated At | Report generation timestamp |

## Markdown Presentation

Use a compact portfolio table, then add short project notes only where nuance is required. Avoid forcing long evidence lists into table cells.

## Google Sheets Behaviour

When updating an existing sheet:

1. Inspect sheet names, headers and existing repository identifiers.
2. Match rows by exact normalized `owner/name`, not display name.
3. Preserve unknown columns and formulas.
4. Update only the requested rows and fields.
5. Add a new row only for a repository on the explicit allowlist.
6. Write dates in `YYYY-MM-DD` unless the existing sheet uses another consistent format.
7. Keep evidence as clickable URLs when supported.
8. Report the exact tab and range changed.

If the user asks only for analysis, do not write to Google Sheets.
