# Wireframe notes: S-F00-01 Sign in: library card number

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Ha

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
| Default | [s_f00_01.png](../img/s_f00_01/s_f00_01.png), [s_f00_01_numbered.png](../img/s_f00_01/s_f00_01_numbered.png) | Card input, send and cancel. | FR-04-01 |
| Empty | Not applicable: this is a form. | — | — |
| Loading | [s_f00_01_loading.png](../img/s_f00_01/s_f00_01_loading.png), [s_f00_01_loading_numbered.png](../img/s_f00_01/s_f00_01_loading_numbered.png) | Lookup in progress, submit disabled. | FR-04-01 |
| Error | [s_f00_01_error.png](../img/s_f00_01/s_f00_01_error.png), [s_f00_01_error_numbered.png](../img/s_f00_01/s_f00_01_error_numbered.png) | Không thể đăng nhập. Bạn kiểm tra thông tin rồi thử lại. The same text is used for any card rejection. | FR-04-01 |
| Error — format | [s_f00_01_error_2.png](../img/s_f00_01/s_f00_01_error_2.png), [s_f00_01_error_2_numbered.png](../img/s_f00_01/s_f00_01_error_2_numbered.png) | Số thẻ thư viện gồm 7 chữ số. Bạn kiểm tra lại nhé. | FR-04-01 |
| Error — network | [s_f00_01_error_3.png](../img/s_f00_01/s_f00_01_error_3.png), [s_f00_01_error_3_numbered.png](../img/s_f00_01/s_f00_01_error_3_numbered.png) | MSG-04, card number retained. | FR-04-20 |
| Success | S-F00-02 | Card found. Open code screen, or its send-error state if delivery failed. | FR-04-01, FR-04-16 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Library card number | Enter or correct seven digits. | stays |
| Send code | Submit with Send code, element 3 (AD-UC-11 r1). Card 0012345 illustrates the valid-lookup path to S-F00-02. Rejections stay here. | S-F00-02 / stays |
| Cancel | Return to the origin (L8-01). | S-F01-01 / S-F02-01 / S-F02-02 / S-F03-02 / S-F03-03 / S-F03-06 / S-F03-07 / Existing OPAC main menu (exit) |
| Try again | Retry after a network failure. | stays |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f00-01).
