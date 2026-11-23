# Wireframe notes: S-F03-06 AI Chatbot Book Search

Actor: Reader · Frame: 360px (export 3x = 1080px) · UI conventions: v0.8 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back navigation | Screen header | Returns to existing OPAC main menu | — |
| 2 | Screen title | Screen header | “Trợ lý tìm sách AI” | — |
| 3 | Reader message bubble | Chat bubble | Natural-language inquiry entered by reader; styled with reader bubble background (`colour/info-bg`) | FR-03-09, FR-03-10 |
| 4 | Chatbot reply bubble | Chat bubble | Conversational assistant summary; styled with assistant bubble background (`colour/surface`) | FR-03-09, FR-03-10 |
| 5 | Book result card | Book card | Embedded in assistant reply: book title, author, format label (“Bản giấy” / “Trực tuyến”) with icon, and action text link | FR-03-09 |
| 6 | Book detail action link | Text link | “Xem chi tiết sách” (D25); opens book on OPAC Book Detail, leading to S-F01-01 (UC-01) | FR-01-01, FR-03-09 |
| 7 | Chat input field | Text input | Message input within message composer; placeholder “Nhập câu hỏi tìm sách…” | FR-03-09 |
| 8 | Send inquiry button | Primary button | Primary button labeled “Gửi”; submits query to AI Service; disabled when input is empty or loading | FR-03-09 |
| 9 | Typing / loading indicator | Chat bubble | Assistant bubble displaying “Đang tải…” (MSG-05) during AI catalogue query (up to 10s timeout) | AD-UC-08 Q1, MSG-05 |
| 10 | No matching books reply | Chat bubble | Assistant bubble explaining no catalogue titles matched: “Rất tiếc, thư viện chưa có cuốn sách nào khớp với yêu cầu của bạn. Bạn thử tìm với các chủ đề liên quan xem sao nhé!” | FR-03-16 |
| 11 | AI service error banner | Banner | MSG text: “Tìm kiếm bằng AI đang tạm ngưng. Bạn hãy dùng bộ lọc hình thức.” with embedded link leading to S-F03-01 | FR-03-17 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | [s_f03_06.png](../img/s_f03_06/s_f03_06.png), [s_f03_06_numbered.png](../img/s_f03_06/s_f03_06_numbered.png) | Fresh conversational search screen with ready message composer at bottom. | FR-03-09, FR-03-18 |
| Empty | [s_f03_06_empty.png](../img/s_f03_06/s_f03_06_empty.png) | Empty state identical to Default: empty conversation space with ready message composer (§2.3). | FR-03-09 |
| Loading | [s_f03_06_loading.png](../img/s_f03_06/s_f03_06_loading.png) | User's sent query bubble displayed; assistant bubble below displays “Đang tải…”; composer input is busy. | AD-UC-08 Q1, MSG-05 |
| Success / Results | [s_f03_06_success.png](../img/s_f03_06/s_f03_06_success.png) | Assistant reply containing 4 rich book cards with format labels and “Xem chi tiết sách” links. | FR-03-09, FR-03-10 |
| No-match | [s_f03_06_no_match.png](../img/s_f03_06/s_f03_06_no_match.png) | Assistant conversational message explaining that no titles matched, suggesting alternative search angles. | FR-03-16 |
| Error | [s_f03_06_error.png](../img/s_f03_06/s_f03_06_error.png) | Banner error notifying AI service interruption, providing direct fallback text link to S-F03-01. | FR-03-17 |

## Actions and where they go

| Element / event | User action / system event | Result / destination |
|---|---|---|
| Back navigation | Tap `<` button | Existing OPAC main menu (exit) |
| Send message (signed in) | Submit query with active reader session | stays; displays reader bubble, transitions to Loading, then Success / No-match / Error on S-F03-06 |
| Send message (signed out) | Submit query without active session | M-F00-01 (Sign-in prompt modal with MSG-02: “Bạn cần đăng nhập bằng thẻ thư viện để trò chuyện với trợ lý tìm sách.”); after sign-in through S-F00-01 / S-F00-02, returns to S-F03-06 and sends query (FR-03-18) |
| Xem chi tiết sách | Tap link on book card | OPAC Book Detail › leads to S-F01-01 (UC-01) |
| Dùng bộ lọc hình thức | Tap link in error banner | S-F03-01 (Access-format filter screen, UC-03) |
| Message composer input | Type inquiry text | stays; enables “Gửi” button |

## Open questions

None. Decisions: see [decision_index.md](../../../project_brief/decision_index.md#s-f03-06).
