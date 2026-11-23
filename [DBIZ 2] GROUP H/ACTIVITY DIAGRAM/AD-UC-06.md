# Activity Diagram: AD-UC-06 Access book information and reviews via QR code

| Field | Value |
|---|---|
| AD ID | AD-UC-06 |
| Use case | UC-06 Access book information and reviews via QR code (physical books; reviews via UC-04) |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flows "QR scan", "Book info & availability", "Reviews from other readers") · Use Case Diagram (UC-06, with UC-04 for reviews) · Sequence: [SD-UC-06](../SEQUENCE%20DIAGRAM/SD-UC-06.md) · W0 Table 3 (no QR codes for online-only books), Table 4 (Book QR codes, ILF) · W1 rows FR-02-05, FR-02-06, FR-02-16, FR-02-22 |
| Trigger | The reader scans the QR code on a physical book |
| Preconditions | The book has a QR code (FR-02-07) and a printed label (UC-10). No sign-in is needed to view the page. |
| Success end state | The information and review page of the book is open, the scan count of the QR code is one higher, and the reader has either acted on a review (UC-04) or not. |
| Failure end state | The QR code is linked to no book: the reader sees that the book cannot be found, no scan count changes (FR-02-16), and the link «Về OPAC» leads to the OPAC main menu (D37). |
| FRs covered | FR-02-05, FR-02-06, FR-02-16, FR-02-22; FR-02-02 (next page of reviews, rule of UC-05); FR-02-01, FR-02-03, FR-02-04 through the calls to UC-04 |
| Business rules applied | Only physical books carry QR codes (W0 Table 3, FR-02-07). A QR code linked to no book never raises a scan count (FR-02-16). Reviews are shown 10 per page, as in UC-05; «Xem thêm đánh giá» is offered while more published reviews remain (FR-02-02; D6). |
| Version / status | v1.3 · Draft |
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
    r1("Scan the QR code on a physical book (FR-02-05)")
    mD{" "}
    d2{"What does the reader do next?"}
    r2("Ask for the next page of reviews (FR-02-02)")
    c1[["Write a review (UC-04) (FR-02-01)"]]
    c2[["Edit own review (UC-04) (FR-02-03)"]]
    c3[["Delete own review (UC-04) (FR-02-04)"]]
    m1{" "}
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Find the book linked to the QR code (FR-02-05)")
    d1{"Is the QR code linked to a book?"}
    s2("Display that the book cannot be found (FR-02-16)")
    f1@{ shape: fork }
    s3("Increase the scan count of the QR code by one (FR-02-06)")
    s4("Open the information and review page of the book (FR-02-05)")
    j1@{ shape: join }
    s5("Show the next 10 published reviews (FR-02-02)")
    mS{" "}
    s6("Show each reviewer as the full name<br/>or «Bạn đọc ẩn danh» (FR-02-22)")
    stop1@{ shape: fr-circ }
  end

  start --> r1 --> s1 --> d1
  d1 -->|"[No]"| s2 --> stop1
  d1 -->|"[Yes]"| f1
  f1 --> s3 --> j1
  f1 --> s4 --> j1
  j1 --> mS --> s6 --> mD --> d2
  d2 -->|"[Next page offered and wanted]"| r2 --> s5 --> mS
  d2 -->|"[Write a review]"| c1 --> m1
  d2 -->|"[Edit own review]"| c2 --> m1
  d2 -->|"[Delete own review]"| c3 --> m1
  d2 -->|"[Finish]"| m1
  m1 --> stop2
