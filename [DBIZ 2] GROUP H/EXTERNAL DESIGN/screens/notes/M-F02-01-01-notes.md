# Wireframe notes: M-F02-01-01 Delete your review?

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Confirmation dialog | Modal | “Xoá đánh giá?” · Confirms removal of the reader’s own review from public display | FR-02-04 |
| 2 | Confirm deletion | Destructive button | “Xoá đánh giá”; trash icon before label | FR-02-04 |
| 3 | Cancel deletion | Secondary button | “Huỷ”; closes modal without changing review | FR-02-04 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/M-F02-01-01.png | Confirmation modal over dimmed S-F02-01 parent showing the reader’s own review behind; also reused from S-F02-02 | FR-02-04 |
| Empty | Not applicable: a confirmation modal has no list | — | — |
| Loading | Not applicable: no loading state is defined for this confirmation modal | — | — |
| Error | Not applicable: no modal-level error state is defined; errors belong to the parent screen | — | — |
| Success | Not applicable: confirmation closes the modal and success appears on the parent screen | FR-02-12 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Xoá đánh giá | confirm | stays on S-F02-01 or S-F02-02; review removed from public display and list refreshed |
| Huỷ | cancel | stays on S-F02-01 or S-F02-02; review remains visible |

## Open questions
| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: Does the modal need to identify the selected review text before confirmation?] | Show a concise action confirmation only; the selected review is visible behind the overlay. |
| 2 | [NEEDS CLARIFICATION: Confirm cancel button label “Huỷ” (per UI conventions) vs. “Keep review” (per guidance).] | Use “Huỷ” consistent with UI conventions until team confirms. |