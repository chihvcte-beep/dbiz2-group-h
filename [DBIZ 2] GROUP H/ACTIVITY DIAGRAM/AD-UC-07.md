# Activity Diagram: AD-UC-07 Update and view personal reading history and preferences

| Field | Value |
|---|---|
| AD ID | AD-UC-07 |
| Use case | UC-07 Update and view personal reading history and preferences |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader; two parts start by themselves: a time event (daily loan sync finished) and an accept event (online book opened, from UC-03) |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flows "Reading history & preferences", "Reading history"; Library Internal System flow "Borrow/return records") · Use Case Diagram (UC-07, includes Sign in UC-11) · Sequence: Reader Interaction Flow (UC-07 with UC-09; note on automatic entries) · W0 Table 1 (login required), Table 3 (no automatic progress tracking), Table 4 (Reading history & preferences, ILF; Reader loan records, EIF) · W1 rows FR-03-01, FR-03-02, FR-03-03, FR-03-04, FR-03-05, FR-03-22, FR-04-08 |
| Trigger | (a) The reader opens their reading history and preferences. (b) Time event: the daily loan records sync has finished (FR-04-10). (c) Accept event: a signed-in reader opened an online book from the filter results (AD-UC-03). |
| Preconditions | (a) The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). (b) Loan records of library card accounts are synced daily (FR-04-10). |
| Success end state | (a) The reader has seen their reading history with reading status; every update that passed the check is saved and shown; the reader chooses Finish. (b) Every new borrow record has put its book into that reader's history. (c) The opened online book is in that reader's history. |
| Failure end state | An update fails the check: it is rejected, the saved data stays unchanged and an error message is shown (FR-03-22). Or the reader chose not to sign in. |
| FRs covered | FR-03-01, FR-03-02, FR-03-03, FR-03-04, FR-03-05, FR-03-22, FR-04-08; FR-04-01 through the call to UC-11 |
| Business rules applied | Reading status is Reading or Finished; progress is between 0 and 100 percent (FR-03-04). A failed update keeps the saved data (FR-03-22). Progress is entered by hand in release 1 (W0 Table 3). History entries are added automatically for borrowed books of library card accounts (FR-03-03) and for online books opened by signed-in readers (FR-03-02). The loan records are read, never written (W0 Table 4). |
| Version / status | v1.2 · Draft |
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
    r1("Open reading history and preferences (FR-03-01)")
    d1{"Sign in now?"}
    c1[["Sign in (UC-11) (FR-04-01)"]]
    d2{"What does the reader do?"}
    r2("Submit the reading status and progress of a book (FR-03-04)")
    r3("Submit updated reading preferences (FR-03-05)")
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    m0{" "}
    s0("Check the reader's session (FR-04-08)")
    d0{"Valid session?"}
    s1("Deny access (FR-04-08)")
    s2("Retrieve the reader's Reading history & preferences (FR-03-01)")
    s3("Display the reading history with reading status (FR-03-01)")
    m1{" "}
    s4("Check that the status is Reading or Finished<br/>and the progress is between 0 and 100 percent (FR-03-04)")
    d3{"Does the update pass the check?"}
    s5("Save the reading status and progress (FR-03-04)")
    s6("Display the updated reading history (FR-03-01)")
    s7("Validate the reading preferences (FR-03-05)")
    d4{"Do the preferences pass the validation?"}
    s8("Save the preferences to the reader's profile (FR-03-05)")
    s9("Display the updated preferences (FR-03-05)")
    me{" "}
    s10("Reject the update, keep the saved data<br/>and display an error message (FR-03-22)")
    t1@{ shape: hourglass }
    s11("Find the new borrow records<br/>of library card accounts (FR-03-03)")
    mg{" "}
    d5{"Is there a new borrow record<br/>left to process?"}
    s12("Add the borrowed book to that<br/>reader's reading history (FR-03-03)")
    stop3@{ shape: fr-circ }
    e1@{ shape: odd, label: "Online book opened by a<br/>signed-in reader (AD-UC-03)" }
    s13("Add the book to the reader's reading history (FR-03-02)")
    stop4@{ shape: fr-circ }
  end

  start --> r1 --> m0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| c1 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| s2 --> s3 --> m1
  m1 --> d2
  d2 -->|"[Update reading status and progress]"| r2 --> s4 --> d3
  d3 -->|"[Yes]"| s5 --> s6 --> m1
  d3 -->|"[No]"| me
  d2 -->|"[Update reading preferences]"| r3 --> s7 --> d4
  d4 -->|"[Yes]"| s8 --> s9 --> m1
  d4 -->|"[No]"| me
  me --> s10 --> m1
  d2 -->|"[Finish]"| stop2

  t1 -->|"Daily loan records sync finished"| s11 --> mg --> d5
  d5 -->|"[Yes]"| s12 --> mg
  d5 -->|"[No]"| stop3

  e1 --> s13 --> stop4
