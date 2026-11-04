# Activity Diagram: AD-UC-05 View book reviews

| Field | Value |
|---|---|
| AD ID | AD-UC-05 |
| Use case | UC-05 View book reviews |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flow "Reviews from other readers") · Use Case Diagram (UC-05, extended by Report a review UC-14) · Sequence: User Review Interaction Flow (UC-05 with UC-04) · W0 Table 1 (no login), Table 4 (Book review, ILF) · W1 rows FR-02-02, FR-02-13, FR-02-15 |
| Trigger | The reader asks to see the reviews of a book |
| Preconditions | None: no sign-in is needed to read reviews (W0 Table 1). |
| Success end state | The reader has read the reviews one page at a time, without any removed review, and either finishes or goes on to report a review (UC-14). |
| Failure end state | The book is not found or has no reviews: the request ends without a review list and the reader sees that there are no reviews to show (FR-02-15). |
| FRs covered | FR-02-02, FR-02-13, FR-02-15; FR-02-09 through the call to UC-14 |
| Business rules applied | Removed reviews are never shown (FR-02-13). Reviews are shown one page at a time and the next page is offered only if more reviews exist (FR-02-02). |
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
    r1("Ask to see the reviews of a book (FR-02-02)")
    d4{"What does the reader do next?"}
    r2("Ask for the next page of reviews (FR-02-02)")
    c1[["Report a review (UC-14) (FR-02-09)"]]
    stop2@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Find the book (FR-02-02)")
    d1{"Is the book found?"}
    s2("Find the reviews of the book (FR-02-02)")
    s3("Leave out reviews removed from public display (FR-02-13)")
    d2{"Are there reviews to show?"}
    mn{" "}
    s4("End the request without a review list and show<br/>that there are no reviews to show (FR-02-15)")
    m1{" "}
    s5("Take the next page of reviews (FR-02-02)")
    s6("Display the page of reviews (FR-02-02)")
    d3{"Are there more pages after this one?"}
    s7("Offer the next page (FR-02-02)")
    m3{" "}
    stop1@{ shape: fr-circ }
  end

  start --> r1 --> s1 --> d1
  d1 -->|"[No]"| mn
  d1 -->|"[Yes]"| s2 --> s3 --> d2
  d2 -->|"[No]"| mn
  mn --> s4 --> stop1
  d2 -->|"[Yes]"| m1 --> s5 --> s6 --> d3
  d3 -->|"[Yes]"| s7 --> m3
  d3 -->|"[No]"| m3
  m3 --> d4
  d4 -->|"[Next page offered and wanted]"| r2 --> m1
  d4 -->|"[Report a review]"| c1 --> stop2
  d4 -->|"[Finish]"| stop3
```

Reading notes:

- `mn` gathers the two "nothing to show" cases (book not found, no reviews) into one end action.
- The paging loop comes back through `m1`. The guard `[Next page offered and wanted]` can only be
  true after `s7` has offered a next page, so the three guards of `d4` do not overlap.
- `c1` is a call to UC-14; reporting is drawn in AD-UC-14.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Ask to see the reviews of a book | FR-02-02 |
| s1 | Action | Find the book | FR-02-02 |
| d1 | Decision | Is the book found? | FR-02-15 |
| s2 | Action | Find the reviews of the book | FR-02-02 |
| s3 | Action | Leave out reviews removed from public display | FR-02-13 |
| d2 | Decision | Are there reviews to show? | FR-02-15 |
| s4 | Action | End the request without a review list and show that there are no reviews to show | FR-02-15 |
| s5 | Action | Take the next page of reviews | FR-02-02 |
| s6 | Action | Display the page of reviews | FR-02-02 |
| d3 | Decision | Are there more pages after this one? | FR-02-02 |
| s7 | Action | Offer the next page | FR-02-02 |
| d4 | Decision (Reader) | What does the reader do next? | FR-02-02, FR-02-09 |
| r2 | Action (Reader) | Ask for the next page of reviews | FR-02-02 |
| c1 | Call (Reader) | Report a review (UC-14) | FR-02-09 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [No] | book ID 99999 is not in the catalogue | the reader asks for its reviews | no review list is shown and a one-line message says there are no reviews to show |
| d1 [Yes] → d2 [No] | the book has 2 reviews, both Removed | the reader asks for its reviews | no review list is shown and a one-line message says there are no reviews to show |
| d2 [Yes] → d3 [Yes] | the book has 25 published reviews and a page holds 10 | the reader asks for its reviews | reviews 1 to 10 are shown and a next page is offered |
| d3 [No] | the book has 7 published reviews | the reader asks for its reviews | all 7 are shown and no next page is offered |
| d4 [Next page offered and wanted] | page 1 of 3 is shown | the reader asks for the next page | reviews 11 to 20 are shown |
| d4 [Report a review] | a page of reviews is shown | the reader selects Report on review #91 | the flow continues in UC-14 |
| d4 [Finish] | a page of reviews is shown | the reader leaves the page | the activity ends |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Review | Published (read), Removed (read and left out by `s3`) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Ask to see the reviews of a book, Ask for the next page | (Lesson 8) |
| Report a review (goes to UC-14) | (Lesson 8) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | how many reviews are on one page, and in what order? | No (decided) | Decided 2026-11-04 (default adopted): 10 per page, newest first. |
| 2 | FR-02-15 says the request ends "without displaying a review list". Does the reader still see a short message such as "No reviews yet"? | No (decided) | Decided 2026-11-04 (default adopted): Yes, a one-line message that there are no reviews to show; FR-02-15 wording updated in W1 and `s4` updated here. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-05 appears in the diagram | Pass (3 of 3 W1 rows whose source trace names UC-05) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
