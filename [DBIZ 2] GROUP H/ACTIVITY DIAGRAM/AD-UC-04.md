# Activity Diagram: AD-UC-04 Write, edit and delete own book reviews

| Field | Value |
|---|---|
| AD ID | AD-UC-04 |
| Use case | UC-04 Write, edit and delete own book reviews |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flows "Reviews", "Reviews from other readers") · Use Case Diagram (UC-04, includes Sign in UC-11) · Sequence: User Review Interaction Flow (edit and delete), Book Review API Interaction (write, from a QR scan) · W0 Table 1 (login required), Table 4 (Book review, ILF) · W1 rows FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12, FR-04-08 |
| Trigger | The reader asks to write, edit or delete a review on a book |
| Preconditions | The book is in the synced catalogue. The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). |
| Success end state | The review is saved, replaced or removed from public display, and the reader sees a confirmation and the updated review list of the book (FR-02-12). |
| Failure end state | Nothing is saved: the text failed the check or the review is not the reader's own (error message, FR-02-11); or the reader cancelled the deletion; or the reader chose not to sign in. |
| FRs covered | FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12, FR-04-08; FR-04-01 through the call to UC-11 |
| Business rules applied | Review text is not empty, at most 2,000 characters, plain text (FR-02-01, FR-02-03). A reader edits or deletes only their own review (FR-02-03, FR-02-04, FR-02-11). Deletion needs a confirmation (FR-02-04). Review actions need a signed-in reader (FR-04-08). |
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
  subgraph RDR["Reader"]
    start@{ shape: sm-circ }
    r1("Request a review action on a book (FR-04-08)")
    d1{"Sign in now?"}
    c1[["Sign in (UC-11) (FR-04-01)"]]
    d2{"Which action?"}
    r2("Submit a new review text (FR-02-01)")
    r3("Submit an edited text of own review (FR-02-03)")
    r4("Choose own review to delete (FR-02-04)")
    d6{"Confirm the deletion?"}
    r5("Cancel the deletion (FR-02-04)")
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    m0{" "}
    s0("Check the reader's session (FR-04-08)")
    d0{"Valid session?"}
    s1("Deny the request (FR-04-08)")
    s2("Check the text: not empty, at most<br/>2,000 characters, plain text (FR-02-01)")
    d3{"Does the text pass the check?"}
    s3("Save the review against that book and that reader (FR-02-01)")
    d4{"Is it the reader's own review?"}
    s4("Check the edited text with the same rules (FR-02-03)")
    d5{"Does the text pass the check?"}
    s5("Replace the review text, keeping<br/>the link to the same book (FR-02-03)")
    d7{"Is it the reader's own review?"}
    s6("Remove the review from public display (FR-02-04)")
    me{" "}
    s7("Reject the action and show an error message (FR-02-11)")
    m2{" "}
    s8("Show a confirmation and the<br/>updated review list of the book (FR-02-12)")
    stop3@{ shape: fr-circ }
    stop4@{ shape: fr-circ }
  end

  start --> r1 --> m0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| c1 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| d2
  d2 -->|"[Write]"| r2 --> s2 --> d3
  d3 -->|"[Yes]"| s3 --> m2
  d3 -->|"[No]"| me
  d2 -->|"[Edit]"| r3 --> d4
  d4 -->|"[No]"| me
  d4 -->|"[Yes]"| s4 --> d5
  d5 -->|"[Yes]"| s5 --> m2
  d5 -->|"[No]"| me
  d2 -->|"[Delete]"| r4 --> d6
  d6 -->|"[No]"| r5 --> stop2
  d6 -->|"[Yes]"| d7
  d7 -->|"[Yes]"| s6 --> m2
  d7 -->|"[No]"| me
  me --> s7 --> stop3
  m2 --> s8 --> stop4
