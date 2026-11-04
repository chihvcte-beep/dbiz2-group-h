# Activity Diagram: AD-UC-10 Print QR code labels for physical books

| Field | Value |
|---|---|
| AD ID | AD-UC-10 |
| Use case | UC-10 Print QR code labels for physical books (QR codes are generated automatically) |
| Feature | F-02 Reviews & QR |
| Primary actor | On-site Staff; the automatic QR generation is started by time (daily sync finished) |
| Lanes | On-site Staff · Library Core System |
| Inputs (L3-L5) | Context Diagram (On-site Staff flows "Print QR request", "QR code labels", "Staff sign-in"; Library Internal System flows "Book catalog & availability", "Staff accounts") · Use Case Diagram (UC-10) · Sequence: QR Code Label Printing · W0 Table 1 (staff login), Table 3 (no QR codes for online-only books), Table 4 (Book QR codes, ILF) · W1 rows FR-02-07, FR-02-08, FR-02-17, FR-02-18, FR-04-07, FR-04-08, FR-04-12 |
| Trigger | (a) On-site Staff select physical books and choose Print labels. (b) Time event: the daily catalogue sync has finished. |
| Preconditions | Staff have an internal library account (FR-04-07). The catalogue is synced daily (FR-04-09). |
| Success end state | (a) Staff hold a printed QR label sheet for the selected books that have a QR code, and an audit entry is written. (b) Every new physical book from the sync has a unique QR code. |
| Failure end state | Staff are not signed in and do not sign in; or no book is selected (staff are asked to select one); or none of the selected books has a QR code (no sheet is produced). |
| FRs covered | FR-02-07, FR-02-08, FR-02-17, FR-02-18, FR-04-07, FR-04-08, FR-04-12 |
| Business rules applied | Only physical books get QR codes (W0 Table 3, FR-02-07). A label sheet needs at least one selected book that has a QR code (FR-02-17, FR-02-18). Every label print writes an audit entry (FR-04-12). The staff page needs a staff session and role (FR-04-08). |
| Version / status | v1.1 · Draft |
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
    m0{" "}
    a1("Select physical books on the staff page (FR-02-08)")
    a2("Choose Print labels (FR-02-08)")
    d1{"Sign in now?"}
    a3("Sign in with the internal library account (FR-04-07)")
    a4("Receive the printable QR label sheet (FR-02-08)")
    a5("Print the QR code labels (FR-02-08)")
    stop1@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s0("Check the staff session and role (FR-04-08)")
    d0{"Valid staff session and role?"}
    s1("Deny the request (FR-04-08)")
    d2{"Is at least one book selected?"}
    s2("Ask the staff to select at least one physical book (FR-02-17)")
    d3{"Do all selected books have a QR code?"}
    s3("Leave out the books without a QR code<br/>and list them to the staff (FR-02-18)")
    d4{"Is any selected book left?"}
    m1{" "}
    s4("Produce the printable QR label sheet<br/>for the selected books (FR-02-08)")
    s5("Write an audit entry for the label print (FR-04-12)")
    stop2@{ shape: fr-circ }
    t1@{ shape: hourglass }
    s6("Find the books added by the sync (FR-02-07)")
    mg{" "}
    d5{"Is there a new physical book without a QR code?"}
    s7("Generate a unique QR code linked to the physical book (FR-02-07)")
    stop4@{ shape: fr-circ }
  end

  start --> m0 --> a1 --> a2 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| a3 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| d2
  d2 -->|"[No]"| s2 --> m0
  d2 -->|"[Yes]"| d3
  d3 -->|"[Yes]"| m1
  d3 -->|"[No]"| s3 --> d4
  d4 -->|"[Yes]"| m1
  d4 -->|"[No]"| stop2
  m1 --> s4 --> s5 --> a4 --> a5 --> stop3

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

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| a1 | Action (Staff) | Select physical books on the staff page | FR-02-08 |
| a2 | Action (Staff) | Choose Print labels | FR-02-08 |
| s0 | Action | Check the staff session and role | FR-04-08 |
| d0 | Decision | Valid staff session and role? | FR-04-08 |
| s1 | Action | Deny the request | FR-04-08 |
| d1 | Decision (Staff) | Sign in now? | FR-04-07 |
| a3 | Action (Staff) | Sign in with the internal library account | FR-04-07 |
| d2 | Decision | Is at least one book selected? | FR-02-17 |
| s2 | Action | Ask the staff to select at least one physical book | FR-02-17 |
| d3 | Decision | Do all selected books have a QR code? | FR-02-18 |
| s3 | Action | Leave out the books without a QR code and list them to the staff | FR-02-18 |
| d4 | Decision | Is any selected book left? | FR-02-18 |
| s4 | Action | Produce the printable QR label sheet for the selected books | FR-02-08 |
| s5 | Action | Write an audit entry for the label print | FR-04-12 |
| a4 | Action (Staff) | Receive the printable QR label sheet | FR-02-08 |
| a5 | Action (Staff) | Print the QR code labels | FR-02-08 |
| t1 | Time event | Daily catalogue sync finished | FR-02-07 |
| s6 | Action | Find the books added by the sync | FR-02-07 |
| d5 | Decision | Is there a new physical book without a QR code? | FR-02-07 |
| s7 | Action | Generate a unique QR code linked to the physical book | FR-02-07 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the staff member is not signed in | they choose Print labels and decline to sign in | the request is denied; no sheet is produced |
| d0 [No] → d1 [Yes] | the staff member is not signed in | they sign in with internal account "staff.lan" | they return to the book selection |
| d0 [Yes] → d2 [No] | a signed-in staff member has selected no book | they choose Print labels | no sheet is produced and they are asked to select at least one physical book |
| d2 [Yes] → d3 [Yes] | 3 selected books all have QR codes | staff choose Print labels | a sheet with 3 labels is produced, an audit entry is written, and staff print it |
| d3 [No] → d4 [Yes] | 3 books are selected and 1 has no QR code yet | staff choose Print labels | the sheet holds 2 labels and the third book is listed as having no QR code |
| d4 [No] | 2 books are selected and neither has a QR code | staff choose Print labels | both books are listed; no sheet is produced |
| d5 [Yes] | the 02:00 sync added 5 physical books and 2 online-only books | the sync finishes | 5 unique QR codes are generated, one per physical book |
| d5 [No] | the sync added only online-only books | the sync finishes | no QR code is generated |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| QR code | Generated (written by `s7`, read by `d3`) |
| QR label sheet | produced by `s4`; not stored |
| Audit entry | written by `s5` |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Staff action | Screen ID |
|---|---|
| Select physical books on the staff page, Choose Print labels | (Lesson 8) |
| Sign in with the internal library account | (Lesson 8) |
| Receive and print the QR label sheet | (Lesson 8) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | the QR generation is started by time, not by staff. The workshop guide asks for a separate use case for a process nobody starts by hand. Keep it in UC-10, as its name says, or move it to a sync use case? | No (decided) | Decided 2026-11-04 (default adopted): Kept in UC-10, as its name says. |
| 2 | what happens if a QR code cannot be generated for a book? | No (decided) | Decided 2026-11-04 (default adopted): It is tried again at the next sync; until then the book shows up in the "no QR code" list of `s3`. |
| 3 | label size and number of labels per sheet? | No (decided) | Decided 2026-11-04 (default adopted): A4 sheet; the layout is set in Lesson 8. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-10 appears in the diagram | Pass (5 of 5 W1 rows whose source trace names UC-10) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
