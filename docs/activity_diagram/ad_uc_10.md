# Activity Diagram: AD-UC-10 Print QR code labels for physical books

| Field | Value |
|---|---|
| AD ID | AD-UC-10 |
| Use case | UC-10 Print QR code labels for physical books (QR codes are generated automatically) |
| Feature | F-02 Reviews & QR |
| Primary actor | On-site Staff; the automatic QR generation is started by time (daily sync finished) |
| Lanes | On-site Staff · Library Core System |
| Inputs (L3-L5) | Context Diagram (On-site Staff flows "Print QR request", "QR code labels", "Staff sign-in"; Library Internal System flows "Book catalog & availability", "Staff accounts") · Use Case Diagram (UC-10) · Sequence: [SD-UC-10](../system_design/sequence_diagram/sd_uc_10.md) · W0 Table 1 (staff login), Table 3 (no QR codes for online-only books), Table 4 (Book QR codes, ILF) · W1 rows FR-02-07, FR-02-08, FR-02-17, FR-02-18, FR-04-07, FR-04-08, FR-04-12, FR-04-18, FR-02-23 (D3), FR-02-25 (D40), FR-04-21 (D7); FR-02-07 as changed by D40; FR-02-08 as changed by D3, D12 and D41 |
| Trigger | (a) On-site Staff open the staff page to print QR labels. (b) Time event: the daily catalogue sync has finished. |
| Preconditions | Staff have an internal library account (FR-04-07). The catalogue is synced daily (FR-04-09). |
| Success end state | (a) Staff hold a printed QR label sheet for the selected books that have a QR code; after staff confirm «Đã in xong» those books are recorded as label-printed, an audit entry is written and the books leave the list; staff may then print another sheet or sign out. Staff can also reprint the existing QR code of a labelled book for its other copies. (b) Every new physical book title from the sync has one unique QR code, shared by all its copies. |
| Failure end state | Staff cannot sign in (wrong account or no staff role) and stop trying; or no book is waiting for a label (the list is empty); or no book is selected (staff are asked to select one); or none of the selected books has a QR code and staff do not select other books (no sheet is produced). |
| FRs covered | FR-02-07, FR-02-08, FR-02-17, FR-02-18, FR-02-23, FR-02-25, FR-04-07, FR-04-08, FR-04-12, FR-04-18, FR-04-21 |
| Business rules applied | Only physical books get QR codes (W0 Table 3, FR-02-07). A label sheet needs at least one selected book that has a QR code (FR-02-17, FR-02-18). Every label print confirmed with «Đã in xong» and every successful staff sign-in writes an audit entry (FR-04-12; D32, D30). The staff page opens only with a staff session and role: staff sign in before the page opens (FR-04-08, FR-04-07). A wrong account or an account without the staff role is rejected with an error message, and staff may try again (FR-04-18). The list shows only physical books from the synced catalogue that have never had a QR label printed, 20 per page, ordered by floor, room and shelf; ticks are kept across pages (FR-02-23; D3). One QR code per book title, shared by all its copies: the first print gives one label per title, and labels for other copies are reprinted from the «Đã in nhãn» filter with the same code and no shelf location (FR-02-07, FR-02-25; D40). The sheet is A4 portrait decal, 3 × 8 = 24 labels of 70×37 mm per page; more than 24 selected books continue on further A4 pages ([ui_conventions.md](../external_design/ui_conventions.md) section 3; D4, D41). The books on the sheet are recorded as label-printed only when staff confirm that the sheet was printed («Đã in xong»); closing the preview («Đóng») or a failed print records nothing and the books stay in the list (FR-02-08; D12). The label and the order of the list use the book's primary shelf location returned by the sync — the same location shown on S-F01-01 — also for a title whose copies sit on several shelves (FR-02-23; D13). The staff session does not end by time: it ends only when staff choose Sign out (FR-04-21; D7). |
| Version / status | v1.7 · Draft |
| Author | Owner C (F-02) |

## 1. Diagram

