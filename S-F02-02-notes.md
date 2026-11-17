# Wireframe notes: S-F02-02 Book information and reviews (QR landing page)

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Hoa

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Title “Thông tin và đánh giá sách”; Back destination not defined for QR entry | — |
| 2 | Book information | Book row | Book catalogue › neutral grey “Cover” placeholder, title, author, subjects, summary; sample “Principles of Economics” | FR-02-05 |
| 3 | OPAC book link | Text link | “Xem sách trên OPAC” → existing OPAC Book Detail | FR-02-05 |
| 4 | Review editor (same review panel as S-F02-01) | Text area with counter | Book review › review text; shared review-panel structure | FR-02-01, FR-02-03, FR-02-04, FR-02-11 |
| 5 | Review item | Review item | Same Review item component as S-F02-01; own review actions Edit/Delete; no Report on QR page | FR-02-13 |
| 6 | Anonymous posting | Checkbox | “Đăng ẩn danh”; full registered name or “Bạn đọc ẩn danh” | FR-02-22 |
| 7 | Review guideline | Text link | Same guideline link as S-F02-01; destination URL not supplied | AD-UC-13 Q1 |
| 8 | Submit review | Primary button | “Đăng đánh giá” / “Lưu thay đổi” | FR-02-01, FR-02-03 |
| 9 | Page-level feedback | Banner | QR error “Không tìm thấy sách.”; MSG-04 network error | FR-02-16, FR-04-20 |
| 10 | Empty list message | Empty state | “Không có đánh giá nào để hiển thị.” while book information remains visible | FR-02-15 |
| 11 | Success confirmation | Toast | “Đã đăng đánh giá.” / “Đã cập nhật đánh giá.” / “Đã xoá đánh giá.” | FR-02-12 |
| 12 | Loading placeholder | Skeleton | Replaces book information and review content | MSG-05 |
| 13 | Field validation feedback | Inline error | Shared review-panel text validation | FR-02-01, FR-02-11 |
| 14 | Retry action | Secondary button | “Thử lại” inside MSG-04 Banner | FR-04-20 |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F02-02.png | Book title, author, subjects, summary, OPAC link and shared review panel | FR-02-05, FR-02-01 |
| Empty | img/S-F02-02-empty.png | Book found, no published reviews; book information stays visible | FR-02-15 |
| Loading | img/S-F02-02-loading.png | Skeleton for book information and reviews | MSG-05 |
| Error | img/S-F02-02-error.png | Invalid QR: “Không tìm thấy sách.”; numbered variant included | FR-02-16 |
| Error-2 | img/S-F02-02-error-2.png | MSG-04 network error with retry action; numbered variant included | FR-04-20 |
| Success | img/S-F02-02-success.png | Review action confirmation and refreshed review content | FR-02-12 |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| Back | tap | stays (QR-entry Back destination unresolved) |
| Xem sách trên OPAC | tap | Existing OPAC Book Detail (exit) |
| Shared review panel / Submit review | write and submit | stays |
| Shared review panel / Submit while signed out | request sign-in | M-F00-01 (reused; owned by Ha), then S-F00-01 → S-F00-02 → S-F02-02 |
| Review guideline | open library review rules | stays (destination URL unresolved) |
| Own review / Sửa | edit and save own review | stays; if signed out, M-F00-01 then return to S-F02-02 |
| Own review / Xoá đánh giá | request deletion | M-F02-01-01; if signed out, M-F00-01 then return to S-F02-02 |
| Thử lại | retry after load failure | stays |

## Open questions
| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: What should the Screen header Back action do when this screen is opened directly by scanning a QR code?] | Keep the convention-required Back control visible; no destination is asserted. |
| 2 | [NEEDS CLARIFICATION: AD-UC-06 says the review panel is the same as S-F02-01, while UI conventions restrict Report to S-F02-01. Confirm that Report remains absent here.] | No Report action, as explicitly required by AD-UC-06 / L8-07. |
| 3 | [NEEDS CLARIFICATION: Exact URL for “quy định viết đánh giá” is not supplied.] | Use the shared review panel label; URL unresolved. |
| 4 | [NEEDS CLARIFICATION: AD-UC-06 says reviews follow UC-05 paging rules, but Load more is listed only for S-F02-01 in UI conventions. Should S-F02-02 also expose next-page navigation?] | Do not add a Load more control to S-F02-02 until the team confirms it. |
| 5 | [NEEDS CLARIFICATION: UI conventions list Book row usage on other screens, not S-F02-02. Is it approved as the QR book-information block here?] | Reuse the existing Book row style without adding a cover image or access-format content. |