```

Reading notes:

- The activity has three starts:
  - the initial node starts the reader's own flow;
  - the hourglass `t1` is a **time event**: when the daily loan sync finishes, the history is filled
    from the new borrow records with no person involved;
  - the notched flag `e1` is an **accept event**: it waits for the signal that a signed-in reader
    opened an online book in AD-UC-03.
- `s13` is the same step as `s5` in AD-UC-03, seen from the history side. It runs once per opening;
  it is not a second entry.
- `m1` is the merge every reader update comes back through, so the reader can make several updates
  before choosing Finish. `me` gathers both kinds of rejected update into one error action (`s10`),
  which returns to `m1`: a rejected update does not end the activity.
- The loop `d5 [Yes] → s12 → mg` handles one borrow record at a time.
- v1.1 adds `t1`, `s11`, `d5`, `s12`, `e1` and `s13`, so the diagram now covers all six FRs whose
  W1 source trace names UC-07.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Open reading history and preferences | FR-03-01 |
| s0 | Action | Check the reader's session | FR-04-08 |
| d0 | Decision | Valid session? | FR-04-08 |
| s1 | Action | Deny access | FR-04-08 |
| d1 | Decision (Reader) | Sign in now? | FR-04-08 |
| c1 | Call (Reader) | Sign in (UC-11) | FR-04-01 |
| s2 | Action | Retrieve the reader's Reading history & preferences | FR-03-01 |
| s3 | Action | Display the reading history with reading status | FR-03-01 |
| d2 | Decision (Reader) | What does the reader do? | FR-03-04, FR-03-05 |
| r2 | Action (Reader) | Submit the reading status and progress of a book | FR-03-04 |
| s4 | Action | Check that the status is Reading or Finished and the progress is between 0 and 100 percent | FR-03-04 |
| d3 | Decision | Does the update pass the check? | FR-03-04, FR-03-22 |
| s5 | Action | Save the reading status and progress | FR-03-04 |
| s6 | Action | Display the updated reading history | FR-03-01 |
| r3 | Action (Reader) | Submit updated reading preferences | FR-03-05 |
| s7 | Action | Validate the reading preferences | FR-03-05 |
| d4 | Decision | Do the preferences pass the validation? | FR-03-05, FR-03-22 |
| s8 | Action | Save the preferences to the reader's profile | FR-03-05 |
| s9 | Action | Display the updated preferences | FR-03-05 |
| s10 | Action | Reject the update, keep the saved data and display an error message | FR-03-22 |
| t1 | Time event | Daily loan records sync finished | FR-03-03 (sync itself: FR-04-10) |
| s11 | Action | Find the new borrow records of library card accounts | FR-03-03 |
| d5 | Decision | Is there a new borrow record left to process? | FR-03-03 |
| s12 | Action | Add the borrowed book to that reader's reading history | FR-03-03 |
| e1 | Accept event | Online book opened by a signed-in reader (AD-UC-03) | FR-03-02 |
| s13 | Action | Add the book to the reader's reading history | FR-03-02 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the reader is not signed in | they open reading history and decline to sign in | access is denied; nothing is shown |
| d0 [No] → d1 [Yes] | the reader is not signed in | they sign in with card 0012345 | the session is checked again and the reading history is shown |
| d0 [Yes] | the signed-in reader has 3 history entries | they open reading history | the 3 entries are shown with their reading status |
| d2 [Update reading status and progress] → d3 [Yes] | "Principles of Economics" is in the history as Reading, 20 percent | the reader submits Reading, 65 percent | the entry shows Reading, 65 percent |
| d3 [No] | the same entry is Reading, 20 percent | the reader submits progress 120 percent | the update is rejected, the entry stays at 20 percent and an error message is shown |
| d2 [Update reading preferences] → d4 [Yes] | the reader has no preferences | they choose the subjects Economics and Marketing | the preferences are saved and shown |
| d4 [No] | the reader's preferences are Economics | they submit a subject that is not in the subject list | the update is rejected, Economics stays saved and an error message is shown |
| d2 [Finish] | the history is shown | the reader leaves the page | the activity ends |
| t1 → d5 [Yes] | the 02:00 loan sync brought 2 new borrow records: card 0012345 borrowed "Principles of Economics", card 0067890 borrowed "Marketing Management" | the sync finishes | each book is added to the history of its card holder, one entry each, with status Reading, 0 percent |
| d5 [No] | the loan sync brought no new borrow record | the sync finishes | no history entry is added |
| e1 (no decision) | reader 0012345 is signed in | they open "Digital Marketing Basics" from the Online results in UC-03 | the book is added to reader 0012345's reading history with status Reading, 0 percent |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Reading history entry | Reading, Finished (written by `s5`); entries added by `s12` and `s13` start as Reading, 0 percent (question 1) |
| Reading preferences | no state values; saved by `s8` |
| Reader loan records (EIF) | none written; read by `s11` |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List. The time-event and accept-event parts have no
screen.

| Reader action | Screen ID |
|---|---|
| Open reading history and preferences (r1) | S-F03-02 (from a link in the existing OPAC personal area) |
| Sign in now? (d1) | S-F03-02 (modal M-F00-01 "Sign in to continue?") |
| Sign in (UC-11) (c1) | S-F00-01 → S-F00-02, then back to S-F03-02 |
| What does the reader do? (d2), Submit the reading status and progress of a book (r2), Submit updated reading preferences (r3) | S-F03-02 |
| See the updated reading history or preferences (s6, s9) | S-F03-02 (success state) |
| See the error message (s10) | S-F03-02 (error state, saved data kept) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | what reading status does an automatic entry (`s12`, `s13`) get? FR-03-02 and FR-03-03 do not say. | No (decided) | Decided 2026-11-04 (default adopted): Reading, 0 percent, until the reader changes it. |
| 2 | if a reader borrows the same book again, is a second history entry added? | No (decided) | Decided 2026-11-04 (default adopted): Yes, one entry per borrow record, as FR-03-03 is written; merging repeats would need a new FR. |
| 3 | what does "validate the reading preferences" check (FR-03-05)? | No (decided) | Decided 2026-11-04 (default adopted): Every chosen subject must exist in the synced catalogue subject list. |
| 4 | may a book be Finished with progress below 100 percent? | No (decided) | Decided 2026-11-04 (default adopted): Yes; it is saved as entered. |
| 5 | Resolved 2026-11-04: the `e1` part depends on online books opening on the current OPAC through a link from this platform (AD-UC-03 open question 1). | No (resolved) | Confirmed by the team. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-07 appears in the diagram | Pass (6 of 6 W1 rows whose source trace names UC-07) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