Notation follows the DBIZ2 activity profile and the GeeksforGeeks notation sheet the team uses.
Rendered with `swimlane-beta`, which needs Mermaid 11.16 or later.

```mermaid
---
config:
  theme: base
  themeVariables:
    primaryColor: "#d5e8d4"
    primaryBorderColor: "#333333"
    lineColor: "#000000"
    clusterBkg: "#ffffff"
    clusterBorder: "#333333"
---
swimlane-beta TB
  subgraph STF["On-site Staff"]
    start@{ shape: sm-circ }
    a0("Open the staff page (FR-04-08)")
    m0{" "}
    a3("Sign in with the internal library account (FR-04-07)")
    d1{"Try again?"}
    mA{" "}
    a10("Open QR label printing (FR-02-23)")
    mB{" "}
    a1("Select physical books in the list (FR-02-08)")
    d7{"Select books on another page?"}
    a6("Open another page of the list (FR-02-23)")
    a2("Choose Print labels (FR-02-08)")
    a4("Receive the printable QR label sheet (FR-02-08)")
    a5("Print the QR code labels (FR-02-08)")
    d9{"Did the labels print correctly?"}
    a8("Confirm that the sheet was printed («Đã in xong») (FR-02-08)")
    a9("Close the preview without confirming («Đóng») (FR-02-08)")
    d11{"Print another sheet?"}
    d12{"Select other books?"}
    d13{"Which books does the staff member want?"}
    a11("Choose the «Đã in nhãn» filter (FR-02-25)")
    mD{" "}
    a12("Select the books to reprint, on any page of the list (FR-02-25)")
    a13("Choose Reprint labels («In lại nhãn») (FR-02-25)")
    a14("Print the reprinted labels (FR-02-25)")
    d16{"Did the reprinted labels print correctly?"}
    a15("Confirm that the sheet was printed («Đã in xong») (FR-02-25)")
    a16("Close the preview without confirming («Đóng») (FR-02-25)")
    m4{" "}
    d8{"Sign out?"}
    a7("Choose Sign out (FR-04-21)")
    stop1@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s0("Check the staff session and role (FR-04-08)")
    d0{"Valid staff session and role?"}
    s1("Deny the request and show the staff sign-in (FR-04-08)")
    s8("Verify the account and the staff role<br/>against the internal library accounts (FR-04-07)")
    d6{"Valid account with the staff role?"}
    s9("Reject the sign-in and show an error message (FR-04-18)")
    s10("Start a staff session and open the staff page (FR-04-07)")
    s15("Write an audit entry for the staff sign-in (FR-04-12)")
    mC{" "}
    s11("List the physical books that have never had a QR label<br/>printed, 20 per page, by floor, room and shelf (FR-02-23)")
    d10{"Is any book waiting for a QR label?"}
    s16("Display that every physical book<br/>already has a printed label (FR-02-23)")
    s12("Show that page of the list, keeping the ticks (FR-02-23)")
    d2{"Is at least one book selected?"}
    s2("Ask the staff to select at least one physical book (FR-02-17)")
    d3{"Do all selected books have a QR code?"}
    s3("Leave out the books without a QR code<br/>and list them to the staff (FR-02-18)")
    d4{"Is any selected book left?"}
    m1{" "}
    s4("Produce the printable QR label sheet for the<br/>selected books, 24 labels per A4 page (FR-02-08)")
    s13("Record that a label has been printed<br/>for each book on the sheet (FR-02-08)")
    s5("Write an audit entry for the label print (FR-04-12)")
    s17("List the physical books that already have a printed<br/>label, 20 per page, by floor, room and shelf (FR-02-25)")
    d14{"Does any book already have a printed label?"}
    s18("Display that no book has a printed label yet (FR-02-25)")
    d15{"Is at least one book selected to reprint?"}
    s19("Ask the staff to select at least one book (FR-02-17)")
    s20("Produce the reprint sheet: existing QR code and<br/>title, no shelf location (FR-02-25)")
    s21("Write an audit entry for the label reprint (FR-04-12)")
    m5{" "}
    s14("End the staff session and show the staff sign-in (FR-04-21)")
    stop5@{ shape: fr-circ }
    t1@{ shape: hourglass }
    s6("Find the books added by the sync (FR-02-07)")
    mg{" "}
    d5{"Is there a new physical book without a QR code?"}
    s7("Generate one unique QR code linked to the book title (FR-02-07)")
    stop4@{ shape: fr-circ }
  end

  start --> a0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> m0 --> a3 --> s8 --> d6
  d6 -->|"[No]"| s9 --> d1
  d1 -->|"[Yes]"| m0
  d1 -->|"[No]"| stop1
  d6 -->|"[Yes]"| s10 --> s15 --> mA
  d0 -->|"[Yes]"| mA
  mA --> a10 --> mC --> d13
  d13 -->|"[Books awaiting a label]"| s11 --> d10
  d13 -->|"[Books already labelled]"| a11 --> s17 --> d14
  d14 -->|"[No]"| s18 --> m4
  d14 -->|"[Yes]"| mD --> a12 --> a13 --> d15
  d15 -->|"[No]"| s19 --> mD
  d15 -->|"[Yes]"| s20 --> a14 --> d16
  d16 -->|"[Yes]"| a15 --> s21 --> m5
  d16 -->|"[No]"| a16 --> mD
  d10 -->|"[No]"| s16 --> m4
  d10 -->|"[Yes]"| mB --> a1 --> d7
  d7 -->|"[Yes]"| a6 --> s12 --> mB
  d7 -->|"[No]"| a2 --> d2
  d2 -->|"[No]"| s2 --> mB
  d2 -->|"[Yes]"| d3
  d3 -->|"[Yes]"| m1
  d3 -->|"[No]"| s3 --> d4
  d4 -->|"[Yes]"| m1
  d4 -->|"[No]"| d12
  d12 -->|"[Yes]"| mB
  d12 -->|"[No]"| m4
  m1 --> s4 --> a4 --> a5 --> d9
  d9 -->|"[Yes]"| a8 --> s13 --> s5 --> m5
  m5 --> d11
  d9 -->|"[No]"| a9 --> mB
  d11 -->|"[Yes]"| mC
  d11 -->|"[No]"| m4
  m4 --> d8
  d8 -->|"[Yes]"| a7 --> s14 --> stop5
  d8 -->|"[No]"| stop3

  t1 -->|"Daily catalogue sync finished"| s6 --> mg --> d5
  d5 -->|"[Yes]"| s7 --> mg
  d5 -->|"[No]"| stop4
```

