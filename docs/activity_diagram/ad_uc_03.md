# Activity Diagram: AD-UC-03 Filter books by access format (online, physical or both)

| Field | Value |
|---|---|
| AD ID | AD-UC-03 |
| Use case | UC-03 Filter books by access format (online, physical or both) |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flows "Filters queries", "Reading format"; Library Internal System flow "Book catalog & availability") · Use Case Diagram (UC-03) · Sequence: [SD-UC-03](../system_design/sequence_diagram/sd_uc_03.md) · W0 Table 3 (FR-03-14 and FR-03-15 cut; no viewer or download on this platform), Table 4 (Online book read log, ILF; Reading history & preferences, ILF) · W1 rows FR-03-12, FR-03-23, FR-03-13, FR-03-02 |
| Trigger | The reader opens the access-format filter |
| Preconditions | No sign-in is needed (W0 Table 1). The catalogue, with the access format of each book, has been synced (FR-04-09). |
| Success end state | The reader sees the books in the chosen access format, each with its access-format label. Every online book the reader opened from the results is recorded in the anonymous read log and, for a signed-in reader, in their reading history. |
| Failure end state | No book matches: the reader is told no books were found and may choose another format. |
| FRs covered | FR-03-12, FR-03-23, FR-03-13, FR-03-02; FR-01-01 through the call to UC-01 |
| Business rules applied | Three choices only: Online, Physical or Both (FR-03-12). An empty result invites another choice instead of ending the search (FR-03-23). Every online-book read is logged without any reader identity (FR-03-13). Only a signed-in library card reader gets a history entry (FR-03-02). The book itself opens on the current OPAC; this platform builds no viewer or download (W0 Table 3). Results are shown 20 per page; choosing another access format returns to page 1 (FR-03-12; D9, D14, D33). |
| Version / status | v1.4 · Draft |
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
    r1("Open the access-format filter (FR-03-12)")
    m1{" "}
    r2("Choose an access format:<br/>Online, Physical or Both (FR-03-12)")
    d2{"What does the reader do next?"}
    r3("Open an online book from the results (FR-03-13)")
    r4("Open another page of the results (FR-03-12)")
    c1[["View book shelf location (UC-01) (FR-01-01)"]]
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Retrieve the books in the selected access format (FR-03-12)")
    d1{"Are there matching books?"}
    s2("Display the matching books with their<br/>access-format labels, 20 per page (FR-03-12)")
    s3("Display that no books were found (FR-03-23)")
    m2{" "}
    s4("Record the book and the time of the read<br/>without any reader identity (FR-03-13)")
    d3{"Is the reader signed in<br/>with a library card?"}
    s5("Add the book to the reader's reading history (FR-03-02)")
    s6("Show that page of the results (FR-03-12)")
  end

  start --> r1 --> m1 --> r2 --> s1 --> d1
  d1 -->|"[Yes]"| s2 --> m2
  d1 -->|"[No]"| s3 --> m2
  m2 --> d2
  d2 -->|"[Choose another access format]"| m1
  d2 -->|"[Open another page]"| r4 --> s6 --> m2
  d2 -->|"[Open an online book]"| r3 --> s4 --> d3
  d3 -->|"[Yes]"| s5 --> m2
  d3 -->|"[No]"| m2
  d2 -->|"[Open a physical book]"| c1 --> stop2
  d2 -->|"[Finish]"| stop1
