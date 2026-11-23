# Decision Index: Group H Library Core System

The single record of every decided question for the Group H external design and activity diagrams. All other
documents state only the resulting requirement and cite the ID listed here (for example `D7`, `AD-UC-09 Q2`,
`L8-01`, `UI Q4`). Nothing in the design documents is open: anything still to be done is a task in
[Pending tasks](#pending-tasks), not a question.

| Field | Value |
|---|---|
| Version | v1.6 · 23/11/2026 |
| Covers | [external_design/](../external_design/) (screen list, screen transition, usage flow, UI conventions, 15 screen specs and wireframe notes) [activity_diagram/](../activity_diagram/) (AD-UC-01 … AD-UC-15, activity index) [system_design/](../system_design/) (use cases, SD-UC-01 … SD-UC-15, system architecture), [requirements/](../requirements/) (FR list, cost) and this [project_brief/](.) folder |
| Removed guide files | The `huong-dan/` guide folder was removed on 23/11/2026 when the repository was reorganised. Citations to it below stay as the historical source; the files remain in Git history at commit `4e55347`. |
| How to use | Find the ID cited in a document, read the decision here. To change a decision, add a new row (new ID) that supersedes the old one; never edit a document's requirement without a row here. |

## Group decisions 22112026

Group decisions of 22/11/2026, taken after the screen-spec review. D30 and later rows were added on 23/11/2026.

| ID | Question | Decision | Applies to |
|---|---|---|---|
| D1 | Sign-in started from a signed-in action: keep or drop the pending action? | Keep. After the OTP is accepted the reader returns to the screen where sign-in started and the pending action (save book, post review, report …) continues automatically. «Huỷ» returns to the starting screen with the action still waiting; nothing on screen is lost. | S-F00-01, S-F00-02, M-F00-01, AD-UC-04, screen-transition |
| D2 | Mask the email on the OTP screen? | No. The registered email is shown in full. | S-F00-02 |
| D3 | Which books does S-F02-03 list? | Physical books in the synced catalogue that have never had a QR label printed (new books from the latest sync appear and stay until printed). | S-F02-03, AD-UC-10, FR-02-23 |
| D3b | Ticks across pages | Kept across pages; «Đã chọn <n> sách» next to «In nhãn». | S-F02-03 |
| D3c | Page size | 20 rows per page. | S-F02-03, S-F03-01 |
| D3d | Sort order | Floor → room → shelf (walking order along the shelves). | S-F02-03, FR-02-23 |
| D4 | QR label content and sheet | A4 portrait decal, 3 columns × 8 rows = 24 labels of 70×37 mm. Each label: QR code left; book title (max 2 lines, cut with "…"); «Tầng · Phòng · Kệ»; «Quét để xem thông tin và đánh giá». One label per book title, not per copy. | S-F02-03, M-F02-03-01, ui-conventions |
| D5 | Back button on S-F02-02 | None, in every case: S-F02-02 opens only by scanning the QR label with the phone camera. Exit = «Xem sách trên OPAC». | S-F02-02, ui-conventions, screen-transition |
| D6 | «Xem thêm đánh giá» on S-F02-02 | Yes, 10 reviews per page as on S-F02-01; shown while more published reviews remain (also S-F02-01). | S-F02-01, S-F02-02, AD-UC-06 |
| D7 | Staff sign-out and session length | «Đăng xuất» Secondary button in the header of S-F04-01, S-F02-03, S-F02-04 → S-F00-03. The staff session has no time-out; it ends only on «Đăng xuất». | Staff screens, FR-04-21, AD-UC-10, AD-UC-13 |
| D8 | Narrower screens | **Superseded: Reader part by D44, Staff part by D45.** Reader: designed at 360px, usable from 320px with no horizontal scroll; on wider screens one column, max 640px, centred. Staff: designed at 1280px, supported from 1024px; 1024–1279px columns shrink; below 1024px two-column layouts stack; not supported on phones. | ui-conventions §6.1, S-F00-03, S-F04-01 |
| D9 | S-F03-01: book with both formats; paging | Both Format labels shown; results paginated, 20 per page. | S-F03-01 |
| D10a | «Xu hướng» tag on S-F03-07 | Yes: books added from trending titles (FR-03-20) carry the Trend tag «Xu hướng». | S-F03-07, ui-conventions |
| D10b | «Sở thích» on S-F03-07 | Always shown (Secondary button) in every signed-in state; S-F03-07 → S-F03-02 at any time. | S-F03-07, screen-transition |
| D11 | Reason text for each recommendation | No, not in release 1. No new FR. | S-F03-07 |
| D12 | When is a book recorded as label-printed? | Only when staff choose «Đã in xong» in M-F02-03-01. «Đóng» or a failed print records nothing; the books stay in the list. | S-F02-03, M-F02-03-01, AD-UC-10, FR-02-08 |
| D13 | Title with copies on several shelves | Label and sort order use the primary shelf location returned by the sync (the one shown on S-F01-01). | S-F02-03, M-F02-03-01, FR-02-23 |
| D14 | S-F03-01: changing the access format | Results return to page 1. | S-F03-01 |
| D15 | Wording proposed during the review | Approved: S-F02-03 empty state «Tất cả sách bản giấy đã được in nhãn. Sách mới sẽ hiện ở đây sau lần đồng bộ danh mục tiếp theo.» (MSG-11) · S-F00-02 «Mã đã được gửi tới <email>.» (MSG-10). | S-F02-03, S-F00-02, ui-conventions §4 |
| D16 | Component for «Đã chọn <n> sách» | New component Selection counter (`.selection-counter`). | S-F02-03, ui-conventions §3 |
| D17 | Two Primary buttons in M-F02-03-01 | «In» is the Primary button; «Đã in xong» is a Secondary button. One Primary button per screen, no exception. | M-F02-03-01, ui-conventions |
| D18 | Ticks after «Đóng» in M-F02-03-01 | Kept, so staff can print again straight away. | S-F02-03, M-F02-03-01 |
| D19 | S-F03-01: which access format is selected when the screen first opens? | **None selected.** No results are shown until the reader chooses a format. | S-F03-01 |
| D20 | Review-guideline link «Xem quy định viết đánh giá của thư viện» on S-F02-01 / S-F02-02 (the library has no review-guideline page) | **Remove the link.** Under the review editor show one short hint line: «Đánh giá không được chứa từ ngữ xúc phạm, quảng cáo hoặc thông tin cá nhân.» (MSG-14). Staff use exactly these three criteria when removing a reported review (UC-13); supersedes AD-UC-13 Q1. No new screen. | S-F02-01 §3 #5, S-F02-02 §3 #6, notes; ui-conventions §3 Text area with counter, §4 MSG-14; AD-UC-13 business rules, `d3` |
| D21 | Component of the book block at the top of S-F02-01 and S-F02-02 | **Book row**, without a Format label. ui-conventions §3 Book row "Used on" adds S-F02-01, S-F02-02. | S-F02-01, S-F02-02, ui-conventions §3 |
| D22 | Should the confirmation modals M-F02-01-01, M-F02-01-02 and M-F02-04-01 quote the review text? | **No.** Short confirmation only; the review stays visible behind the dimmed overlay. | M-F02-01-01, M-F02-01-02, M-F02-04-01 (S-F02-01 §3.1–§3.2, S-F02-04 §3.1) |
| D23 | Map unavailable when S-F01-02 was opened from the OPAC menu (MSG-07 mentions shelf details "above") | New message **MSG-12** for the menu entry: «Bản đồ tạm thời không hiển thị được. Bạn thử lại sau nhé.» MSG-07 stays for opening the map from a book. | S-F01-02, ui-conventions §4 |
| D24 | S-F03-02 empty reading-history text | **Approved** as **MSG-13**: «Chưa có lịch sử đọc nào. Sách bạn mượn hoặc đọc trực tuyến sẽ tự động xuất hiện tại đây.» | S-F03-02, ui-conventions §4 |
| D25 | S-F03-06 link text on the book card | **«Xem chi tiết sách»**. | S-F03-06 |
| D26 | The 17 L8 rows "Default applied 2026-11-08; team to confirm", marked resolved from documents: L8-04, L8-05, L8-06, L8-07, L8-09, L8-10, L8-11, L8-12, L8-13, L8-14, L8-15, L8-16, L8-17, L8-18, L8-19, L8-21, L8-22 | **Confirmed**, as already used in screen-list, usage-flow and the specs. | activity-index L8 rows |
| D27 | AD-UC-01 Q1 (one line per copy on S-F01-01) vs D13 (primary shelf location) | S-F01-01 keeps **one line per physical copy, the primary shelf location (from the sync) listed first**; that primary location is the one used on QR labels and for the S-F02-03 order. | S-F01-01, ui-conventions §2, AD-UC-01 |
| D28 | Title font: SVN-Gilroy is not on Google Fonts and its licence is not free | **Plus Jakarta Sans** (Google Fonts, Vietnamese subset) for titles; Inter stays for all other text. Existing PNGs are not re-exported for the font only. | ui-conventions §1, §6 `font/heading`, font notes; [ui_tokens.css](../external_design/screens/src/ui_tokens.css) |
| D29 | Staff sign-in form drawn against the left edge of the 1280px frame | The form sits in one **Sign-in card centred horizontally and vertically**, title inside the card, Primary button full card width (reference: centred sign-in card layout). S-F00-03 redrawn in HTML and re-exported. | ui-conventions §3 Sign-in card, §6 `size/sign-in-card`; S-F00-03 |
| D30 | Does a staff sign-in write an audit entry? FR-04-12 says every sign-in does, but AD-UC-10 and AD-UC-13 drew none. | **Yes** (23/11/2026). A successful staff sign-in writes an audit entry with actor, action and time, right after the staff session starts. A rejected sign-in writes none, as for the reader sign-in (AD-UC-11). | AD-UC-10 `s15`, AD-UC-13 `s12`, SD-UC-10, SD-UC-13, S-F00-03, screen-list |
| D31 | S-F00-02 Error-4: the code could not be sent, but the email line MSG-10 says it was sent | **Hide MSG-10 (#13) in Error-4 only.** Every other S-F00-02 state keeps the full email line (D2, D15). Decided 23/11/2026. | S-F00-02 #13, Error-4; ui-conventions §4 MSG-10 |
| D32 | When is the label-print audit entry written (FR-04-12)? It was written when the sheet was produced, so «Đóng» without printing still left a "printed" entry. | **When staff choose «Đã in xong»**, right after the books are recorded as label-printed. Producing the sheet, «Đóng» or a failed print writes no entry. Decided 23/11/2026. | AD-UC-10 `s5`; S-F02-03; M-F02-03-01; screen-list |
| D33 | Paging of S-F03-01 (D9, D14) was in no FR. | Added to the text of **FR-03-12** in W1: 20 per page with page navigation; another access format returns to page 1. No new FR. Decided 23/11/2026. | W1 FR-03-12; AD-UC-03; S-F03-01 |
| D34 | Where is the reader's own «Đăng nhập» link on the OPAC? | **Only on the OPAC main menu**, as the screen transition draws it; every other sign-in starts from modal M-F00-01. Refines L8-13. Decided 23/11/2026. | screen-list S-F00-01; S-F00-01; screen-transition |
| D35 | Back on S-F03-01 when it was opened from the chatbot. | Back returns to **S-F03-06**; when opened from the OPAC it returns to the OPAC results. Approved with the 15-point fix list, 23/11/2026. | S-F03-01; screen-transition |
| D36 | A staff session already ended elsewhere (for example «Đăng xuất» in another tab). D7 has no time-out, but the specs of S-F02-03 and S-F04-01 re-check the session. | Keep the check: the next action on any staff screen changes nothing and opens **S-F00-03**. This is not a time-out. Approved with the 15-point fix list, 23/11/2026. | S-F04-01; S-F02-03; S-F02-04; screen-transition |
| D37 | S-F02-02 "Không tìm thấy sách": there is no book for «Xem sách trên OPAC», so the state was a dead end. | The error state shows a Text link **«Về OPAC»** to the existing OPAC main menu. No new FR. Approved with the 15-point fix list, 23/11/2026. | S-F02-02; AD-UC-06; screen-transition |
| D38 | Team capacity for DBIZ3: 360 or 240 person-hours? | **360 person-hours** (6 people × 12 weeks × 5 h; Parameters §6). Replaces the 240 h in W5_Handover open question 6. Decided 23/11/2026. | [GROUP-H_UC_FR_COST.xlsx @ cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/blob/cd61897/%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx): Parameters §6, W2_Rollup, W5_Handover |
| D39 | A signed-out reader sees Report on every review; after sign-in the action continues by itself (D1), so a reader could report their own review, against UI Q14. | **Block it.** After sign-in the system checks who wrote the review; on the reader's own review it saves nothing and shows «Bạn không thể báo cáo đánh giá của chính mình.» New **FR-02-24** (Could). Decided by Chi, 23/11/2026. | W1 FR-02-24; AD-UC-14 `d3`, `s5`; SD-UC-14; S-F02-01; screen-list |
| D40 | One label per title (D4): how does a second physical copy get a QR label? | **All copies of a title share one QR code; staff only reprint it.** S-F02-03 gets the filter «Chưa in nhãn» / «Đã in nhãn»; under «Đã in nhãn» staff tick books and choose «In lại nhãn». A reprinted label has the QR code, title and scan line, **no shelf location**, because the copy may sit on another shelf. Its «Đã in xong» writes the audit entry and changes no status. New **FR-02-25** (Should); FR-02-07 changed. Refines D4 and D13. Decided by Chi, 23/11/2026. | W1 FR-02-07, FR-02-25; AD-UC-10 `d13`–`d16`, `a11`–`a16`, `s17`–`s21`; SD-UC-10; S-F02-03; M-F02-03-01; ui-conventions; screen-list; screen-transition |
| D41 | Staff can tick more than 24 books, but a sheet holds 24 labels. | **The sheet continues on further A4 pages** in the same preview; «Đã in xong» records every book on all pages. FR-02-08 changed. Decided by Chi, 23/11/2026. | W1 FR-02-08; AD-UC-10 `s4`; SD-UC-10; S-F02-03; M-F02-03-01; ui-conventions |
| D42 | FR-03-02 and FR-03-13 said "opens or downloads an online book", but the platform has no viewer or download and cannot see what happens on the OPAC (W5 open question 1). | **Record the selection.** Both FRs now fire when a reader selects an online book in the results of this platform («Mở trên OPAC»); reading or downloading on the existing OPAC is not tracked. No cost change. Decided by Chi, 23/11/2026. | W1 FR-03-02, FR-03-13; W5 question 1; AD-UC-03 `r3`, `s4`, `s5`; AD-UC-07 `e1` |
| D43 | Does the 360 h team capacity cover Must + Should only, or also the Could pool (W5 open question 6)? | **Must + Should.** The Could pool is optional. Must + Should = 345.6 h, within 360 h. Decided by Chi, 23/11/2026. | W5 question 6; W2_Rollup |
| D44 | The Reader screen specs give 360px as the smallest supported width, but D8 said usable from 320px. | **Reader screens are supported from 360px**, the design frame; narrower widths are not supported. The specs keep their px values. Decided by Chi, 23/11/2026. | ui-conventions §5, §6.1; UI Q7 |
| D45 | Staff specs disagreed: S-F02-04 gave 1280px as the smallest width, S-F00-03, S-F02-03 and S-F04-01 followed D8 (from 1024px). | **Staff screens are supported from 1280px**, the design frame; narrower widths are not supported, so no layout shrinks or stacks. Decided by Chi, 23/11/2026. | ui-conventions §5, §6.1; UI Q7; S-F00-03, S-F02-03, S-F02-04, S-F04-01 §8 |
| D46 | Colour of a Text link inside an error Banner («Về OPAC» on S-F02-02 was red, «Lọc theo hình thức» on S-F03-06 was blue). | **`colour/error-red`, underlined**, in every error Banner (contrast 4.92:1; `colour/link` is 4.26:1). Set once in [ui_tokens.css](../external_design/screens/src/ui_tokens.css). The S-F02-02 link is «Xem sách trên OPAC» everywhere. Decided by Chi, 23/11/2026. | ui-conventions §3 Text link; S-F02-02; S-F03-06; [ui_tokens.css](../external_design/screens/src/ui_tokens.css) |
| D47 | Answers from the library (W5 questions 2, 3, 4; L8-13). | (a) The internal system holds the access format of every book. (b) The library agrees to the new links on the existing OPAC pages. (c) Library staff tell the team when a room is added, renamed or removed, and watch errors and availability after release. W5 question 5 (privacy notice and retention of the anonymous read log) stays open, not blocking. Reported by Chi, 23/11/2026. | W5 questions 2–4; L8-13; FR-03-12, FR-01-05, FR-04-15 |
| D48 | The daily sync had no use case (Inputs check 3, L8-20). | **UC-15 Sync data from the library internal system**, started by time, F-04, Must (FR-04-09). W0 Table 1 and the W1 source traces of FR-04-09, FR-04-10, FR-04-11 and FR-01-05 name UC-15; AD-UC-15 and SD-UC-15 drawn. The Use Case Diagram PDF still has to show it. Decided by Chi, 23/11/2026. | W0 Table 1, Table 2 F-04; W1; AD-UC-15; SD-UC-15; screen-list; usage-flow; activity-index |
| D49 | Workbook clean-up of 23/11/2026. | FR-02-15 split in two sentences (book not found: no list; book without reviews: invite the first review), as AD-UC-05 and SD-UC-05 draw it. FR-02-08 FP type EQ → **EI** (it now records data); sizes of FR-02-08, FR-02-23 and FR-04-21 unchanged. W1 column G now holds the real prerequisite of each FR (first L3 row). Decided by Chi, 23/11/2026. | W1 FR-02-15, FR-02-08, column G |
| D50 | FR-04-13 "Deploy automatically" (Must) deploys only when the tests of FR-04-14 (Should) pass. | **FR-04-14 "Run automated tests on every change" raised to Must** (W4 rule R1, effort unchanged). Must: 252.4 person-hours, 68.92 million VND, 49.8% of in-scope effort (under 60%). Must + Should and the full scope do not change. Decided by Chi, 23/11/2026. | W4 FR-04-14; W2_Rollup; README |
| D51 | Workbook or Markdown as the source of FRs and cost? | **Markdown.** From 23/11/2026 the FRs are kept in [fr_list.md](../requirements/fr_list.md), the scope tables in [scope.md](scope.md) and [use_case.md](../system_design/use_case.md), and effort, cost and cash flow in [cost.md](../requirements/cost.md). The workbook is frozen at commit [cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/tree/cd61897/%5BDBIZ%202%5D%20GROUP%20H) and is not edited again. Labels W0 … W6 used in other documents now point to these files (map in [README.md](../../README.md#workbook-labels)). AI tools do not read cost.md ([AGENTS.md](../../AGENTS.md)). Decided by Chi, 23/11/2026. | Supersedes "New or changed FRs are written directly in the workbook" (§ New FRs proposed by ui-conventions) |
| D52 | How should the repository be laid out? | **Everything in `docs/`, file and folder names in lower-case snake_case** (`ad_uc_01.md`, `screen_spec_s_f00_01.md`). Folders: `project_brief/` (CVCA, context diagram, scope, this index), `system_design/` (use cases, sequence diagrams, system architecture), `requirements/` (FR list, cost), `activity_diagram/`, `external_design/`. CVCA, Context and Use Case diagrams redrawn in Mermaid with the changes agreed on 23/11/2026; the PDFs and the workbook stay unchanged in Git history at commit [cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/tree/cd61897/%5BDBIZ%202%5D%20GROUP%20H); the local `archive/` copy is not pushed (.gitignore). IDs inside documents (AD-UC-01, S-F00-01, FR-02-08) do not change. Every file mention is a clickable link. Decided by Chi, 23/11/2026. | Whole repository; [README.md](../../README.md) |

### Requirement changes from these decisions

| FR | Change | Status in GROUP-H_UC_FR_COST.xlsx |
|---|---|---|
| FR-02-23 (new) | WHEN signed-in On-site Staff open QR label printing, the system SHALL list the physical books in the synced catalogue that have not yet had a QR label printed, 20 per page, ordered by each book's primary shelf location (floor, room, shelf code). | In W1 (rows 138–139) and W4 (row 96), 23/11/2026 |
| FR-04-21 (new) | WHEN signed-in On-site Staff choose Sign out, the system SHALL end the staff session and SHALL open the staff sign-in screen; the staff session SHALL remain valid until the staff member signs out. | In W1 (rows 144–145) and W4 (row 99), 23/11/2026 |
| FR-02-08 (changed) | …and WHEN the staff confirm that the sheet was printed («Đã in xong»), the system SHALL record that a label has been printed for each book on the sheet. | Updated in W1 (rows 30–31), 23/11/2026 |
| FR-03-12 (changed) | WHEN a reader selects an access format (Online, Physical, or Both), the system SHALL filter and retrieve matching books and display the results with their corresponding access-format labels, 20 per page with page navigation. WHEN the reader selects another access format, the system SHALL return the results to page 1. | Updated in W1 (rows 56–57), 23/11/2026 (D33) |
| FR-02-24 (new) | IF a signed-in Reader reports a review that they wrote, THEN the system SHALL not save the report and SHALL display that a reader cannot report their own review. | In W1 (rows 140–141) and W4 (row 97), Could, 23/11/2026 (D39) |
| FR-02-25 (new) | WHEN signed-in On-site Staff select physical books that already have a printed label and choose Reprint labels («In lại nhãn»), the system SHALL produce a printable sheet with the existing QR code and the title of each selected book, without generating a new code and without a shelf location, and WHEN the staff confirm that the sheet was printed («Đã in xong»), the system SHALL write the audit entry and SHALL keep those books in the list of labelled books. | In W1 (rows 142–143) and W4 (row 98), Should, 23/11/2026 (D40) |
| FR-02-07 (changed) | …SHALL generate one unique QR code linked to that book title; all physical copies of the title share this code. | Updated in W1, 23/11/2026 (D40) |
| FR-02-08 (changed) | …a printable sheet of QR code labels for the selected books, 24 labels per A4 page, continuing on further A4 pages when more than 24 books are selected… | Updated in W1, 23/11/2026 (D41) |
| FR-03-02 (changed) | WHEN a signed-in library card reader selects an online book in the results of this platform to open it on the OPAC, the system SHALL add that book to the reading history of that reader. | Updated in W1 (name, criterion, work item), 23/11/2026 (D42) |
| FR-03-13 (changed) | WHEN any reader selects an online book in the results of this platform to open it on the OPAC, the system SHALL record the book and the time of the selection without any reader identity. | Updated in W1, 23/11/2026 (D42) |
| FR-02-15 (changed) | IF the requested book does not exist, THEN the system SHALL end the request without displaying a review list and SHALL display that there are no reviews to show. IF the book exists but has no published review, THEN the system SHALL display that the book has no reviews yet and SHALL invite the reader to write the first review. | Updated in W1, 23/11/2026 (D49) |

# Shared documents

## ui-conventions

Sources: [ui_conventions.md](../external_design/ui_conventions.md) header table "Step 2 decisions" (Q1–Q7), §7 "Open questions" and "Closed on …" lists,
the "Status" column of the §1 modal table, the font and colour notes, and §7 "New FRs proposed by this document".

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| UI Q1 | Interface language | **Vietnamese** — the website is for Vietnamese users; every interface text is Vietnamese with full diacritics; no language switch (no FR asks for one). | 14/11/2026 · group | ui-conventions §1 |
| UI Q2 | Reader frame | 360px, exported 3x (1080px). | 14/11/2026 · group | ui-conventions §6; Reader specs |
| UI Q3 | Staff frame | 1280px, exported 1x. | 14/11/2026 · group | ui-conventions §6; staff specs |
| UI Q4 | Follow the look of the current OPAC? | **Yes: use the colour palette of the current OPAC (opac.nlv.gov.vn).** No logo, library name or OPAC images are copied. | 13/11/2026 · group | ui-conventions §6 colours; §3 Floor plan |
| UI Q5 | Fonts | **Two fonts:** Plus Jakarta Sans for titles (D28, 22/11/2026; was SVN-Gilroy, the current OPAC font), Inter for all other text. | 13/11/2026, confirmed 14/11/2026, changed 22/11/2026 (D28) · group | ui-conventions §6 `font/heading`, `font/body`, font notes |
| UI Q6 | Wireframe fidelity | Mid: token colours, real text, grey "Cover" blocks, no images. | 14/11/2026 · group | ui-conventions §3 Book row, §6 intro |
| UI Q7 | Screens narrower or wider than the frame | See D8, D44 and D45 (ui-conventions §6.1: Reader supported from 360px, one column up to 640px; Staff from 1280px, not on smaller screens). | 22/11/2026 · group decision | ui-conventions §5, §6.1; every spec §8 |
| UI Q8 | Library card number format | Exactly 7 digits; may start with 0 (keep leading zeros, store as text); no spaces. | 13/11/2026 · group (ui-conventions v0.3, v0.4) | ui-conventions §2; S-F00-01 |
| UI Q9 | How is the reviewer's name shown? | The reader chooses, per review: the full name exactly as registered on the library card account, or «Bạn đọc ẩn danh» (Checkbox «Đăng ẩn danh», unchecked by default; FR-02-22). | 13/11/2026 · group (ui-conventions v0.4, v0.5) | ui-conventions §2 Reviewer name; S-F02-01, S-F02-02 |
| UI Q10 | The brand colour is red and red also means error: how are they kept apart? | Two separate tokens, `colour/brand-red` #8B0000 (current OPAC colour) and `colour/error-red` #C62828. The Primary button is always a solid brand-red fill with white text and no icon; an error is never a solid fill (light #FDECEA background, red border and text, "!" icon, under the field; the field gets a 2px red border). | 14/11/2026 · group | ui-conventions §6 colour notes; §3 Inline error |
| UI Q11 | OTP code length | 6 digits (FR-04-04 updated in W1 on 14/11/2026). | 14/11/2026 · group | ui-conventions §2; S-F00-02 |
| UI Q12 | Where does MSG-06 send the reader? | The information desk on the ground floor. Same as AD-UC-01 Q2. | 14/11/2026 · group | ui-conventions §4 MSG-06 |
| UI Q13 | Accept the FRs proposed by ui-conventions (FR-02-22 anonymous review, FR-04-19 OTP attempts left, FR-04-20 network or loading error)? | **Accepted**; they are rows 132–137 of W1_FunctionList (FE + BE rows). Their initial priorities (former §7 open question 1, "confirm with the group") are resolved from documents: W4_Prioritization records FR-02-22 Should, FR-04-19 Should, FR-04-20 Must (workbook read 22/11/2026). Costing in W2 is a pending task. | 19/11/2026 · team; priorities resolved from documents 22/11/2026 | ui-conventions §2, §4 MSG-04; screen-list notes |
| UI Q14 | May a reader report their own review? | No: Report is offered only on other readers' reviews. Same as AD-UC-14 Q2. | 19/11/2026 · team | ui-conventions §3 Review item |
| UI Q15 | Label sheet for M-F02-03-01 (former §7 open question 2) | See D4 | 22/11/2026 · group decision | ui-conventions §3 Label sheet |
| UI Q16 | The §3 rule "one Primary button per screen" had an exception for M-F02-03-01 («In» and «Đã in xong» both Primary). Keep it? | See D17 — no exception; «In» is Primary, «Đã in xong» is Secondary. | 22/11/2026 · group decision | ui-conventions §1 labels, §3 Secondary button, Label sheet, Rules |
| UI Q17 | Exact titles of the modals M-F02-01-01, M-F02-01-02 and M-F02-03-01 (were `[NEEDS CLARIFICATION: confirm exact title in modal notes]`) | Resolved from documents (element 1 of each modal's notes): M-F02-01-01 «Xoá đánh giá?», M-F02-01-02 «Báo cáo đánh giá?», M-F02-03-01 «Xem trước trang nhãn mã QR». M-F02-04-01 keeps «Gỡ đánh giá?», not «Gỡ đánh giá này?» (19/11 review). | 22/11/2026 · resolved from documents | ui-conventions §1 modal table |

### New FRs proposed by ui-conventions (moved from §7)

Accepted by the team on 19/11/2026 and reported as present in [GROUP-H_UC_FR_COST.xlsx @ cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/blob/cd61897/%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx), sheet W1_FunctionList, rows 132–137 (FE + BE L3 rows each), per the 19/11 review. Verify the latest workbook before release.
IDs are the next free numbers in W1 (FR-02-21 and FR-04-18 were the last ones on 14/11/2026).

| FR | Feature | Name | Actor | EARS acceptance criterion | Used in |
|---|---|---|---|---|---|
| FR-02-22 | F-02 | Post a review under the reader's name or anonymously | Library Core System | WHEN a signed-in reader submits or edits a review, the system SHALL let the reader choose to post it anonymously, and SHALL display the reader's full name as registered on the library card account, or "Bạn đọc ẩn danh" when the reader chose to post anonymously. | Section 2 Reviewer name; Checkbox "Đăng ẩn danh" on S-F02-01, S-F02-02; Review item |
| FR-04-19 | F-04 | Show the remaining OTP attempts | Library Core System | IF a reader submits an incorrect OTP and fewer than 5 incorrect attempts have been made for that OTP, THEN the system SHALL display the number of attempts left. | Section 2 OTP attempts left; S-F00-02 |
| FR-04-20 | F-04 | Handle a network or loading error | Library Core System | IF a screen cannot load or save its data because of a network or server error, THEN the system SHALL keep the data already shown, display an error message that the page could not load, and SHALL allow the user to try again. | MSG-04; Banner error on every screen |
| FR-02-23 (in W1 since 23/11/2026) | F-02 | List physical books awaiting a QR label | Library Core System | WHEN signed-in On-site Staff open QR label printing, the system SHALL list the physical books in the synced catalogue that have not yet had a QR label printed, 20 per page, ordered by floor, room and shelf code of each book's primary shelf location returned by the sync. | S-F02-03 list; Pagination; Selected books count |
| FR-04-21 (in W1 since 23/11/2026) | F-04 | Sign out of the staff page | Library Core System | WHEN signed-in On-site Staff choose Sign out, the system SHALL end the staff session and SHALL open the staff sign-in screen. The system SHALL keep the staff session valid until the staff member signs out (no time-out). | Screen header «Đăng xuất» on S-F04-01, S-F02-03, S-F02-04 |

FR-02-23 and FR-04-21 come from Group decision 22/11/2026 (D3, D7). They were added to W1 and W4 on 23/11/2026.
Same decision, changed FR: **FR-02-08** adds "…and WHEN the staff confirm that the sheet was
printed («Đã in xong»), the system SHALL record that a label has been printed for each book on the sheet." (wording
of the follow-up Group decision 22/11/2026, D12; FR-02-23 ordering uses the primary shelf location, D13).
~~New or changed FRs are written directly in the workbook; no separate file is kept for them.~~ Superseded by D51: new or changed FRs are written directly in [fr_list.md](../requirements/fr_list.md).

## screen-list

Sources: [screen_list.md](../external_design/screen_list.md) "Notes on the table", "Modals and overlays", "What is deliberately not a screen" (decision
narratives and inline group-decision citations).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| SL-1 | Which new FRs come from the 22/11/2026 decisions, and do they raise screen priorities? | See D3, D7, D12, D13: FR-02-23 (list physical books awaiting a QR label), FR-04-21 (staff sign-out, no staff time-out) and the FR-02-08 change (record on «Đã in xong»). FR-04-21 is Should and does not raise the priority of S-F00-03, S-F02-03, S-F02-04 or S-F04-01 (priority rule L8-14). They are in W1 and W4 since 23/11/2026; costing them is a pending task. | 22/11/2026 · group decision | screen-list "Notes on the table"; S-F02-03, S-F04-01 rows |
| SL-2 | Is modal M-F00-02 "Staff sign-in required" still needed? | No; dropped on 2026-11-08 because staff sign in on S-F00-03 before the staff page opens. See L8-02. | 2026-11-08 · team | screen-list "What is deliberately not a screen" |
| SL-3 | M-F02-03-01: button types, and what happens to the ticks after «Đóng»? | See D17 («In» Primary; «Đã in xong», «Đóng» Secondary) and D18 (ticks kept on S-F02-03 so staff can print again straight away). | 22/11/2026 · group decision | screen-list M-F02-03-01 and S-F02-03 rows |

## screen-transition

Sources: [screen_transition.md](../external_design/screen_transition.md) prose under both diagrams and "Checks before you save" (decision narratives and inline
citations).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| ST-1 | Where does the reader land after sign-in or «Huỷ», and is the pending action kept? | See L8-01 and D1 (the eight "[OTP accepted]" arrows are one rule; «Huỷ» follows the same return rule and is not drawn). | 2026-11-08 · team; 22/11/2026 · group decision | Reader diagram, sign-in return rule |
| ST-2 | How does the reader leave S-F02-02, and does it have Back? | «Xem sách trên OPAC» to the existing Book Detail (L8-08); no Back (D5). | 2026-11-08 · team; 22/11/2026 · group decision | Reader diagram; check "No dead end" |
| ST-3 | When can the reader go from S-F03-07 to S-F03-02? | Any time through «Sở thích» (D10b), or through «Thiết lập sở thích đọc ngay» when there is no reading data yet. | 22/11/2026 · group decision | Reader diagram; usage-flow path UC-09 to UC-07 |
| ST-4 | How do staff leave the staff screens; is there a session time-out arrow? | «Đăng xuất» on S-F04-01, S-F02-03, S-F02-04 → S-F00-03 (FR-04-21; D7); no time-out, so no "session expired" arrow. | 22/11/2026 · group decision | Staff diagram |
| ST-5 | Why do the usage-flow paths assume joined flows? | The single-use-case flows were joined on 2026-11-09 (L8-22). | 2026-11-09 · team | Check "Usage-flow paths" |

## usage-flow

Sources: [usage_flow.md](../external_design/usage_flow.md) "Note" (Inputs check rows logged as open questions) and prose citing activity-index open
questions.

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| UF-1 | activity-index Inputs check rows 3, 4, 5 and 7 were "logged as open questions" in usage-flow: are they open questions? | No: they are work items in their source documents (Use Case Diagram, sequence diagrams) and do not change the usage flows. They are listed under Pending tasks (same tasks as in the activity part: Inputs check 3, 4, 5, 7). Rows 4, 5 and 7 were closed on 23/11/2026 (SD-UC-01 … SD-UC-14). | 22/11/2026 · reclassified under the 22/11 decision-index rule | usage-flow "Note" |
| UF-2 | Keep the flows that had one use case on each path? | Joined into 3 Reader flows and 1 staff flow. See L8-22. | 2026-11-09 · team | usage-flow, all four flows; checks |
| UF-3 | Keep the arrow UC-05 to UC-04 although AD-UC-05 has no branch to UC-04? | Kept: S-F02-01 hosts both use cases. See L8-17 (adding the branch to AD-UC-05 is a pending task). | 2026-11-08 · team | usage-flow "Reader: read and review a book" |
| UF-4 | Which use case owns FR-01-03; what does the arrow UC-01 to UC-02 mean? | UC-01; the arrow stands for browsing the map further. See L8-18. | 2026-11-08 · team | usage-flow "Reader: find my way in the library" |
| UF-5 | Which diagram owns the history entry when an online book is opened (FR-03-02)? | UC-07 (`e1`), triggered by AD-UC-03 `s5`. See L8-19. | 2026-11-08 · team | usage-flow "Use cases without a flow" |
| UF-6 | Name and ID of the planned sync use case | Listed without an ID as "Sync data from the library internal system (planned)" until the Integrator gives it an ID and draws its diagram. See L8-20. | 2026-11-08 · team | usage-flow "Use cases without a flow"; screen-list "What is deliberately not a screen" |

# Screens and modals

## S-F00-01

Sources: [screen_spec_s_f00_01.md](../external_design/screens/specs/screen_spec_s_f00_01.md) §9; [s_f00_01_notes.md](../external_design/screens/notes/s_f00_01_notes.md) "Open questions".

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F00-01 Q-Cancel | On «Huỷ», should the sign-in origin keep or drop the pending action? | See D1 | 22/11/2026 · group decision | S-F00-01 §3.1, §5 #3 and #5, SR-004; S-F00-02; M-F00-01 |
| S-F00-01 notes Q-Format | What format does the library card number have? | Exactly seven digits, kept as text so a leading zero is not lost (ui-conventions §2). | 13/11/2026 (ui-conventions v0.3) · team | S-F00-01 #2, SR-001 |

## M-F00-01

Sources: [m_f00_01_notes.md](../external_design/screens/notes/m_f00_01_notes.md) "Open questions" (the modal's spec is [screen_spec_s_f00_01.md](../external_design/screens/specs/screen_spec_s_f00_01.md) §3.1).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| M-F00-01 notes Q-Shared | Do all entry screens use the same sign-in prompt? | Yes: one shared modal M-F00-01 on all seven entry screens (S-F01-01, S-F02-01, S-F02-02, S-F03-02, S-F03-03, S-F03-06, S-F03-07); see L8-01 (activity index). Pending action kept after «Huỷ» and continued after OTP: see D1. | 08/11/2026 · team; 22/11/2026 · group decision (D1) | M-F00-01; S-F00-01 §3.1 |

## S-F00-02

Sources: [screen_spec_s_f00_02.md](../external_design/screens/specs/screen_spec_s_f00_02.md) §9; [s_f00_02_notes.md](../external_design/screens/notes/s_f00_02_notes.md) "Open questions".

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F00-02 Q-Email | Mask the email address on the OTP screen? | See D2 (no masking). Wording «Mã đã được gửi tới <email>.»: see D15. | 22/11/2026 · group decision | S-F00-02 #13, §4 Default, SR-006 |
| S-F00-02 Q-Cancel | On «Huỷ», how is the pending action restored without a valid session? | See D1 | 22/11/2026 · group decision | S-F00-02 §1, §5 #5, SR-005, SR-006 |
| S-F00-02 notes Q1 | Should the form display a masked email address? | See D2 | 22/11/2026 · group decision | S-F00-02 notes #13 |
| S-F00-02 notes Q2 | On «Huỷ», how does the origin restore a protected action without a valid session? | See D1 | 22/11/2026 · group decision | S-F00-02 notes Actions |
| S-F00-02 notes Q-Attempts | Show the number of attempts left? | Yes, 4 to 1 (ui-conventions §2; FR-04-19). | 14/11/2026 (ui-conventions v0.6) · team | S-F00-02 #8, SR-002 |

## S-F00-03

Sources: [screen_spec_s_f00_03.md](../external_design/screens/specs/screen_spec_s_f00_03.md) header, §2, §9, "Review handoff"; [s_f00_03_notes.md](../external_design/screens/notes/s_f00_03_notes.md) "Open questions".

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F00-03 Q1 | Is a separate HTML export required besides the Draw.io source? | **Resolved from documents:** no. `huong-dan/screen-spec-chung.md` §4.1 accepts the wireframe source as HTML, `.drawio` or a Figma link; the source is [wireframes_f00_f02_f04.drawio](../external_design/screens/src/wireframes_f00_f02_f04.drawio). | 22/11/2026 · resolved from documents (also the screen-spec review of 22/11/2026, §3) | S-F00-03 header "Wireframe source" |
| S-F00-03 Q5 | The form sat against the left edge of the 1280px frame | See D29: centred Sign-in card; source now [s_f00_03.html](../external_design/screens/src/s_f00_03.html) (replaces the S-F00-03 page of [wireframes_f00_f02_f04.drawio](../external_design/screens/src/wireframes_f00_f02_f04.drawio)); all 9 PNGs re-exported. | 22/11/2026 · group decision (D29) | S-F00-03 header, §2, §3 #1, notes |
| S-F00-03 Q2 | Which Default / Loading / Error PNG exports exist, and are they re-exported at 1280px? | **Resolved from documents:** `screens/img/` holds [s_f00_03.png](../external_design/screens/img/s_f00_03/s_f00_03.png), -loading, -error, -error-2, each with a -numbered copy, all 1280 × 900 px (checked 22/11/2026). The colour-token check is a pending task. | 22/11/2026 · resolved from the image files | S-F00-03 §2 |
| S-F00-03 Q3 | Correct the Draw.io colours to v0.8 tokens and verify the 1280px width (the §7 review had flagged 1693px). | **Resolved from documents (width):** all exports are now 1280px. Colour-token check moved to Pending tasks. | 22/11/2026 · resolved from the image files | S-F00-03 §2 |
| S-F00-03 Q4 | Staff layout below the 1280px design frame? | See D8 | 22/11/2026 · group decision | S-F00-03 §8 |
| S-F00-03 notes Q-Rejection | Do a wrong account and an account without the staff role show different messages? | No: one generic rejection for both (FR-04-18); see L8-03 (activity index). | 08/11/2026 · team | S-F00-03 #6, §4 Error, SR-003 |

## S-F01-01

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F01-01 Q1 | Is «Đã lưu sách vào danh sách của bạn.» the approved success Toast wording for FR-03-06? | **Yes.** The screen owner writes the screen's own wording following the ui-conventions §4 patterns; the text follows the Success pattern "what is done" (like «Đã đăng đánh giá.»). The wording check is part of the ui-conventions §7 re-review (Pending tasks). | 22/11/2026 · Resolved from documents (ui-conventions §4 "Patterns" and Success row) | S-F01-01 §3 #8, §4 Success; notes #10 |
| S-F01-01 Q2 | Should the already-saved feedback (FR-03-24) stay an informational Toast? | **Yes.** ui-conventions §4 "Already done" gives exactly «Sách này đã có trong danh sách của bạn.» (FR-03-24); §3 Toast has an informational state. | 22/11/2026 · Resolved from documents (ui-conventions §3 Toast, §4) | S-F01-01 §3, §4 Message — already saved |
| S-F01-01 Q3 | Multiple physical copies: grouped, or one shelf-location line each? | **One Shelf location line per physical copy**, the primary shelf location from the sync listed first: see D27. | 22/11/2026 · Resolved from documents (AD-UC-01 Q1, decided 04/11/2026; ui-conventions §2 Shelf location; FR-01-01); order: D27 | S-F01-01 §3 #3, SR-001 |
| S-F01-01 Q4 | Are the final numbered and state exports separate 1080px images that comply with v0.8? | **Size: yes** — every default, state and numbered PNG of S-F01-01 is a separate file 1080px wide (checked 22/11/2026). Compliance with the conventions is a re-review → Pending tasks. | 22/11/2026 · Resolved from files (`screens/img/S-F01-01/S-F01-01*.png`) | S-F01-01 §2, checklist |
| S-F01-01 Q5 | Committed wireframe source path under `screens/src/`? | No wireframe source file of S-F01-01 is in the repository; the header field now states this. Committing the source is a to-do → Pending tasks. | 22/11/2026 · Resolved from files (`screens/src/` listing) | S-F01-01 header "Wireframe source" |
| S-F01-01 notes Q1 | UI Conventions §3 names no standalone "Book title" component. | Use **Section title** ("heading for a group of content, including book sections", used on S-F01-01). Notes #2 component changed from "Heading / text" to Section title; spec §3 #2 already used it. | 22/11/2026 · Resolved from documents (ui-conventions §3 Section title) | notes #2; spec §3 #2 |
| S-F01-01 notes Q2 | Exact wording of the successful-save Toast. | Same as S-F01-01 Q1. | 22/11/2026 · Resolved from documents | notes #10 |
| S-F01-01 notes Q3 | Must the second copy's floor, room and shelf codes be confirmed against synced data? | **No confirmation needed.** The screen shows the synced shelf location of each copy (FR-01-01; data source in spec §3 #3); the wireframe values are examples (ui-conventions Q6: mid-fidelity wireframes with example text). | 22/11/2026 · Resolved from documents (FR-01-01; ui-conventions Q6) | notes #5; spec §8 |
| D27 (S-F01-01) | AD-UC-01 Q1 (one line per copy) vs D13 (primary shelf location) on S-F01-01 | See D27 | 22/11/2026 · group decision (D27) | S-F01-01 §3 #3, §4 Default, SR-001; notes #4, Default; ui-conventions §2 Shelf location |

## S-F01-02

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F01-02 Q1 | The numbered image has no marker 2 for the title: update the image, or keep the title inside element 1? | **Already fixed in the image:** the current [s_f01_02_numbered.png](../external_design/screens/img/s_f01_02/s_f01_02_numbered.png) shows marker 1 on Back and marker 2 on the title. Spec §3 rows 1 (Back button) and 2 (Screen title) now match the notes. | 22/11/2026 · Resolved from files ([s_f01_02_numbered.png](../external_design/screens/img/s_f01_02/s_f01_02_numbered.png)) | S-F01-02 §3 #1, #2; checklist |
| S-F01-02 Q2 | Exact floor inventory and complete room-code inventory from synced data? | **Not needed for the spec.** Floors, rooms and room codes are read from the synced floor and room data when the map opens (FR-01-02; room codes are those of the Library Internal System, AD-UC-02 business rules / FR-01-04). Wireframe values (Tầng 1–3, R-201–R-204) are examples. | 22/11/2026 · Resolved from documents (FR-01-02; AD-UC-02 §1) | S-F01-02 §8, SR-001, SR-010; notes #4 |
| S-F01-02 Q3 | Floor-plan geometry / data source? | **Block plan, one tile per room, no real library drawing**, built from the synced floor and room data. | 22/11/2026 · Resolved from documents (ui-conventions §3 Floor plan and Room tile, Q4; FR-01-02) | S-F01-02 §3 #4, §8 |
| S-F01-02 Q4 | Are all state images exported separately at 1080px and compliant with v0.8? | **Size: yes** — every default, state and numbered PNG of S-F01-02 is a separate file 1080px wide (checked 22/11/2026). Compliance check → Pending tasks. | 22/11/2026 · Resolved from files (`screens/img/S-F01-02/S-F01-02*.png`) | S-F01-02 §2, checklist |
| S-F01-02 Q5 | Committed wireframe source path under `screens/src/`? | No source file in the repository; header field states this. To-do → Pending tasks. | 22/11/2026 · Resolved from files | S-F01-02 header |
| S-F01-02 notes Q2 | Confirm the complete synced floor and room-code inventory. | Same as S-F01-02 Q2. | 22/11/2026 · Resolved from documents | notes #4 |
| S-F01-02 §3 #5 label | The spec used the English label "Your book is here" for the book's room. | **«Sách của bạn ở đây»**, as in ui-conventions §3 Room tile and §5, and in the S-F01-02 notes #5. Corrected in spec §3 #5, §4 Success, SR-008. | 22/11/2026 · Resolved from documents (ui-conventions §3, §5) | S-F01-02 §3 #5, §4, SR-008 |
| S-F01-02 notes Q1 | MSG-07 says shelf details remain "above", but a reader who opens the map from the OPAC menu has none. | See D23 | 22/11/2026 · group decision (D23) | S-F01-02 §3 #7, §4 Error, §5 #4, SR-006, §7 FR-01-10; notes #7, States, Actions; ui-conventions §4 MSG-12 |

## S-F02-01

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F02-01 Q1 | May a reader report their own review? | See AD-UC-14 Q2: **No.** «Báo cáo đánh giá» only on other readers' reviews; own reviews show «Sửa» and «Xoá đánh giá». | 19/11/2026 · team (AD-UC-14 Q2) | S-F02-01 SR-002, §3 #7–#8; M-F02-01-02 |
| S-F02-01 Q3 | Does «Xem thêm đánh giá» (#9) append the next 10 reviews or replace the page? | **Append** below the list; the button hides when no published reviews remain. The product has two separate components: Load more button (reviews, S-F02-01/S-F02-02) and Pagination («Trang trước» / «Trang sau», replaces the page, S-F02-03/S-F03-01). D6 makes S-F02-02 behave the same, and S-F02-02 #10 appends. | 22/11/2026 · Resolved from documents (ui-conventions §3 Load more button vs Pagination; D6; FR-02-02) | S-F02-01 §3 #9, §5 row 10; notes #9 |
| S-F02-01 Q6 | Confirm modal titles «Xoá đánh giá?» (M-F02-01-01), «Báo cáo đánh giá?» (M-F02-01-02) and the cancel label «Huỷ». | **Confirmed.** ui-conventions §1 makes the modal notes the source of truth for modal titles, and the notes give these titles; «Huỷ» is the standard "Cancel (in a modal)" label. Listed as answered (ui-conventions §1) in the review of 22/11/2026. ui-conventions §1 modal table still to be filled → Pending tasks. | 22/11/2026 · Resolved from documents (ui-conventions §1; M-F02-01-01 / M-F02-01-02 notes) | S-F02-01 §3.1, §3.2; ui-conventions §1 |
| S-F02-01 SR-004 | When is «Xem thêm đánh giá» shown? | See D6 (shown whenever more published reviews remain, not "more than 10 remain"). | 22/11/2026 · group decision (D6) | S-F02-01 SR-004, §3 #9; notes #9 |
| S-F02-01 notes Q1 | May a reader report their own review? | Same as S-F02-01 Q1 (see AD-UC-14 Q2). | 19/11/2026 · team (AD-UC-14 Q2) | notes #8 |
| S-F02-01 notes Q3 | Append or replace? | Same as S-F02-01 Q3. | 22/11/2026 · Resolved from documents | notes #9 |
| S-F02-01 Q4 | Is Book row approved for #2 Book context (ui-conventions §3 did not list S-F02-01)? | See D21 | 22/11/2026 · group decision (D21) | S-F02-01 §3 #2; ui-conventions §3 Book row |
| S-F02-01 Q5 | Should M-F02-01-01 and M-F02-01-02 quote the selected review text? | See D22 | 22/11/2026 · group decision (D22) | S-F02-01 §3.1 #1, §3.2 #1 |
| S-F02-01 notes Q4 | Is Book row approved as the book-context block? | See D21 | 22/11/2026 · group decision (D21) | notes #2 |
| S-F02-01 Q2 | Destination URL of the review-guideline link (#5 «Xem quy định viết đánh giá của thư viện»)? | See D20: the link is removed; #5 is now the hint line MSG-14 under the review field. | 22/11/2026 · group decision (D20) | S-F02-01 §3 #5, §5 (link row removed) |
| S-F02-01 notes Q2 | Destination URL of the library review guideline? | See D20 (same as S-F02-01 Q2). | 22/11/2026 · group decision (D20) | notes #5 |

## M-F02-01-01

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| M-F02-01-01 notes Q2 | Cancel label «Huỷ» (UI conventions) or "Keep review" (assignment guide)? | **«Huỷ».** ui-conventions §1 standard label "Cancel (in a modal) = Huỷ"; ui-conventions is the file every notes file follows. The guide line that still says "Keep review" → Pending tasks. | 22/11/2026 · Resolved from documents (ui-conventions §1; S-F02-01 Q6) | M-F02-01-01 #3; S-F02-01 §3.1 #3 |
| M-F02-01-01 notes Q1 | Does the modal need to identify the selected review text? | See D22 | 22/11/2026 · group decision (D22) | M-F02-01-01 #1 |

## M-F02-01-02

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| M-F02-01-02 notes Q2 | May a reader report their own review? | See AD-UC-14 Q2: **No**; the modal opens only from «Báo cáo đánh giá» on another reader's review. | 19/11/2026 · team (AD-UC-14 Q2) | M-F02-01-02 |
| M-F02-01-02 notes Q1 | Should the confirmation body quote the selected review? | See D22 | 22/11/2026 · group decision (D22) | M-F02-01-02 #1 |

## S-F02-02

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F02-02 Q1 | What does Back do when the page is opened by scanning the QR code? | See D5 (no Back button in any state; exit by the OPAC Text link). | 22/11/2026 · group decision (D5) | S-F02-02 §1, §3 #1, SR-008; notes #1 |
| S-F02-02 Q2 | Does S-F02-02 have «Xem thêm đánh giá»? | See D6 (yes, same as S-F02-01, 10 per page, shown while more published reviews remain). | 22/11/2026 · group decision (D6) | S-F02-02 §3 #10, §5 row 1, SR-009; notes #10 |
| S-F02-02 Q3 | May S-F02-02 show «Báo cáo đánh giá» on other readers' reviews? | **No.** Report (UC-14) only on S-F02-01, because AD-UC-06 has no Report call. | 08/11/2026 · team (L8-07) | S-F02-02 SR-001, §3 #8–#9 |
| S-F02-02 notes Q1 | Back action when opened from the QR scan. | See D5. | 22/11/2026 · group decision (D5) | notes #1 |
| S-F02-02 notes Q2 | AD-UC-06 says "same review panel as S-F02-01"; confirm Report stays absent. | **Absent.** Same as S-F02-02 Q3. | 22/11/2026 · Resolved from documents (L8-07; AD-UC-06) | notes #8–#9 |
| S-F02-02 notes Q4 | Next-page navigation for reviews? | See D6. | 22/11/2026 · group decision (D6) | notes #10 |
| S-F02-02 §2 numbering | Why are elements numbered #1–#10 / #11–#15? | Numbered image re-exported 22/11/2026 after D5 (Back removed) and D6 (Load more added). | 22/11/2026 · group decision (D5, D6) | S-F02-02 §2 |
| S-F02-02 Q5 | Is Book row approved for #2 Book information (ui-conventions §3 did not list S-F02-02)? | See D21 | 22/11/2026 · group decision (D21) | S-F02-02 §3 #2; ui-conventions §3 Book row |
| S-F02-02 notes Q5 | Is Book row approved as the QR book-information block? | See D21 | 22/11/2026 · group decision (D21) | notes #2 |
| S-F02-02 Q4 | Destination URL of the review-guideline link (#6 «Xem quy định viết đánh giá của thư viện»)? | See D20: the link is removed; #6 is now the hint line MSG-14 under the review field. | 22/11/2026 · group decision (D20) | S-F02-02 §3 #6, §5 (link row removed) |
| S-F02-02 notes Q3 | URL for «quy định viết đánh giá» not supplied. | See D20 (same as S-F02-02 Q4). | 22/11/2026 · group decision (D20) | notes #6 |

## S-F02-03

Sources: [screen_spec_s_f02_03.md](../external_design/screens/specs/screen_spec_s_f02_03.md) §1, §3, §5–§7, §9; [s_f02_03_notes.md](../external_design/screens/notes/s_f02_03_notes.md) "Open questions" and "Decision update" paragraphs.

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F02-03 Q3 | How do staff find the physical books to select? | See D3, D3c, D3d, D12, D13. (Earlier answer, 21/11/2026: "newly synced physical books, newest first, with pagination" — superseded.) | 22/11/2026 · group decision | S-F02-03 §1, #4, §4, SR-006; FR-02-23 |
| S-F02-03 Q4 | What is on each QR label and how many labels per A4 sheet? | See D4. (Earlier answer, 21/11/2026: QR + title + shelf location, 2 × 5 — superseded.) | 22/11/2026 · group decision | M-F02-03-01 #2, SR-007 |
| S-F02-03 Q-Selection | Must ticks carry across pages? | See D3b | 22/11/2026 · group decision | S-F02-03 #3, #13, §5 #2–#3, SR-010 |
| S-F02-03 Q-SignOut | Do staff need a sign-out action, and when does the staff session end? | See D7 | 22/11/2026 · group decision | S-F02-03 #14, §5 #9, SR-011 |
| S-F02-03 Q-Printed | When is a book recorded as label-printed? | See D12 (button type: see D17) | 22/11/2026 · group decision | S-F02-03 §1, §5 #4, #10, SR-005, SR-012; FR-02-08 |
| S-F02-03 Q-Shelf | Which location is used for a title whose copies sit on several shelves? | See D13 | 22/11/2026 · group decision | S-F02-03 #4, SR-006, SR-007 |
| S-F02-03 Q-Wording | Empty-state wording (#11) and the «Đã chọn <n> sách» component | See D15 (wording), D16 (Selection counter) | 22/11/2026 · group decision | S-F02-03 #11, #13 |
| S-F02-03 notes Q1 | Q3: How should staff find physical books to select? | See D3, D12 | 22/11/2026 · group decision | S-F02-03 notes #4 |
| S-F02-03 notes Q2 | Should checked books carry over when staff change pages? | See D3b | 22/11/2026 · group decision | S-F02-03 notes #13 |

## M-F02-03-01

Sources: [m_f02_03_01_notes.md](../external_design/screens/notes/m_f02_03_01_notes.md) "Open questions" and "Decision update"; [screen_spec_s_f02_03.md](../external_design/screens/specs/screen_spec_s_f02_03.md) §3.1, §4, §5, §6.

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| M-F02-03-01 notes Q1 | Q4: Which fields besides the QR code go on the label? | See D4 (QR left; title max 2 lines; «Tầng n · Phòng code · Kệ code»; «Quét để xem thông tin và đánh giá»). Superseded the drawn default "QR, title and shelf location". | 22/11/2026 · group decision | M-F02-03-01 #2 |
| M-F02-03-01 notes Q2 | Q4: How many labels per A4 page? | See D4 | 22/11/2026 · group decision | M-F02-03-01 #2, SR-007 |
| M-F02-03-01 notes Q3 | When is a book recorded as label-printed? | See D12 | 22/11/2026 · group decision | M-F02-03-01 #6 |
| M-F02-03-01 notes Q4 | Which shelf location goes on the label when copies sit on several shelves? | See D13 | 22/11/2026 · group decision | M-F02-03-01 #2 |
| M-F02-03-01 Q-Button | Which button is Primary in the preview: «In» or «Đã in xong»? | See D17 («In» Primary; «Đã in xong» Secondary; no exception to one Primary per screen) | 22/11/2026 · group decision | S-F02-03 §3.1 #6, SR-008; M-F02-03-01 notes #6 |
| M-F02-03-01 Q-Ticks | Are ticks kept after «Đóng»? | See D18 | 22/11/2026 · group decision | S-F02-03 §4 modal "Closed without confirming", §5 #8, SR-012; M-F02-03-01 notes #4 |

## S-F02-04

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F02-04 Q1 | Is the two-column layout (open-report queue left, selected review right, at 1280px) approved? | See D45 (staff screens are supported from 1280px, so the two columns never stack; was D8, from 1024px). | 22/11/2026 · group decision (D8) | S-F02-04 §3 #2–#3, §8 |
| S-F02-04 Q2 | Should S-F02-04 show a report-reason field? | **No.** The reader gives no reason when reporting, so there is nothing to show. Listed as answered in the review of 22/11/2026. | 22/11/2026 · Resolved from documents (AD-UC-14 Q1; L8-10; FR-02-09) | S-F02-04 §3 #3 |
| S-F02-04 Q3 (Toasts) | Separate Toasts for Remove and Dismiss? | **Yes:** «Đã gỡ đánh giá.» (FR-02-10) and «Đã bỏ qua báo cáo.» (FR-02-20) — two different actions, each Toast says what was done. The modal-quote part of Q3: see S-F02-04 Q3 (D22). | 22/11/2026 · Resolved from documents (screen-spec guide §3; ui-conventions §1, §4 Success; review of 22/11/2026) | S-F02-04 §3 #9, SR-005 |
| S-F02-04 #11 / SR-007 / FR-04-21 | Staff sign-out and session time-out. | See D7 («Đăng xuất» in the header in every state; session ends only on sign-out → S-F00-03; new FR-04-21). | 22/11/2026 · group decision (D7) | S-F02-04 §1, §3 #11, §5 row 8, SR-007, §7 FR-04-21; notes #11 |
| S-F02-04 notes Q1 | Is a two-column queue plus detail view acceptable? | See D8. Same as S-F02-04 Q1. | 22/11/2026 · group decision (D8) | notes #2–#3 |
| S-F02-04 notes Q2 | Separate success message for Dismiss vs Remove? | Same as S-F02-04 Q3 (Toasts). | 22/11/2026 · Resolved from documents | notes #9 |
| S-F02-04 notes Q3 | Staff-approved display field for report reason? | Same as S-F02-04 Q2. | 22/11/2026 · Resolved from documents | notes #3 |
| S-F02-04 Q3 | Should M-F02-04-01 quote the selected review text? | See D22 | 22/11/2026 · group decision (D22) | S-F02-04 §3.1 #1 |

## M-F02-04-01

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| M-F02-04-01 Default (D7) | Why is «Đăng xuất» visible behind the modal? | See D7 (staff header «Đăng xuất» in every state of S-F02-04). | 22/11/2026 · group decision (D7) | notes, States drawn: Default |
| M-F02-04-01 notes Q1 | Should the modal include the selected review text or only the action consequence? | See D22 | 22/11/2026 · group decision (D22) | M-F02-04-01 #1 |

## S-F03-01

Sources: [screen_spec_s_f03_01.md](../external_design/screens/specs/screen_spec_s_f03_01.md) header, §2, §3, §4, §9, checklist, "Review handoff"; [s_f03_01_notes.md](../external_design/screens/notes/s_f03_01_notes.md) "Open questions". Q1 (the initial selection, numbered Q5 in `screen-spec-chung.md`): see D19.

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F03-01 Q2 | Final wording of the no-results message? | **Resolved from documents:** «Không tìm thấy sách. Hãy chọn hình thức khác.» — identical in [ui_conventions.md](../external_design/ui_conventions.md) §4 (No results, FR-03-23) and the wireframe notes #7. | 22/11/2026 · resolved from documents | S-F03-01 #5, §4 Empty |
| S-F03-01 Q3 | Trigger and content of the error state; does FR-04-20 apply? | **Resolved from documents:** a network/load failure shows the MSG-04 Banner with «Thử lại», keeping the selected format and data shown (the wireframe notes #8, #9 and Error row; [screen_list.md](../external_design/screen_list.md) lists S-F03-01 under FR-04-20). Added #8, #9, §5 #11, SR-013 and FR-04-20 in §7. | 22/11/2026 · resolved from documents | S-F03-01 #8, #9, §4 Error, §5 #11, SR-013, §7 |
| S-F03-01 Q4 | Exact W0 Table 4 field names for title, author, cover and access format? | **Resolved from documents:** W0 Table 4 names only the data group "Book catalogue" (titles, authors, access formats); `Book catalogue › title / author / access format` is the level used by all specs. The cover is a grey placeholder with no data (ui-conventions Q6). | 22/11/2026 · resolved from documents (also the review of 22/11/2026) | S-F03-01 #4 |
| S-F03-01 Q5 | Has [s_f03_01_success.png](../external_design/screens/img/s_f03_01/s_f03_01_success.png) been uploaded? | **Resolved from documents:** yes, [s_f03_01_success.png](../external_design/screens/img/s_f03_01/s_f03_01_success.png) exists (1080 px wide). | 22/11/2026 · resolved from the image files | S-F03-01 §2 |
| S-F03-01 Q6 | Do the notes carry the metadata `Reader · 360px · v0.8 · <author>`? | **Resolved from documents:** yes, [s_f03_01_notes.md](../external_design/screens/notes/s_f03_01_notes.md) line 3. | 22/11/2026 · resolved from documents | S-F03-01 notes |
| S-F03-01 Q7 | Where is the source of the wireframe? | **Resolved from documents (fact):** there is no S-F03-01 source in `screens/src/`; the state images are cropped from [s_f03_01_states.png](../external_design/screens/img/s_f03_01/s_f03_01_states.png). Committing the source is a pending task. | 22/11/2026 · resolved from the files | S-F03-01 header "Wireframe source" |
| S-F03-01 Q8 | With «Cả hai», how is a book with both formats labelled? (notes Q2) | See D9 | 22/11/2026 · group decision | S-F03-01 #4, SR-004 |
| S-F03-01 Q9 | Pagination or «Xem thêm» for a long list? (notes Q3) | See D9 | 22/11/2026 · group decision | S-F03-01 #10, §5 #10, SR-011 |
| S-F03-01 Q10 | What happens to the page when the reader changes the access format? | See D14 | 22/11/2026 · group decision | S-F03-01 §5 #2, #7, SR-012 |
| S-F03-01 notes Q2 | How should a book with both formats be labelled? | See D9 | 22/11/2026 · group decision | S-F03-01 notes #6 |
| S-F03-01 notes Q3 | Pagination or «Xem thêm»? | See D9 | 22/11/2026 · group decision | S-F03-01 notes Results |
| S-F03-01 Q1 | Which access format is selected when S-F03-01 first opens? (spec §9 row 1; the spec cited it as "Q5", its number in `screen-spec-chung.md`) | See D19 | 22/11/2026 · group decision (D19) | S-F03-01 §3 #3, §4 Default, SR-009 |
| S-F03-01 notes Q1 | Initial state of the three-option selector on first entry? | See D19 | 22/11/2026 · group decision (D19) | notes States drawn: Default |

## S-F03-02

Sources: [screen_spec_s_f03_02.md](../external_design/screens/specs/screen_spec_s_f03_02.md) §9; [s_f03_02_notes.md](../external_design/screens/notes/s_f03_02_notes.md) "Open questions" (same numbering).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F03-02 Q1 | What is the initial status of automatically added history entries? | «Đang đọc» (Reading) with 0 % progress until the reader changes it. Same as AD-UC-07 Q1. | 04/11/2026 · team (default adopted) | S-F03-02 history entries (#4–#6) |
| S-F03-02 Q2 | If a reader borrows the same physical book twice, are there two history rows? | Yes, one history entry per borrow record (FR-03-03). Same as AD-UC-07 Q2. | 04/11/2026 · team (default adopted) | SR-F03-02-005 |
| S-F03-02 Q3 | Can a book be marked «Đã đọc xong» when progress is under 100 %? | Yes; status and progress are separate inputs and are saved as entered. Same as AD-UC-07 Q4. | 04/11/2026 · team (default adopted) | SR-F03-02-004 |
| S-F03-02 Q5 | Which component is used to choose several subject preferences: Checkbox or a chip component? | **Multi-select chips**, not Checkbox. Resolved from documents: [ui_conventions.md](../external_design/ui_conventions.md) §3 (v0.8) defines "Multi-select chips — choose multiple reading interests (FR-03-05), used on S-F03-02"; confirmed in the screen-spec review of 22/11/2026, S-F03-02 row 5. | 22/11/2026 · resolved from documents | S-F03-02 #13, §2 Default, §4 Default, §5 row 7, §8; notes #13 |
| S-F03-02 Q4 | Exact Vietnamese text of the empty reading-history state? | See D24 | 22/11/2026 · group decision (D24) | S-F03-02 §3 #15, §4 Empty; ui-conventions §4 MSG-13 |
| S-F03-02 notes Q4 | Exact Vietnamese text of the empty reading-history state? | See D24 | 22/11/2026 · group decision (D24) | notes #15 |


## S-F03-03

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F03-03 Q1 | Confirm the example titles, authors and shelf codes against the synced catalogue. | **No confirmation needed.** The list shows the reader's saved books with their synced shelf locations (FR-03-07); wireframe values are examples (ui-conventions Q6). | 22/11/2026 · Resolved from documents (FR-03-07; ui-conventions Q6) | S-F03-03 §8 |
| S-F03-03 Q2 | Is «Đã bỏ sách khỏi danh sách.» accepted as the removal Toast? | **Yes.** Screen owner's wording following the ui-conventions §4 Success pattern "Đã …"; this is what the 21/11 wireframe review (item 9) asked for. | 22/11/2026 · Resolved from documents (ui-conventions §4; wireframe review of 21/11/2026 S-F03-03 #9) | S-F03-03 §3 #10; notes #10 |
| S-F03-03 Q3 | Is MSG-04 / FR-04-20 the network-error treatment for this screen? | **Yes.** FR-04-20 applies to every screen that loads or saves data, S-F03-03 included; MSG-04 is the shared "any screen, load failed" message. "Provisional mapping" wording removed from §4, SR-009, §7. | 22/11/2026 · Resolved from documents ([screen_list.md](../external_design/screen_list.md) notes on FR-04-20; ui-conventions §4 MSG-04) | S-F03-03 §4 Error, SR-009, §7 |
| S-F03-03 Q4 | Confirm the empty-list copy against the shared messages. | **Confirmed:** ui-conventions §4 Empty state example is exactly «Bạn chưa lưu sách nào. Bấm Lưu vào danh sách ở trang vị trí kệ sách.» (FR-03-25). Also listed as answered in the review of 22/11/2026. | 22/11/2026 · Resolved from documents (ui-conventions §4) | S-F03-03 §3 #7, §4 Empty |
| S-F03-03 Q5 | Priority: Must (separate UC-12 screen list) or Should (global screen list)? | **Should.** Priority = highest W4 priority among the FRs of the screen's own use case (UC-12: FR-03-06, FR-03-07, FR-03-24, FR-03-25 Should; FR-03-08 Could); borrowed FR-04-08 / FR-01-07 do not raise it. The separate UC-12 list is no longer in the repository. | 22/11/2026 · Resolved from documents ([screen_list.md](../external_design/screen_list.md) row S-F03-03 and priority note; L8-14; W4) | S-F03-03 header Priority |
| S-F03-03 Q6 | Are all state panels exported at 1080px and compliant with v0.8? | **Size: yes** — every default, state and numbered PNG of S-F03-03 is a separate file 1080px wide (checked 22/11/2026). Compliance check → Pending tasks. | 22/11/2026 · Resolved from files (`screens/img/S-F03-03/S-F03-03*.png`) | S-F03-03 §2, checklist |
| S-F03-03 Q7 | Committed wireframe source path under `screens/src/`? | No source file in the repository; header field states this. To-do → Pending tasks. | 22/11/2026 · Resolved from files | S-F03-03 header |
| S-F03-03 notes Q1 | Confirm the example book data. | Same as S-F03-03 Q1. | 22/11/2026 · Resolved from documents | notes |
| S-F03-03 notes Q2 | Is «Đã bỏ sách khỏi danh sách.» accepted? | Same as S-F03-03 Q2 (notes #10 now gives the exact text, no "e.g."). | 22/11/2026 · Resolved from documents | notes #10 |

## S-F03-06

Sources: [screen_spec_s_f03_06.md](../external_design/screens/specs/screen_spec_s_f03_06.md) §9; [s_f03_06_notes.md](../external_design/screens/notes/s_f03_06_notes.md) "Open questions" (same numbering).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F03-06 Q1 | What is the maximum AI reply time before the fallback notice is shown? | 10 seconds. Same as AD-UC-08 Q1. | 04/11/2026 · team (default adopted) | SR-F03-06-002; §4 Loading and Error |
| S-F03-06 Q2 | Is the "temporarily unavailable" notice saved in the reader's conversation history? | No; only the reader's message is saved. Same as AD-UC-08 Q2. | 04/11/2026 · team (default adopted) | SR-F03-06-003 |
| S-F03-06 Q3 | Can readers clear or delete their chatbot conversation history? | No delete function in release 1; conversations are kept for the whole release. Same as AD-UC-08 Q3. | 04/11/2026 · team (default adopted) | SR-F03-06-004 |
| S-F03-06 Q4 | Link text on the book card: «Xem chi tiết sách» or «Xem sách»? | See D25 | 22/11/2026 · group decision (D25) | S-F03-06 §3 #6 |
| S-F03-06 notes Q4 | Link text on the book card? | See D25 | 22/11/2026 · group decision (D25) | notes #6 |

## S-F03-07

Sources: [screen_spec_s_f03_07.md](../external_design/screens/specs/screen_spec_s_f03_07.md) §9; [s_f03_07_notes.md](../external_design/screens/notes/s_f03_07_notes.md) "Open questions" (same numbering).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F03-07 Q1 | Which measure defines "popular books" in the cold-start state if QR scan counting is cut? | The number of loans in the synced loan records (FR-04-10). Same as AD-UC-09 Q1. | 04/11/2026 · team (default adopted) | SR-F03-07-004 |
| S-F03-07 Q2 | What counts as "trending" when a short list is topped up (FR-03-20)? | The most borrowed books of the same subject in the last 30 days. Same as AD-UC-09 Q2. | 04/11/2026 · team (default adopted) | SR-F03-07-003; #10 |
| S-F03-07 Q3 | How many recommendations does S-F03-07 show at most? | 10 books. Same as AD-UC-09 Q3. | 04/11/2026 · team (default adopted) | SR-F03-07-002 |
| S-F03-07 Q4 | Should each row show a recommendation reason (e.g. «Khớp sở thích: Kinh tế», «vì bạn đã đọc X»)? | See D11 | 22/11/2026 · group decision | SR-F03-07-010; notes #13 |
| S-F03-07 Q5 | Is the header shortcut «Sở thích» shown in every state or only in cold-start? | See D10b | 22/11/2026 · group decision | #3, §1, §5 row 3, SR-F03-07-009; notes #3 |
| S-F03-07 Q6 | Do books added from trending titles carry a «Xu hướng» tag? | See D10a | 22/11/2026 · group decision | #13, SR-F03-07-008; notes #13 |

## S-F04-01

Sources: [screen_spec_s_f04_01.md](../external_design/screens/specs/screen_spec_s_f04_01.md) header, §2, §3, §9, checklist, "Review handoff"; [s_f04_01_notes.md](../external_design/screens/notes/s_f04_01_notes.md) "Open questions".

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| S-F04-01 Q1 | Should the staff page include an explicit sign-out action? | See D7 | 22/11/2026 · group decision | S-F04-01 #7, §1, §5 #5, SR-006; FR-04-21 |
| S-F04-01 notes Q1 | Should staff be offered an explicit sign-out action? | See D7 | 22/11/2026 · group decision | S-F04-01 notes #7 |
| S-F04-01 Q2 | Is UC-13 / «Đánh giá bị báo cáo» included in the current deliverable? | **Resolved from documents:** yes, at Could priority. [screen_list.md](../external_design/screen_list.md) lists S-F02-04 as Could and names «Reported reviews» on S-F04-01 among the Could parts that disappear without removing the screen if UC-13 is cut (see also L8-14). The spec keeps the entry conditional. | 22/11/2026 · resolved from documents (also the review of 22/11/2026, §3) | S-F04-01 #3, §5 #3, SR-004 |
| S-F04-01 Q3 | Do the Default, Loading and Error PNGs exist at 1280px and follow the v0.8 tokens? | **Resolved from documents (existence, width):** [s_f04_01.png](../external_design/screens/img/s_f04_01/s_f04_01.png), -loading, -error and their -numbered copies exist, 1280 × 900 px (checked 22/11/2026). Colour-token check moved to Pending tasks. | 22/11/2026 · resolved from the image files | S-F04-01 §2 |
| S-F04-01 Q4 | Staff layout below the 1280px design frame? | See D8 | 22/11/2026 · group decision | S-F04-01 §8 |
| S-F04-01 Q5 | Is the HTML demonstration in the notes a required deliverable? | **Resolved from documents:** no; `huong-dan/screen-spec-chung.md` §4.1 accepts the `.drawio` source. | 22/11/2026 · resolved from documents | S-F04-01 header "Wireframe source" |
| S-F04-01 Header-AD | Which activity diagrams show S-F04-01 ("confirm diagram references against the team's current index")? | **Resolved from documents:** AD-UC-10 (a0, d8, a7) and AD-UC-13 (a0, a1, d7, a6), as mapped in [screen_list.md](../external_design/screen_list.md). | 22/11/2026 · resolved from documents | S-F04-01 header |

# Activity diagrams

## AD-UC-01

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-01 Q1 | A book with several physical copies on different shelves: which shelf location is shown? | Every copy's floor, room and shelf code is shown, one line per copy; the primary shelf location from the sync is listed first (see D27). | 2026-11-04 · team (default adopted); order: 22/11/2026 · group decision (D27) | AD-UC-01 `s4`; S-F01-01 |
| AD-UC-01 Q2 | Does "direct the reader to library staff" name a place, such as the information desk on each floor? | A fixed message names the information desk on the ground floor. | 2026-11-04 · team (default adopted) | AD-UC-01 `s3` (FR-01-07); S-F01-01 |
| AD-UC-01 Q3 | FR-01-03 is Could after W4. If the release cuts it, is UC-01 still accepted with the shelf code only? | Yes; if FR-01-03 is cut, the map branch is removed and `s4` ends the flow. The branch stays until the release scope is fixed. | 2026-11-04 · team (default adopted) | AD-UC-01 `d3`–`s8` |
| D27 (AD-UC-01) | AD-UC-01 Q1 vs D13: which copy's shelf location comes first? | See D27 | 22/11/2026 · group decision (D27) | AD-UC-01 `s4`; S-F01-01 |

## AD-UC-02

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-02 Q1 | Which floor is shown first when the map is opened from the menu? | The ground floor (lowest floor number). | 2026-11-04 · team (default adopted) | AD-UC-02 `s5`; S-F01-02 |
| AD-UC-02 Q2 | When the selected floor's plan cannot be read (`d5 [No]`), does the previous floor's map stay on screen? | Yes; the message is shown above the previous floor's map. | 2026-11-04 · team (default adopted) | AD-UC-02 `s7`; S-F01-02 |
| AD-UC-02 Q3 | FR-01-03 is Could after W4. If it is cut, `d2`, `d3`, `s3` and `s4` are removed and the map always opens plain. | Keep the branch until the release scope is fixed. | 2026-11-04 · team (default adopted) | AD-UC-02 `d2`, `d3`, `s3`, `s4` |

## AD-UC-03

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-03 Q1 | This platform builds no viewer or download (W0 Table 3, FR-03-14 and FR-03-15 Won't). Can FR-03-02 and FR-03-13 still be met? | Yes. The current OPAC opens and downloads online books. Each online book in the results links to the book on the current OPAC, and the platform records that click as "opened" for FR-03-13 and FR-03-02; both FRs stay in scope. | 2026-11-04 · team (confirmed) | AD-UC-03 `r3`, `s4`, `s5`; AD-UC-07 `e1`; S-F03-01 |
| AD-UC-03 Q2 | Does "Both" mean books that have both formats, or every book in either format? | Books that have both a physical copy and an online version. | 2026-11-04 · team (default adopted) | AD-UC-03 `s1`; S-F03-01 |
| AD-UC-03 Q3 | Does the filter apply to the whole catalogue or to the current OPAC search result? | The whole synced catalogue (see also L8-12). | 2026-11-04 · team (default adopted) | AD-UC-03 `s1`; S-F03-01 |
| AD-UC-03 Q4 | If a signed-in reader opens the same online book again, is a second history entry added? | Yes, one entry per opening, as FR-03-02 is written; merging repeats would need a new FR. | 2026-11-04 · team (default adopted) | AD-UC-03 `s5`; AD-UC-07 `s13` |

## AD-UC-04

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-04 Q1 | May a reader write more than one review for the same book? | Yes; FR-02-01 sets no limit. | 2026-11-04 · team (default adopted) | AD-UC-04 `s3` |
| AD-UC-04 Q2 | Is an edited review marked "edited" with a date? | No marker in release 1. | 2026-11-04 · team (default adopted) | AD-UC-04 `s5`; S-F02-01, S-F02-02 |
| AD-UC-04 Q3 | How long is a removed review kept in storage? | Kept with state Removed; no automatic purge in release 1. | 2026-11-04 · team (default adopted) | AD-UC-04 `s6`, §4 |
| AD-UC-04 Q4 | FR-02-03 and FR-02-04 are Could. If they are cut, the Edit and Delete branches of `d2` are removed. | Keep both branches until the release scope is fixed. | 2026-11-04 · team (default adopted) | AD-UC-04 `d2` |
| AD-UC-04 Q5 | When the reader signs in in the middle of a review action, or cancels sign-in («Huỷ»), is the pending action kept or dropped? | See D1 | 22/11/2026 · group decision | AD-UC-04 business rules, reading notes, tests |

## AD-UC-05

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-05 Q1 | How many reviews are on one page, and in what order? | 10 per page, newest first. | 2026-11-04 · team (default adopted) | AD-UC-05 `s5`; S-F02-01 |
| AD-UC-05 Q2 | FR-02-15 says the request ends "without displaying a review list". Does the reader still see a short message such as "No reviews yet"? | Yes, a one-line message that there are no reviews to show; FR-02-15 wording updated in W1 and `s4` updated. | 2026-11-04 · team (default adopted) | AD-UC-05 `s4`; FR-02-15; S-F02-01 |

## AD-UC-06

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-06 Q1 | If the same phone scans the same code several times within a minute, is every scan counted? | Yes, every scan counts. | 2026-11-04 · team (default adopted) | AD-UC-06 `s3` |
| AD-UC-06 Q2 | FR-02-06 was moved to Could in W4. If it is cut, `f1`, `s3` and `j1` are removed and the page opens directly. | Keep the fork until the release scope is fixed. | 2026-11-04 · team (default adopted) | AD-UC-06 `f1`, `s3`, `j1` |
| AD-UC-06 Q3 | The scan count also feeds the popular-books fallback in UC-09 (FR-03-19). If FR-02-06 is cut, what does UC-09 use instead? | Loan counts from the synced loan records (AD-UC-09 Q1). | 2026-11-04 · team (default adopted) | AD-UC-09 `s3` |
| AD-UC-06 Q4 | Does the QR page offer «Xem thêm đánh giá» like S-F02-01? | See D6 | 22/11/2026 · group decision | AD-UC-06 `r2`, `s5`, `mD` (v1.2); S-F02-02 |

## AD-UC-07

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-07 Q1 | What reading status does an automatic entry (`s12`, `s13`) get? FR-03-02 and FR-03-03 do not say. | Reading, 0 percent, until the reader changes it. | 2026-11-04 · team (default adopted) | AD-UC-07 `s12`, `s13`, §4; AD-UC-03 §4; activity-index object states |
| AD-UC-07 Q2 | If a reader borrows the same book again, is a second history entry added? | Yes, one entry per borrow record, as FR-03-03 is written; merging repeats would need a new FR. | 2026-11-04 · team (default adopted) | AD-UC-07 `s12` |
| AD-UC-07 Q3 | What does "validate the reading preferences" check (FR-03-05)? | Every chosen subject must exist in the synced catalogue subject list. | 2026-11-04 · team (default adopted) | AD-UC-07 `s7`, `d4`; S-F03-02 |
| AD-UC-07 Q4 | May a book be Finished with progress below 100 percent? | Yes; it is saved as entered. | 2026-11-04 · team (default adopted) | AD-UC-07 `s4`; S-F03-02 |
| AD-UC-07 Q5 | The `e1` part depends on online books opening on the current OPAC through a link from this platform. | Confirmed (AD-UC-03 Q1). | 2026-11-04 · team (confirmed) | AD-UC-07 `e1`, `s13` |

## AD-UC-08

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-08 Q1 | What is "in time" for an AI reply (FR-03-17)? | 10 seconds. | 2026-11-04 · team (default adopted) | AD-UC-08 `d2`; S-F03-06 |
| AD-UC-08 Q2 | Is the "temporarily unavailable" notice saved in the conversation history? | No; only the reader message is saved. | 2026-11-04 · team (default adopted) | AD-UC-08 `s2`, `s4` |
| AD-UC-08 Q3 | How long are chatbot conversations kept, and can a reader delete them? | Kept for the whole release; no delete function in release 1. | 2026-11-04 · team (default adopted) | AD-UC-08 `s2`, `s5`; S-F03-06 |

## AD-UC-09

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-09 Q1 | FR-03-19 ranks popular books by QR scan count, but counting scans (FR-02-06) was moved to Could. If it is cut, what decides "popular"? | The number of loans in the synced loan records (FR-04-10). | 2026-11-04 · team (default adopted) | AD-UC-09 `s3`; AD-UC-06 Q3 |
| AD-UC-09 Q2 | What counts as "trending" in FR-03-20? | The most borrowed books of the same subject in the last 30 days. | 2026-11-04 · team (default adopted) | AD-UC-09 `s4`; S-F03-07 |
| AD-UC-09 Q3 | How many books does the list show? | 10. | 2026-11-04 · team (default adopted) | AD-UC-09 `s5`; S-F03-07 |

## AD-UC-10

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-10 Q1 | The QR generation is started by time, not by staff. The workshop guide asks for a separate use case for a process nobody starts by hand. Keep it in UC-10, as its name says, or move it to a sync use case? | Kept in UC-10, as its name says (see also Inputs check 3). | 2026-11-04 · team (default adopted) | AD-UC-10 `t1`–`s7` |
| AD-UC-10 Q2 | What happens if a QR code cannot be generated for a book? | It is tried again at the next sync; until then the book shows up in the "no QR code" list of `s3`. | 2026-11-04 · team (default adopted) | AD-UC-10 `s3`, `s7` |
| AD-UC-10 Q3 | Label size and number of labels per sheet? | See D4 (2026-11-04 default was "A4 sheet; layout set in Lesson 8", replaced by D4). | 2026-11-04 · team; 22/11/2026 · group decision | AD-UC-10 business rules, `s4`; M-F02-03-01 |
| AD-UC-10 Q4 | Staff must be signed in before the staff page opens (FR-04-08). A rejected staff sign-in had no FR. | See L8-02 and L8-03 (session checked on opening the staff page; edge-case FR-04-18 "Reject invalid staff sign-in" added to W1 on 2026-11-08: UC-10, UC-13; Must; NC). | 2026-11-08 · team | AD-UC-10 `s0`–`s10`, `d6`, `s9`, `d1` |
| AD-UC-10 Q5 | Which physical books does the staff page list for selection, and are labels recorded as printed? | See D3, D3b, D3c, D3d (list, ticks across pages, 20 per page, floor → room → shelf). The recording part was replaced by D12 (AD-UC-10 Q7). | 22/11/2026 · group decision | AD-UC-10 `s11`, `d7`, `a6`, `s12`; FR-02-23; S-F02-03 |
| AD-UC-10 Q6 | Can staff sign out, and does the staff session time out? | See D7 | 22/11/2026 · group decision | AD-UC-10 `d8`, `a7`, `s14`; FR-04-21 |
| AD-UC-10 Q7 | When is a book recorded as label-printed: when the sheet is produced, or after it is really printed? | See D12 (button types: D17; ticks after «Đóng»: D18) | 22/11/2026 · group decision | AD-UC-10 `d9`, `a8`, `a9`, `s13`; FR-02-08; M-F02-03-01 |
| AD-UC-10 Q8 | A title whose copies sit on several shelves: which location is used for the label and the order of the list? | See D13 | 22/11/2026 · group decision | AD-UC-10 `s11`, business rules, test "s11 (primary shelf location)" |
| AD-UC-10 Q9 | Does a staff sign-in write an audit entry? FR-04-12 says every sign-in does. | See D30 | 23/11/2026 · group decision | AD-UC-10 `s15`; FR-04-12 |

## AD-UC-11

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-11 Q1 | "Register" is in the use case name, but online registration and account linking (FR-04-02, FR-04-03, FR-04-05, FR-04-06) are Won't. Rename UC-11 to "Sign in with library card and email OTP"? | The name "Register and sign in (library card with email OTP)" is kept. | 2026-11-04 · team (default adopted) | UC-11 name; AD-UC-11 reading notes |
| AD-UC-11 Q2 | Who sends the OTP email? The Context Diagram shows "Email OTP" going straight to the Reader and has no email service. | No outside email service and no separate lane; the Context Diagram stays as it is (see also Inputs check 2). | 2026-11-04 · team (default adopted) | AD-UC-11 `s4`; Context Diagram |
| AD-UC-11 Q3 | Is there a limit on how many new OTPs a reader may request? | No limit in release 1; the 5-attempt rule applies to each OTP. | 2026-11-04 · team (default adopted) | AD-UC-11 `d5`, `r3`; S-F00-02 |
| AD-UC-11 Q4 | Should the "card not found" message avoid saying whether a card number exists? | Yes, one general message for every rejection. | 2026-11-04 · team (default adopted) | AD-UC-11 `s2`, `s11`; S-F00-01 |

## AD-UC-12

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-12 Q1 | Is there a limit on how many books a reader can save? | No limit. | 2026-11-04 · team (default adopted) | AD-UC-12 `s3` |
| AD-UC-12 Q2 | What happens to a saved book that the sync removes from the catalogue? | It stays in the list and shows "shelf location unavailable" (FR-01-07). | 2026-11-04 · team (default adopted) | AD-UC-12 `d5`, `s6`; S-F03-03 |
| AD-UC-12 Q3 | If a request to save an online-only book reaches the system, is it rejected? | Save is offered only on physical books; no server-side check is drawn. | 2026-11-04 · team (default adopted) | AD-UC-12 `r2`; S-F01-01 |

## AD-UC-13

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-13 Q1 | Where are "the rules" written that staff judge reviews against? | The library's review guideline, linked from the review form. **Superseded by D20** (22/11/2026): there is no guideline page and no link; staff judge against the three criteria of the hint line MSG-14 (no offensive language, no advertising, no personal information). | 2026-11-04 · team (default adopted) | AD-UC-13 `d3`; S-F02-01; S-F02-02 |
| AD-UC-13 Q2 | Is the author told when their review is removed? | No notice in release 1. | 2026-11-04 · team (default adopted) | AD-UC-13 `s5` |
| AD-UC-13 Q3 | Wrong W1 source trace: FR-04-05 (link an online account to a library card) and FR-04-06 (reject linking when both profiles hold data) name UC-13, but they belong to an older account-linking use case, are Won't, and have nothing to do with removing reviews. | They are not part of UC-13 and are not drawn or counted. W1 corrected on 2026-11-04: their source trace now names UC-11 (online part, cut in W4). | 2026-11-04 · team (resolved) | AD-UC-13 Inputs; W1 FR-04-05, FR-04-06 |
| AD-UC-13 Q4 | The sequence User Review Reporting Flow uses FR-02-10 for opening the reported-reviews list; the diagram uses FR-02-14, as W1 does. | The diagram stays on FR-02-14 (as W1). The sequence was fixed on 23/11/2026 (SD-UC-13, Inputs check 7). | 2026-11-04 · team; 23/11/2026 · group decision | AD-UC-13 `a1`, `s2`; SD-UC-13 |
| AD-UC-13 Q5 | Confirm the state names of a review report: Open, Dismissed, Upheld. | These three names are used until the data model is set in DBIZ3. | 2026-11-04 · team (default adopted) | AD-UC-13 §4; AD-UC-14 §4; activity-index object states |
| AD-UC-13 Q6 | Staff must be signed in before the staff page opens (FR-04-08). A rejected staff sign-in had no FR. | See L8-02 and L8-03 (same as AD-UC-10 Q4). | 2026-11-08 · team | AD-UC-13 `s0`–`s10`, `d6`, `s9`, `d1` |
| AD-UC-13 Q7 | Can staff sign out, and does the staff session time out? | See D7 | 22/11/2026 · group decision | AD-UC-13 `d7`, `a6`, `s11`; FR-04-21 |
| AD-UC-13 Q8 | Does a staff sign-in write an audit entry? FR-04-12 says every sign-in does. | See D30 | 23/11/2026 · group decision | AD-UC-13 `s12`; FR-04-12 |

## AD-UC-14

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| AD-UC-14 Q1 | Must the reader give a reason for the report? | No reason field; FR-02-09 asks for none (see also L8-10). | 2026-11-04 · team (default adopted) | AD-UC-14 `r2`; M-F02-01-02 |
| AD-UC-14 Q2 | May a reader report their own review? | **No.** Report is offered only on other readers' reviews; on their own review the reader has Edit and Delete (ui-conventions §3, Review item). The earlier default (2026-11-04) was "Yes". | 2026-11-19 · team (changed) | AD-UC-14 `r1`; S-F02-01 |
| AD-UC-14 Q3 | Wrong W1 source trace: FR-02-10 (review and remove reported reviews) names UC-14, but it is done by On-site Staff and is drawn in AD-UC-13. UC-14 ends when the report is saved. | FR-02-10 is not part of UC-14 and is not drawn or counted; it is cited only as a business rule (a reported review stays public until staff remove it). W1 corrected on 2026-11-04: its source trace now names UC-13 only. | 2026-11-04 · team (resolved) | AD-UC-14 Inputs, business rules; W1 FR-02-10 |

## AD-UC-15

None. UC-15 and AD-UC-15 come from D48.

## activity-index

General: all open questions in the AD files were decided on 2026-11-04 by adopting their defaults (rows
above marked "default adopted").

Inputs check (Block 1: what Lesson 3 and Lesson 4 gave us). The open finding (3) is listed under
Pending tasks. Findings 4, 5 and 7 were closed on 23/11/2026.

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| Inputs check 1 | The AI Service appears as a lifeline "inside Library Core System" in the sequences AI Service Chatbot and Reader Interaction Flow, and was drawn as a box nested in the system lane in UC-08 and UC-09. It is not an outside party on the Context Diagram, and `swimlane-beta` does not draw nested lanes. | AI steps are drawn in the Library Core System lane with the prefix "AI Service:" (AD-UC-08, AD-UC-09). Done (Owner D). | 2026-11-04 · Owner D | AD-UC-08 `a1`; AD-UC-09 `a1` |
| Inputs check 2 | The system emails the OTP (FR-04-04), but the Context Diagram has no email service: "Email OTP" goes straight to the Reader. | No outside email service; the Context Diagram and AD-UC-11 stay as they are (AD-UC-11 Q2). Done (Owner A). | 2026-11-04 · team | Context Diagram; AD-UC-11 |
| Inputs check 3 | Processes started by time have no use case of their own: daily sync of catalogue, shelf placement, floors and rooms (FR-04-09), loan records (FR-04-10), sync failures (FR-04-11), room-code check (FR-01-05). Two timed steps are drawn inside other use cases as time events: QR generation (FR-02-07) in AD-UC-10 and history entries from loans (FR-03-03) in AD-UC-07. | QR generation stays in AD-UC-10 and loan history entries stay in AD-UC-07 (AD-UC-10 Q1). A use case "Sync data from the library internal system" (started by time) is added for FR-04-09, FR-04-10, FR-04-11 and FR-01-05: pending task (Integrator), see L8-20. | 2026-11-04 · team | Use Case Diagram; AD-UC-07 `t1`; AD-UC-10 `t1`; [screen_list.md](../external_design/screen_list.md); [usage_flow.md](../external_design/usage_flow.md) |
| Inputs check 4 | Several sequence diagrams tell two use cases: User Interface Flow (UC-01 + UC-02), User Review Interaction Flow (UC-05 + UC-04), Book Review API Interaction (UC-06 + UC-04), Reader Interaction Flow (UC-07 + UC-09), User Review Reporting Flow (UC-14 + UC-13). | Split into one sequence per use case. Done 23/11/2026: SD-UC-01 … SD-UC-14. | 2026-11-04 · team; 23/11/2026 · group decision | SD-UC-01 … SD-UC-14 |
| Inputs check 5 | `opt` / `alt` used for a reader's choice: map link (User Interface Flow), edit or delete own review (User Review Interaction Flow), view history or set preferences (Reader Interaction Flow). | The choices are decisions in AD-UC-02, AD-UC-04 and AD-UC-07; in the sequences keep `alt` only for interaction conditions such as an API error. Done 23/11/2026: actor choices are marked sections in SD-UC-01 … SD-UC-14. | 2026-11-04 · team; 23/11/2026 · group decision | SD-UC-01 … SD-UC-14; AD-UC-02 `d4`; AD-UC-04 `d2`; AD-UC-07 `d2` |
| Inputs check 6 | W1 source traces that name the wrong use case: FR-04-05 and FR-04-06 → UC-13 (old account-linking use case, Won't); FR-02-10 → UC-14 (removal is done by staff in UC-13). | AD-UC-13 and AD-UC-14 leave these rows out and say why (v1.1). W1 corrected on 2026-11-04: FR-04-05 and FR-04-06 trace to UC-11 (online part, cut in W4; W0 Table 3), FR-02-10 traces to UC-13 only (AD-UC-13 Q3, AD-UC-14 Q3). Done (Integrator). | 2026-11-04 · Integrator | W1; AD-UC-13; AD-UC-14 |
| Inputs check 7 | The sequence User Review Reporting Flow cites FR-02-10 for opening the reported-reviews list; W1 has FR-02-14 for that step. | Sequence step changed to FR-02-14. Done 23/11/2026 in SD-UC-13 (AD-UC-13 Q4). | 2026-11-04 · team; 23/11/2026 · group decision | SD-UC-13 |
| Inputs check 8 | FRs missing from their diagrams: FR-03-02 and FR-03-13 (UC-03) and FR-03-02 and FR-03-03 (UC-07). FR-03-02 and FR-03-13 need an online book to be opened "from this platform", but the viewer and download were cut (FR-03-14, FR-03-15 Won't). | Drawn in v1.1: AD-UC-03 adds "Open an online book from the results" with the anonymous read log and the history entry; AD-UC-07 adds a time event (loan sync, FR-03-03) and an accept event (online book opened, FR-03-02). Both rest on online books in the results linking to the current OPAC, with the click recorded (AD-UC-03 Q1). Done (Owner D). | 2026-11-04 · team | AD-UC-03 `r3`, `s4`, `s5`; AD-UC-07 `t1`, `e1` |

Open questions from Lesson 8 (external design), collected from [usage_flow.md](../external_design/usage_flow.md),
[screen_list.md](../external_design/screen_list.md) and [screen_transition.md](../external_design/screen_transition.md) (2026-11-08). Rows marked "Confirmed 22/11/2026 · group decision (D26)" were
"Default applied 2026-11-08; team to confirm": the default is the answer that the external-design documents
named in the row already use, and it was confirmed on 22/11/2026 (D26).

| ID | Question | Decision / answer | Date · basis | Applies to |
|---|---|---|---|---|
| L8-01 | Reader sign-in: how does a reader answer "Sign in now?" (d1 in AD-UC-04, 07, 08, 09, 12, 14), and where does the reader land afterwards? | One shared modal M-F00-01 "Sign in to continue?" on the screen where the reader asked. "Sign in" opens S-F00-01; "Not now" ends the request. Return to the starting screen and the pending action: see D1. FR-03-18-FE and FR-03-21-FE reworded in W1 on 2026-11-08 to match. | 2026-11-08 · team; 22/11/2026 · group decision (D1) | M-F00-01; S-F00-01; S-F00-02; AD-UC-04, 07, 08, 09, 12, 14 `d1`; [screen_transition.md](../external_design/screen_transition.md) |
| L8-02 | Staff sign-in: where do On-site Staff sign in, and when is the staff session checked? | Staff sign in on S-F00-03 before the staff page opens (FR-04-08); after sign-in S-F04-01 opens (FR-04-07). AD-UC-10 v1.2 and AD-UC-13 v1.3 redrawn; modal M-F00-02 dropped. Staff session time-out and sign-out: see D7 (AD-UC-10 v1.4, AD-UC-13 v1.4). | 2026-11-08 · team; 22/11/2026 · group decision (D7) | AD-UC-10, AD-UC-13 `s0`–`s10`; S-F00-03; S-F04-01 |
| L8-03 | Staff sign-in: a rejected staff sign-in (wrong account, or no staff role) had no FR and was not drawn. | Branch added to AD-UC-10 and AD-UC-13 (`d6`, `s9`, `d1` "Try again?"); error state of S-F00-03. New edge-case FR-04-18 "Reject invalid staff sign-in" added to W1 on 2026-11-08: IF On-site Staff submit credentials the internal library accounts do not accept, or an account without the staff role, THEN the system SHALL reject the sign-in, display an error message and allow the staff to try again (UC-10, UC-13; Must; NC). | 2026-11-08 · team | AD-UC-10, AD-UC-13 `d6`, `s9`, `d1`; S-F00-03; W1 FR-04-18 |
| L8-04 | Staff page: is the staff page a product screen? | Yes: S-F04-01 Staff page (F-04, FR-04-07 "staff page menu") with "Print QR labels" and "Reported reviews". | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md) row S-F04-01 | S-F04-01; AD-UC-10, AD-UC-13 §5 |
| L8-05 | Chatbot: when does the chatbot ask the reader to sign in? | After the reader sends the first message, as AD-UC-08 draws it, not when S-F03-06 opens. | Confirmed 22/11/2026 · group decision (D26); source: AD-UC-08 `r1` → `s0`; screen spec S-F03-06 | S-F03-06; AD-UC-08 |
| L8-06 | Saved books: where does the reader press Save (UC-12 r2)? | On S-F01-01, for physical books only (FR-03-06-FE). "Saved" and "Already saved" are states of S-F01-01. No direct link from there to the saved list; the reader opens "Saved books" from the OPAC personal area. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md) S-F01-01, S-F03-03; [screen_spec_s_f01_01.md](../external_design/screens/specs/screen_spec_s_f01_01.md) SR-008 | S-F01-01; S-F03-03; AD-UC-12 §5 |
| L8-07 | QR page: after a QR scan, where are Write, Edit and Delete own review done? | On S-F02-02 itself, with the same review panel as S-F02-01 and modal M-F02-01-01. Report (UC-14) only on S-F02-01, because AD-UC-06 has no Report call. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md) S-F02-02; [screen_spec_s_f02_02.md](../external_design/screens/specs/screen_spec_s_f02_02.md) | S-F02-02; AD-UC-06 §5 |
| L8-08 | QR page: S-F02-02 had no way to another screen (dead end). | A "View this book on the OPAC" link opens the book's existing OPAC Book Detail page. | 2026-11-08 · team | S-F02-02 |
| L8-09 | QR labels: is the printable QR label sheet a separate page? | No: modal M-F02-03-01 "QR label sheet preview" on S-F02-03 with a Print button (FR-02-08-FE). The browser print dialog is not a product screen. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md), Modals: M-F02-03-01 | M-F02-03-01; AD-UC-10 §5 |
| L8-10 | Report a review: where does the reader submit a report (AD-UC-14 r2)? | Modal M-F02-01-02 "Report this review?" on S-F02-01, no reason field (AD-UC-14 Q1). | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md), Modals: M-F02-01-02 | M-F02-01-02; AD-UC-14 §5 |
| L8-11 | Map: AD-UC-01 s6, s7 (map unavailable, room cannot be identified): does the reader stay on S-F01-01? | S-F01-02 opens and shows the message with the shelf details kept visible, as in AD-UC-02 s2 and s4. | Confirmed 22/11/2026 · group decision (D26); source: AD-UC-01 §5; [screen_list.md](../external_design/screen_list.md) S-F01-02 | S-F01-02; AD-UC-01 §5 |
| L8-12 | Access-format filter: FR-03-12-FE says "filter on the advanced filter panel", but S-F03-01 is a new product page over the whole synced catalogue (AD-UC-03 Q3). | S-F03-01 stays a product page reached by a link from the OPAC catalogue / search results. FR-03-12-FE reworded in W1 on 2026-11-08. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md) S-F03-01 | S-F03-01; W1 FR-03-12-FE |
| L8-13 | OPAC links: how do readers reach the F-03 screens and the sign-in screen from the OPAC? | Plain new links on existing OPAC pages (catalogue / search results, main menu, personal area, "Sign in"). No floating chat widget, no "Reader Dashboard". The library's agreement to add the links is a pending task. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md) introduction and entry points | [screen_list.md](../external_design/screen_list.md) entry points; S-F00-01; S-F03-01 … S-F03-07 |
| L8-14 | Priority: how is a screen's priority set? | Highest W4 priority among the FRs of the screen's own use cases; borrowed rules (FR-04-08, FR-01-07) do not raise it. Result: S-F02-04 Could; S-F03-01, S-F03-02, S-F03-03 Should. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md), notes on the table | [screen_list.md](../external_design/screen_list.md) Priority column |
| L8-15 | Screen IDs: close the gap left by S-F03-04 and S-F03-05? | No. S-F03-04 and S-F03-05 are retired and never reused; S-F03-06 and S-F03-07 stay. | Confirmed 22/11/2026 · group decision (D26); source: [screen_list.md](../external_design/screen_list.md) has no S-F03-04 / S-F03-05 rows | [screen_list.md](../external_design/screen_list.md) |
| L8-16 | Use case names: W0 Table 1 has long names for UC-06 and UC-12; this index uses short forms. | W0 Table 1 names are used in [usage_flow.md](../external_design/usage_flow.md) (boxes and tables). | Confirmed 22/11/2026 · group decision (D26); source: [usage_flow.md](../external_design/usage_flow.md) | [usage_flow.md](../external_design/usage_flow.md) |
| L8-17 | UC-05 to UC-04: AD-UC-05 has no branch to UC-04, while AD-UC-06 has. Keep the usage-flow arrow UC-05 to UC-04? | Kept: S-F02-01 hosts both use cases. Adding the branch to AD-UC-05 is a pending task. | Confirmed 22/11/2026 · group decision (D26); source: [usage_flow.md](../external_design/usage_flow.md) | [usage_flow.md](../external_design/usage_flow.md); AD-UC-05 |
| L8-18 | FR-01-03 owner: which use case owns FR-01-03 (the book's room highlighted on the map)? It is drawn in AD-UC-01 and AD-UC-02. | UC-01, as drawn in AD-UC-01; the usage-flow arrow UC-01 to UC-02 stands for browsing the map further. | Confirmed 22/11/2026 · group decision (D26); source: [usage_flow.md](../external_design/usage_flow.md) | AD-UC-01 `s8`; AD-UC-02 `s3`; [usage_flow.md](../external_design/usage_flow.md) |
| L8-19 | FR-03-02 owner: the history entry when a signed-in reader opens an online book is drawn in AD-UC-03 (`s5`) and AD-UC-07 (`e1`). Which diagram owns it? | UC-07 (accept event `e1`), with AD-UC-03 `s5` as the step that triggers it; listed once under "Use cases without a flow". | Confirmed 22/11/2026 · group decision (D26); source: [usage_flow.md](../external_design/usage_flow.md) | AD-UC-03 `s5`; AD-UC-07 `e1`; [usage_flow.md](../external_design/usage_flow.md) |
| L8-20 | Sync use case: name and ID of the planned use case for the daily sync with the library internal system (Inputs check 3). | Listed without an ID as "Sync data from the library internal system (planned)" until the Integrator gives it an ID and draws its diagram (pending task). | 2026-11-08 · team | [usage_flow.md](../external_design/usage_flow.md); [screen_list.md](../external_design/screen_list.md) |
| L8-21 | AD-UC-12: r1 "Request a saved-books action" is the same click as r2 (Save) or r3 (open the list). | Mapped to S-F01-01 or S-F03-03 (AD-UC-12 §5). Tidying the AD is a pending task. | Confirmed 22/11/2026 · group decision (D26); source: AD-UC-12 §5 | AD-UC-12 `r1` |
| L8-22 | Usage flows: four usage flows had only one use case on each path ("find a reading room in the library", "keep my reading history and reading list", "label new physical books", "moderate reported reviews"). Keep them as separate flows? | Joined: Reader has 3 flows ("find my way in the library" = find a book + find a room + saved books; "choose what to read" = discover books + reading history and preferences; "read and review a book"), On-site Staff has 1 flow ("keep physical books and reviews in order" = UC-10 + UC-13 from the same staff page). The usage-flow arrow UC-01 to UC-11 is now UC-12 to UC-11, because UC-12 is the use case that asks for sign-in (AD-UC-12 `c1`). | Confirmed 22/11/2026 · group decision (D26); source: [usage_flow.md](../external_design/usage_flow.md) | [usage_flow.md](../external_design/usage_flow.md) |

# Tasks and review records

## Pending tasks

Work still to be done. These are tasks, not open questions.

| Task | Source |
|---|---|
| ~~Draw #13 email line «Mã đã được gửi tới <email>.» (email in full, not masked) above the code field in the Default and every other S-F00-02 state, and re-export~~ — **closed 23/11/2026:** drawn in [s_f00_02.html](../external_design/screens/src/s_f00_02.html) and re-exported (Error-4 excepted by D31) | S-F00-02 W1 (D2, D15) |
| ~~Check the S-F00-03 images against the v0.8 §6 colour tokens (ui-conventions §7 consistency review flagged non-token Draw.io colours); correct if needed~~ — **closed 23/11/2026:** [s_f00_03.html](../external_design/screens/src/s_f00_03.html) uses only [ui_tokens.css](../external_design/screens/src/ui_tokens.css) colours (checked by script); images exported from it | S-F00-03 Q2, Q3 |
| ~~Draw «Đăng xuất» Secondary button (#7) in the Screen header of the S-F04-01 Default, Loading and Error images~~ — **closed 23/11/2026:** drawn in [s_f04_01.html](../external_design/screens/src/s_f04_01.html) and re-exported | S-F04-01 W1 (D7) |
| ~~Check the S-F04-01 images against the v0.8 §6 colour tokens; correct if needed~~ — **closed 23/11/2026:** [s_f04_01.html](../external_design/screens/src/s_f04_01.html) uses only [ui_tokens.css](../external_design/screens/src/ui_tokens.css) colours (checked by script); images exported from it | S-F04-01 Q3 |
| ~~Draw «Đăng xuất» Secondary button (#14) in the Screen header of every S-F02-03 state~~ — **closed 23/11/2026:** drawn in [s_f02_03.html](../external_design/screens/src/s_f02_03.html) and re-exported | S-F02-03 W1 (D7) |
| ~~Draw «Đã chọn <n> sách» Selection counter (#13) next to «In nhãn»; on the Next page image show it counting ticks kept from other pages~~ — **closed 23/11/2026:** drawn in [s_f02_03.html](../external_design/screens/src/s_f02_03.html) and re-exported | S-F02-03 W2 (D3b, D16) |
| ~~Redraw the S-F02-03 Empty state with «Tất cả sách bản giấy đã được in nhãn. Sách mới sẽ hiện ở đây sau lần đồng bộ danh mục tiếp theo.» (replacing «Chưa có sách bản giấy…»); sample rows in floor → room → shelf order~~ — **closed 23/11/2026:** drawn in [s_f02_03.html](../external_design/screens/src/s_f02_03.html) and re-exported | S-F02-03 W3 (D3, D15) |
| ~~Redraw the label sheet as A4 portrait 3 × 8 (70×37 mm) with the agreed label layout in M-F02-03-01 and the S-F02-03 Success image~~ — **closed 23/11/2026:** drawn in [s_f02_03.html](../external_design/screens/src/s_f02_03.html) and re-exported | S-F02-03 W4; M-F02-03-01 notes Q2 (D4) |
| ~~Draw «Đã in xong» as a **Secondary** button (#6) next to «In» / «Đóng» in M-F02-03-01 («In» stays the only Primary)~~ — **closed 23/11/2026:** drawn in [s_f02_03.html](../external_design/screens/src/s_f02_03.html) and re-exported | S-F02-03 W5; M-F02-03-01 notes Q3 (D12, D17) |
| ~~Update shared documents that still call «Đã in xong» a Primary button: [screen_list.md](../external_design/screen_list.md) (M-F02-03-01 row: "«Đã in xong» (Primary)") and [ui_conventions.md](../external_design/ui_conventions.md) §7 consistency row M-F02-03-01 ("new Primary button «Đã in xong»")~~ — **closed 23/11/2026:** screen-list and ui-conventions call it a Secondary button; the older wording is only in the review records | D17 |
| ~~Draw #10 Pagination («Trang trước» / «Trang sau») under the results, add a Next page state image, and show both Format labels on a book with both formats in the Results image~~ — **closed 23/11/2026:** drawn in [s_f03_01.html](../external_design/screens/src/s_f03_01.html); Results (both Format labels on a book with both formats) and Next page exported | S-F03-01 W1 (D9) |
| ~~Commit the editable S-F03-01 wireframe source to `screens/src/` and name it in the spec header~~ — **closed 23/11/2026:** [s_f03_01.html](../external_design/screens/src/s_f03_01.html), named in the spec header | S-F03-01 Q7 |
| ~~Cross-review the notes and specs of this group (S-F00-01, S-F00-02, S-F00-03, S-F04-01, S-F02-03, M-F00-01, M-F02-03-01)~~ — **dropped 23/11/2026:** removed from the task list by Chi | Notes "Review status"; spec "Review handoff" |
| ~~Cross-review the S-F03-01 spec~~ — **dropped 23/11/2026:** removed from the task list by Chi | S-F03-01 "Review handoff" |
| ~~Final consistency review / consolidation (26/11/2026); change Status to Reviewed when the images are verified~~ — **dropped 23/11/2026:** removed from the task list by Chi | Spec "Review handoff"; notes "Review status" |
| ~~Commit the wireframe source of S-F01-01, S-F01-02 and S-F03-03 under `screens/src/` (HTML or .drawio), then write its path in each spec's "Wireframe source" field.~~ — **closed 23/11/2026:** [s_f01_01.html](../external_design/screens/src/s_f01_01.html), [s_f01_02.html](../external_design/screens/src/s_f01_02.html), [s_f03_03.html](../external_design/screens/src/s_f03_03.html), named in the spec headers | S-F01-01 Q5, S-F01-02 Q5, S-F03-03 Q7; review of 22/11/2026 §4 |
| ~~Re-review the exports (S-F01-01, S-F01-02, S-F03-03) against ui-conventions and update their ui-conventions §7 rows (they still record "Fail: 1740px"; the images are now 1080px). Includes the wording check of «Đã lưu sách vào danh sách của bạn.» and «Đã bỏ sách khỏi danh sách.».~~ — **closed 23/11/2026:** re-exported at 1080px from the new sources; «Đã lưu sách vào danh sách của bạn.» and «Đã bỏ sách khỏi danh sách.» as in the specs; S-F01-02 shows its own room codes per floor; S-F03-03 sample data consistent | S-F01-01 Q4, S-F01-02 Q4, S-F03-03 Q6; removed "Draft review note" paragraphs |
| ~~Group review of S-F01-01, S-F01-02, S-F03-03 (Status stays "Draft" until reviewed).~~ — **dropped 23/11/2026:** removed from the task list by Chi | Removed Status suffix "pending group review …" and checklist item "Group review and approval completed" |
| ~~Fill the ui-conventions §1 modal-title rows: M-F02-01-01 «Xoá đánh giá?», M-F02-01-02 «Báo cáo đánh giá?» (replace the NEEDS CLARIFICATION cells).~~ — **closed 23/11/2026:** the §1 modal table has «Xoá đánh giá?» and «Báo cáo đánh giá?» | S-F02-01 Q6 |
| ~~Align line 97 of the wireframe guide ("Delete review" / "Keep review") with «Xoá đánh giá» / «Huỷ».~~ — **closed 23/11/2026:** the guide file was removed; M-F02-01-01 already uses «Xoá đánh giá» / «Huỷ». | M-F02-01-01 notes Q2 |
| ~~Restore the sheet W2_Costing: the workbook holds only a broken link to it, so the cost cells of W2_Rollup, W4, W5 and W6 show `#VALUE!` for every FR. Make it cover all 132 L3 rows (the link reads rows 9–128 only), including FR-02-22, FR-04-19, FR-04-20, FR-02-23 and FR-04-21~~ — **closed 23/11/2026:** W2_Costing rebuilt from the formulas in Parameters §8; it covers all 132 L3 rows and the workbook has no formula errors. | ui-conventions §7 open question 1 (UI Q13); workbook check 23/11/2026 |
| ~~Get the SVN-Gilroy font file and its licence from the library before DBIZ3~~ — **closed by D28** (Plus Jakarta Sans, free on Google Fonts) | ui-conventions §6 font notes (UI Q5) |
| Verify the final W1/W4 workbook and all exported PNGs before ui-conventions is marked v1.0 | ui-conventions last line `[NEEDS CLARIFICATION: … verify the final W1/W4 workbook and all exported PNGs …]` |
| ~~Re-review every row marked "Re-review pending" in the ui-conventions consistency review (Review records below) and record v0.9 results~~ — **dropped 23/11/2026:** removed from the task list by Chi | ui-conventions §7 consistency review |
| Give every screen and modal separate exported state PNGs (not only a combined `-states.png`); re-export the wireframes whose basis changed in v0.9: S-F00-01, S-F00-02, M-F00-01, S-F02-01, S-F02-02, S-F02-03, M-F02-03-01, S-F02-04, S-F03-01, S-F03-07, S-F04-01 | ui-conventions §7 change log v0.8 / v0.9 "Screens to re-export" column |
| ~~Re-export [ui_components.html](../external_design/screens/src/ui_components.html) and [ui_components.png](../external_design/screens/img/ui_components.png) to show the v0.9 components (Pagination, Trend tag, Selection counter, staff «Đăng xuất», «Đã in xong» as Secondary)~~ — **closed 23/11/2026:** re-exported with the staff Segmented control, «Đã in xong» as Secondary, the reprinted label and the error-Banner link | ui-conventions §7 consistency review; v0.9 change log |
| ~~S-F03-02 wireframe: replace the subject checkbox grid with Multi-select chips (`.multi-select-chips` in [ui_tokens.css](../external_design/screens/src/ui_tokens.css)) and re-export the S-F03-02 images~~ — **closed 23/11/2026:** Multi-select chips in [s_f03_02.html](../external_design/screens/src/s_f03_02.html); images re-exported; empty text = MSG-13 | S-F03-02 Q5 |
| ~~Split the sequence diagrams that tell two use cases; keep `alt` only for interaction conditions; change FR-02-10 to FR-02-14 in User Review Reporting Flow — same tasks as in the activity part~~ — **closed 23/11/2026:** SD-UC-01 … SD-UC-14 redrawn from the 10 original diagrams. | usage-flow "Note" rows 4, 5, 7 |
| ~~Add the use case "Sync data from the library internal system" (started by time) for FR-04-09, FR-04-10, FR-04-11 and FR-01-05, give it an ID and draw its activity diagram~~ — **closed 23/11/2026:** UC-15, AD-UC-15, SD-UC-15 (D48) | Inputs check 3; L8-20 |
| ~~Split the sequence diagrams that tell two use cases into one sequence per use case~~ — **closed 23/11/2026:** one file per use case, SD-UC-01 … SD-UC-14. | Inputs check 4 |
| ~~In the sequences, keep `alt` only for interaction conditions (reader choices are decisions in AD-UC-02, AD-UC-04, AD-UC-07)~~ — **closed 23/11/2026:** actor choices are marked sections; `alt` / `opt` are system conditions only. | Inputs check 5 |
| ~~Change the step of sequence User Review Reporting Flow that opens the reported-reviews list from FR-02-10 to FR-02-14~~ — **closed 23/11/2026:** SD-UC-13 cites FR-02-14. | Inputs check 7; AD-UC-13 Q4 |
| ~~Add the staff sign-in audit entry (D30) to the S-F00-03 spec (FR-04-12) and to the audit row of [screen_list.md](../external_design/screen_list.md) (AD-UC-10 `s15`, AD-UC-13 `s12`)~~ — **closed 23/11/2026:** S-F00-03 §5, SR-009 and §7; [screen_list.md](../external_design/screen_list.md) audit row. | D30 |
| ~~Add the branch UC-05 → UC-04 to AD-UC-05 when it is next revised~~ — **closed 23/11/2026:** AD-UC-05 v1.2 calls UC-04 (`c2`, `c3`, `c4`). | L8-17 |
| ~~Tidy AD-UC-12 `r1` (same click as `r2` / `r3`) when it is next revised~~ — **closed 23/11/2026:** AD-UC-12 v1.3 and SD-UC-12 v2.2 | L8-21 |
| ~~Get the library's agreement to add the new links on the existing OPAC pages~~ — **closed 23/11/2026:** the library agrees (D47) | L8-13 |
| ~~Review the workbook entries of 23/11/2026: FR-02-08 FP type (still EQ; it now records data, so it may be EI) and whether FR-02-08-BE needs a larger size or a new work item (W4 rule: change effort only when the technical scope really changes); whether the paging added to FR-03-12 (D33) changes its size; the proposed sizes of FR-02-23 and FR-04-21; the proposed priority of FR-02-23 (Must, rule R1), then check that Must share stays under 60% once W2_Costing is back~~ — **closed 23/11/2026:** FR-02-08 is EI; sizes kept, because FR-02-08-BE only adds one label flag per book (D49); FR-03-12 paging and FR-02-23 / FR-04-21 sizes kept; Must share 47.1% | D3, D7, D12 |
| ~~Redraw the S-F02-02 invalid-QR error image with the «Về OPAC» link (#16) and re-export it~~ — **closed 23/11/2026:** [s_f02_02_error.png](../external_design/screens/img/s_f02_02/s_f02_02_error.png) exported from [s_f02_02.html](../external_design/screens/src/s_f02_02.html), and panel 4 of [s_f02_02_states.png](../external_design/screens/img/s_f02_02/s_f02_02_states.png) updated. The link uses `colour/error-red` (4.92:1 on the error Banner; `colour/link` is only 4.26:1). | D37 |
| ~~Align the sequence diagrams with the activity diagrams of 23/11/2026: SD-UC-10 (audit entry after «Đã in xong», opening QR label printing, empty list, print another sheet), SD-UC-04, SD-UC-08, SD-UC-12 (the action continues after sign-in), SD-UC-03 (paging), SD-UC-05 (calls UC-04), SD-UC-06 and SD-UC-04 (reviewer name), SD-UC-11 (attempts left)~~ — **closed 23/11/2026:** the eight diagrams are v2.1 (sequence-index v2.1). | D1, D32, D33 |
| ~~Review the proposed workbook entries of D39 and D40: FR-02-24 (Could, NC, FE + BE size S) and FR-02-25 (Should, EQ, FE + BE size S). They add 10.8 person-hours and 2.84 million VND to the full scope~~ — **closed 23/11/2026:** sizes accepted by Chi | D39, D40 |
| ~~Run the AI critic prompt on each AD and log the findings (§7 row "Not yet run by the team")~~ — **dropped 23/11/2026:** removed from the task list by Chi | AD-UC-01 … AD-UC-14 §7 |
| ~~Fill in the exit ticket after the peer review~~ — **dropped 23/11/2026:** removed from the task list by Chi | activity-index "Exit ticket" |
| ~~Add UC-15 to the Use Case Diagram PDF; remove the arrows UC-14 → UC-06 and On-site Staff → UC-11; add UC-05 → UC-04 and UC-05 → UC-14. Remove "availability" from the Context Diagram and the CVCA. The editable sources of these PDFs are not in the repository~~ — **closed 23/11/2026:** the three diagrams were redrawn in Mermaid with these changes ([use_case.md](../system_design/use_case.md), [context_diagram.md](context_diagram.md), [cvca.md](cvca.md)); the PDFs stay unchanged in Git history at commit [cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/tree/cd61897/%5BDBIZ%202%5D%20GROUP%20H) (D52) | D48; check of 23/11/2026 |
| ~~Decide FR-04-13 "Deploy automatically" (Must): it needs FR-04-14 "Run automated tests on every change" (Should). Raise FR-04-14 to Must or remove the test condition from FR-04-13~~ — **closed 23/11/2026:** FR-04-14 raised to Must (D50) | W1 column G (D49) |
| Choose the technology for DBIZ3 and record each choice as a decision row: languages and frameworks, database product, hosting and the test/deploy tool (FR-04-13, FR-04-14), AI model, how the OTP email is sent without an outside email service (AD-UC-11 Q2), how the Library Internal System is read | [system_architecture.md](../system_design/system_architecture.md#9-not-decided-here) |
| Fix the cash-flow figures listed in [cost.md §10](../requirements/cost.md#10-known-inconsistencies-to-fix) (base scenario year-0 investment, pessimistic heading and decision signal) | Workbook export of 23/11/2026 (D51) |
| W5 question 5: does the anonymous read log (FR-03-13) need a privacy notice or a retention period? Not blocking | D47 |

## Review records

Records of checks and reviews moved out of the design documents.

Render check, 22/11/2026: all 14 activity diagrams (AD-UC-01 … AD-UC-14), the screen-transition diagrams and the usage-flow diagrams were opened and rendered with Mermaid 12.3.0 in Chrome (swimlane-beta for the activity diagrams); all render. Each AD §7 records it as "Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass".

### Screen specs: S-F00, S-F02-03, S-F03-01, S-F04

| Record | Content (moved from the files) | Source |
|---|---|---|
| Notes self-check | "Review status: self-checked against the assignment and the two shared UI/UX handbooks. Cross-review and final consistency review are pending." | notes S-F00-01, S-F00-02, S-F00-03, S-F04-01, S-F02-03, M-F00-01, M-F02-03-01 |
| S-F00-03 / S-F04-01 Draft review note | The numbered image was linked from the GitHub repository (raw URL) rather than edited or copied; state image paths were "pending confirmation"; images "not yet approved against UI Conventions v0.8". Replaced on 22/11/2026 by the local `img/<ID>/<ID>-numbered.png` (same file). | [screen_spec_s_f00_03.md](../external_design/screens/specs/screen_spec_s_f00_03.md) §2; [screen_spec_s_f04_01.md](../external_design/screens/specs/screen_spec_s_f04_01.md) §2 |
| S-F00-03 handoff 21/11/2026 | The colour-token corrections and the separate state exports belong in `screens/img/`; the existing numbered image was reported as 1693px and had to be re-exported at 1280px; paths and images are verified after upload; spec stays Draft. The §7 consistency review flagged the Draw.io colours as non-token and the 1693px export. (22/11/2026: all S-F00-03 exports are 1280px.) | [screen_spec_s_f00_03.md](../external_design/screens/specs/screen_spec_s_f00_03.md) §2 |
| S-F04-01 working rule | "Do not modify the wireframe owner's Draw.io or PNG files as part of this Screen Spec. Any mockup corrections must be reported to the wireframe owner." The state table had a "Verification: Pending check" column for Default, Loading and Error (removed; see Pending tasks). | [screen_spec_s_f04_01.md](../external_design/screens/specs/screen_spec_s_f04_01.md) §2 |
| Review handoff 21/11/2026 (S-F00-03, S-F04-01) | Do not edit another member's source or images. Cross-review, then consolidation on 26/11/2026. Status Draft until the state PNGs exist, render on GitHub and meet v0.8. Destination `external_design/screens/specs/screen_spec_<id>.md`. | [screen_spec_s_f00_03.md](../external_design/screens/specs/screen_spec_s_f00_03.md), [screen_spec_s_f04_01.md](../external_design/screens/specs/screen_spec_s_f04_01.md) |
| Review handoff 21/11/2026 (S-F03-01) | Cross-review, then consolidation on 26/11/2026; Draft until the state PNGs exist and meet v0.8. Draft review note: the state images are cropped from the composite [s_f03_01_states.png](../external_design/screens/img/s_f03_01/s_f03_01_states.png); verify against v0.8 before approval. The numbered image was linked from GitHub (now the local [s_f03_01_numbered.png](../external_design/screens/img/s_f03_01/s_f03_01_numbered.png)). | [screen_spec_s_f03_01.md](../external_design/screens/specs/screen_spec_s_f03_01.md) §2 and end |
| M-F00-01 shared handoff | "Shared handoff for the screen owners: use [m_f00_01.png](../external_design/screens/img/m_f00_01/m_f00_01.png), its HTML source, and MSG-01 / MSG-02 / MSG-03. The blurred/dimmed context illustrates S-F01-01 only. The modal is shared by all seven listed entry screens. No group notification has been sent." (The content sentence stays in the notes; S-F02-01 and S-F02-02 specs already link to S-F00-01 §3.1.) | notes/M-F00-01 |
| S-F02-03 / M-F02-03-01 decision updates | "Decision update, 21/11/2026" (confirmed Q3 newly synced list newest first; Q4 2 × 5) and "Decision update, 22/11/2026" / "Follow-up decision update" paragraphs (D3, D4, D7, D12, D13, D15, D16). Now indexed in rows S-F02-03 Q3, Q4 and the D-section. | notes/S-F02-03, notes/M-F02-03-01 |

### Screen specs: S-F01, S-F02-01/02/04, S-F03-03

| Record | Content | Date · by | Outcome |
|---|---|---|---|
| Draft review note in S-F01-01, S-F01-02, S-F03-03 §2 | "Do not treat the exports as approved until the required size and UI-conventions checks are complete." | before 22/11/2026 | Size check done 22/11/2026 (all 1080px, separate files); conventions check is a pending task. Note removed from the specs. |
| Status field of S-F01-01, S-F01-02 ("Draft — pending group review and wireframe/export verification") and S-F03-03 ("Draft — pending group review and priority reconciliation") | Working status text outside the template values | before 22/11/2026 | Set to "Draft" (template value). Priority reconciled (S-F03-03 Q5); review is a pending task. |

### Screen specs: S-F03-02/06/07 and shared documents

#### ui-conventions: checks run on 22/11/2026

| Record | Date | Source |
|---|---|---|
| Modal titles re-checked against all five modal notes (former `[NEEDS CLARIFICATION: Recheck modal titles …]`): all five now filled in ui-conventions §1 (UI Q17). | 22/11/2026 | ui-conventions last line |
| [ui_tokens.css](../external_design/screens/src/ui_tokens.css) now contains `.pagination` (line 276), `.trend-tag`, `.selection-counter` and `.multi-select-chips`; the consistency-review sentence "Pagination (`.pagination`) … not in it yet" is out of date. The staff header «Đăng xuất» uses the existing Secondary button style. | 22/11/2026 | ui-conventions §7 consistency review |
| Workbook read: W1 and W4 contain FR-02-22, FR-04-19, FR-04-20 (W4 priorities Should, Should, Must); FR-02-23 and FR-04-21 are absent from every sheet. | 22/11/2026 | ui-conventions §7 open question 1 |

#### screen-transition and usage-flow: Mermaid parser check, 22/11/2026

Scripted check with Mermaid 11.4.1 (`mermaid.parse`, jsdom): screen-transition Reader diagram (57 arrows) and staff
diagram (13 arrows) parse without error; the four usage-flow diagrams (14, 17, 14, 7 arrows) parse without error. A
deliberately broken control diagram was rejected, so the check does detect errors. This replaces the screen-transition
note "the 2026-11-22 edits … have not been run through the parser again: re-check on mermaid.live".

#### ui-conventions §7 consistency review (moved verbatim from ui-conventions v0.9, 22/11/2026)

Update after D17 (22/11/2026): in the M-F02-03-01 row, «Đã in xong» is now a **Secondary** button, not "new Primary
button"; the other rows are unchanged.

Preliminary audit populated from the ui-conventions review (19/11/2026), **not a fresh inspection of all 20 rendered screens**. "Not verified" is not Pass. Every screen/modal also requires separate exported state PNGs (not only a combined `-states.png`). HTML, images, messages and keyboard access must be rechecked after fixes. Do not mark v1.0 until all checks are verified.

Rows whose basis changed in v0.9 (a group
decision D1–D11 or a re-exported wireframe) are marked "Re-review pending"; their earlier finding is kept for
history and is not a result for v0.9. Shared files: [ui_tokens.css](../external_design/screens/src/ui_tokens.css) is aligned to v0.8, plus the Trend tag
(`.trend-tag`) and the Selection counter (`.selection-counter`) for v0.9; Pagination (`.pagination`) and the staff header «Đăng xuất» are not in it yet.
[ui_components.html](../external_design/screens/src/ui_components.html) and [ui_components.png](../external_design/screens/img/ui_components.png) must be re-exported to show the v0.9 components.

| Screen / modal | Colours only from tokens | Component names as section 3 | Messages follow section 4 | Accessibility (section 5) | Image size correct | Result | Date |
|---|---|---|---|---|---|---|---|
| S-F00-01 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 773px (expected 1080px) | **Re-review pending** — basis changed in v0.9: D1 (pending action kept; «Huỷ» instead of Back), D8. Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F00-02 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 773px (expected 1080px) | **Re-review pending** — basis changed in v0.9: D1, D2 (email not masked), D8, D15 (email line MSG-10 approved). Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F00-03 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 1693px (expected 1280px) | **Re-review pending** — basis changed in v0.9: D7 (sign-out lands here), D8 staff responsive. Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F01-01 | Not verified: source missing | Fail: names outside §3 | Not verified | Not verified | Fail: 1740px (expected 1080px) | Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review) |
| S-F01-02 | Not verified: source missing | Fail: names outside §3 | Not verified | Not verified | Pass (reported) | Needs correction: separate state PNGs required; source HTML/draw.io missing at review; notes Author missing | 21/11/2026 (based on 19/11 review) |
| S-F02-01 | Not verified: source missing | Not verified | Not verified | Not verified | Pass (reported) | **Re-review pending** — basis changed in v0.9: D6 (Load more shown while more reviews remain); wireframe rebuilt with [ui_tokens.css](../external_design/screens/src/ui_tokens.css) 22/11. Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F02-02 | Not verified: source missing | Not verified | Not verified | Not verified | Pass (reported) | **Re-review pending** — basis changed in v0.9: D5 (no Back), D6 (Load more); wireframe rebuilt with [ui_tokens.css](../external_design/screens/src/ui_tokens.css) 22/11. Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F02-03 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 1693px (expected 1280px) | **Re-review pending** — basis changed in v0.9: D3 (list of books never label-printed, 20 per page, shelf order, ticks kept, «Đã chọn n sách»), D4, D7 («Đăng xuất»), D8, D12 (list keeps books until «Đã in xong»), D13 (primary shelf location), D15 (empty-state wording), D16 (Selection counter). Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F02-04 | Not verified: source missing | Not verified | Not verified | Not verified | Pass (reported) | **Re-review pending** — basis changed in v0.9: D7 («Đăng xuất»), D8 (stack below 1024px); wireframe rebuilt with [ui_tokens.css](../external_design/screens/src/ui_tokens.css) 22/11. Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F03-01 | Not verified: source missing | Fail: names outside §3 | Not verified | Not verified | Fail: 1740px (expected 1080px) | **Re-review pending** — basis changed in v0.9: D9 (both Format labels, Pagination 20 per page), D8, D14 (back to page 1 when the format changes). Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review; notes Frame/version/Author missing | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F03-02 | Fail: HTML has off-token colours | Fail: names outside §3 | Not verified | Not verified | Fail: 1740px (expected 1080px) | Needs correction: separate state PNGs required; use shared [ui_tokens.css](../external_design/screens/src/ui_tokens.css)/state template and approved titles | 21/11/2026 (based on 19/11 review) |
| S-F03-03 | Not verified: source missing | Fail: names outside §3 | Not verified | Not verified | Fail: 1740px (expected 1080px) | Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review) |
| S-F03-06 | Fail: HTML has off-token colours | Fail: names outside §3 | Not verified | Not verified | Fail: 1740px (expected 1080px) | Needs correction: separate state PNGs required; use shared [ui_tokens.css](../external_design/screens/src/ui_tokens.css)/state template and approved titles | 21/11/2026 (based on 19/11 review) |
| S-F03-07 | Fail: HTML has off-token colours | Fail: names outside §3 | Not verified | Not verified | Fail: 1740px (expected 1080px) | **Re-review pending** — basis changed in v0.9: D10a (Trend tag), D10b («Sở thích» always shown, Secondary button), D11, D8. Earlier finding: Needs correction: separate state PNGs required; use shared [ui_tokens.css](../external_design/screens/src/ui_tokens.css)/state template and approved titles | 21/11/2026 (based on 19/11 review); re-review pending |
| S-F04-01 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 1693px (expected 1280px) | **Re-review pending** — basis changed in v0.9: D7 («Đăng xuất» in header), D8. Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| M-F00-01 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 773px (expected 1080px) | **Re-review pending** — basis changed in v0.9: D1; section 3 modal exception («Đăng nhập» opens S-F00-01). Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| M-F02-01-01 | Not verified: source missing | Not verified | Not verified | Not verified | Pass (reported) | **Re-review pending** — basis changed in v0.9: images re-exported 22/11 from the rebuilt S-F02-01 wireframe. Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review); re-review pending |
| M-F02-01-02 | Not verified: source missing | Not verified | Not verified | Not verified | Pass (reported) | **Re-review pending** — basis changed in v0.9: images re-exported 22/11 from the rebuilt S-F02-01 wireframe. Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review); re-review pending |
| M-F02-03-01 | Fail: draw.io uses non-token colours | Not verified | Not verified | Not verified | Fail: 1693px (expected 1280px) | **Re-review pending** — basis changed in v0.9: D4 (label sheet A4 3 × 8, 70×37 mm, agreed label content, one label per title), D12 (new Primary button «Đã in xong»), D13 (primary shelf location on the label). Earlier finding: Needs correction: separate state PNGs required; replace dark primary and grey error styling with tokens | 21/11/2026 (based on 19/11 review); re-review pending |
| M-F02-04-01 | Not verified: source missing | Not verified | Not verified | Not verified | Pass (reported) | **Re-review pending** — basis changed in v0.9: images re-exported 22/11 from the rebuilt S-F02-04 wireframe. Earlier finding: Needs correction: separate state PNGs required; source HTML/draw.io missing at review | 21/11/2026 (based on 19/11 review); re-review pending |

### Activity diagrams

| Record | Date | Source |
|---|---|---|
| Section 5 "Screens touched" is filled in all 14 activity diagrams; the book links and the format-filter link used by the screen transition are drawn as calls in AD-UC-03 v1.3, AD-UC-08 v1.2 and AD-UC-09 v1.2. | 2026-11-08 | activity-index ("Closed on 2026-11-08") |
| W1 updated: FR-04-18 added (rows FR-04-18-FE and FR-04-18-BE, L8-03); FR-03-12-FE (L8-12), FR-03-18-FE and FR-03-21-FE (L8-01) reworded to match the external design. | 2026-11-08 | activity-index ("W1 updated on 2026-11-08") |
| AD-UC-04 v1.2: "Delete" still means hidden from public display (state `Removed`), consistent in `s6`, section 4 and AD-UC-04 Q3 (checked by reading). | 2026-11-22 | AD-UC-04 §7 (shortened) |
| AD-UC-06 v1.2: `d2` was "Act on a review?" and was renamed "What does the reader do next?" because it also offers the next page; its "[No]" guard became "[Finish]" (D6). | 2026-11-22 | AD-UC-06 reading notes (moved) |
| AD-UC-10 v1.4: `a9` returns through the existing merge `mB` (now four incoming flows); `s13` and `d8` each have one incoming flow (checked by reading). | 2026-11-22 | AD-UC-10 §7 (shortened) |
| AD-UC-14 v1.3: AD-UC-14 Q2 changed to "No" on 2026-11-19. | 2026-11-19 | AD-UC-14 header (moved) |
