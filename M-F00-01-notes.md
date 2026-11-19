# Wireframe notes: M-F00-01 Sign in to continue?

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Ha

## Elements

| # | Element | Component | Content / data source | FR |
| --- | --- | --- | --- | --- |
| 1 | Title | Modal | Đăng nhập để tiếp tục? | FR-04-08 |
| 2 | Message | Modal | MSG-01, MSG-02 or MSG-03 | FR-04-08, FR-03-18, FR-03-21 |
| 3 | Sign in | Primary button | Đăng nhập | FR-04-08 |
| 4 | Not now | Secondary button | Để sau | FR-04-08 |

## States drawn

| State | Image | What the user sees | FR |
| --- | --- | --- | --- |
| Default | img/M-F00-01.png, img/M-F00-01-numbered.png | General (MSG-01): “Bạn cần đăng nhập bằng thẻ thư viện để làm việc này.” | FR-04-08 |
| Wording variant — chatbot | Same layout as Default | Chatbot (MSG-02): “Bạn cần đăng nhập bằng thẻ thư viện để trò chuyện với trợ lý tìm sách.” | FR-03-18 |
| Wording variant — recommendations | Same layout as Default | Recommendations (MSG-03): “Gợi ý riêng cho bạn cần tài khoản thẻ thư viện. Hãy đăng nhập để xem.” | FR-03-21 |
| Empty | Not applicable: the modal only asks the reader to choose. | — | — |
| Loading | Not applicable: the modal only asks the reader to choose. | — | — |
| Error | Not applicable: the modal only asks the reader to choose. | — | — |
| Success | Not applicable: the modal only asks the reader to choose. | — | — |

## Actions and where they go

| Element | User action | Goes to |
| --- | --- | --- |
| Sign in | Open reader sign-in. After OTP acceptance resume the requested action at the origin (L8-01). | S-F00-01 |
| Not now | Close and end the pending request. | S-F01-01, S-F02-01, S-F02-02, S-F03-02, S-F03-03, S-F03-06, S-F03-07 |

## Open questions

Review status: self-checked against the assignment and the two shared UI/UX handbooks. Cross-review by Hoa and final consistency review by Linh are pending.

| # | Question | Default drawn |
| --- | --- | --- |
| — | — | All seven entry screens use the same modal. |

Shared handoff for Nhi, Hoa and Trieu: use img/M-F00-01.png, its HTML source, and MSG-01 / MSG-02 / MSG-03 above. The blurred/dimmed context illustrates S-F01-01 only. The modal is shared by all seven listed entry screens. No group notification has been sent.
