# Wireframe notes: M-F02-01-02 Report this review?

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Report confirmation dialog | Modal | “Báo cáo đánh giá?” · Short confirmation, no reason field; the review text is not quoted, it stays visible behind the dimmed overlay (D22) | FR-02-09 |
| 2 | Submit report | Primary button | “Báo cáo đánh giá” | FR-02-09, FR-02-21 |
| 3 | Cancel report | Secondary button | “Huỷ”; closes modal without saving report | FR-02-09 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/M-F02-01-02.png | Confirmation modal over dimmed S-F02-01 parent showing another reader’s review behind; no reason input | FR-02-09 |
| Empty | Not applicable: confirmation modal has no list | — | — |
| Loading | Not applicable: no modal-level loading state is specified | — | — |
| Error | Not applicable: duplicate-report feedback is shown on parent S-F02-01 | FR-02-21 |
| Success | Not applicable: confirmation appears on parent S-F02-01 after modal closes | FR-02-09 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Báo cáo đánh giá | confirm report | stays on S-F02-01; report saved and success feedback shown |
| Huỷ | cancel | stays on S-F02-01; no report saved |

## Open questions

None. Decisions: see [decision-index.md](../../decision-index.md#m-f02-01-02).