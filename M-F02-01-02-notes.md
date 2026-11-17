# Wireframe notes: M-F02-01-02 Report this review?

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Report confirmation dialog | Modal | “Báo cáo đánh giá?” · No reason field | FR-02-09 |
| 2 | Submit report | Primary button | “Báo cáo đánh giá” | FR-02-09, FR-02-21 |
| 3 | Cancel report | Secondary button | “Huỷ”; closes modal without saving report | FR-02-09 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/M-F02-01-02.png | Confirmation modal over dimmed S-F02-01 parent; no reason input | FR-02-09 |
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
| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: Should the confirmation body quote the selected review, or is a generic confirmation sufficient?] | Generic confirmation only; selected review remains visible behind the overlay. |
| 2 | [NEEDS CLARIFICATION: AD-UC-14 allows reporting own reviews, but UI conventions v0.7 says Report is for other readers’ reviews. Confirm which governs.] | Modal is available only from a Report action rendered on another reader’s review item. |
