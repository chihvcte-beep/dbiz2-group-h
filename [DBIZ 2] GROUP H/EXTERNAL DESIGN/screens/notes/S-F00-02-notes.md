# Wireframe notes: S-F00-02 Verify email OTP

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Back | Screen header | Quay lại | L8-01 |
| 2 | Title | Screen header | Nhập mã xác thực | FR-04-01 |
| 3 | Validity | Code input | MSG-09 | FR-04-04 |
| 4 | Email code | Code input | Six digits sent to Reader accounts › declared email | FR-04-04 |
| 5 | Sign in | Primary button | Đăng nhập (disabled during recovery) | FR-04-01 |
| 6 | Send a new code | Secondary button | Gửi mã mới (primary during recovery) | FR-04-04, FR-04-16 |
| 7 | Cancel | Secondary button | Huỷ | L8-01 |
| 8 | Incorrect code | Inline error | Attempts left (4 to 1) | FR-04-17, FR-04-19 |
| 9 | Recovery / load error | Banner | Invalidated, expired / used, send failure, or MSG-04 | FR-04-01, FR-04-04, FR-04-16, FR-04-17, FR-04-20 |
| 10 | Verification pending | Skeleton | MSG-05 | FR-04-04 |
| 11 | New code sent | Toast | Đã gửi mã mới. | FR-04-04 |
| 12 | Try again | Secondary button | Thử lại | FR-04-20 |
| 13 | Email address | Code input | Reader accounts › registered email in full, not masked: “Mã đã được gửi tới <email>.” (D2, D15). Not shown in Error-4 (D31). | FR-04-01 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/S-F00-02/S-F00-02.png, img/S-F00-02/S-F00-02-numbered.png | MSG-09, the registered email in full (#13) and a six-digit input. | FR-04-04 |
| Empty | Not applicable: this is a form. | — | — |
| Loading | img/S-F00-02/S-F00-02-loading.png, img/S-F00-02/S-F00-02-loading-numbered.png | Verification in progress. | FR-04-04 |
| Error | img/S-F00-02/S-F00-02-error.png, img/S-F00-02/S-F00-02-error-numbered.png | Mã chưa đúng. Bạn còn 3 lần thử. | FR-04-17, FR-04-19 |
| Error-2 | img/S-F00-02/S-F00-02-error-2.png, img/S-F00-02/S-F00-02-error-2-numbered.png | Bạn đã nhập sai 5 lần. Mã này không còn dùng được, hãy bấm Gửi mã mới. | FR-04-17 |
| Error-3 | img/S-F00-02/S-F00-02-error-3.png, img/S-F00-02/S-F00-02-error-3-numbered.png | Mã đã hết hạn hoặc đã được sử dụng. Hãy bấm Gửi mã mới. | FR-04-01, FR-04-04 |
| Error-4 | img/S-F00-02/S-F00-02-error-4.png, img/S-F00-02/S-F00-02-error-4-numbered.png | Không gửi được mã. Hãy bấm Gửi mã mới để thử lại. The email line (#13) is hidden (D31). | FR-04-16 |
| Error — network | img/S-F00-02/S-F00-02-error-5.png, img/S-F00-02/S-F00-02-error-5-numbered.png | MSG-04, entered code retained. | FR-04-20 |
| Success — new code | img/S-F00-02/S-F00-02-success.png, img/S-F00-02/S-F00-02-success-numbered.png | Đã gửi mã mới. A fresh code replaces the old one. | FR-04-04 |
| Success — accepted | Return transition | Resume the requested action at its origin. | FR-04-01, L8-01 |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Back | Return to card entry. | S-F00-01 |
| Email code | Enter the six-digit code received by email. | stays |
| Sign in | Submit the code (AD-UC-11 r2). Return on acceptance. On rejection stay and show the matching branch. | S-F01-01 / S-F02-01 / S-F02-02 / S-F03-02 / S-F03-03 / S-F03-06 / S-F03-07 / Existing OPAC entry page (exit) |
| Send a new code | Request a new email code (AD-UC-11 d5, r3). The old one is invalidated. | stays |
| Cancel | Return to the sign-in origin (L8-01). | S-F01-01 / S-F02-01 / S-F02-02 / S-F03-02 / S-F03-03 / S-F03-06 / S-F03-07 / Existing OPAC entry page (exit) |
| Try again | Retry after a network failure. | stays |

## Open questions

None. Decisions: see [decision-index.md](../../decision-index.md#s-f00-02).