Reading notes:

- The activity has two starts. The initial node starts the staff flow. The hourglass `t1` is a
  **time event**: the QR generation starts by itself when the daily sync finishes, and no person
  clicks anything. The time expression is written on its outgoing arrow.
- The loop `d5 [Yes] → s7 → mg` handles one new physical book at a time and comes back through the
  merge `mg`.
- Staff sign in with their own action "Sign in with the internal library account" (FR-04-07), not
  with UC-11, because UC-11 is the reader sign-in.
- The session is checked at the start: the staff page opens only for a signed-in staff member
  (FR-04-08, L8-02), so staff sign in before they select books. `m0` is the merge staff come back
  through after a rejected sign-in; `mA` gathers the signed-in paths (already signed in, just signed
  in) before staff choose «In nhãn mã QR» on the staff page (`a10`).
- `d6 [No]` covers a wrong account and an account without the staff role (FR-04-18, L8-03). The
  staff session does not end by time (FR-04-21, D7); it ends only when staff choose Sign out.
- A successful staff sign-in writes an audit entry (`s15`, FR-04-12, D30), as the reader sign-in
  does in AD-UC-11 `s8`. A rejected sign-in writes none.
- `s11` lists the physical books that have never had a QR label printed (new books since the last
  sync appear here and stay until their label is printed), 20 per page, by floor, room and shelf, so
  the sheet follows the walking order along the shelves (D3, D3c, D3d). Staff move between pages
  with `d7` / `a6` / `s12`; ticks are kept across pages and the screen shows how many books are
  selected (D3b). `mB` gathers the list, another page, the request to select a book (`s2` keeps the
  list and the ticks) and the return from «Đóng» (`a9`). Books left out by `s3` stay in the list.
  Sign out (`d8`, `a7`, `s14`) is drawn once, after printing; «Đăng xuất» is on every staff screen,
  so staff can sign out at any time (D7).