```

Reading notes:

- `c1` is a call to another use case (the rake symbol): sign-in is drawn once in AD-UC-11, not
  copied here. After sign-in the flow re-enters through the merge `m0` and the session is checked
  again.
- `me` gathers every rejection so one action (`s7`) shows the error; `m2` gathers every success so
  one action (`s8`) shows the confirmation.
- "Delete" removes the review from public display (state `Removed`); it is not erased from storage.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Request a review action on a book | FR-04-08 |
| s0 | Action | Check the reader's session | FR-04-08 |
| d0 | Decision | Valid session? | FR-04-08 |
| s1 | Action | Deny the request | FR-04-08 |
| d1 | Decision (Reader) | Sign in now? | FR-04-08 |
| c1 | Call (Reader) | Sign in (UC-11) | FR-04-01 |
| d2 | Decision (Reader) | Which action? | FR-02-01, FR-02-03, FR-02-04 |
| r2 | Action (Reader) | Submit a new review text | FR-02-01 |
| s2 | Action | Check the text: not empty, at most 2,000 characters, plain text | FR-02-01 |
| d3 | Decision | Does the text pass the check? | FR-02-01, FR-02-11 |
| s3 | Action | Save the review against that book and that reader | FR-02-01 |
| r3 | Action (Reader) | Submit an edited text of own review | FR-02-03 |
| d4 | Decision | Is it the reader's own review? | FR-02-03, FR-02-11 |
| s4 | Action | Check the edited text with the same rules | FR-02-03 |
| d5 | Decision | Does the text pass the check? | FR-02-03, FR-02-11 |
| s5 | Action | Replace the review text, keeping the link to the same book | FR-02-03 |
| r4 | Action (Reader) | Choose own review to delete | FR-02-04 |
| d6 | Decision (Reader) | Confirm the deletion? | FR-02-04 |
| r5 | Action (Reader) | Cancel the deletion | FR-02-04 |
| d7 | Decision | Is it the reader's own review? | FR-02-04, FR-02-11 |
| s6 | Action | Remove the review from public display | FR-02-04 |
| s7 | Action | Reject the action and show an error message | FR-02-11 |
| s8 | Action | Show a confirmation and the updated review list of the book | FR-02-12 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the reader is not signed in | they choose Write review and then decline to sign in | the request is denied and nothing is saved |
| d0 [No] → d1 [Yes] | the reader is not signed in | they choose Write review and sign in with card 0012345 | the session is checked again and the review form opens |
| d0 [Yes] → d2 [Write] → d3 [Yes] | a signed-in reader | they submit a 350-character plain-text review | the review is saved for that book and reader; a confirmation and the updated list are shown |
| d3 [No] | a signed-in reader | they submit a review of 2,001 characters | nothing is saved and an error message says the text is too long |
| d2 [Edit] → d4 [Yes] → d5 [Yes] | the reader owns review #88 on the book | they submit a new 500-character text | review #88 shows the new text, still on the same book; a confirmation is shown |
| d4 [No] | review #91 belongs to another reader | the reader sends an edit for #91 | nothing changes and an error message is shown |
| d5 [No] | the reader owns review #88 | they submit an empty text | review #88 keeps its old text and an error message is shown |
| d2 [Delete] → d6 [No] | the reader owns review #88 | they choose Delete and then Cancel | review #88 stays public; the activity ends |
| d6 [Yes] → d7 [Yes] | the reader owns review #88 | they choose Delete and confirm | review #88 is no longer shown publicly; a confirmation and the updated list are shown |
| d7 [No] | review #91 belongs to another reader | the reader sends a confirmed delete for #91 | review #91 stays public and an error message is shown |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Review | Published (written by `s3`, `s5`), Removed (written by `s6`) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Request a review action on a book (r1), Which action? (d2) | S-F02-01 (or S-F02-02 when reached by QR, UC-06) |
| Sign in now? (d1) | S-F02-01 / S-F02-02 (modal M-F00-01 "Sign in to continue?") |
| Sign in (UC-11) (c1) | S-F00-01 → S-F00-02, then back to S-F02-01 / S-F02-02 |
| Submit a new review text (r2), Submit an edited text of own review (r3), Choose own review to delete (r4) | S-F02-01 / S-F02-02 (review panel) |
| Confirm the deletion? (d6), Cancel the deletion (r5) | S-F02-01 / S-F02-02 (modal M-F02-01-01 "Delete your review?") |
| See the error message (s7) | S-F02-01 / S-F02-02 (error state) |
| See the confirmation and the updated review list (s8) | S-F02-01 / S-F02-02 (success state) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | may a reader write more than one review for the same book? | No (decided) | Decided 2026-11-04 (default adopted): Yes; FR-02-01 sets no limit. |
| 2 | is an edited review marked "edited" with a date? | No (decided) | Decided 2026-11-04 (default adopted): No marker in release 1. |
| 3 | how long is a removed review kept in storage? | No (decided) | Decided 2026-11-04 (default adopted): Kept with state Removed; no automatic purge in release 1. |
| 4 | FR-02-03 and FR-02-04 are Could. If they are cut, the Edit and Delete branches of `d2` are removed. | No (decided) | Decided 2026-11-04 (default adopted): Keep both branches until the release scope is fixed. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-04 appears in the diagram | Pass (5 of 5 W1 rows whose source trace names UC-04) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
