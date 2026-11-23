# Wireframe notes: S-F02-03 QR code label printing

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.8 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Back | Screen header | Quay lại | FR-02-08 |
| 2 | Title | Screen header | In nhãn mã QR | FR-02-08 |
| 3 | Select physical books | Checkbox | Selection for each physical book | FR-02-08 |
| 4 | Physical book | Book row | Book catalogue › title, author, access format; ordered by the book's primary shelf location returned by the sync (floor → room → shelf; D13) | FR-02-08, FR-02-23 |
| 5 | Pagination | Secondary button | Trang trước / Trang sau | FR-02-08 |
| 6 | Print labels | Primary button | In nhãn | FR-02-08, FR-02-17, FR-02-18 |
| 8 | Validation / load error | Banner | No selection or MSG-04 | FR-02-17, FR-04-20 |
| 9 | Books without QR codes | Banner | Book catalogue › title for each omitted book | FR-02-18 |
| 10 | Catalogue loading | Skeleton | MSG-05 | FR-02-08 |
| 11 | No books awaiting a label | Empty state | “Tất cả sách bản giấy đã được in nhãn. Sách mới sẽ hiện ở đây sau lần đồng bộ danh mục tiếp theo.” (D3, D15) | FR-02-23 |
| 12 | Try again | Secondary button | Thử lại | FR-04-20 |
| 13 | Selected count | Selection counter | Đã chọn <n> sách, next to In nhãn; counts ticks on all pages (D3b, D16) | FR-02-08 |
| 14 | Sign out | Secondary button | Đăng xuất, in the Screen header → S-F00-03 (D7) | FR-04-21 |
| 15 | Label status filter | Segmented control | Chưa in nhãn (selected on opening) / Đã in nhãn; changing it returns to page 1 and clears the ticks (D40) | FR-02-23, FR-02-25 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/S-F02-03/S-F02-03.png, img/S-F02-03/S-F02-03-numbered.png | Physical books in floor → room → shelf order, checkboxes, Đã chọn <n> sách and Print labels. | FR-02-08 |
| Empty | img/S-F02-03/S-F02-03-empty.png, img/S-F02-03/S-F02-03-empty-numbered.png | No physical books are waiting for a QR label (#11). | FR-02-08 |
| Loading | img/S-F02-03/S-F02-03-loading.png, img/S-F02-03/S-F02-03-loading-numbered.png | Skeleton while opening the book list. | FR-02-08 |
| Error — no selection | img/S-F02-03/S-F02-03-error.png, img/S-F02-03/S-F02-03-error-numbered.png | Hãy chọn ít nhất 1 sách bản giấy. | FR-02-17 |
| Error — all lack QR | img/S-F02-03/S-F02-03-error-2.png, img/S-F02-03/S-F02-03-error-2-numbered.png | Modern Business Ethics and Essentials of Library Science are listed. No sheet is produced. | FR-02-18 |
| Error — network | img/S-F02-03/S-F02-03-error-3.png, img/S-F02-03/S-F02-03-error-3-numbered.png | MSG-04, existing selections retained. | FR-04-20 |
| Warning — some lack QR | img/S-F02-03/S-F02-03-warning.png, img/S-F02-03/S-F02-03-warning-numbered.png | Modern Business Ethics is listed as omitted. | FR-02-18 |
| Success | img/S-F02-03/S-F02-03-success.png | Two QR labels from three selected books. M-F02-03-01 overlays the list. The books leave the list only after «Đã in xong»; after «Đóng» they stay listed (D12). | FR-02-08, FR-02-18 |
| Next page | img/S-F02-03/S-F02-03-page-2.png | Second page; ticks on other pages stay counted in Đã chọn <n> sách. | FR-02-08 |
| Reprint list | img/S-F02-03/S-F02-03-reprint.png, img/S-F02-03/S-F02-03-reprint-numbered.png | Filter on Đã in nhãn: labelled books, ticks and In lại nhãn (D40). | FR-02-25 |
| Reprint list — empty | img/S-F02-03/S-F02-03-reprint-empty.png | Chưa có sách nào được in nhãn. | FR-02-25 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Back | Return to the staff page. | S-F04-01 |
| Select physical books | Check or uncheck books (AD-UC-10 a1). | stays |
| Pagination | Move between pages of physical books. | stays |
| Print labels | Build a sheet with Print labels, element 6 (AD-UC-10 a2). Include only eligible checked books and list omitted titles. | M-F02-03-01 / stays |
| Print labels | Recheck staff session before creating a sheet (FR-04-08). | S-F00-03 |
| Try again | Retry after a network failure. | stays |
| Sign out | End the staff session (FR-04-21). | S-F00-03 |
| Label status filter | Switch between Chưa in nhãn and Đã in nhãn (AD-UC-10 d13, a11). | stays |
| In lại nhãn | Build a reprint sheet from the ticked labelled books (AD-UC-10 a13). | M-F02-03-01 / stays |

## Open questions

None. Decisions: see [decision-index.md](../../decision-index.md#s-f02-03).

Sample-only catalogue additions: Introduction to Public Policy — Hoa Tran; Modern Business Ethics — An Nguyen; Essentials of Library Science — Linh Do; Foundations of Statistics — Ha Le; labelled-book samples: Library Management Today — Mai Tran, Research Methods Handbook — Quang Vu, Microeconomics in Practice — Thu Pham, Applied Corporate Finance — Nam Hoang. Principles of Economics uses placeholder author Minh Anh Pham. These names are fictional wireframe data.
