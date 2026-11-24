# Instructions for AI assistants

This repository holds the analysis and design documents of Group H. Start with [README.md](README.md).

## Do not read the cost files

- Do **not** open, read, search, quote or summarise [docs/function_list/cost.md](docs/function_list/cost.md) or
  anything in `docs/archive/` (a local-only folder, not on GitHub; the frozen workbook there holds the same figures).
- Requirements, diagrams, screens and decisions never need cost data. Work from
  [fr_list.md](docs/function_list/fr_list.md), which has no effort or money.
- Exception: the user asks for cost, effort, capacity or cash-flow work in so many words. Then read only the part of
  cost.md the task needs.
- When you search the repository, exclude these paths (for example `--glob '!docs/function_list/cost.md'
  --glob '!docs/archive/**'`).

## Rules when you edit

- Source of truth for FRs: [fr_list.md](docs/function_list/fr_list.md). Never create a separate file for new or changed
  FRs. After changing an FR, tell the user that [cost.md](docs/function_list/cost.md) needs a matching update by the
  cost owner; do not update it yourself unless asked.
- A changed decision needs a new row in [decision_index.md](docs/project/decision_index.md).
- File and folder names: lower-case snake_case, inside `docs/`. Folders follow the teacher's LabDesk example (D53):
  `project/`, `context/`, `use_case/`, `architecture/`, `activity/`, `function_list/`, `external_design/`. IDs inside documents stay upper case (`AD-UC-01`).
- Every mention of another file in the repository is a relative Markdown link that resolves.
- Documents are written in English; on-screen text is Vietnamese with diacritics.
