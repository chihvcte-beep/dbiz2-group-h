# Wireframe notes: S-F00-03 Staff sign in

Actor: On-site Staff · Frame: 1280px · UI conventions: v0.9 · Author: Ha · Source: [s_f00_03.html](../src/s_f00_03.html) (centred Sign-in card, D29)

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Sign-in card (title) | Đăng nhập nhân viên | FR-04-07 |
| 2 | Staff account | Text input | Staff accounts › staff account name | FR-04-07 |
| 3 | Password | Password input | Internal library account password (masked) | FR-04-07 |
| 4 | Show password | Password input | Hiện / Ẩn | FR-04-07 |
| 5 | Sign in | Primary button | Đăng nhập | FR-04-07 |
| 6 | Rejection / load error | Banner | Generic rejection or MSG-04 | FR-04-18, FR-04-20 |
| 7 | Checking credentials | Skeleton | MSG-05 | FR-04-07 |
| 8 | Try again | Secondary button | Thử lại | FR-04-20 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | [s_f00_03.png](../img/s_f00_03/s_f00_03.png), [s_f00_03_numbered.png](../img/s_f00_03/s_f00_03_numbered.png) | Sign-in card centred in the frame: title, account and password fields, full-width «Đăng nhập». | FR-04-07 |
| Empty | Not applicable: this is a form. | — | — |
| Loading | [s_f00_03_loading.png](../img/s_f00_03/s_f00_03_loading.png), [s_f00_03_loading_numbered.png](../img/s_f00_03/s_f00_03_loading_numbered.png) | Credential and role check. | FR-04-07 |
| Error | [s_f00_03_error.png](../img/s_f00_03/s_f00_03_error.png), [s_f00_03_error_numbered.png](../img/s_f00_03/s_f00_03_error_numbered.png) | Không thể đăng nhập. Bạn kiểm tra thông tin tài khoản rồi thử lại. The same text covers invalid credentials and a missing staff role. | FR-04-18 |
| Error — network | [s_f00_03_error_2.png](../img/s_f00_03/s_f00_03_error_2.png), [s_f00_03_error_2_numbered.png](../img/s_f00_03/s_f00_03_error_2_numbered.png) | MSG-04. Account name retained. | FR-04-20 |
| Success | S-F04-01 | Valid staff session starts and the staff page opens. | FR-04-07 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Staff account and Password | Enter internal library credentials. | stays |
| Show password | Toggle password visibility. | stays |
| Sign in | Submit or retry with Sign in, element 5 (AD-UC-10 a3, AD-UC-13 a2, d1). The preview uses staff.lan and a non-empty sample password; lib.reader demonstrates rejection. | S-F04-01 / stays |
| Try again | Retry after a network failure. | stays |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f00-03).
