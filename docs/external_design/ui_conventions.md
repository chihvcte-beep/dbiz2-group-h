# UI Conventions: Group H Library Core System

<!--
DBIZ2 Lesson 8 template. File: EXTERNAL [ui_conventions.md](ui_conventions.md)
One page. It keeps screens consistent with each other when different members, or different AI
tools, draw them. In DBIZ3 the coding agent reads this file before it builds any screen.
-->

Version v0.13 · 23/11/2026 · Owner: Linh · Reviewer: Chi · Applies to the 15 screens and 5 modals in [screen_list.md](screen_list.md) (v1.0, 2026-11-08).

Every wireframe, notes file and screen spec follows this file. A value (colour, size, wording pattern) is defined
once, here; [ui_tokens.css](screens/src/ui_tokens.css) copies section 6 exactly. Sections 1–5 follow `ui-conventions-template.md`;
section 6 follows the teacher's LabDesk example; section 7 is added by the Lesson 8 guide. The decisions behind
these values (`UI Q1` … and the group decisions `D1` …) are recorded in [decision_index.md](../project_brief/decision_index.md#ui-conventions).

## 1. Language and tone

- Interface language: **Vietnamese** (UI Q1). Every text on wireframes and in the product is
  Vietnamese with full diacritics; this document and the screen specs stay in English. No language switch: no FR asks for one.
- Address the reader or staff member as "bạn". Short, plain sentences; no jargon such as "session", "OTP" or "token"
  in reader-facing text — say "mã" and "đăng nhập".
- Button labels are verbs that say what will happen. Never "OK", "Gửi đi", "Có" or "Không". Standard labels, used
  exactly as written on every screen:

| Action | Label | Where |
|---|---|---|
| Show shelf location | Xem vị trí kệ sách | OPAC link → S-F01-01 |
| Save to my list | Lưu vào danh sách | S-F01-01 (FR-03-06) |
| View on map | Xem trên bản đồ | S-F01-01 (FR-01-03) |
| Send code | Gửi mã | S-F00-01 |
| Send a new code | Gửi mã mới | S-F00-02 (FR-04-04, FR-04-16) |
| Sign in | Đăng nhập | S-F00-02, S-F00-03, M-F00-01 |
| Not now | Để sau | M-F00-01 |
| Post review | Đăng đánh giá | S-F02-01, S-F02-02 (FR-02-01) |
| Edit (own review) | Sửa | Review item |
| Save changes | Lưu thay đổi | S-F02-01, S-F02-02, S-F03-02 |
| Delete review (reader, own) | Xoá đánh giá | Review item, M-F02-01-01 (FR-02-04) |
| Report review | Báo cáo đánh giá | Review item, M-F02-01-02 (FR-02-09) |
| Load more reviews | Xem thêm đánh giá | S-F02-01, S-F02-02 (FR-02-02) |
| Previous page / Next page | Trang trước / Trang sau | Pagination: S-F02-03, S-F03-01 |
| Reading preferences | Sở thích | S-F03-07 header → S-F03-02 |
| Sign out (staff) | Đăng xuất | Staff screen header: S-F04-01, S-F02-03, S-F02-04 (FR-04-21) |
| Remove (saved book) | Bỏ khỏi danh sách | S-F03-03 (FR-03-08) |
| Print labels | In nhãn | S-F02-03 (FR-02-08) |
| Print | In | M-F02-03-01 |
| Confirm the sheet was printed | Đã in xong | M-F02-03-01 (FR-02-08): Secondary button; the only action that records the books as label-printed (D12, D17); on a reprint it writes only the audit entry (D40) |
| Reprint labels | In lại nhãn | S-F02-03 under the filter «Đã in nhãn» (FR-02-25): Primary button (D40) |
| Remove review (staff) | Gỡ đánh giá | S-F02-04, M-F02-04-01 (FR-02-10) |
| Dismiss report | Bỏ qua báo cáo | S-F02-04 (FR-02-20) |
| Send chat message | Gửi | S-F03-06 |
| Cancel (in a modal) | Huỷ | modals; also S-F00-01, S-F00-02 (returns to the starting screen, pending action kept) |
| Try again | Thử lại | MSG-04 |
| Back | Quay lại | Screen header |
| Close print preview | Đóng | M-F02-03-01 |

- One action, one name, on every screen: "Lưu vào danh sách" is never also "Thêm" or "Đánh dấu"; "Bỏ khỏi danh sách"
  (saved book) is never "Xoá"; "Xoá đánh giá" (reader, own review) and "Gỡ đánh giá" (staff, FR-02-10) stay different
  because they are different actions.
- Screen titles: Vietnamese title per screen, same meaning as the "Screen name" column of [screen_list.md](screen_list.md):

| Screen | Title | Screen | Title |
|---|---|---|---|
| S-F00-01 | Đăng nhập | S-F02-04 | Đánh giá bị báo cáo |
| S-F00-02 | Nhập mã xác thực | S-F03-01 | Lọc theo hình thức |
| S-F00-03 | Đăng nhập nhân viên | S-F03-02 | Lịch sử đọc và sở thích |
| S-F01-01 | Vị trí kệ sách | S-F03-03 | Sách đã lưu |
| S-F01-02 | Bản đồ thư viện | S-F03-06 | Trợ lý tìm sách AI |
| S-F02-01 | Đánh giá sách | S-F03-07 | Sách gợi ý cho bạn |
| S-F02-02 | Thông tin và đánh giá sách | S-F04-01 | Trang nhân viên |
| S-F02-03 | In nhãn mã QR | | |

Modal titles and actions (use the screen/modal notes as the source of truth; do not invent new flows):

| Modal | Title | Actions / labels | Source |
|---|---|---|---|
| M-F00-01 | Đăng nhập để tiếp tục? | Đăng nhập (Primary) · Để sau (Secondary) | MSG-01; [m_f00_01_notes.md](screens/notes/m_f00_01_notes.md) |
| M-F02-01-01 | Xoá đánh giá? | Xoá đánh giá (Destructive) · Huỷ (Secondary) | [m_f02_01_01_notes.md](screens/notes/m_f02_01_01_notes.md); UI Q17 |
| M-F02-01-02 | Báo cáo đánh giá? | Báo cáo đánh giá (Primary) · Huỷ (Secondary) | [m_f02_01_02_notes.md](screens/notes/m_f02_01_02_notes.md); UI Q17 |
| M-F02-03-01 | Xem trước trang nhãn mã QR | In (Primary) · Đã in xong (Secondary) · Đóng (Secondary) | [m_f02_03_01_notes.md](screens/notes/m_f02_03_01_notes.md); D12, D17; UI Q17 |
| M-F02-04-01 | Gỡ đánh giá? | Gỡ đánh giá (Destructive) · Huỷ (Secondary) | [m_f02_04_01_notes.md](screens/notes/m_f02_04_01_notes.md); UI Q17 |

- Sentence case: only the first word and proper names are capitalised ("Sách đã lưu", not "Sách Đã Lưu").
  Codes keep their case (OPAC, QR, R-204).
- Every font must render "Ầ ẩ ẫ ậ ỗ ự ỹ Đđ" without broken marks (handbook section 3). Inter and Plus Jakarta Sans both do.

## 2. Formats

| Item | Format | Example | Source / note |
|---|---|---|---|
| Date | dd/MM/yyyy | 16/10/2026 | Teacher example (LabDesk) |
| Time | HH:mm, 24-hour | 09:00 | Teacher example |
| Library card number | exactly 7 digits, may start with 0 (keep leading zeros, store as text), no spaces; numeric keyboard on phones | 0012345 | UI Q8; AD-UC-11 section 3. Inline error if not 7 digits: "Số thẻ thư viện gồm 7 chữ số. Bạn kiểm tra lại nhé." (input check only; whether the card exists is FR-04-01) |
| OTP code | 6 digits | 482913 | FR-04-04 (6-digit code, updated in W1 14/11/2026); AD-UC-11 section 3 |
| OTP validity | "Mã có hiệu lực trong 5 phút." | | FR-04-04 |
| OTP attempts left | shown after each wrong code: "Mã chưa đúng. Bạn còn `<n>` lần thử." (n = 4…1); after the 5th: "Bạn đã nhập sai 5 lần. Mã này không còn dùng được, hãy bấm Gửi mã mới." | Mã chưa đúng. Bạn còn 3 lần thử. | FR-04-17, FR-04-19 |
| Shelf location | Tầng `<n>` · Phòng `<code>` · Kệ `<code>` | Tầng 2 · Phòng R-204 · Kệ S-12 | AD-UC-01 section 3; one line per physical copy, the primary shelf location returned by the sync first; that primary location is the one on the QR label and in the S-F02-03 order (AD-UC-01 Q1; D13; D27; FR-01-01) |
| Room on the map | `<room name>` (`<room code>`), Tầng `<n>` | Phòng đọc A (R-204), Tầng 2 | FR-01-11 |
| Access format label | Trực tuyến · Bản giấy | | FR-03-12; always icon + word (section 5). A book with both formats shows both labels, «Bản giấy» and «Trực tuyến» (D9) |
| Access format choice | Trực tuyến · Bản giấy · Cả hai | | FR-03-12 |
| Reading status | Đang đọc · Đã đọc xong | | FR-03-04 |
| Reading progress | whole number 0–100 followed by "%" | 45% | FR-03-04 |
| Review length counter | `<n>/2.000` with dot thousands separator (Vietnamese) | 128/2.000 | FR-02-01 |
| Review date | dd/MM/yyyy | 02/11/2026 | as Date |
| Book title / author | as in the catalogue; cut with "…" after 2 lines | Digital Marketing Basics | Book catalogue (W0 Table 4) |
| Staff account | internal account name | staff.lan | AD-UC-10 section 3 |
| Selected books count | Đã chọn `<n>` sách | Đã chọn 3 sách | S-F02-03, next to «In nhãn»; counts ticks on every page; shown with the Selection counter component (section 3; D3b, D16) |
| QR label text | book title (max 2 lines, cut with "…"); Shelf location line (not on a reprinted label, D40); small line "Quét để xem thông tin và đánh giá" | Tầng 2 · Phòng R-204 · Kệ S-12 | Label sheet (section 3); D4, D40 |
| Reviewer name | the reader chooses, per review: their full name exactly as registered on the library card account (from the Library Internal System, not editable here), or anonymous "Bạn đọc ẩn danh" | Nguyễn Văn An · Bạn đọc ẩn danh | UI Q9. Control: Checkbox "Đăng ẩn danh" under the review text area, unchecked by default. FR-02-22. |
| Numbers | dot thousands separator, comma decimal (Vietnamese) | 1.250 lượt quét | Vietnamese convention |
| Currency | not used | — | No screen shows money (no FR) |
| Phone | not used | — | No screen shows a phone number (no FR) |
| Names | reader: see Reviewer name; staff: account name | staff.lan | as above |

## 3. Components (use these names in every Screen Spec)

Names in the first column are the only names used in the "Component" column of wireframe notes and the "Type"
column of screen specs. CSS class = the name in kebab-case (`.primary-button`, `.book-row`, `.room-tile`).
The template's generic "List item" is split into the product's own list items: Book row, Review item, Book card.

| Component | When to use | Used on | Notes (limits · style · states) |
|---|---|---|---|
| Screen header | top of every screen: Back button + screen title | all screens | Back is a 44×44px icon button with "Quay lại" as its accessible name; title one line (section 1 shortening rule). States: default, focus. Exceptions (D1, D5, D7): **S-F00-01** (opened from «Đăng nhập» in M-F00-01) has no Back — its Secondary button «Huỷ» returns to the starting screen and the pending action is kept; a modal, M-F00-01 included, has no Screen header. **S-F02-02** has no Back in any case: it opens only from the QR label scan (also after sign-in); the way out is the Text link «Xem sách trên OPAC». **Staff screens** (S-F04-01, S-F02-03, S-F02-04): Secondary button «Đăng xuất» on the right side of the header (FR-04-21). **S-F00-03** has no Screen header bar: its title sits at the top of the Sign-in card (D29) |
| Primary button | the one main action when a screen has one | at most one per screen; not required on S-F04-01 | One visible per screen at a time. Solid `colour/brand-red` fill, white text, no icon; full width at 360px; height 48px (Reader) / 40px (Staff). States: default, hover, focus, pressed, disabled |
| Secondary button | other actions, Cancel, Not now, «Đăng xuất» (staff header), «Sở thích» (S-F03-07 header), «Đã in xong» (M-F02-03-01) | many screens, every modal | Outline `colour/border`, text `colour/text`; same height as Primary. States: default, hover, focus, pressed, disabled |
| Destructive button | the confirm action of a delete or remove modal | M-F02-01-01, M-F02-04-01 | Outline 2px `colour/error-red`, text `colour/error-red`, trash icon before the label — so it never looks like the red Primary button. Only inside a modal. States: default, hover, focus, pressed |
| Text link | go to another page (e.g. "View this book on the OPAC", "use the format filter", "Set your reading preferences") | S-F02-02, S-F03-06, S-F03-07 | `colour/link` (OPAC blue), underlined. Inside an error Banner the link uses `colour/error-red`, underlined, because `colour/link` is only 4.26:1 there (4.92:1 for error red; D46). Never used for an action that changes data |
| Text input | one-line entry | S-F00-01 (card number, 7 digits, numeric keyboard), S-F00-03 (staff account) | Label above the field; 16px text; height 48px (Reader) / 40px (Staff). States: default, focus, disabled, error (2px `colour/error-red` border + Inline error) |
| Code input | enter the email code | S-F00-02 | One field, 6 digits, numeric keyboard on phones; not split into boxes. States as Text input |
| Password input | staff password | S-F00-03 | Text input with a "Hiện" / "Ẩn" text button. States as Text input |
| Sign-in card | the staff sign-in form | S-F00-03 | One card (`colour/card`, 1px `colour/border-light`, `radius`, `shadow/modal`, 32px padding), max width `size/sign-in-card` 400px, **centred horizontally and vertically** in the frame — never aligned to the left edge. Inside, top to bottom: screen title (centred, `font/heading`), error Banner when needed, fields, Primary button at full card width. On the Reader sign-in screens (S-F00-01, S-F00-02) the form already fills the 360px frame, and from 640px it follows the centred one-column rule of section 6.1 (D29) |
| Text area with counter | write or edit a review | S-F02-01, S-F02-02 | Counter `<n>/2.000` under the right edge; counter turns `colour/error-red` with icon above 2.000 (FR-02-01). Hint line under the field (below the Inline error when shown): MSG-14, small `colour/text-muted` text, not a link (D20). States as Text input |
| Segmented control | choose ONE of a few fixed options | S-F03-01 (Trực tuyến / Bản giấy / Cả hai), S-F01-02 (floor), S-F02-03 (Chưa in nhãn / Đã in nhãn, D40) | Selected segment: `colour/brand-red` fill + white text + check icon. States: default, selected, focus, disabled |
| Select | choose reading status | S-F03-02 | Options "Đang đọc", "Đã đọc xong" (FR-03-04). States as Text input |
| Number input | reading progress | S-F03-02 | 0–100, "%" suffix outside the field (FR-03-04). States as Text input |
| Checkbox | select several books; post a review anonymously | S-F02-03; S-F02-01, S-F02-02 ("Đăng ẩn danh") | 24×24px box, 44px row height for the hit area. States: unchecked, checked, focus, disabled |
| Book row | one book in a list: cover placeholder, title, author, Format label | S-F03-01, S-F03-03, S-F03-07, S-F02-03; S-F02-01, S-F02-02 (book block at the top, no Format label; D21) | Grey "Cover" block, no real cover images (UI Q6). Whole row tappable when it opens a page; disabled state only if an unavailable action is explicitly required, otherwise N/A |
| Book card | compact book inside a chatbot reply | S-F03-06 | Title, author, Format label, Text link to the book |
| Format label | Trực tuyến / Bản giấy tag | S-F03-01, S-F03-03, S-F03-06, S-F03-07, S-F02-03 | Icon + word, outline style, never colour alone (section 5). A book with both formats shows both labels side by side, «Bản giấy» and «Trực tuyến» (D9) |
| Trend tag | marks a book added from trending titles (FR-03-20) | S-F03-07 | Text «Xu hướng», always shown (never colour or icon alone); pill (radius 999px), `colour/info-bg` fill, 1px `colour/info-border` border, `colour/info-text` small text; optional 16px icon before the text. Passive display: no focus, hover or disabled state. CSS `.trend-tag` (in [ui_tokens.css](screens/src/ui_tokens.css)). D10a |
| Shelf location line | one line "Floor · Room · Shelf" for one copy | S-F01-01, S-F01-02, S-F03-03, M-F02-03-01 | Format in section 2; map-pin icon before it |
| Floor plan | block plan of one floor, one tile per room | S-F01-02 | Neutral surface; no real library drawing (UI Q4) |
| Room tile | one room on the Floor plan | S-F01-02 | States: default (white, `colour/border`), selected (`colour/brand-red` fill, white text), highlighted = book's room (`colour/highlight` fill + 3px `colour/highlight-border` + "Sách của bạn ở đây" label) |
| Review item | one review: reviewer name or "Bạn đọc ẩn danh", date, text, actions | S-F02-01, S-F02-02, S-F02-04 | Own review: Edit, Delete review. Others' review: Report review (S-F02-01 only). Text buttons |
| Load more button | next page of reviews | S-F02-01, S-F02-02 | Secondary button style, full width, "Xem thêm đánh giá" (FR-02-02); 10 reviews per page; shown while more published reviews remain (D6); states: default, hover, focus, disabled while loading |
| Pagination | move between pages of a long list | S-F02-03, S-F03-01 | 20 rows per page (D3c, D9). Two Secondary buttons under the list, «Trang trước» and «Trang sau»; «Trang trước» disabled on the first page, «Trang sau» disabled on the last page. On S-F02-03 ticks are kept across pages and «Đã chọn `<n>` sách» shows next to «In nhãn» (D3b). States: default, hover, focus, disabled. CSS `.pagination` (in [ui_tokens.css](screens/src/ui_tokens.css)) |
| Selection counter | passive text next to a bulk action, counting the items ticked on all pages | S-F02-03 («Đã chọn `<n>` sách» next to «In nhãn») | Format in section 2 (Selected books count). Counts ticks on every page of the list, not only the page shown. Passive display: not a button, no focus, hover or disabled state; small or body text in `colour/text`. CSS `.selection-counter` (in [ui_tokens.css](screens/src/ui_tokens.css)). D16 |
| Chat bubble | reader message / chatbot reply | S-F03-06 | Reader: right, `colour/info-bg`; chatbot: left, `colour/surface`. Text always `colour/text` |
| Message composer | type and send a chatbot message | S-F03-06 | Text input + Primary button "Gửi", fixed at the bottom |
| Menu tile | big task choice on the staff page | S-F04-01 | Icon + title + one-line description; whole tile clickable; 2 tiles |
| Banner | non-blocking message that stays on the screen | many screens | 4 kinds: info, success, warning, error. Each = icon + text + left border colour (section 6). Top of the content |
| Inline error | validation error of one field | forms | Directly under the field in error: light `colour/error-red-bg` background, 1px `colour/error-red` border, `colour/error-red` text, always a "!" icon. The field itself gets a 2px `colour/error-red` border; the message text is required, never the border colour alone |
| Modal | confirm or cancel ONE action | the 5 modals in [screen_list.md](screen_list.md) | Never for navigation, except «Đăng nhập» in M-F00-01, which opens S-F00-01 (rules below); no new modals. Parent screen dimmed by `colour/overlay`. Buttons: Primary/Destructive right, Secondary left (Staff); stacked, primary on top (Reader) |
| Toast | short confirmation after success | e.g. "Đã đăng đánh giá.", "Đã gửi báo cáo." | Bottom centre, `colour/text` background, white text, disappears after 4 seconds; states: success and informational (not two identical default examples); never the only place an error is shown |
| Empty state | why the list is empty + next step | many screens | Icon + one sentence + optional Text link or Secondary button |
| Skeleton | grey blocks while loading | Loading state of every screen | `colour/skeleton`; same shape as the content it replaces |
| Label sheet | printable sheet of QR labels | M-F02-03-01 | A4 portrait decal sheet, 3 columns × 8 rows = 24 labels of 70×37 mm. Each label: QR code on the left; on the right the book title (max 2 lines, cut with "…"), the Shelf location line «Tầng `<n>` · Phòng `<code>` · Kệ `<code>`» and a small line «Quét để xem thông tin và đánh giá». **One label per book title**, not per copy, on the first print; all copies share the title's QR code, and a label for another copy is reprinted from the filter «Đã in nhãn» with **no Shelf location line** (D40). More than 24 books continue on further A4 pages (D41). The Shelf location line is the book's **primary shelf location returned by the sync** — the same location shown on S-F01-01 — and the S-F02-03 list is sorted by it (D13). The books on the sheet are recorded as label-printed **only when staff choose «Đã in xong»** (Secondary button next to the Primary button «In» and the Secondary button «Đóng»; D12, D17); «Đóng» or a failed print records nothing: the books stay in the S-F02-03 list with their ticks kept, so staff can print again straight away (FR-02-08; D12, D18). Sheet and label content: D4 |
| Multi-select chips | choose multiple reading interests (FR-03-05) | S-F03-02 | Each chip toggles independently; states: unselected, selected (fill + check icon), focus, disabled; do not use Segmented control for multi-select |
| Section title | heading for a group of content, including book sections | S-F01-01, S-F03-02, S-F03-06, S-F03-07, as needed | Heading text follows section 1; uses `font/size` section title; no action or focus state. Use this name instead of Section header |
| Text button | in-place text action (e.g. review Edit/Delete) | S-F02-01, S-F02-02, S-F02-04, S-F00-03 | Does not navigate; states: default, hover, focus, disabled; `.danger` variant uses `colour/error-red` with a clear text label for destructive actions |
| Status badge | displays a reading status, not an action | S-F03-02, S-F03-07 where specified by notes | Text labels "Đang đọc" / "Đã đọc xong"; icon + text where status relies on colour; passive display; no focus/disabled state |
| Progress bar & label | display reading progress | S-F03-02 | 0–100% with a visible numeric percentage; track and fill must be distinguishable without colour alone; passive display, not an editable slider |

Rules:

- **One Primary button** visible on a screen at a time, with no exception. In M-F02-03-01 «In» is the Primary button;
  «Đã in xong» and «Đóng» are Secondary buttons (D17).
- **A modal never navigates.** It only confirms or cancels one action. The 5 modals of [screen_list.md](screen_list.md) are the only modals.
  One exception: «Đăng nhập» in M-F00-01 opens S-F00-01 ([screen_list.md](screen_list.md), L8-01). After the code is accepted the reader
  returns to the starting screen and the pending action continues by itself; «Huỷ» on S-F00-01 / S-F00-02 returns to the
  starting screen with the pending action still waiting, and nothing on that screen is lost (D1).
- **Staff sign-out.** Every staff screen (S-F04-01, S-F02-03, S-F02-04) has «Đăng xuất» in the header; it ends the staff
  session and opens S-F00-03. The staff session does not end by time: staff stay signed in until they choose «Đăng xuất»
  (FR-04-21; D7).
- Every screen describes its states: default, loading, empty (if it has a list), error, success (handbook section 6).

## 4. Messages

Patterns. The screen owner writes each screen's own wording in the wireframe notes, following these patterns;
the reviewer (Chi) checks it in the consistency review.

| Situation | Pattern | Example (from our product) |
|---|---|---|
| Validation error | what is wrong + how to fix it | "Bạn chưa viết nội dung đánh giá. Hãy nhập ít nhất 1 ký tự." (FR-02-01, FR-02-11) |
| Validation error | what is wrong + how to fix it | "Hãy chọn ít nhất 1 sách bản giấy." (FR-02-17) |
| System error | what happened + what to do now | "Tìm kiếm bằng AI đang tạm ngưng. Bạn hãy dùng bộ lọc hình thức." (FR-03-17) |
| Empty state | why it is empty + next step | "Bạn chưa lưu sách nào. Bấm Lưu vào danh sách ở trang vị trí kệ sách." (FR-03-25) |
| No results | what was not found + what to try | "Không tìm thấy sách. Hãy chọn hình thức khác." (FR-03-23) |
| Success | what is done | "Đã đăng đánh giá." (FR-02-12) |
| Already done | what already exists | "Sách này đã có trong danh sách của bạn." (FR-03-24) |
| Information | fact + what it means | "Sách này chỉ có bản trực tuyến, không có vị trí trên kệ." (FR-01-06) |

Shared wording — use exactly as written:

| ID | Where | Text | Source |
|---|---|---|---|
| MSG-01 | M-F00-01, general | Title "Đăng nhập để tiếp tục?" · Body "Bạn cần đăng nhập bằng thẻ thư viện để làm việc này." · Buttons "Đăng nhập" (Primary), "Để sau" (Secondary) | FR-04-08 |
| MSG-02 | M-F00-01, chatbot | Body "Bạn cần đăng nhập bằng thẻ thư viện để trò chuyện với trợ lý tìm sách." | FR-03-18 |
| MSG-03 | M-F00-01, recommendations | Body "Gợi ý riêng cho bạn cần tài khoản thẻ thư viện. Hãy đăng nhập để xem." | FR-03-21 |
| MSG-04 | any screen, load failed | Banner error "Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại." + Secondary button "Thử lại" | FR-04-20 (new) |
| MSG-05 | Loading | No text; Skeleton only. If a wait has text: "Đang tải…" | handbook (Doherty) |
| MSG-06 | S-F01-01, S-F03-03 | "Chưa có vị trí kệ của sách này. Bạn hỏi quầy thông tin ở tầng trệt nhé." | FR-01-07; AD-UC-01 Q2 |
| MSG-07 | S-F01-02, opened from a book | "Bản đồ tạm thời không hiển thị được. Thông tin vị trí kệ vẫn ở phía trên." | FR-01-10 |
| MSG-08 | S-F01-02 | "Không tìm thấy phòng này trên bản đồ. Thông tin vị trí kệ vẫn ở phía trên." | FR-01-09 |
| MSG-09 | S-F00-02 | "Mã có hiệu lực trong 5 phút." | FR-04-04 |
| MSG-10 | S-F00-02, line above the code field | "Mã đã được gửi tới `<email>`." — the email in full, as registered, not masked; not shown when the code could not be sent (S-F00-02 Error-4) | FR-04-04; D2, D15, D31 |
| MSG-11 | S-F02-03, Empty state | "Tất cả sách bản giấy đã được in nhãn. Sách mới sẽ hiện ở đây sau lần đồng bộ danh mục tiếp theo." | FR-02-23; D15 |
| MSG-12 | S-F01-02, opened from the OPAC menu | "Bản đồ tạm thời không hiển thị được. Bạn thử lại sau nhé." | FR-01-10; D23 |
| MSG-13 | S-F03-02, Empty state (reading history) | "Chưa có lịch sử đọc nào. Sách bạn mượn hoặc đọc trực tuyến sẽ tự động xuất hiện tại đây." | FR-03-01; D24 |
| MSG-14 | S-F02-01, S-F02-02, hint line under the review field | "Đánh giá không được chứa từ ngữ xúc phạm, quảng cáo hoặc thông tin cá nhân." — the three criteria staff apply when they remove a reported review (UC-13) | FR-02-01, FR-02-10; D20 |

Where messages go:

| Message | Component |
|---|---|
| Error in one field | Inline error under the field |
| Error, warning or information about the whole screen | Banner at the top of the content |
| Short success after an action | Toast (and the refreshed list, FR-02-12) |
| Question before an action | Modal (only the 5 listed) |
| Empty list | Empty state in place of the list |

## 5. Accessibility minimums

- Text contrast at least 4.5:1; large text (24px, or 19px bold) at least 3:1 (WCAG 2.2, 1.4.3). All pairs in section 6 pass.
- Borders of inputs, room tiles and other controls at least 3:1 against their background (WCAG 2.2, 1.4.11).
- Never colour alone (WCAG 2.2, 1.4.1):
  - Format label: icon + word "Trực tuyến" / "Bản giấy".
  - Highlighted room on the map: fill + thick border + text label "Sách của bạn ở đây".
  - Errors: colour + error icon + text, never only a red border.
  - Selected segment: fill + check icon.
- Target size: at least 24×24 CSS px everywhere (WCAG 2.2, 2.5.8); on Reader screens at least 44×44 px (handbook section 5).
- Every input has a visible label above it; placeholder text never replaces a label.
- Visible focus ring (`colour/focus`, 2px, 2px offset) on every interactive element — staff use the keyboard.
- Text inputs on phones use 16px text so iPhone does not zoom.
- Smallest supported width: 360px for Reader screens (the design frame; D44), 1280px for staff screens (the design frame; D45) (section 6.1).

## 6. Design tokens

Every mockup uses only these values. Reader screens are drawn at 360px and exported at 3x (images 1080px wide);
staff screens (S-F00-03, S-F04-01, S-F02-03, S-F02-04, M-F02-03-01, M-F02-04-01) are drawn at 1280px and exported
at 1x (UI Q2, UI Q3). Wireframe fidelity is mid: token colours, real text, grey "Cover" blocks, no images (UI Q6).

Colours follow the palette of the current OPAC (UI Q4), read from its stylesheet `nlv.css` on 13/11/2026:
`--primary-color #8b0000`, `--background-color #fafafa`, `--secondary-color #edf0f2`, `--gray-color #4b5563`,
`--secondary-blue-color #1074c3`, `--bib-type-background #ffebee`, `--border-color #d9d9d9`. Only colour values are
reused; no logo, library name or image. Where an OPAC value fails WCAG for our use, a darker value is used and the
reason is written in the "From OPAC" column.

| Token | Value | From OPAC | Used for |
|---|---|---|---|
| colour/brand-red | #8B0000 | `--primary-color` | brand colour: Primary button fill, selected segment, selected room tile. Never used for errors |
| colour/on-primary | #FFFFFF | `--white-color` | text and icons on primary |
| colour/brand-red-soft | #FFEBEE | `--bib-type-background` | Format label background, hover of Secondary button |
| colour/link | #1074C3 | `--secondary-blue-color` | Text link on white or background only |
| colour/text | #1F2937 | — (OPAC uses #000; handbook asks for very dark grey) | titles, body text in bubbles, Toast background |
| colour/text-body | #374151 | — | body text, review text |
| colour/text-muted | #4B5563 | `--gray-color` | hints, dates, author, counter |
| colour/border | #7A8492 | — (OPAC #D9D9D9 is 1.4:1, fails 1.4.11) | input, Secondary button, room tile, checkbox edges |
| colour/border-light | #D9D9D9 | `--border-color` | card and divider lines (decoration only) |
| colour/background | #FAFAFA | `--background-color` | page background |
| colour/surface | #EDF0F2 | `--secondary-color` | Floor plan, chatbot Chat bubble, Skeleton |
| colour/card | #FFFFFF | `--white-color` | cards, inputs, modal panel |
| colour/skeleton | #EDF0F2 | `--secondary-color` | loading placeholders |
| colour/disabled | #C5CBD3 | — | disabled button fill |
| colour/error-red | #C62828 | — | errors and destructive actions: Inline error text, border and "!" icon, 2px border of a field in error, error Banner border, Destructive button and `.text-button.danger` (e.g. "Xoá đánh giá"). Never used as a solid fill |
| colour/error-red-bg | #FDECEA | — | background of Inline error and error Banner |
| colour/success-border | #2F7D46 | — | success Banner border and icon |
| colour/success-text | #14532D | — | success text |
| colour/success-bg | #E8F5EC | — | success Banner background |
| colour/warning-border | #B45309 | — | warning Banner border and icon |
| colour/warning-text | #7A3E06 | — | warning text |
| colour/warning-bg | #FDF3E3 | — | warning Banner background |
| colour/info-border | #1074C3 | `--secondary-blue-color` | info Banner border and icon |
| colour/info-text | #0B4F86 | — (#1074C3 on info-bg is 4.3:1, fails 1.4.3) | info text, links inside an info Banner |
| colour/info-bg | #E8F2FB | — | info Banner background, reader Chat bubble |
| colour/highlight | #FDE9A8 | — | fill of the room that holds the book |
| colour/highlight-border | #8A5A00 | — | 3px border of that room |
| colour/focus | #1074C3 | `--secondary-blue-color` | 2px focus ring (blue, so it shows on red buttons too) |
| colour/overlay | rgba(0, 0, 0, 0.5) | — | dimmed screen behind a modal; translucent hover treatment on Primary button when specified by [ui_tokens.css](screens/src/ui_tokens.css) |
| font/heading | Plus Jakarta Sans, fallback Inter, Arial, sans-serif | Google Fonts (D28) | screen titles, modal titles, section titles, Menu tile title |
| font/body | Inter, fallback Arial, sans-serif | — | all other text: body, labels, buttons, inputs, messages |
| font/size | title 20px (Reader) / 24px (Staff), section title 18px, body 16px, label and button 16px (Reader) / 14px (Staff), small 12px; book author 16px (Reader) / 14px (Staff) | |
| font/weight | heading 700; body regular 400, medium 500 (labels, buttons), semibold 600 | |
| font/line-height | body 1.5, titles 1.3 | |
| space/unit | 4px; all spacing is a multiple of 4. Screen padding 16px (Reader) / 32px (Staff); gap inside a group 8–16px; between groups 24px | |
| size/control | height 48px (Reader), 40px (Staff); icon 20px / 24px; Reader minimum target 44×44px | buttons, inputs, interactive targets |
| size/border | 1px default hairline, 2px focus and error, 3px highlighted room | strokes in components |
| space/scale | 4px unit; scale `space-1` through `space-12` means 4px through 48px in increments of 4px | CSS spacing variables; check against [ui_tokens.css](screens/src/ui_tokens.css) |
| radius | 8px for buttons, inputs, cards, banners, room tiles, modals; 999px for Format label | one radius level |
| frame/width | 360px (Reader, export 3x = 1080px); 1280px (Staff, export 1x); other widths: section 6.1 | every mockup |
| shadow/modal | 0 16px 24px -3px rgba(0, 0, 0, 0.1) | OPAC `--shadow-lg` | modal panel, Sign-in card |
| size/sign-in-card | max width 400px | — | Sign-in card (S-F00-03) |

Font notes: Plus Jakarta Sans for titles, Inter for all other text (UI Q5, changed by D28). Both are free on Google
Fonts and include the Vietnamese subset. Plus Jakarta Sans replaces SVN-Gilroy, the font of the current OPAC, because
SVN-Gilroy is not on Google Fonts and its licence is not free; Plus Jakarta Sans has a very similar geometric shape.
PNGs exported before 22/11/2026 still show Inter in the titles (SVN-Gilroy was never loaded); they are not re-exported
for the font only.

Colour notes (UI Q10): the brand colour is red, and red also means error. They are two separate
tokens, `colour/brand-red` (#8B0000, the current OPAC colour) and `colour/error-red` (#C62828), so changing one never
changes the other. They never look alike: the Primary button is always a SOLID brand-red fill with white text and no
icon; an error is never a solid fill — it is a light #FDECEA background with red border and text, always a "!" icon,
directly under the field, and the field gets a 2px red border.

Every mockup uses only these values.

Contrast, calculated with the WCAG 2.2 relative-luminance formula:

| Pair | Ratio | Needed |
|---|---|---|
| on-primary white on primary #8B0000 | 10.0:1 | 4.5:1 (1.4.3) |
| primary #8B0000 on background #FAFAFA | 9.6:1 | 4.5:1 (1.4.3) |
| primary #8B0000 on primary-soft #FFEBEE (Format label) | 8.8:1 | 4.5:1 (1.4.3) |
| text #1F2937 on background #FAFAFA | 14.1:1 | 4.5:1 (1.4.3) |
| text #1F2937 on surface #EDF0F2 | 12.8:1 | 4.5:1 (1.4.3) |
| text-body #374151 on white | 10.3:1 | 4.5:1 (1.4.3) |
| text-muted #4B5563 on white | 7.6:1 | 4.5:1 (1.4.3) |
| text-muted #4B5563 on background #FAFAFA | 7.2:1 | 4.5:1 (1.4.3) |
| text-muted #4B5563 on surface #EDF0F2 | 6.6:1 | 4.5:1 (1.4.3) |
| link #1074C3 on white | 4.9:1 | 4.5:1 (1.4.3) |
| link #1074C3 on background #FAFAFA | 4.7:1 | 4.5:1 (1.4.3) |
| ~~link #1074C3 on info-bg #E8F2FB~~ | 4.3:1 — **fails**, replaced by info-text | 4.5:1 (1.4.3) |
| info-text #0B4F86 on info-bg #E8F2FB | 7.5:1 | 4.5:1 (1.4.3) |
| error-red #C62828 on white | 5.6:1 | 4.5:1 (1.4.3) |
| error-red #C62828 on error-red-bg #FDECEA (Inline error) | 4.9:1 | 4.5:1 (1.4.3) |
| text #1F2937 on error-red-bg #FDECEA | 12.8:1 | 4.5:1 (1.4.3) |
| success-text #14532D on success-bg #E8F5EC | 8.1:1 | 4.5:1 (1.4.3) |
| warning-text #7A3E06 on warning-bg #FDF3E3 | 7.6:1 | 4.5:1 (1.4.3) |
| text #1F2937 on highlight #FDE9A8 | 12.2:1 | 4.5:1 (1.4.3) |
| white on text #1F2937 (Toast) | 14.7:1 | 4.5:1 (1.4.3) |
| ~~OPAC border #D9D9D9 on white~~ | 1.4:1 — **fails**, replaced by border | 3:1 (1.4.11) |
| border #7A8492 on white (input, room tile edge) | 3.8:1 | 3:1 (1.4.11) |
| border #7A8492 on background #FAFAFA | 3.6:1 | 3:1 (1.4.11) |
| error-red #C62828 on white (2px field border) | 5.6:1 | 3:1 (1.4.11) |
| error-red #C62828 on background #FAFAFA | 5.4:1 | 3:1 (1.4.11) |
| success-border #2F7D46 on white | 5.1:1 | 3:1 (1.4.11) |
| warning-border #B45309 on white | 5.0:1 | 3:1 (1.4.11) |
| info-border #1074C3 on white | 4.9:1 | 3:1 (1.4.11) |
| highlight-border #8A5A00 on white | 5.9:1 | 3:1 (1.4.11) |
| focus #1074C3 on white | 4.9:1 | 3:1 (1.4.11) |

Two OPAC values failed and were replaced (struck through above). `colour/border-light` #D9D9D9 is kept only for
dividers, which are decoration, so 1.4.11 does not apply. The disabled button (white on #C5CBD3) is exempt: WCAG
1.4.3 does not apply to inactive components. The blue numbered circles on `*-numbered.png` images are notes for
readers, not part of the product, so they are not a token.

### 6.1 Responsive layout

Rules from D8, D44 and D45 (UI Q7). Mockups stay at the frame widths above; each screen spec §8 says what collapses or
stacks under these rules.

| Actor | Designed at | Supported range | Rule |
|---|---|---|---|
| Reader | 360px | from 360px | No horizontal scroll at 360px; narrower widths are not supported (D44). On wider screens the content stays **one column, max width 640px, centred** |
| Staff | 1280px | from 1280px | Narrower widths are not supported, so layouts never shrink or stack (D45). Staff screens are **not supported on tablets or phones** |

## 7. Change log

| Version | Date | Change |
|---|---|---|
| v0.1 | 13/11/2026 | First release: sections 1–6 |
| v0.2 | 13/11/2026 | Colours from the current OPAC palette; SVN-Gilroy for titles, Inter for text; Destructive button made outline; sections 1–5 aligned to the template |
| v0.3 | 13/11/2026 | Vietnamese interface: standard labels and screen titles, MSG-01–09, Vietnamese number format; library card number of 7 digits |
| v0.4 | 13/11/2026 | Card number may start with 0; reviewer chooses name or anonymous («Đăng ẩn danh») |
| v0.5 | 13/11/2026 | Reviewer name = full name as registered on the library card |
| v0.6 | 14/11/2026 | OTP attempts left; FR-02-22, FR-04-19, FR-04-20 added (MSG-04) |
| v0.7 | 14/11/2026 | Tokens `colour/brand-red` and `colour/error-red` split; Inline error style; Primary button without icon; OTP of 6 digits; MSG-06 wording |
| v0.8 | 21/11/2026 | 19/11 review applied: missing components and Vietnamese labels, modal naming, token and size notes |
| v0.9 | 22/11/2026 | D1–D16 applied: section 6.1 Responsive layout; Screen header exceptions and staff «Đăng xuất»; Pagination, Trend tag, Selection counter; Label sheet and «Đã in xong»; MSG-10, MSG-11 |
| v0.9 | 22/11/2026 | D17–D18 applied: «Đã in xong» is a Secondary button and the one-Primary rule has no exception; ticks kept after «Đóng». Modal titles filled from the modal notes. Decisions, consistency review and new-FR notes moved to [decision_index.md](../project_brief/decision_index.md#ui-conventions) |
| v0.10 | 23/11/2026 | D40–D41 applied: Segmented control on S-F02-03, «In lại nhãn», reprinted label without Shelf location line, label sheet of several A4 pages |
| v0.11 | 23/11/2026 | D44 applied: Reader screens supported from 360px (was 320px) |
| v0.12 | 23/11/2026 | D45 applied: Staff screens supported from 1280px (was 1024px) |
| v0.13 | 23/11/2026 | D46: links inside an error Banner use `colour/error-red`; the S-F02-02 link is «Xem sách trên OPAC» everywhere |
| v0.9 | 22/11/2026 | D21, D23, D24, D27 applied: Book row also on S-F02-01, S-F02-02 (no Format label); MSG-07 limited to the map opened from a book; MSG-12 (map unavailable, opened from the OPAC menu); MSG-13 (empty reading history); Shelf location lists the primary location first |
| v0.9 | 22/11/2026 | D28: title font Plus Jakarta Sans (Google Fonts) replaces SVN-Gilroy. D29: new component Sign-in card — the staff sign-in form is centred in the frame; S-F00-03 redrawn in HTML ([s_f00_03.html](screens/src/s_f00_03.html)) and re-exported; token `size/sign-in-card` |
| v0.9 | 22/11/2026 | D20 applied: no review-guideline link; MSG-14 hint line under the review field (Text area with counter) on S-F02-01, S-F02-02 |
| v0.9 | 23/11/2026 | D31: MSG-10 is not shown in the send-failure state of S-F00-02 (Error-4) |
