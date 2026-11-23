# Activity Diagram: AD-UC-05 View book reviews

| Field | Value |
|---|---|
| AD ID | AD-UC-05 |
| Use case | UC-05 View book reviews |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flow "Reviews from other readers") · Use Case Diagram (UC-05, extended by Report a review UC-14) · Sequence: [SD-UC-05](../system_design/sequence_diagram/sd_uc_05.md) · W0 Table 1 (no login), Table 4 (Book review, ILF) · W1 rows FR-02-02, FR-02-13, FR-02-15 |
| Trigger | The reader asks to see the reviews of a book |
| Preconditions | None: no sign-in is needed to read reviews (W0 Table 1). |
| Success end state | The reader has read the reviews one page at a time, without any removed review, and either finishes or goes on to report a review (UC-14) or to write, edit or delete own review (UC-04). |
| Failure end state | The book is not found: the request ends without a review list and the reader sees that there are no reviews to show (FR-02-15). A book with no reviews yet shows the same empty message, and the reader can write the first review (UC-04). |
| FRs covered | FR-02-02, FR-02-13, FR-02-15; FR-02-09 through the call to UC-14; FR-02-01, FR-02-03, FR-02-04 through the calls to UC-04 |
| Business rules applied | Removed reviews are never shown (FR-02-13). Reviews are shown one page at a time and the next page is offered only if more reviews exist (FR-02-02). |
| Version / status | v1.2 · Draft |
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
    c2[["Write a review (UC-04) (FR-02-01)"]]
    c3[["Edit own review (UC-04) (FR-02-03)"]]
    c4[["Delete own review (UC-04) (FR-02-04)"]]
    m4{" "}
    stop2@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
    stop4@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Find the book (FR-02-02)")
    d1{"Is the book found?"}
    s2("Find the reviews of the book (FR-02-02)")
    s3("Leave out reviews removed from public display (FR-02-13)")
    d2{"Are there reviews to show?"}
    s4("End the request without a review list and show<br/>that there are no reviews to show (FR-02-15)")
    s8("Show that the book has no reviews yet<br/>and invite the first review (FR-02-15)")
    m1{" "}
    s5("Take the next page of reviews (FR-02-02)")
    s6("Display the page of reviews (FR-02-02)")
    d3{"Are there more pages after this one?"}
    s7("Offer the next page (FR-02-02)")
    m3{" "}
    stop1@{ shape: fr-circ }
  end

  start --> r1 --> s1 --> d1
  d1 -->|"[No]"| s4 --> stop1
  d1 -->|"[Yes]"| s2 --> s3 --> d2
  d2 -->|"[No]"| s8 --> m3
  d2 -->|"[Yes]"| m1 --> s5 --> s6 --> d3
  d3 -->|"[Yes]"| s7 --> m3
  d3 -->|"[No]"| m3
  m3 --> d4
  d4 -->|"[Next page offered and wanted]"| r2 --> m1
  d4 -->|"[Report a review]"| c1 --> stop2
  d4 -->|"[Write a review]"| c2 --> m4
  d4 -->|"[Edit own review]"| c3 --> m4
  d4 -->|"[Delete own review]"| c4 --> m4
  m4 --> stop4
  d4 -->|"[Finish]"| stop3
```

Reading notes:

- A book that is not found ends at `s4`. A book with no reviews yet goes on through `s8` to `d4`,
  because S-F02-01 keeps the review editor there and invites the first review.
- The paging loop comes back through `m1`. The guard `[Next page offered and wanted]` can only be
  true after `s7` has offered a next page, and `[Report a review]`, `[Edit own review]` and
  `[Delete own review]` only when such a review is on the page, so the guards of `d4` do not overlap.
- `c1` is a call to UC-14; reporting is drawn in AD-UC-14. `c2`, `c3` and `c4` call UC-04 at the
  chosen action, as in AD-UC-06; they back the usage-flow arrow UC-05 to UC-04 (L8-17).

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
| s8 | Action | Show that the book has no reviews yet and invite the first review | FR-02-15 |
| s5 | Action | Take the next page of reviews | FR-02-02 |
| s6 | Action | Display the page of reviews | FR-02-02 |
| d3 | Decision | Are there more pages after this one? | FR-02-02 |
| s7 | Action | Offer the next page | FR-02-02 |
| d4 | Decision (Reader) | What does the reader do next? | FR-02-02, FR-02-09, FR-02-01, FR-02-03, FR-02-04 |
| r2 | Action (Reader) | Ask for the next page of reviews | FR-02-02 |
| c1 | Call (Reader) | Report a review (UC-14) | FR-02-09 |
| c2 | Call (Reader) | Write a review (UC-04) | FR-02-01 |
| c3 | Call (Reader) | Edit own review (UC-04) | FR-02-03 |
| c4 | Call (Reader) | Delete own review (UC-04) | FR-02-04 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [No] | book ID 99999 is not in the catalogue | the reader asks for its reviews | no review list is shown and a one-line message says there are no reviews to show |
| d1 [Yes] → d2 [No] | the book has 2 reviews, both Removed | the reader asks for its reviews | no review list is shown, a one-line message says there are no reviews to show, and the reader can write the first review |
| d2 [Yes] → d3 [Yes] | the book has 25 published reviews and a page holds 10 | the reader asks for its reviews | reviews 1 to 10 are shown and a next page is offered |
| d3 [No] | the book has 7 published reviews | the reader asks for its reviews | all 7 are shown and no next page is offered |
| d4 [Next page offered and wanted] | page 1 of 3 is shown | the reader asks for the next page | reviews 11 to 20 are shown |
| d4 [Report a review] | a page of reviews is shown | the reader selects Report on review #91 | the flow continues in UC-14 |
| d4 [Write a review] | the book has no reviews yet | the reader writes the first review | the flow continues in UC-04 at Write |
| d4 [Edit own review] | the reader has review #88 on this book | the reader chooses Edit on #88 | the flow continues in UC-04 at Edit |
| d4 [Delete own review] | the reader has review #88 on this book | the reader chooses Delete on #88 | the flow continues in UC-04 at Delete |
| d4 [Finish] | a page of reviews is shown | the reader leaves the page | the activity ends |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Review | Published (read), Removed (read and left out by `s3`) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Ask to see the reviews of a book (r1) | Existing OPAC Book Detail "Reviews" (entry point, outside the product) → S-F02-01 |
| What does the reader do next? (d4), Ask for the next page of reviews (r2) | S-F02-01 |
| Report a review (UC-14) (c1) | S-F02-01 (Report on a review; see AD-UC-14) |
| Write a review (c2), Edit own review (c3), Delete own review (c4) (UC-04) | S-F02-01 (review panel; delete confirms in M-F02-01-01) |
| See that there are no reviews to show (s4), or that the book has no reviews yet (s8) | S-F02-01 (empty state) |

## 6. Open questions

None. Decisions: see [decision_index.md](../project_brief/decision_index.md#ad-uc-05).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-05 appears in the diagram | Pass (3 of 3 W1 rows whose source trace names UC-05) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| v1.2: calls `c2`, `c3`, `c4` to UC-04 (L8-17), `s8`, merge `m4`, guards on all `d4` flows | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| Renders after v1.2 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