```

Reading notes:

- The fork `f1` and join `j1` say that counting the scan and opening the page have no required
  order. The reader acts on the page only after both are done.
- `c1`, `c2` and `c3` call UC-04 at the chosen action. Sign-in, text checks and confirmations are
  drawn once in AD-UC-04, not repeated here.
- The page shows reviews with the same rules as UC-05: one page at a time, removed reviews left out.
- S-F02-02 has «Xem thêm đánh giá», as S-F02-01 (D6). `s4` opens the page with the first 10
  published reviews; `r2` → `s5` shows the next 10 and comes back through the merges `mS` and `mD`. The
  guard "[Next page offered and wanted]" holds only while more published reviews remain (FR-02-02).
- `s6` shows each review under the full name or «Bạn đọc ẩn danh» (FR-02-22). The choice itself is
  made in UC-04.
- After `s2` there is no book to open, so the error state offers the link «Về OPAC» to the existing
  OPAC main menu (D37). It only leaves the page, so it is not drawn as a step.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Scan the QR code on a physical book | FR-02-05 |
| s1 | Action | Find the book linked to the QR code | FR-02-05 |
| d1 | Decision | Is the QR code linked to a book? | FR-02-16 |
| s2 | Action | Display that the book cannot be found | FR-02-16 |
| f1 | Fork | (two parallel flows) | FR-02-05, FR-02-06 |
| s3 | Action | Increase the scan count of the QR code by one | FR-02-06 |
| s4 | Action | Open the information and review page of the book | FR-02-05 |
| j1 | Join | (both flows done) | FR-02-05, FR-02-06 |
| d2 | Decision (Reader) | What does the reader do next? | FR-02-02, FR-02-01, FR-02-03, FR-02-04 |
| r2 | Action (Reader) | Ask for the next page of reviews | FR-02-02 |
| s5 | Action | Show the next 10 published reviews | FR-02-02 |
| s6 | Action | Show each reviewer as the full name or «Bạn đọc ẩn danh» | FR-02-22 |
| c1 | Call (Reader) | Write a review (UC-04) | FR-02-01 |
| c2 | Call (Reader) | Edit own review (UC-04) | FR-02-03 |
| c3 | Call (Reader) | Delete own review (UC-04) | FR-02-04 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [No] | QR code QR-000777 is linked to no book | the reader scans it | the page says the book cannot be found and offers «Về OPAC»; no scan count changes |
| d1 [Yes] | QR code QR-000123 is linked to "Principles of Economics" and has scan count 41 | the reader scans it | the book's information and review page opens and the scan count becomes 42 |
| s6 | a review on the book was posted anonymously | the reader opens the page | that review is shown under «Bạn đọc ẩn danh»; other reviews show the full name |
| d2 [Write a review] | the page of "Principles of Economics" is open | the reader chooses Write review | the flow continues in UC-04 at Write |
| d2 [Edit own review] | the reader has review #88 on this book | the reader chooses Edit on #88 | the flow continues in UC-04 at Edit |
| d2 [Delete own review] | the reader has review #88 on this book | the reader chooses Delete on #88 | the flow continues in UC-04 at Delete |
| d2 [Next page offered and wanted] | "Principles of Economics" has 23 published reviews and the page shows the first 10 | the reader chooses «Xem thêm đánh giá» | reviews 11–20 are shown and «Xem thêm đánh giá» is still offered; after the next choice reviews 21–23 are shown and it is no longer offered |
| d2 [Finish] | the page is open | the reader only reads and leaves | the activity ends; the scan is still counted |

## 4. Object states used

| Object | States in this diagram | Note |
|---|---|---|
| QR code | Generated (read) | `s3` raises the scan count, a counter rather than a state |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Scan the QR code on a physical book (r1) | Phone camera (entry point, outside the product) → S-F02-02 |
| See that the book cannot be found (s2) | S-F02-02 (error state, with the link «Về OPAC» to the OPAC main menu) |
| What does the reader do next? (d2), Write a review (UC-04) (c1), Edit own review (UC-04) (c2) | S-F02-02 (review panel, as in AD-UC-04) |
| Ask for the next page of reviews (r2), see the next 10 reviews (s5) | S-F02-02 (Load more button «Xem thêm đánh giá») |
| Delete own review (UC-04) (c3) | S-F02-02 (modal M-F02-01-01 "Delete your review?") |

## 6. Open questions

None. Decisions: see [decision-index.md](../EXTERNAL%20DESIGN/decision-index.md#ad-uc-06).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Pass (`f1` → `j1`; `j1` was drawn as a fork bar before and is now a join) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-06 appears in the diagram | Pass (4 of 4 W1 rows whose source trace names UC-06, with FR-02-22 since v1.3) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| v1.2 next-page branch (D6): guards on all `d2` flows, merge `mD` before `d2`, each new action cites one FR | Pass (checked by reading) | AI assistant | 2026-11-22 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| v1.3: `s6` (FR-02-22) through merge `mS`; invalid-QR way out noted | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| Renders after v1.3 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
