# Activity Diagram: AD-UC-12 Save physical books to a personal list and remove them

| Field | Value |
|---|---|
| AD ID | AD-UC-12 |
| Use case | UC-12 Save physical books to a personal list for finding them later in the library, and remove them from the list |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flows "Save / remove book", "Saved list", "Shelf location & library map") · Use Case Diagram (UC-12, includes Sign in UC-11) · Sequence: [SD-UC-12](../use_case/sd_uc_12.md) · W0 Table 1 (login required), Table 4 (Saved books list, ILF; Book placement & library layout, EIF) · W1 rows FR-03-06, FR-03-07, FR-03-08, FR-03-24, FR-03-25, FR-01-07, FR-04-08 |
| Trigger | The reader asks for a saved-books action: save a physical book, or open the saved books list |
| Preconditions | The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). |
| Success end state | The chosen books are added to or removed from the reader's saved list, and the list shows the shelf location of each book; the reader chooses Finish. |
| Failure end state | The book is already saved (FR-03-24), or the list is empty (FR-03-25), or the reader chose not to sign in. |
| FRs covered | FR-03-06, FR-03-07, FR-03-08, FR-03-24, FR-03-25, FR-01-07, FR-04-08; FR-04-01 through the call to UC-11 |
| Business rules applied | Only physical books can be saved (UC-12 name, FR-03-06). A book appears in the list only once (FR-03-24). A missing or inconsistent shelf location is shown as unavailable, with the same rule as UC-01 (FR-01-07). A save or an open-list request made before sign-in is kept and continues by itself after sign-in (D1). |
| Version / status | v1.3 · Draft |
| Author | Owner D (F-03) |

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
  subgraph RDR["Reader"]
    start@{ shape: sm-circ }
    d1{"Sign in now?"}
    c1[["Sign in (UC-11) (FR-04-01)"]]
    m1{" "}
    d2{"Which action?"}
    r2("Select Save on a physical book (FR-03-06)")
    r3("Open the saved books list (FR-03-07)")
    d6{"Remove a saved book?"}
    r4("Select Remove on a saved book (FR-03-08)")
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    m0{" "}
    s0("Check the reader's session (FR-04-08)")
    d0{"Valid session?"}
    s1("Deny access (FR-04-08)")
    d7{"Which action was requested?"}
    d3{"Is the book already in the saved list?"}
    s2("Display that the book is already saved (FR-03-24)")
    s3("Add the book to the reader's saved books list (FR-03-06)")
    m2{" "}
    s4("Retrieve the saved books with their synced shelf locations (FR-03-07)")
    d4{"Is the list empty?"}
    s5("Display that no books have been saved yet (FR-03-25)")
    d5{"Does any saved book have a missing<br/>or inconsistent shelf location?"}
    s6("Show shelf location unavailable for those books<br/>and direct the reader to library staff (FR-01-07)")
    m3{" "}
    s7("Display the saved books with the<br/>shelf location of each book (FR-03-07)")
    s8("Delete the book from the reader's saved books list (FR-03-08)")
  end

  start --> m1 --> d2
  d2 -->|"[Save a book]"| r2 --> m0
  d2 -->|"[View saved books]"| r3 --> m0
  m0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| c1 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| d7
  d7 -->|"[Save a book]"| d3
  d3 -->|"[Yes]"| s2 --> m1
  d3 -->|"[No]"| s3 --> m1
  d7 -->|"[View saved books]"| m2 --> s4 --> d4
  d4 -->|"[Yes]"| s5 --> m1
  d4 -->|"[No]"| d5
  d5 -->|"[Yes]"| s6 --> m3
  d5 -->|"[No]"| m3
  m3 --> s7 --> d6
  d6 -->|"[Yes]"| r4 --> s8 --> m2
  d6 -->|"[No]"| m1
  d2 -->|"[Finish]"| stop2
