# Instructions for AI assistants

This repository holds the analysis and design documents of Group H. Start with [README.md](README.md).

## Do not read the cost files

- Do **not** open, read, search, quote or summarise [docs/function-list/cost.md](docs/function-list/cost.md) or
  anything in `docs/archive/` (a local-only folder, not on GitHub; the frozen workbook there holds the same figures).
- Requirements, diagrams, screens and decisions never need cost data. Work from
  [fr-list.md](docs/function-list/fr-list.md), which has no effort or money.
- Exception: the user asks for cost, effort, capacity or cash-flow work in so many words. Then read only the part of
  cost.md the task needs.
- When you search the repository, exclude these paths (for example `--glob '!docs/function-list/cost.md'
  --glob '!docs/archive/**'`).

## Rules when you edit

- Source of truth for FRs: [fr-list.md](docs/function-list/fr-list.md). Never create a separate file for new or changed
  FRs. After changing an FR, tell the user that [cost.md](docs/function-list/cost.md) needs a matching update by the
  cost owner; do not update it yourself unless asked.
- A changed decision needs a new row in [decision-index.md](docs/project/decision-index.md).
- File and folder names: lower-case words joined by hyphens (`fr-list.md`, `ad-uc-01.md`), inside `docs/` (D54).
  Folders follow the teacher's LabDesk example (D53):
  `project/`, `context/`, `use-case/`, `architecture/`, `activity/`, `function-list/`, `external-design/`. IDs inside documents stay upper case (`AD-UC-01`).
- Every mention of another file in the repository is a relative Markdown link that resolves.
- Documents are written in English; on-screen text is Vietnamese with diacritics.
