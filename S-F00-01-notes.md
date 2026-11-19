# Wireframe notes: S-F00-01 Sign in: library card number

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Screen header | Đăng nhập | FR-04-01 |
| 2 | Library card number | Text input | Reader accounts › library card number (seven digits, leading zero kept) | FR-04-01 |
| 3 | Send code | Primary button | Gửi mã | FR-04-01 |
| 4 | Cancel | Secondary button | Huỷ | L8-01 |
| 5 | Card format error | Inline error | Số thẻ thư viện gồm 7 chữ số. Bạn kiểm tra lại nhé. | FR-04-01 |
| 6 | Rejection / load error | Banner | Generic rejection or MSG-04 | FR-04-01, FR-04-20 |
| 7 | Card lookup | Skeleton | MSG-05 | FR-04-01 |
| 8 | Try again | Secondary button | Thử lại | FR-04-20 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/S-F00-01.png, img/S-F00-01-numbered.png | Card input, send and cancel. | FR-04-01 |
| Empty | Not applicable: this is a form. | — | — |
| Loading | img/S-F00-01-loading.png, img/S-F00-01-loading-numbered.png | Lookup in progress, submit disabled. | FR-04-01 |
| Error | img/S-F00-01-error.png, img/S-F00-01-error-numbered.png | Không thể đăng nhập. Bạn kiểm tra thông tin rồi thử lại. The same text is used for any card rejection. | FR-04-01 |
| Error — format | img/S-F00-01-error-2.png, img/S-F00-01-error-2-numbered.png | Số thẻ thư viện gồm 7 chữ số. Bạn kiểm tra lại nhé. | FR-04-01 |
| Error — network | img/S-F00-01-error-3.png, img/S-F00-01-error-3-numbered.png | MSG-04, card number retained. | FR-04-20 |
| Success | S-F00-02 | Card found. Open code screen, or its send-error state if delivery failed. | FR-04-01, FR-04-16 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Library card number | Enter or correct seven digits. | stays |
| Send code | Submit with Send code, element 3 (AD-UC-11 r1). The preview uses 0012345 to open S-F00-02 and preserves returnTo. Rejections stay here. | S-F00-02 / stays |
| Cancel | Return to the origin (L8-01). | S-F01-01 / S-F02-01 / S-F02-02 / S-F03-02 / S-F03-03 / S-F03-06 / S-F03-07 / Existing OPAC entry page (exit) |
| Try again | Retry after a network failure. | stays |

## Open questions

Review status: self-checked against the assignment and the two shared UI/UX handbooks. Cross-review by Hoa and final consistency review by Linh are pending.

| # | Question | Default drawn |
| --- | --- | --- |
| — | — | The seven-digit format is settled in v0.7 §2. |

Navigation check, 17/11/2026: validated in Chromium using synthetic fixture data. The HTML demonstrates transitions. Production identity and session checks remain backend integration work.