```

Reading notes:

- `m1` is the merge every action comes back through, so the reader can save, view and remove as
  often as they like before choosing Finish.
- The reader chooses the action before the session is checked. After sign-in the flow re-enters at
  `m0` and the system decision `d7` takes the action already chosen, so the book is saved or the
  list opens without the reader choosing again (D1).
- After a removal the list is loaded again through `m2`, so the reader always sees the current list
  with current shelf locations.
- `m3` gathers the two shelf-location cases before the list is displayed.
- v1.3: the first step `r1` "Request a saved-books action" is removed. It was the same click as `r2`
  (Save) or `r3` (open the list) (L8-21).

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| s0 | Action | Check the reader's session | FR-04-08 |
| d0 | Decision | Valid session? | FR-04-08 |
| s1 | Action | Deny access | FR-04-08 |
| d1 | Decision (Reader) | Sign in now? | FR-04-08 |
| c1 | Call (Reader) | Sign in (UC-11) | FR-04-01 |
| d2 | Decision (Reader) | Which action? | FR-03-06, FR-03-07 |
| d7 | Decision | Which action was requested? | FR-03-06, FR-03-07 |
| r2 | Action (Reader) | Select Save on a physical book | FR-03-06 |
| d3 | Decision | Is the book already in the saved list? | FR-03-24 |
| s2 | Action | Display that the book is already saved | FR-03-24 |
| s3 | Action | Add the book to the reader's saved books list | FR-03-06 |
| r3 | Action (Reader) | Open the saved books list | FR-03-07 |
| s4 | Action | Retrieve the saved books with their synced shelf locations | FR-03-07 |
| d4 | Decision | Is the list empty? | FR-03-25 |
| s5 | Action | Display that no books have been saved yet | FR-03-25 |
| d5 | Decision | Does any saved book have a missing or inconsistent shelf location? | FR-01-07 |
| s6 | Action | Show shelf location unavailable for those books and direct the reader to library staff | FR-01-07 |
| s7 | Action | Display the saved books with the shelf location of each book | FR-03-07 |
| d6 | Decision (Reader) | Remove a saved book? | FR-03-08 |
| r4 | Action (Reader) | Select Remove on a saved book | FR-03-08 |
| s8 | Action | Delete the book from the reader's saved books list | FR-03-08 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the reader is not signed in | they select Save and decline to sign in | access is denied; nothing is saved |
| d0 [No] → d1 [Yes] | the reader is not signed in | they select Save and sign in with card 0012345 | the session is checked again and the book is saved without selecting Save again |
| d7 [Save a book] → d3 [Yes] | "Principles of Economics" is already in the reader's list | they select Save on it | nothing is added; a message says the book is already saved |
| d3 [No] | the book is not in the list | the reader selects Save on it | the book is added to the list |
| d7 [View saved books] → d4 [Yes] | the reader's list is empty | they open the saved books list | a message says no books have been saved yet |
| d4 [No] → d5 [No] | the list holds 2 books, both with complete shelf codes | the reader opens the list | both books are shown with floor, room and shelf code |
| d5 [Yes] | 1 of 3 saved books has no room code | the reader opens the list | that book shows "shelf location unavailable, ask library staff"; the other 2 show their shelf codes |
| d6 [Yes] | the list holds 3 books | the reader selects Remove on one | the book is deleted and the list reloads with 2 books |
| d6 [No] | the list is shown | the reader does not remove a book | the action choice is shown again |
| d2 [Finish] | the action choice is shown | the reader leaves | the activity ends |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Saved book entry | Saved (written by `s3`); a removed entry is deleted (`s8`), not kept with a state |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Which action? (d2) | S-F01-01 ("Save to my list") or the "Saved books" link in the existing OPAC personal area → S-F03-03 |
| Sign in now? (d1) | S-F01-01 / S-F03-03 (modal M-F00-01 "Sign in to continue?") |
| Sign in (UC-11) (c1) | S-F00-01 → S-F00-02, then back to S-F01-01 / S-F03-03 |
| Select Save on a physical book (r2) | S-F01-01 |
| See that the book is saved (s3), or already saved (s2) | S-F01-01 (success state / already-saved state) |
| Open the saved books list (r3), Remove a saved book? (d6), Select Remove on a saved book (r4) | S-F03-03 |
| See the saved books with their shelf locations (s7), "shelf location unavailable" for some books (s6) | S-F03-03 |
| See that no books have been saved yet (s5) | S-F03-03 (empty state) |

## 6. Open questions

None. Decisions: see [decision_index.md](../project/decision_index.md#ad-uc-12).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-12 appears in the diagram | Pass (6 of 6 W1 rows whose source trace names UC-12) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| v1.2: action chosen before the session check so it continues after sign-in (D1), `d7` | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| Renders after v1.2 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| v1.3: `r1` removed (L8-21); `start` goes to `m1` | Pass (checked by script) | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