```

Reading notes:

- `m1` is the merge the reader comes back through to choose another format. `m2` gathers the
  results and the online-book branch before the reader's next choice `d2`, so the reader can open
  several online books one after another.
- `r3` hands the reader over to the online book on the current OPAC (W0 Table 3). The platform only
  records that the book was opened: `s4` for everyone, without identity (FR-03-13), and `s5` for a
  signed-in reader's history (FR-03-02). The current OPAC opens and downloads online books
  (AD-UC-03 Q1).
- `s5` is the same step as `s13` in AD-UC-07, where it is drawn from the reading history side as an
  accept event. It runs once per opening; it is not a second entry.
- v1.1 adds `r3`, `s4`, `d3` and `s5`, so the diagram now covers all four FRs whose W1 source trace
  names UC-03.
- v1.3 adds the call `c1`: from a physical book in the results the reader opens the book on the
  existing OPAC Book Detail and asks for its shelf location, which is UC-01 (drawn once in AD-UC-01,
  not copied here). It backs the usage-flow arrow UC-03 to UC-01.
- v1.4 adds paging: `r4` → `s6` shows another page of 20 books and comes back through `m2` (D9,
  D33). Choosing another format goes back through `m1` and starts at page 1 (D14).

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Open the access-format filter | FR-03-12 |
| r2 | Action (Reader) | Choose an access format: Online, Physical or Both | FR-03-12 |
| s1 | Action | Retrieve the books in the selected access format | FR-03-12 |
| d1 | Decision | Are there matching books? | FR-03-23 |
| s2 | Action | Display the matching books with their access-format labels, 20 per page | FR-03-12 |
| s3 | Action | Display that no books were found | FR-03-23 |
| d2 | Decision (Reader) | What does the reader do next? | FR-03-12, FR-03-23, FR-03-13, FR-01-01 |
| r4 | Action (Reader) | Open another page of the results | FR-03-12 |
| s6 | Action | Show that page of the results | FR-03-12 |
| r3 | Action (Reader) | Open an online book from the results | FR-03-13 |
| c1 | Call (Reader) | View book shelf location (UC-01) | FR-01-01 |
| s4 | Action | Record the book and the time of the read without any reader identity | FR-03-13 |
| d3 | Decision | Is the reader signed in with a library card? | FR-03-02 |
| s5 | Action | Add the book to the reader's reading history | FR-03-02 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [Yes] | the catalogue holds 120 physical books and 45 online books | the reader chooses Online | 45 books are listed, each labelled "Online" |
| d1 [No] | the catalogue holds no book with both a physical copy and an online version | the reader chooses Both | the page says no books were found |
| d2 [Choose another access format] | "no books were found" is shown for Both | the reader chooses Physical | the physical books are listed with the label "Physical" |
| d2 [Open another page] | the Physical results hold 45 books and page 1 is shown | the reader chooses «Trang sau» | books 21 to 40 are shown |
| d2 [Choose another access format] (from page 2) | page 2 of the Physical results is shown | the reader chooses Online | the Online results are shown from page 1 |
| d2 [Open an online book] → d3 [Yes] | reader 0012345 is signed in and the Online results are shown | they open "Digital Marketing Basics" | the read log gets one row (book, time, no reader identity) and the book is added to reader 0012345's reading history |
| d3 [No] | the reader is not signed in and the Online results are shown | they open "Digital Marketing Basics" | the read log gets one row (book, time, no reader identity); no history entry is made |
| d2 [Open a physical book] | the Physical results are shown | the reader opens "Principles of Economics" | the book opens on the existing OPAC Book Detail and UC-01 starts (shelf location) |
| d2 [Finish] | a result list is shown | the reader stops filtering | the activity ends; the list stays on screen |

## 4. Object states used

| Object | States in this diagram | Note |
|---|---|---|
| Book catalogue (EIF) | none written | Access formats are read only (W0 Table 4) |
| Online book read log entry | Recorded (written by `s4`) | Holds book and time only, no reader identity |
| Reading history entry | added by `s5` | Starts as Reading, 0 percent (AD-UC-07 Q1) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Open the access-format filter (r1) | S-F03-01 (from a link on the existing OPAC search results) |
| Choose an access format: Online, Physical or Both (r2), What does the reader do next? (d2) | S-F03-01 |
| Open another page of the results (r4), see that page (s6) | S-F03-01 (Pagination) |
| See that no books were found (s3) | S-F03-01 (empty state) |
| Open an online book from the results (r3) | S-F03-01 → exit: online book on the current OPAC (outside the product) |
| View book shelf location (UC-01) (c1) | S-F03-01 → existing OPAC Book Detail → S-F01-01 |

## 6. Open questions

None. Decisions: see [decision_index.md](../project_brief/decision_index.md#ad-uc-03).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.3.0, swimlane-beta) | Pass (re-checked after the new calls) | AI assistant | 2026-11-08 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-03 appears in the diagram | Pass (4 of 4 non-Won't W1 rows whose source trace names UC-03; FR-03-14, FR-03-15 are Won't) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| v1.4: paging `r4`, `s6` through merge `m2`, each new action cites one FR | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| Renders after v1.4 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
