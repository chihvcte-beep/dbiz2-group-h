# Wireframe notes: S-F04-01 Staff page

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.7 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Screen header | Trang nhân viên | FR-04-07 |
| 2 | Print QR labels | Menu tile | In nhãn mã QR | FR-02-08 |
| 3 | Reported reviews | Menu tile | Đánh giá bị báo cáo (Could) | FR-02-14 |
| 4 | Staff page loading | Skeleton | MSG-05 | FR-04-08 |
| 5 | Network error | Banner | MSG-04 | FR-04-20 |
| 6 | Try again | Secondary button | Thử lại | FR-04-20 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/S-F04-01.png, img/S-F04-01-numbered.png | Two staff task tiles. | FR-04-07 |
| Empty | Not applicable: the menu has fixed options. | — | — |
| Loading | img/S-F04-01-loading.png, img/S-F04-01-loading-numbered.png | Skeleton while opening the staff page. | FR-04-08 |
| Error | img/S-F04-01-error.png, img/S-F04-01-error-numbered.png | MSG-04. Requests without a staff session open S-F00-03. | FR-04-20, FR-04-08 |
| Success | Not applicable: opening the menu uses its default state. | — | — |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Staff page address | Open with valid staff session, or route to staff sign-in. | S-F04-01 / S-F00-03 |
| Print QR labels | Open QR label printing. | S-F02-03 |
| Reported reviews | Open the reported reviews list if UC-13 ships. | S-F02-04 |
| Try again | Retry after a network failure. | stays |

## Open questions

Review status: self-checked against the assignment and the two shared UI/UX handbooks. Cross-review by Hoa and final consistency review by Linh are pending.

| # | Question | Default drawn |
| --- | --- | --- |
| 1 | [NEEDS CLARIFICATION: Should staff be offered an explicit sign-out action?] | The two task tiles are the only actions. |

Navigation check, 17/11/2026: validated in Chromium using synthetic fixture data. The HTML demonstrates transitions. Production identity and session checks remain backend integration work.