- Producing the sheet (`s4`) records nothing (D12). After printing, staff decide `d9` "Did the
  labels print correctly?". `[Yes]`: they confirm with «Đã in xong» (`a8`) and only then `s13`
  records each book on the sheet as label-printed, so those books leave the list. `[No]` (a failed
  print, or staff simply close the preview): «Đóng» (`a9`) records nothing and returns through `mB`
  to the list, where the books are still listed with their ticks, so staff can print again (D18).
  The audit entry `s5` is written right after `s13`, when staff confirm «Đã in xong»; producing the
  sheet, «Đóng» or a failed print writes none (D32). `s11` orders the list by each book's
  primary shelf location returned by the sync (the location shown on S-F01-01), and the label shows
  that same location (D13).
- `d10 [No]`: no book is waiting, so S-F02-03 shows its empty state (`s16`, MSG-11, D15). After
  «Đã in xong», `d11 [Yes]` reloads the list through `mC`, so staff can print the next sheet. When
  no selected book has a QR code, `d12` lets staff select other books (back through `mB`) or stop.
  `m4` gathers every way of stopping before `d8`.
- `d13` is the status filter on S-F02-03 (D40). The screen opens on «Chưa in nhãn», the flow already
  described. «Đã in nhãn» (`a11`) lists the labelled books, 20 per page with ticks kept as in the main
  list. Copies of a title share one QR code, so a reprint (`s20`) generates no new code and prints no
  shelf location, because another copy may sit on another shelf. «Đã in xong» (`a15`) writes only an
  audit entry (`s21`): the books stay labelled and stay in this list. «Đóng» (`a16`) records nothing.
