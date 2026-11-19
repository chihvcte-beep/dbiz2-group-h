# Wireframe notes: S-F03-06 AI Chatbot Book Search

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Author: Trieu

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back and screen title | Screen header | Back to existing OPAC main menu; title “Thủ thư AI tìm sách” | — |
| 2 | AI welcome greeting | Message bubble (assistant) | Friendly system greeting introducing conversational search capabilities | FR-03-09 |
| 3 | Query suggestion chips | Chip group | Quick prompts: “Sách về kinh tế vĩ mô”, “Chuỗi cung ứng & Logistics”, “Giáo trình Marketing căn bản” | — |
| 4 | Reader message bubble | Message bubble (user) | Chatbot conversations › reader message; natural-language inquiry entered by reader (e.g. “Tìm giúp tôi sách về quản trị chuỗi cung ứng”) | FR-03-09, FR-03-10 |
| 5 | Chatbot reply bubble | Message bubble (assistant) | Chatbot conversations › chatbot reply; conversational response summarizing matched books | FR-03-09, FR-03-10 |
| 6 | Book result card | Result card | Embedded in assistant reply: book cover placeholder, title, author, access format tag (“Bản giấy” / “Trực tuyến”), and call-to-action link | FR-03-09 |
| 7 | View shelf location link | Card action link | “Xem vị trí trên kệ”; opens book on OPAC Book Detail, leading to S-F01-01 (UC-01) | FR-01-01, FR-03-09 |
| 8 | Chat input field | Text input | Multi-line auto-expanding input; placeholder “Hỏi thủ thư AI về sách bạn cần tìm…” | FR-03-09 |
| 9 | Send inquiry button | Primary icon button | Submits reader query to AI Service; disabled when input is empty or loading | FR-03-09 |
| 10 | Typing indicator | Loading bubble | Three-dot animated indicator: “Thủ thư AI đang tra cứu danh mục sách…” (active up to 10s) | AD-UC-08 Q1 |
| 11 | No matching books reply | Assistant reply bubble | “Rất tiếc, thư viện chưa có cuốn sách nào khớp với yêu cầu của bạn. Bạn thử tìm với các chủ đề liên quan như Logistics, Vận tải quốc tế hoặc Quản trị tác nghiệp xem sao nhé!” | FR-03-16 |
| 12 | AI failure notice banner | System error bubble | “Tính năng tìm kiếm bằng AI tạm thời gián đoạn. Bạn vui lòng thử lại sau hoặc sử dụng bộ lọc hình thức truy cập.” | FR-03-17 |
| 13 | Format filter fallback | Text action link | “Dùng bộ lọc hình thức truy cập” inside error bubble; opens S-F03-01 (UC-03) | FR-03-17, FR-03-12 |
| 14 | Sign-in modal prompt | Modal trigger (M-F00-01) | Triggered when unauthenticated visitor submits first message: “Đăng nhập bằng thẻ thư viện để tiếp tục trò chuyện cùng thủ thư AI” | FR-03-18 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F03-06.png, img/S-F03-06-numbered.png | Empty conversation state showing AI welcome greeting, suggestion prompt chips, and ready chat input field. | FR-03-09, FR-03-18 |
| Loading | img/S-F03-06-loading.png | User's sent inquiry bubble displayed; chatbot typing bubble visible below with disabled input. | AD-UC-08 Q1 |
| Success / Results | img/S-F03-06-success.png | Assistant reply containing 2 rich book result cards with format tags and shelf location links. | FR-03-09, FR-03-10 |
| No-results | img/S-F03-06-no-match.png | Chatbot conversational explanation that no titles matched, suggesting alternative keywords/topics. | FR-03-16 |
| Error | img/S-F03-06-error.png | AI Service timeout (>10s) or error notice with direct fallback link to format filter S-F03-01. | FR-03-17 |

## Actions and where they go

| Element | User action | Goes to |
|---|---|---|
| Back navigation | Tap `<` | Existing OPAC main menu (exit) |
| Suggestion chip | Tap chip | Populates input and submits inquiry on S-F03-06 |
| Send inquiry (signed in) | Submit query | Triggers AI Service; shows Loading, then Success or No-results or Error on S-F03-06 |
| Send inquiry (signed out) | Submit query | Opens M-F00-01 (text FR-03-18); after sign-in through S-F00-01 / S-F00-02, returns to S-F03-06 and sends query |
| Xem vị trí trên kệ | Tap link on book card | OPAC Book Detail › leads to S-F01-01 (UC-01) |
| Dùng bộ lọc hình thức truy cập | Tap fallback link in error notice | Navigates to Access-format filter screen S-F03-01 (UC-03) |
| Input field | Type inquiry | Updates input state; enables Send button |

## Open questions

| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: What is the maximum response timeout before triggering the AI fallback notice?] | Team consensus (2026-11-04): 10 seconds (AD-UC-08 Q1). |
| 2 | [NEEDS CLARIFICATION: Is the temporary unavailable notice saved into reader conversation history?] | Team consensus (2026-11-04): No; reader inquiry is recorded, but system error notices are transient and not saved to conversation history (AD-UC-08 Q2). |
| 3 | [NEEDS CLARIFICATION: Can readers clear or delete their chatbot conversation history?] | Team consensus (2026-11-04): No deletion mechanism in release 1; conversations are retained across sessions (AD-UC-08 Q3). |
| 4 | [NEEDS CLARIFICATION: Should the screen restore previous conversation turns upon opening?] | Default drawn: Screen opens to fresh welcome state; previous history is preserved in backend logs. |

## Scope and implementation notes

- Chatbot interface can be opened by anyone, but submitting an inquiry requires an active library card session (FR-03-18).
- Strictly out of scope (W0 Table 3 / Lesson 8 guidance): floating chatbot widget across other OPAC pages, voice input, image attachments, thumbs up/down rating on AI answers, and reader conversation management dashboard.
- Every reader inquiry and assistant answer is persisted per reader account (FR-03-10).
- The AI error message must always offer the direct fallback path to format filter S-F03-01 (FR-03-17).
