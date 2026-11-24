# Screen List: Group H Library Core System

Group H Library Core System is an add-on to the library's existing OPAC, used by the Reader and by On-site Staff. Existing OPAC pages (catalogue and search results, Book Detail, main menu, personal area, online book page) are entry points and exits, not screens of this product; the product only adds new links to them. Version v1.1 · 2026-11-23 (v1.0 2026-11-08).

Screen ID pattern: `S-<feature>-<nn>`, for example `S-F01-02` is the second screen of feature F-01.
Screens shared by every feature (sign in) use `S-F00-<nn>`.

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F00-01 | Sign in: library card number | Reader | F-00 | A reader without a session wants a signed-in action, or chooses to sign in, and enters the library card number. | "Sign in" in modal M-F00-01 on any reader screen; "Sign in" link added to the existing OPAC main menu (D34) | UC-11 · FR-04-01, FR-04-08 | Must | [screen-spec-s-f00-01.md](screens/specs/screen-spec-s-f00-01.md) |
| S-F00-02 | Verify email OTP | Reader | F-00 | The card number was found; the reader enters the code sent by email or asks for a new one. After the code is accepted the reader goes back to the screen where sign-in started and the pending action continues by itself; «Huỷ» also goes back there, with the action still waiting and nothing lost (D1). | S-F00-01 [card number found] | UC-11 · FR-04-01, FR-04-04, FR-04-16, FR-04-17, FR-04-19 | Must | [screen-spec-s-f00-02.md](screens/specs/screen-spec-s-f00-02.md) |
| S-F00-03 | Staff sign in | On-site Staff | F-00 | Staff open the staff page without a valid staff session and sign in with their internal library account; after sign-in the staff page S-F04-01 opens. A wrong account or an account without the staff role is rejected and staff may try again. Staff who choose «Đăng xuất» land here. | The staff page address, when staff have no valid staff session; «Đăng xuất» on S-F04-01, S-F02-03, S-F02-04 | UC-10, UC-13 · FR-04-07, FR-04-08, FR-04-18, FR-04-21 | Must | [screen-spec-s-f00-03.md](screens/specs/screen-spec-s-f00-03.md) |
| S-F01-01 | Shelf location (with Save to my list) | Reader | F-01 | The reader asks where a book is: floor, room and shelf code, one line per physical copy. For a physical book the reader can also save it to the personal list or open its room on the map. | "Shelf location" on the existing OPAC Book Detail page; back from S-F01-02; back from S-F00-02 after sign-in (Save) | UC-01 · FR-01-01, FR-01-06, FR-01-07, FR-01-03; UC-12 · FR-03-06, FR-03-24 | Must | [screen-spec-s-f01-01.md](screens/specs/screen-spec-s-f01-01.md) |
| S-F01-02 | Interactive digital library map | Reader | F-01 | The reader browses floors and reading rooms and selects a room, or sees the book's room highlighted with the shelf details kept visible. | "Library map" link on the existing OPAC main menu; "View on map" on S-F01-01 | UC-01, UC-02 · FR-01-02, FR-01-03, FR-01-09, FR-01-10, FR-01-11 | Must | [screen-spec-s-f01-02.md](screens/specs/screen-spec-s-f01-02.md) |
| S-F02-01 | Book reviews | Reader | F-02 | The reader reads a book's reviews page by page, writes, edits or deletes own review, or reports a review. | "Reviews" on the existing OPAC Book Detail page; back from S-F00-02 after sign-in | UC-05 · FR-02-02, FR-02-13, FR-02-15; UC-04 · FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12, FR-02-22; UC-14 · FR-02-09, FR-02-21, FR-02-24 | Must | [screen-spec-s-f02-01.md](screens/specs/screen-spec-s-f02-01.md) |
| S-F02-02 | Book information and reviews (QR landing page) | Reader | F-02 | The reader scanned the QR label of a physical book and sees its information and reviews on a phone, with the same write, edit and delete panel as S-F02-01, and reviews 10 per page with "Load more reviews". A "View this book on the OPAC" link opens the book's existing OPAC Book Detail page; it is the only way out: there is no Back, because the page opens only by scanning the QR label (D5). When the QR code is linked to no book, the error state offers «Về OPAC» to the OPAC main menu instead (D37). | Phone camera opens the QR link (the only entry); back from S-F00-02 after sign-in (the same page) | UC-06 · FR-02-05, FR-02-16; UC-05 rule · FR-02-02, FR-02-15; UC-04 (called) · FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12, FR-02-22; UC-05 rule · FR-02-13 | Must | [screen-spec-s-f02-02.md](screens/specs/screen-spec-s-f02-02.md) |
| S-F02-03 | QR code label printing | On-site Staff | F-02 | Staff see the physical books of the synced catalogue that have never had a QR label printed (20 per page, ordered floor → room → shelf of each book's primary shelf location returned by the sync, the same as on S-F01-01), tick books on any page (ticks kept, "Đã chọn <n> sách"), choose Print labels, preview the label sheet (A4 portrait decal, 3 × 8 labels of 70×37 mm, one label per book title) and print it; only when staff then choose "Đã in xong" are the books on the sheet recorded as label-printed, the print audit entry written (D32) and the books removed from the list — after "Đóng" or a failed print they stay listed with their ticks kept, so staff can print again straight away (D3, D4, D12, D13, D18). A sheet continues on further A4 pages when more than 24 books are selected (D41). The filter «Đã in nhãn» lists labelled books so staff can reprint the shared QR code for other copies, with no shelf location (D40). | "Print QR labels" on S-F04-01 | UC-10 · FR-02-23, FR-02-08, FR-02-17, FR-02-18, FR-02-25, FR-04-21 | Must | [screen-spec-s-f02-03.md](screens/specs/screen-spec-s-f02-03.md) |
| S-F02-04 | Reported reviews | On-site Staff | F-02 | Staff go through reported reviews one by one: read the review, then remove it or dismiss the report. | "Reported reviews" on S-F04-01 | UC-13 · FR-02-14, FR-02-10, FR-02-19, FR-02-20, FR-04-21 | Could | [screen-spec-s-f02-04.md](screens/specs/screen-spec-s-f02-04.md) |
| S-F03-01 | Access-format filter and results | Reader | F-03 | The reader chooses Online, Physical or Both and sees matching books from the whole synced catalogue with their format labels (a book with both formats shows both labels), 20 per page with page buttons; choosing another format returns to page 1 (D9, D14); an online book opens on the current OPAC; Back returns to the OPAC results or, when opened from S-F03-06, to the chatbot (D35). | "Filter by access format" link on the existing OPAC catalogue / search results; "use the format filter" link in S-F03-06 when AI search is unavailable | UC-03 · FR-03-12, FR-03-23, FR-03-13 | Should | [screen-spec-s-f03-01.md](screens/specs/screen-spec-s-f03-01.md) |
| S-F03-02 | Reading history and preferences | Reader | F-03 | A signed-in reader checks the reading history with status, updates a book's status and progress, or updates reading preferences. | "Reading history" link on the existing OPAC personal area; "Sở thích" (any time) or the "Set your preferences" prompt on S-F03-07; back from S-F00-02 after sign-in | UC-07 · FR-03-01, FR-03-04, FR-03-05, FR-03-22 | Should | [screen-spec-s-f03-02.md](screens/specs/screen-spec-s-f03-02.md) |
| S-F03-03 | Saved books list | Reader | F-03 | A signed-in reader sees the saved physical books with the shelf location of each, and removes books from the list. | "Saved books" link on the existing OPAC personal area; back from S-F00-02 after sign-in | UC-12 · FR-03-07, FR-03-08, FR-03-25, FR-01-07 | Should | [screen-spec-s-f03-03.md](screens/specs/screen-spec-s-f03-03.md) |
| S-F03-06 | AI chatbot book search | Reader | F-03 | A signed-in reader asks the chatbot for books in their own words and gets replies with book result cards. | "Ask the library chatbot" link on the existing OPAC main menu | UC-08 · FR-03-09, FR-03-16, FR-03-17, FR-03-18 | Could | [screen-spec-s-f03-06.md](screens/specs/screen-spec-s-f03-06.md) |
| S-F03-07 | Book recommendations | Reader | F-03 | A signed-in reader sees a list of recommended books: personalised, topped up with trending books, or popular books when there is no reader data yet. Books added from trending titles carry the Trend tag "Xu hướng"; "Sở thích" in the header is always available and opens S-F03-02 (D10a, D10b). | "Recommended for you" link on the existing OPAC main menu | UC-09 · FR-03-11, FR-03-19, FR-03-20, FR-03-21 | Could | [screen-spec-s-f03-07.md](screens/specs/screen-spec-s-f03-07.md) |
| S-F04-01 | Staff page | On-site Staff | F-04 | The minimal staff page: staff choose a task, "Print QR labels" or "Reported reviews". "Đăng xuất" in the header ends the staff session and opens S-F00-03; the session has no time-out (D7). | Staff page address on library staff computers (with a valid staff session); S-F00-03 after staff sign-in; back from S-F02-03 and S-F02-04 | UC-10, UC-13 · FR-04-07, FR-04-08, FR-04-21 | Must | [screen-spec-s-f04-01.md](screens/specs/screen-spec-s-f04-01.md) |

Notes on the table:

- Priority is the highest W4 priority among the FRs of the screen's own use cases. Rules borrowed from another use case (FR-04-08 sign-in check, FR-01-07 on S-F03-03) do not raise it (L8-14).
- FR-04-08 (sign-in and staff access control) applies to every screen that needs a session. It is cited only on the sign-in screens, the staff page and the reader sign-in modal. The staff page opens only with a staff session, so staff sign in before any staff task (AD-UC-10, AD-UC-13).
- FR-04-20 (handle a network or loading error, message MSG-04 in [ui-conventions.md](ui-conventions.md)) applies to every screen that loads or saves data: S-F00-01, S-F00-02, S-F00-03, S-F01-01, S-F01-02, S-F02-01, S-F02-02, S-F02-03, S-F02-04, S-F03-01, S-F03-02, S-F03-03, S-F03-06, S-F03-07, S-F04-01. Like FR-04-08 it is a borrowed rule: it is listed in each Screen Spec but not repeated in the table above, and it does not raise a screen's priority.
- FR-02-22 (post a review anonymously), FR-04-19 (OTP attempts left) and FR-04-20 come from [ui-conventions.md](ui-conventions.md); they are rows 132–137 of W1 (UI Q13).
- FR-02-23 (list physical books awaiting a QR label) and FR-04-21 (sign out of the staff page; no staff time-out) are new FRs (D3, D7), together with a change to FR-02-08 (record the labels as printed when staff confirm "Đã in xong", D12; FR-02-23 orders by the primary shelf location, D13). FR-04-21 (Should) does not raise the priority of S-F00-03, S-F02-03, S-F02-04 or S-F04-01.
- FR-02-24 (reject a report on the reader's own review, D39) and FR-02-25 (reprint QR labels, D40) are new FRs. FR-02-25 (Should) does not raise the priority of S-F02-03. FR-02-07 and FR-02-08 were changed by D40 and D41.
- Could parts inside Must or Should screens, which disappear without removing the screen if they are cut: "View on map" on S-F01-01 (FR-01-03); Edit and Delete own review on S-F02-01 and S-F02-02 (FR-02-03, FR-02-04); Report on S-F02-01 (FR-02-09, FR-02-21, FR-02-24); preferences part of S-F03-02 (FR-03-05); Remove on S-F03-03 (FR-03-08); "Reported reviews" on S-F04-01 (UC-13).

## Modals and overlays

Modal IDs: `M-F00-<nn>` when the modal is shared by several screens, `M-<screen>-<nn>` otherwise. A modal is never a row of the table above.

| Modal | Opened from screen | Purpose |
|---|---|---|
| M-F00-01 Sign in to continue? | S-F01-01 (Save), S-F02-01, S-F02-02, S-F03-02, S-F03-03, S-F03-06, S-F03-07 | A reader without a valid session asked for a signed-in action. "Sign in" opens S-F00-01 and, after the OTP is accepted, returns to the screen that asked, where the pending action continues by itself (L8-01, D1); "Not now" closes the modal and the request ends. This is the only modal that opens a screen ([ui-conventions.md](ui-conventions.md) section 3). Covers "Sign in now?" (d1) in AD-UC-04, 07, 08, 09, 12, 14 (FR-04-08; wording for the chatbot from FR-03-18, for recommendations from FR-03-21). |
| M-F02-01-01 Delete your review? | S-F02-01, S-F02-02 | Reader confirms or cancels deleting own review (AD-UC-04 d6, r5; AD-UC-06 c3; FR-02-04). |
| M-F02-01-02 Report this review? | S-F02-01 | Reader submits the report on the selected review; no reason field (AD-UC-14 r2; FR-02-09). |
| M-F02-03-01 QR label sheet preview | S-F02-03 | Staff see the printable QR label sheet for the selected books (A4 portrait decal, 3 × 8 = 24 labels of 70×37 mm per page, further A4 pages when more than 24 books are selected; one label per book title; shelf location = the book's primary shelf location from the sync; D4, D13, D41). On a reprint the labels carry the existing QR code and no shelf location, and «Đã in xong» writes only the audit entry (D40) and press Print (Primary), which opens the browser's print dialog (AD-UC-10 a4, a5; FR-02-08). "Đã in xong" (Secondary) records the books on the sheet as label-printed and writes the print audit entry (D32); "Đóng" (Secondary) records nothing: the books stay in the S-F02-03 list with their ticks kept (AD-UC-10 d9, a8, a9; D12, D17, D18). |
| M-F02-04-01 Remove this review? | S-F02-04 | Staff confirm or cancel removing a reported review from public display (AD-UC-13 d4; FR-02-10). |

## What is deliberately not a screen

Messages the system shows (errors, empty lists, no results, confirmations, denied requests) are STATES of the screen the actor is on. They are written in that screen's spec, not here.

| Candidate | Why it is not a screen |
|---|---|
| "Card number not found" (one general rejection message) | Error state of S-F00-01 (FR-04-01; AD-UC-11 s2; AD-UC-11 Q4) |
| "Code could not be sent, request a new OTP" | Error state of S-F00-02 (FR-04-16; AD-UC-11 s5) |
| "Incorrect code, enter it again" | Error state of S-F00-02 (FR-04-17; AD-UC-11 s9) |
| "5 incorrect attempts, code no longer valid" | Error state of S-F00-02 (FR-04-17; AD-UC-11 s10) |
| "Code expired or already used" | Error state of S-F00-02 (FR-04-01; AD-UC-11 s11) |
| Number of OTP attempts left, shown with "Incorrect code" | Part of the error state of S-F00-02 (FR-04-19) |
| "Page could not load, check the connection and try again" (MSG-04) | Error state of every screen that loads or saves data; data already shown is kept and the user can try again (FR-04-20) |
| Signed in successfully | Not a page: the reader goes back to the screen where sign-in started and the pending action continues (FR-04-01; AD-UC-11 s7; D1) |
| Staff signed out | Not a page: the staff sign-in S-F00-03 opens (FR-04-21; AD-UC-10 s14, AD-UC-13 s11) |
| Wrong staff account or no staff role | Error state of S-F00-03 (FR-04-18; AD-UC-10 s9, AD-UC-13 s9); staff may try again (d1) |
| Request denied because there is no session (reader) | Shown as modal M-F00-01 on the screen where the reader asked (FR-04-08, FR-03-18, FR-03-21; s1 in AD-UC-04, 07, 08, 09, 12, 14) |
| Request denied because there is no staff session | Not a message: the staff sign-in S-F00-03 opens instead of the staff page (FR-04-08; AD-UC-10 s1, AD-UC-13 s1) |
| "Available electronically, no shelf location" | Information state of S-F01-01 (FR-01-06; AD-UC-01 s2) |
| "Shelf location unavailable, ask at the ground-floor information desk" | Error state of S-F01-01 (FR-01-07; AD-UC-01 s3; AD-UC-01 Q2) |
| "Book saved" | Success state of S-F01-01 (FR-03-06; AD-UC-12 s3) |
| "Book already saved" | Message state of S-F01-01 (FR-03-24; AD-UC-12 s2) |
| "Map unavailable" (shelf details kept), including for another floor | Error state of S-F01-02 (FR-01-10; AD-UC-01 s6, AD-UC-02 s2, s7) |
| "Room cannot be identified on the map" (shelf details kept) | Error state of S-F01-02 (FR-01-09; AD-UC-01 s7, AD-UC-02 s4) |
| Book's room highlighted / selected room with name, code and floor | Content of S-F01-02 (FR-01-03, FR-01-11; AD-UC-01 s8, AD-UC-02 s3, s8) |
| "No reviews to show" (book not found or no reviews) | Empty state of S-F02-01 (FR-02-15; AD-UC-05 s4) |
| Review text rejected, or not the reader's own review | Error state of S-F02-01 / S-F02-02 (FR-02-11; AD-UC-04 s7) |
| Review saved, replaced or removed, with the refreshed list | Success state of S-F02-01 / S-F02-02 (FR-02-12; AD-UC-04 s8) |
| Reviewer shown as the card full name or "Bạn đọc ẩn danh" | Content rule of S-F02-01 / S-F02-02 (FR-02-22) |
| "Review already reported" | Message state of S-F02-01 (FR-02-21; AD-UC-14 s2) |
| "Report sent" | Confirmation state of S-F02-01 (FR-02-09; AD-UC-14 s4) |
| "You cannot report your own review" | Message state of S-F02-01 (FR-02-24; AD-UC-14 s5; D39) |
| "Book cannot be found" (QR code linked to no book) | Error state of S-F02-02 (FR-02-16; AD-UC-06 s2) |
| "Select at least one physical book" | Validation state of S-F02-03 (FR-02-17; AD-UC-10 s2) |
| "Books left out: no QR code" and "No label sheet produced" | States of S-F02-03 (FR-02-18; AD-UC-10 s3, d4 [No]) |
| "Every physical book already has a printed label" (MSG-11) | Empty state of S-F02-03 (FR-02-23; AD-UC-10 s16; D15) |
| "No book has a printed label yet" | Empty state of the «Đã in nhãn» filter on S-F02-03 (FR-02-25; AD-UC-10 s18; D40) |
| "No reported reviews waiting" | Empty state of S-F02-04 (FR-02-19; AD-UC-13 s3) |
| Review removed / report dismissed, list refreshed | Success states of S-F02-04 (FR-02-10, FR-02-20; AD-UC-13 s5, s7) |
| "No books found, choose another format" | Empty state of S-F03-01 (FR-03-23; AD-UC-03 s3) |
| Status, progress or preference update rejected (saved data kept) | Error state of S-F03-02 (FR-03-22; AD-UC-07 s10) |
| Updated history or preferences shown | Success state of S-F03-02 (FR-03-01, FR-03-05; AD-UC-07 s6, s9) |
| "No books saved yet" | Empty state of S-F03-03 (FR-03-25; AD-UC-12 s5) |
| "Shelf location unavailable, ask library staff" for one saved book | State of that row of S-F03-03 (FR-01-07; AD-UC-12 s6) |
| Saved book removed, list refreshed | Success state of S-F03-03 (FR-03-08; AD-UC-12 s8) |
| Chatbot "no results, try other terms or subjects" | Reply state of S-F03-06 (FR-03-16; AD-UC-08 s7) |
| "AI search temporarily unavailable, use the format filter" | Error state of S-F03-06 with a link to S-F03-01 (FR-03-17; AD-UC-08 s4) |
| Popular books with "Set your reading preferences" prompt | State of S-F03-07 with a link to S-F03-02 (FR-03-19; AD-UC-09 s3) |
| Trending books added to a short list | Content rule of S-F03-07 (FR-03-20; AD-UC-09 s4) |
| Existing OPAC catalogue / search results, Book Detail, main menu, personal area | Existing OPAC pages outside the product: entry points only. The product adds links to them (S-F01-01, S-F01-02, S-F02-01, S-F03-01, S-F03-02, S-F03-03, S-F03-06, S-F03-07, S-F00-01) |
| Online book page and PDF download | Existing current-OPAC page: an exit from S-F03-01 (AD-UC-03 r3; AD-UC-03 Q1) |
| Phone camera and the browser print dialog | Belong to the phone and the browser, not to the product (AD-UC-06 r1, AD-UC-10 a5) |
| Generate QR codes after the daily catalogue sync | Time-triggered, no user interface (FR-02-07; AD-UC-10 t1, s6, s7) |
| Record that a book's QR label was printed | Background step after staff choose "Đã in xong" in M-F02-03-01 (not when the sheet is produced), no user interface of its own; the book then leaves the S-F02-03 list (FR-02-08; AD-UC-10 s13; D12) |
| Count QR scans | Background step when the QR page opens, no user interface (FR-02-06; AD-UC-06 s3) |
| History entries from synced loans | Time-triggered after the daily loan sync, no user interface (FR-03-03, FR-04-10; AD-UC-07 t1, s11, s12) |
| Anonymous online-book read log and history entry when an online book is opened | Background steps when the reader opens an online book from S-F03-01 (FR-03-13, FR-03-02; AD-UC-03 s4, s5, AD-UC-07 e1, s13) |
| Saving chatbot messages and replies | Background, no user interface (FR-03-10; AD-UC-08 s2, s5) |
| AI search and recommendation scoring | Background inside the system, no user interface (FR-03-09, FR-03-11; AD-UC-08 a1, AD-UC-09 a1) |
| Generating and emailing the OTP, invalidating an old OTP | Background, no user interface (FR-04-04; AD-UC-11 s3, s4, s12) |
| Audit entries for reader and staff sign-in, label printing and review removal | Background, no user interface (FR-04-12; D30; AD-UC-11 s8, AD-UC-10 s5 and s15, AD-UC-13 s6 and s12) |
| UC-15 Sync data from the library internal system | Time-triggered, no user interface (FR-04-09, FR-04-10, FR-04-11, FR-01-05; AD-UC-15; D48) |
| Digital floor plan preparation, deployment, automated tests | Work of the project team, no screen (FR-01-04, FR-04-13, FR-04-14) |
| S-F03-04, S-F03-05 | Retired IDs from an old draft (Saved books list, Advanced filter panel). Never reused |
| M-F03-06-01, M-F03-07-01, M-F00-Err, S-F00-01S, S-F00-04, M-F00-02 | Old draft IDs, replaced by M-F00-01, an error state of S-F00-03, S-F00-03 and S-F04-01. M-F00-02 "Staff sign-in required" is dropped: staff sign in before the staff page opens (L8-02) |
| Floating chatbot widget, "Reader Dashboard" | In no FR or activity diagram; entry points are plain links on OPAC pages |
| Online book viewer and PDF download on this platform | Won't (W0 Table 3; FR-03-15) |
| Access formats shown on the book detail page | Won't (W0 Table 3; FR-03-14) |
| Online reader account registration, Google sign-in, linking an online account to a library card | Won't (W0 Table 3; FR-04-02, FR-04-03, FR-04-05, FR-04-06) |
| Staff screen to edit floor plans and rooms | Won't (W0 Table 3) |
| Full librarian / admin workspace | Won't (W0 Table 3); staff have only the minimal staff page S-F04-01 |
| Keyword search | Won't (W0 Table 3); already on the current OPAC |
| Borrowing, returning and renewing loans; editing shelf codes and layout | Won't (W0 Table 3); stays in the library's internal system |
| Reviews report or dashboard for library staff | Won't (W0 Table 3) |
| Error tracking, health check and alerts dashboard | Won't (W0 Table 3; FR-04-15) |
| Like / dislike rating, list of books in a room, copy availability, collection status filter | Won't (W0 Table 3); not rebuilt |

## Activity diagram actions mapped to screens

Every node in the Reader and On-site Staff lanes of AD-UC-01 to AD-UC-14: actions, calls to other use cases and actor decisions. Merge nodes (`m*`), start and final nodes are not actions and are left out. The Library Internal System lane in AD-UC-11 (i1) is an outside system and has no screen.

| AD | Node | Actor action | Screen / modal |
|---|---|---|---|
| AD-UC-01 | r1 | Open a book's detail page and request its shelf location | Entry: existing OPAC Book Detail → S-F01-01 |
| AD-UC-01 | d3 | What does the reader do next? | S-F01-01 |
| AD-UC-01 | r2 | Request the library map for the book's room | S-F01-01 → S-F01-02 |
| AD-UC-01 | c1 | Save the book to my list (UC-12) | S-F01-01 ("Save to my list") |
| AD-UC-02 | r1 | Request the digital library map | S-F01-02 (from the OPAC main menu link or S-F01-01) |
| AD-UC-02 | d4 | What does the reader do next? | S-F01-02 |
| AD-UC-02 | r2 | Request to view another floor | S-F01-02 |
| AD-UC-02 | r3 | Select a reading room on the map | S-F01-02 |
| AD-UC-03 | r1 | Open the access-format filter | S-F03-01 (from the OPAC catalogue / search results link) |
| AD-UC-03 | r2 | Choose an access format: Online, Physical or Both | S-F03-01 |
| AD-UC-03 | d2 | What does the reader do next? | S-F03-01 |
| AD-UC-03 | r4 | Open another page of the results | S-F03-01 (Pagination) |
| AD-UC-03 | r3 | Open an online book from the results | S-F03-01 → exit: online book on the current OPAC |
| AD-UC-03 | c1 | View book shelf location (UC-01) | S-F03-01 → existing OPAC Book Detail → S-F01-01 |
| AD-UC-04 | r1 | Request a review action on a book | S-F02-01 (or S-F02-02 when called from UC-06) |
| AD-UC-04 | d1 | Sign in now? | M-F00-01 |
| AD-UC-04 | c1 | Sign in (UC-11) | S-F00-01 → S-F00-02 → back to S-F02-01 / S-F02-02 |
| AD-UC-04 | d2 | Which action? | S-F02-01 / S-F02-02 |
| AD-UC-04 | r6 | Choose to post under own name or anonymously | S-F02-01 / S-F02-02 (Checkbox «Đăng ẩn danh») |
| AD-UC-04 | r7 | Choose to show own name or post anonymously | S-F02-01 / S-F02-02 (Checkbox «Đăng ẩn danh») |
| AD-UC-04 | r2 | Submit a new review text | S-F02-01 / S-F02-02 (review form) |
| AD-UC-04 | r3 | Submit an edited text of own review | S-F02-01 / S-F02-02 |
| AD-UC-04 | r4 | Choose own review to delete | S-F02-01 / S-F02-02 |
| AD-UC-04 | d6 | Confirm the deletion? | M-F02-01-01 |
| AD-UC-04 | r5 | Cancel the deletion | M-F02-01-01 |
| AD-UC-05 | r1 | Ask to see the reviews of a book | Entry: existing OPAC Book Detail "Reviews" → S-F02-01 |
| AD-UC-05 | d4 | What does the reader do next? | S-F02-01 |
| AD-UC-05 | r2 | Ask for the next page of reviews | S-F02-01 |
| AD-UC-05 | c1 | Report a review (UC-14) | S-F02-01 |
| AD-UC-05 | c2 | Write a review (UC-04) | S-F02-01 (review panel) |
| AD-UC-05 | c3 | Edit own review (UC-04) | S-F02-01 |
| AD-UC-05 | c4 | Delete own review (UC-04) | S-F02-01 → M-F02-01-01 |
| AD-UC-06 | r1 | Scan the QR code on a physical book | Entry: phone camera → S-F02-02 |
| AD-UC-06 | d2 | What does the reader do next? | S-F02-02 |
| AD-UC-06 | r2 | Ask for the next page of reviews | S-F02-02 ("Xem thêm đánh giá") |
| AD-UC-06 | c1 | Write a review (UC-04) | S-F02-02 (review form) |
| AD-UC-06 | c2 | Edit own review (UC-04) | S-F02-02 |
| AD-UC-06 | c3 | Delete own review (UC-04) | S-F02-02 → M-F02-01-01 |
| AD-UC-07 | r1 | Open reading history and preferences | S-F03-02 (from the OPAC personal area link, or «Sở thích» on S-F03-07) |
| AD-UC-07 | d1 | Sign in now? | M-F00-01 |
| AD-UC-07 | c1 | Sign in (UC-11) | S-F00-01 → S-F00-02 → back to S-F03-02 |
| AD-UC-07 | d2 | What does the reader do? | S-F03-02 |
| AD-UC-07 | r2 | Submit the reading status and progress of a book | S-F03-02 |
| AD-UC-07 | r3 | Submit updated reading preferences | S-F03-02 |
| AD-UC-08 | r1 | Send an inquiry message to the chatbot | S-F03-06 |
| AD-UC-08 | d1 | Sign in now? | M-F00-01 |
| AD-UC-08 | c1 | Sign in (UC-11) | S-F00-01 → S-F00-02 → back to S-F03-06 |
| AD-UC-08 | d4 | What does the reader do next? | S-F03-06 |
| AD-UC-08 | c2 | View book shelf location (UC-01) | S-F03-06 → existing OPAC Book Detail → S-F01-01 |
| AD-UC-08 | c3 | Filter books by access format (UC-03) | S-F03-06 → S-F03-01 |
| AD-UC-08 | r2 | Open an online book from a result card on the OPAC | S-F03-06 → existing OPAC Book Detail (exit) |
| AD-UC-09 | r1 | Open the recommendations section | S-F03-07 (from the OPAC main menu link) |
| AD-UC-09 | d1 | Sign in now? | M-F00-01 |
| AD-UC-09 | c1 | Sign in (UC-11) | S-F00-01 → S-F00-02 → back to S-F03-07 |
| AD-UC-09 | r2 | View the recommended books | S-F03-07 |
| AD-UC-09 | d4 | What does the reader do next? | S-F03-07 |
| AD-UC-09 | c2 | View book shelf location (UC-01) | S-F03-07 → existing OPAC Book Detail → S-F01-01 |
| AD-UC-09 | c3 | Update reading preferences (UC-07) | S-F03-07 → S-F03-02 → back to S-F03-07 |
| AD-UC-09 | r3 | Open a recommended online book on the OPAC | S-F03-07 → existing OPAC Book Detail (exit) |
| AD-UC-10 | a0 | Open the staff page | S-F04-01 (signed in) or S-F00-03 (no staff session) |
| AD-UC-10 | a3 | Sign in with the internal library account | S-F00-03 → S-F04-01 |
| AD-UC-10 | d1 | Try again? | S-F00-03 (error state) |
| AD-UC-10 | a10 | Open QR label printing | S-F04-01 («In nhãn mã QR») → S-F02-03 |
| AD-UC-10 | a1 | Select physical books in the list | S-F02-03 (opened from S-F04-01) |
| AD-UC-10 | d7 | Select books on another page? | S-F02-03 (Pagination) |
| AD-UC-10 | a6 | Open another page of the list | S-F02-03 (Pagination) |
| AD-UC-10 | a2 | Choose Print labels | S-F02-03 |
| AD-UC-10 | a4 | Receive the printable QR label sheet | M-F02-03-01 |
| AD-UC-10 | a5 | Print the QR code labels | M-F02-03-01 (Print button; browser print dialog) |
| AD-UC-10 | d9 | Did the labels print correctly? | M-F02-03-01 |
| AD-UC-10 | a8 | Confirm that the sheet was printed | M-F02-03-01 ("Đã in xong" button) |
| AD-UC-10 | a9 | Close the preview without confirming | M-F02-03-01 ("Đóng" button) → S-F02-03 |
| AD-UC-10 | d11 | Print another sheet? | S-F02-03 |
| AD-UC-10 | d12 | Select other books? | S-F02-03 (warning state) |
| AD-UC-10 | d13 | Which books does the staff member want? | S-F02-03 (Segmented control «Chưa in nhãn» / «Đã in nhãn») |
| AD-UC-10 | a11 | Choose the «Đã in nhãn» filter | S-F02-03 |
| AD-UC-10 | a12 | Select the books to reprint, on any page of the list | S-F02-03 |
| AD-UC-10 | a13 | Choose Reprint labels («In lại nhãn») | S-F02-03 |
| AD-UC-10 | a14 | Print the reprinted labels | M-F02-03-01 (Print button; browser print dialog) |
| AD-UC-10 | d16 | Did the reprinted labels print correctly? | M-F02-03-01 |
| AD-UC-10 | a15 | Confirm that the sheet was printed | M-F02-03-01 ("Đã in xong" button) |
| AD-UC-10 | a16 | Close the preview without confirming | M-F02-03-01 ("Đóng" button) → S-F02-03 |
| AD-UC-10 | d8 | Sign out? | S-F04-01, S-F02-03, S-F02-04 (header "Đăng xuất") |
| AD-UC-10 | a7 | Choose Sign out | S-F04-01, S-F02-03, S-F02-04 → S-F00-03 |
| AD-UC-11 | r1 | Submit the library card number | S-F00-01 |
| AD-UC-11 | d6 | Enter the code or request a new OTP? | S-F00-02 |
| AD-UC-11 | r2 | Submit the OTP received by email | S-F00-02 |
| AD-UC-11 | d5 | Request a new OTP? | S-F00-02 |
| AD-UC-11 | r3 | Request a new OTP | S-F00-02 |
| AD-UC-12 | d1 | Sign in now? | M-F00-01 |
| AD-UC-12 | c1 | Sign in (UC-11) | S-F00-01 → S-F00-02 → back to S-F01-01 / S-F03-03 |
| AD-UC-12 | d2 | Which action? | S-F01-01 (Save) / S-F03-03 (view list); the list is first reached by the "Saved books" link on the OPAC personal area |
| AD-UC-12 | r2 | Select Save on a physical book | S-F01-01 |
| AD-UC-12 | r3 | Open the saved books list | S-F03-03 |
| AD-UC-12 | d6 | Remove a saved book? | S-F03-03 |
| AD-UC-12 | r4 | Select Remove on a saved book | S-F03-03 |
| AD-UC-13 | a0 | Open the staff page | S-F04-01 (signed in) or S-F00-03 (no staff session) |
| AD-UC-13 | a2 | Sign in with the internal library account | S-F00-03 → S-F04-01 |
| AD-UC-13 | d1 | Try again? | S-F00-03 (error state) |
| AD-UC-13 | a1 | Open the reported reviews | S-F04-01 → S-F02-04 |
| AD-UC-13 | a3 | Select a reported review | S-F02-04 |
| AD-UC-13 | d3 | Does the review violate the rules? | S-F02-04 |
| AD-UC-13 | a4 | Choose Remove on the review | S-F02-04 |
| AD-UC-13 | d4 | Confirm the removal? | M-F02-04-01 |
| AD-UC-13 | a5 | Dismiss the report | S-F02-04 |
| AD-UC-13 | d5 | Handle another reported review? | S-F02-04 |
| AD-UC-13 | d7 | Sign out? | S-F02-04, S-F04-01 (header "Đăng xuất") |
| AD-UC-13 | a6 | Choose Sign out | S-F02-04, S-F04-01 → S-F00-03 |
| AD-UC-14 | r1 | Select Report on a review | S-F02-01 |
| AD-UC-14 | d1 | Sign in now? | M-F00-01 |
| AD-UC-14 | c1 | Sign in (UC-11) | S-F00-01 → S-F00-02 → back to S-F02-01 |
| AD-UC-14 | r2 | Submit the report for the selected review | M-F02-01-02 |

Total: 112 actor-lane nodes in 14 activity diagrams (AD-UC-15 has no person lane), all on a listed screen or modal (recounted by script on 2026-11-23: 92 before that day's changes, the earlier figure 89 was a miscount; 10 added on 2026-11-23: AD-UC-01 c1, AD-UC-03 r4, AD-UC-04 r6, r7, AD-UC-05 c2, c3, c4, AD-UC-10 a10, d11, d12; 8 added for the reprint, D40: AD-UC-10 d13, a11, a12, a13, a14, d16, a15, a16; later on 23/11/2026: AD-UC-08 r2, AD-UC-09 r3 and AD-UC-11 d6 added, AD-UC-12 r1 removed, L8-21).

## Checks before you save

- [x] Every Screen ID is unique. No ID is used for two different screens.
      15 IDs, all unique. Retired IDs S-F03-04 and S-F03-05 are not reused. Modals have their own `M-` IDs.
- [x] No row is a state (error, empty, loading, success) or a confirmation modal.
      All 15 rows are places the actor navigates to. 43 messages and states are listed under "What is deliberately not a screen"; the 5 confirmation and question dialogs are under "Modals and overlays".
- [x] Every Must use case has at least one screen, or a note saying it has no user interface
      (for example a time-triggered activity).
      Must UCs UC-01 (S-F01-01, S-F01-02), UC-02 (S-F01-02), UC-04 (S-F02-01, S-F02-02), UC-05 (S-F02-01), UC-06 (S-F02-02), UC-10 (S-F04-01, S-F02-03, S-F00-03) and UC-11 (S-F00-01, S-F00-02) all have screens. The time-triggered QR generation of UC-10 has a no-UI note. UC-15 (Must, FR-04-09) is started by time and has no user interface (AD-UC-15).
- [x] Every actor action in the activity diagrams maps to a screen in this list.
      112 of 112 Reader and On-site Staff lane nodes of AD-UC-01 to AD-UC-14 are mapped to a listed screen or modal (section above).
- [x] Every screen serves at least one FR. A screen that serves none is out of scope or a missing FR.
      Every row cites at least one W1 FR of its own use case; the smallest is S-F04-01 (FR-04-07 "start a staff session and open the staff page", FR-04-08).