- A sheet holds 24 labels per A4 page. When more than 24 books are selected, `s4` continues on further
  A4 pages, and «Đã in xong» records every book on all pages (D41).

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| a0 | Action (Staff) | Open the staff page | FR-04-08 |
| s0 | Action | Check the staff session and role | FR-04-08 |
| d0 | Decision | Valid staff session and role? | FR-04-08 |
| s1 | Action | Deny the request and show the staff sign-in | FR-04-08 |
| a3 | Action (Staff) | Sign in with the internal library account | FR-04-07 |
| s8 | Action | Verify the account and the staff role against the internal library accounts | FR-04-07 |
| d6 | Decision | Valid account with the staff role? | FR-04-07, FR-04-18 |
| s9 | Action | Reject the sign-in and show an error message | FR-04-18 |
| d1 | Decision (Staff) | Try again? | FR-04-18 |
| s10 | Action | Start a staff session and open the staff page | FR-04-07 |
| s15 | Action | Write an audit entry for the staff sign-in | FR-04-12 |
| a10 | Action (Staff) | Open QR label printing | FR-02-23 |
| d13 | Decision (Staff) | Which books does the staff member want? | FR-02-25 |
| a11 | Action (Staff) | Choose the «Đã in nhãn» filter | FR-02-25 |
| s17 | Action | List the physical books that already have a printed label, 20 per page, by floor, room and shelf | FR-02-25 |
| d14 | Decision | Does any book already have a printed label? | FR-02-25 |
| s18 | Action | Display that no book has a printed label yet | FR-02-25 |
| a12 | Action (Staff) | Select the books to reprint, on any page of the list | FR-02-25 |
| a13 | Action (Staff) | Choose Reprint labels («In lại nhãn») | FR-02-25 |
| d15 | Decision | Is at least one book selected to reprint? | FR-02-17 |
| s19 | Action | Ask the staff to select at least one book | FR-02-17 |
| s20 | Action | Produce the reprint sheet: existing QR code and title, no shelf location | FR-02-25 |
| a14 | Action (Staff) | Print the reprinted labels | FR-02-25 |
| d16 | Decision (Staff) | Did the reprinted labels print correctly? | FR-02-25 |
| a15 | Action (Staff) | Confirm that the sheet was printed («Đã in xong») | FR-02-25 |
| s21 | Action | Write an audit entry for the label reprint | FR-04-12 |
| a16 | Action (Staff) | Close the preview without confirming («Đóng») | FR-02-25 |
| s11 | Action | List the physical books that have never had a QR label printed, 20 per page, by floor, room and shelf | FR-02-23 |
| d10 | Decision | Is any book waiting for a QR label? | FR-02-23 |
| s16 | Action | Display that every physical book already has a printed label | FR-02-23 |
| a1 | Action (Staff) | Select physical books in the list | FR-02-08 |
| d7 | Decision (Staff) | Select books on another page? | FR-02-23 |
| a6 | Action (Staff) | Open another page of the list | FR-02-23 |
| s12 | Action | Show that page of the list, keeping the ticks | FR-02-23 |
| a2 | Action (Staff) | Choose Print labels | FR-02-08 |
| d2 | Decision | Is at least one book selected? | FR-02-17 |
| s2 | Action | Ask the staff to select at least one physical book | FR-02-17 |
| d3 | Decision | Do all selected books have a QR code? | FR-02-18 |
| s3 | Action | Leave out the books without a QR code and list them to the staff | FR-02-18 |
| d4 | Decision | Is any selected book left? | FR-02-18 |
| d12 | Decision (Staff) | Select other books? | FR-02-18 |
| s4 | Action | Produce the printable QR label sheet for the selected books, 24 labels per A4 page | FR-02-08 |
| a4 | Action (Staff) | Receive the printable QR label sheet | FR-02-08 |
| a5 | Action (Staff) | Print the QR code labels | FR-02-08 |
| d9 | Decision (Staff) | Did the labels print correctly? | FR-02-08 |
| a8 | Action (Staff) | Confirm that the sheet was printed («Đã in xong») | FR-02-08 |
| s13 | Action | Record that a label has been printed for each book on the sheet | FR-02-08 |
| s5 | Action | Write an audit entry for the label print | FR-04-12 |
| d11 | Decision (Staff) | Print another sheet? | FR-02-08 |
| a9 | Action (Staff) | Close the preview without confirming («Đóng») | FR-02-08 |
| d8 | Decision (Staff) | Sign out? | FR-04-21 |
| a7 | Action (Staff) | Choose Sign out | FR-04-21 |
| s14 | Action | End the staff session and show the staff sign-in | FR-04-21 |
| t1 | Time event | Daily catalogue sync finished | FR-02-07 |
| s6 | Action | Find the books added by the sync | FR-02-07 |
| d5 | Decision | Is there a new physical book without a QR code? | FR-02-07 |
| s7 | Action | Generate one unique QR code linked to the book title | FR-02-07 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d6 [Yes] | the staff member is not signed in | they open the staff page and sign in with internal account "staff.lan", which has the staff role | a staff session starts, an audit entry "staff.lan, staff sign-in, time" is written and the staff page opens; they can select books |
| d6 [No] → d1 [Yes] | the staff member is not signed in | they enter a wrong password for "staff.lan", then the right one | the first try is rejected with an error message; the second try opens the staff page |
| d6 [No] → d1 [No] | internal account "lib.reader" exists but has no staff role | they sign in with it and then give up | the sign-in is rejected with an error message; no audit entry is written; the staff page does not open |
| d0 [Yes] | the staff member already has a valid staff session | they open the staff page | the page opens without asking to sign in |
| d0 [Yes] → d2 [No] | a signed-in staff member has selected no book | they choose Print labels | no sheet is produced and they are asked to select at least one physical book |
| s11 | the 02:00 sync added 25 physical books and none has had a label printed | signed-in staff open QR label printing | the 25 books are listed, 20 on page 1 and 5 on page 2, ordered by floor, room and shelf |
| s11 (primary shelf location) | "Digital Marketing Basics" has copies on Tầng 2 · Phòng R-204 · Kệ S-12 and on Tầng 3 · Phòng R-301 · Kệ S-02; the sync returns Tầng 2 · Phòng R-204 · Kệ S-12 as its primary shelf location | signed-in staff open QR label printing and print its label | the book is sorted among the floor 2 books, and its label shows «Tầng 2 · Phòng R-204 · Kệ S-12», the same location as on S-F01-01 |
| d7 [Yes] | staff ticked 2 books on page 1 | they open page 2, tick 1 book and come back to page 1 | the 2 ticks on page 1 are still there and the screen shows that 3 books are selected |
| d2 [Yes] → d3 [Yes] | 3 selected books all have QR codes | staff choose Print labels | a sheet with 3 labels is produced and staff print it; no audit entry is written yet and the 3 books are not yet recorded as label-printed |
| d9 [Yes] | staff printed a sheet with 3 labels and the labels came out correctly | they choose «Đã in xong» | the 3 books are recorded as label-printed, an audit entry "staff.lan, label print, time" is written, and the books leave the list; their ticks are cleared |
| d9 [No] | staff printed a sheet with 3 labels and the printer jammed | they choose «Đóng» | nothing is recorded and no audit entry is written; the 3 books are still in the list with their ticks, and staff can choose Print labels again |
| s4 (more than 24 books) | staff selected 30 books that all have QR codes | they choose Print labels and then «Đã in xong» | the sheet has 2 A4 pages (24 + 6 labels) and all 30 books are recorded as label-printed |
| d3 [No] → d4 [Yes] | 3 books are selected and 1 has no QR code yet | staff choose Print labels | the sheet holds 2 labels and the third book is listed as having no QR code |
| d4 [No] → d12 [Yes] | 2 books are selected and neither has a QR code | staff choose Print labels, then tick 2 other books | both books are listed, no sheet is produced, and staff stay on the list and can print the other books |
| d12 [No] | 2 books are selected and neither has a QR code | staff choose Print labels and stop | both books are listed and no sheet is produced; staff may sign out |
| d10 [No] | every physical book already has a printed label | signed-in staff open QR label printing | the list is empty and the message «Tất cả sách bản giấy đã được in nhãn…» (MSG-11) is shown |
| d11 [Yes] | 25 books were waiting and staff confirmed a sheet of 20 | they choose to print another sheet | the list reloads with the other 5 books |
| d11 [No] | staff confirmed a sheet with «Đã in xong» | they stop printing | the flow goes on to "Sign out?" |
| d13 [Books already labelled] → d16 [Yes] | "Principles of Economics" has a printed label and a second copy on another shelf | staff choose «Đã in nhãn», tick the book, choose «In lại nhãn», print and choose «Đã in xong» | one label with the same QR code and no shelf location is printed, no new code is generated, an audit entry is written and the book stays in the labelled list |
| d14 [No] | no book has a printed label yet | staff choose «Đã in nhãn» | the list is empty and a message says no book has a printed label yet |
| d15 [No] | no labelled book is ticked | staff choose «In lại nhãn» | no sheet is produced and they are asked to select at least one book |
| d16 [No] | the reprint jammed in the printer | staff choose «Đóng» | nothing is recorded, no audit entry is written and the ticks are kept |
| d8 [Yes] | staff have printed a label sheet and chosen «Đã in xong» | they choose «Đăng xuất» | the staff session ends and the staff sign-in opens |
| d8 [No] | staff have printed a label sheet | they leave the staff page open | the activity ends; the staff session stays valid with no time-out |
| d5 [Yes] | the 02:00 sync added 5 physical books and 2 online-only books | the sync finishes | 5 unique QR codes are generated, one per physical book |
| d5 [No] | the sync added only online-only books | the sync finishes | no QR code is generated |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| QR code | Generated (written by `s7`, read by `d3`); Label printed (written by `s13`, only after `a8` «Đã in xong»; books in this state are left out of the list of `s11`) |
| Staff session | Signed-in (written by `s10`), Ended (written by `s14`) |
| QR label sheet | produced by `s4`; not stored |
| Audit entry | written by `s5` (label print, after `a8` «Đã in xong»), `s21` (label reprint, after `a15` «Đã in xong») and `s15` (staff sign-in) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| On-site Staff action | Screen ID |
|---|---|
| Open the staff page (a0) | S-F04-01 when signed in; S-F00-03 when not (s1) |
| Sign in with the internal library account (a3), Try again? (d1) | S-F00-03 |
| See that the sign-in was rejected (s9) | S-F00-03 (error state) |
| Staff page opens after sign-in (s10) | S-F00-03 → S-F04-01 |
| Open QR label printing (a10) | S-F04-01 («In nhãn mã QR») → S-F02-03 |
| See the list of books awaiting a QR label (s11) | S-F02-03 |
| See that no book is waiting for a label (s16) | S-F02-03 (empty state, MSG-11) |
| Print another sheet? (d11), Select other books? (d12) | S-F02-03 |
| Select physical books in the list (a1), Select books on another page? (d7), Open another page of the list (a6), Choose Print labels (a2) | S-F02-03 (Checkbox, Pagination, «Đã chọn `<n>` sách», «In nhãn») |
| See the request to select at least one physical book (s2) | S-F02-03 (error state) |
| See the books left out because they have no QR code (s3) | S-F02-03 (warning state) |
| Receive the printable QR label sheet (a4), Print the QR code labels (a5) | S-F02-03 (modal M-F02-03-01 "QR label sheet preview"; its «In» Primary button opens the browser print dialog, D17) |
| Did the labels print correctly? (d9), Confirm that the sheet was printed (a8), Close the preview without confirming (a9) | M-F02-03-01 («Đã in xong» Secondary button, D17; «Đóng» Secondary button → back to S-F02-03 with the ticks kept, D18) |
| Which books? (d13), Choose the «Đã in nhãn» filter (a11), Select the books to reprint (a12), Choose «In lại nhãn» (a13) | S-F02-03 (Segmented control #15, Checkbox, Pagination, «In lại nhãn») |
| See that no book has a printed label yet (s18) | S-F02-03 (Empty state of «Đã in nhãn») |
| Print the reprinted labels (a14), Did they print correctly? (d16), Confirm (a15), Close (a16) | M-F02-03-01 (reprint variant) |
| Sign out? (d8), Choose Sign out (a7), staff sign-in shown (s14) | «Đăng xuất» in the header of S-F04-01, S-F02-03 or S-F02-04 → S-F00-03 |

## 6. Open questions

None. Decisions: see [decision_index.md](../project_brief/decision_index.md#ad-uc-10).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.3.0, swimlane-beta) | Pass (re-checked after the v1.2 sign-in change) | AI assistant | 2026-11-08 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-10 appears in the diagram | Pass (5 of 5 W1 rows whose source trace names UC-10, plus FR-04-18) | AI assistant | 2026-11-08 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| v1.3 (D3, D7): guards on `d7` and `d8`, merge `mB` before `a1`, each new action cites one FR | Pass (checked by reading) | AI assistant | 2026-11-22 |
| v1.4 (D12, D13): guards on `d9`, `a9` returns through merge `mB`, each new action cites one FR | Pass (checked by reading) | AI assistant | 2026-11-22 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| v1.5 (D30): `s15` added between `s10` and `mA`, the new action cites one FR | Pass (checked by reading) | AI assistant | 2026-11-23 |
| Renders after v1.5 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| v1.6: `a10`, empty list `d10`/`s16`, loops `d11`/`d12`, merges `mC`/`m4`, audit `s5` moved after `s13` | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| Renders after v1.6 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| v1.7 (D40, D41): filter `d13`, reprint path `a11`–`a16`, `s17`–`s21`, merges `mD` and `m5`, 24 labels per A4 page | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
