# Wireframe notes: S-F02-03 QR code label printing

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.7 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Back | Screen header | Quay lại | FR-02-08 |
| 2 | Title | Screen header | In nhãn mã QR | FR-02-08 |
| 3 | Select physical books | Checkbox | Selection for each physical book | FR-02-08 |
| 4 | Physical book | Book row | Book catalogue › title, author, access format | FR-02-08 |
| 5 | Pagination | Secondary button | Trang trước / Trang sau (provisional) | FR-02-08 |
| 6 | Print labels | Primary button | In nhãn | FR-02-08, FR-02-17, FR-02-18 |
| 8 | Validation / load error | Banner | No selection or MSG-04 | FR-02-17, FR-04-20 |
| 9 | Books without QR codes | Banner | Book catalogue › title for each omitted book | FR-02-18 |
| 10 | Catalogue loading | Skeleton | MSG-05 | FR-02-08 |
| 11 | No physical books | Empty state | No physical books available | FR-02-08 |
| 12 | Try again | Secondary button | Thử lại | FR-04-20 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/S-F02-03.png, img/S-F02-03-numbered.png | Physical books, checkboxes and Print labels. | FR-02-08 |
| Empty | img/S-F02-03-empty.png, img/S-F02-03-empty-numbered.png | No synced physical books to select. | FR-02-08 |
| Loading | img/S-F02-03-loading.png, img/S-F02-03-loading-numbered.png | Skeleton while opening the book list. | FR-02-08 |
| Error — no selection | img/S-F02-03-error.png, img/S-F02-03-error-numbered.png | Hãy chọn ít nhất 1 sách bản giấy. | FR-02-17 |
| Error — all lack QR | img/S-F02-03-error-2.png, img/S-F02-03-error-2-numbered.png | Modern Business Ethics and Essentials of Library Science are listed. No sheet is produced. | FR-02-18 |
| Error — network | img/S-F02-03-error-3.png, img/S-F02-03-error-3-numbered.png | MSG-04, existing selections retained. | FR-04-20 |
| Warning — some lack QR | img/S-F02-03-warning.png, img/S-F02-03-warning-numbered.png | Modern Business Ethics is listed as omitted. | FR-02-18 |
| Success | img/S-F02-03-success.png | Two QR labels from three selected books. M-F02-03-01 overlays the list. | FR-02-08, FR-02-18 |
| Next page | img/S-F02-03-page-2.png | Provisional second page of synced books. | FR-02-08 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Back | Return to the staff page. | S-F04-01 |
| Select physical books | Check or uncheck books (AD-UC-10 a1). | stays |
| Pagination | Move between pages of physical books (provisional). | stays |
| Print labels | Build a sheet with Print labels, element 6 (AD-UC-10 a2). The HTML preview reads the checked rows, includes only eligible books and lists omitted book titles. | M-F02-03-01 / stays |
| Print labels | Recheck staff session before creating a sheet (FR-04-08). | S-F00-03 |
| Try again | Retry after a network failure. | stays |

## Open questions

Review status: self-checked against the assignment and the two shared UI/UX handbooks. Cross-review by Hoa and final consistency review by Linh are pending.

| # | Question | Default drawn |
| --- | --- | --- |
| 1 | [NEEDS CLARIFICATION: Blocking — how should staff find physical books to select?] | Provisional list of newly synced physical books, newest first, with pagination. |
| 2 | [NEEDS CLARIFICATION: Should checked books carry over when staff change pages?] | The preview uses the selections on the illustrated page. |

Sample-only catalogue additions: Introduction to Public Policy — Hoa Tran; Modern Business Ethics — An Nguyen; Essentials of Library Science — Linh Do; Foundations of Statistics — Ha Le. Principles of Economics uses placeholder author Minh Anh Pham. These names are fictional wireframe data.

Navigation check, 17/11/2026: validated in Chromium using synthetic fixture data. The HTML demonstrates transitions. Production identity and session checks remain backend integration work.
