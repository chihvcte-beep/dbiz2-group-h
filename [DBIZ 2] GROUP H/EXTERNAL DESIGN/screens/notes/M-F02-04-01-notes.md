# Wireframe notes: M-F02-04-01 Remove this review?

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.8 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Removal confirmation dialog | Modal | “Gỡ đánh giá?” · Short text explaining the selected review will no longer be publicly displayed; the review text is not quoted, it stays visible behind the dimmed overlay (D22) | FR-02-10 |
| 2 | Confirm removal | Destructive button | “Gỡ đánh giá”; trash icon before label | FR-02-10, FR-04-12 |
| 3 | Cancel removal | Secondary button | “Huỷ”; leaves review public and report Open | FR-02-10 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/M-F02-04-01.png | Confirmation modal over dimmed S-F02-04 parent showing selected review #91 and the header «Đăng xuất» button behind (D7); numbered variant in M-F02-04-01-numbered.png (#1–#3, re-exported 22/11/2026) | FR-02-10 |
| Empty | Not applicable: confirmation modal has no list | — | — |
| Loading | Not applicable: no modal-level loading state is specified | — | — |
| Error | Not applicable: no modal-level error state is specified | — | — |
| Success | Not applicable: parent S-F02-04 refreshes after confirmation; audit entry is written | FR-02-10, FR-04-12 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Gỡ đánh giá | confirm | stays on S-F02-04; review removed from public display, report Upheld, audit entry written |
| Huỷ | cancel | stays on S-F02-04; review stays public and remains in the open queue |

## Open questions

None. Decisions: see [decision-index.md](../../decision-index.md#m-f02-04-01).