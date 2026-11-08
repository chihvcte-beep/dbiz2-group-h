# Activity Diagram: AD-UC-01 View book shelf location

| Field | Value |
|---|---|
| AD ID | AD-UC-01 |
| Use case | UC-01 View book shelf location |
| Feature | F-01 Book Location & Library Map |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader; flow "Shelf location & library map"; Library Internal System flow "Shelf placement, floors & rooms") · Use Case Diagram (UC-01) · Sequence: User Interface Flow (UC-01, UC-02) · W0 Table 1, Table 4 (Book placement & library layout, EIF) · W1 rows FR-01-01, FR-01-03, FR-01-06, FR-01-07, FR-01-09, FR-01-10 |
| Trigger | The reader opens a book's detail page and asks for its shelf location |
| Preconditions | None for the reader: no sign-in is needed (W0 Table 1). The catalogue and shelf placement have been synced from the Library Internal System (FR-04-09). |
| Success end state | The reader sees the floor, room and shelf code of the book. If they asked for it, the library map shows the book's room highlighted, with the shelf details still visible. |
| Failure end state | The reader is told why no shelf location can be shown (online-only book, or missing or inconsistent codes), or why the map cannot show the room (floor plan unavailable, room not on the plan). Shelf details already shown stay visible. |
| FRs covered | FR-01-01, FR-01-03, FR-01-06, FR-01-07, FR-01-09, FR-01-10 |
| Business rules applied | A shelf location is shown only for a book that has a physical copy and complete, consistent floor, room and shelf codes (FR-01-01, FR-01-06, FR-01-07). Shelf details stay visible whatever happens to the map (FR-01-03, FR-01-09, FR-01-10). |
| Version / status | v1.1 · Draft |
| Author | Owner A (F-01) |

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
    r1("Open a book's detail page and request its shelf location (FR-01-01)")
    d3{"View the book's room on the map?"}
    r2("Request the library map for the book's room (FR-01-03)")
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Retrieve the book's format and physical location data (FR-01-01)")
    d1{"Does the book have a physical copy?"}
    s2("Display that the book is available electronically<br/>and no physical shelf location applies (FR-01-06)")
    d2{"Are the floor, room and shelf codes<br/>complete and consistent?"}
    s3("Display that the shelf location is unavailable<br/>and direct the reader to library staff (FR-01-07)")
    s4("Display the floor, room and shelf code (FR-01-01)")
    s5("Retrieve the floor plan of the book's floor (FR-01-03)")
    d4{"Is the floor plan available and readable?"}
    s6("Keep the shelf details visible<br/>and display that the map is unavailable (FR-01-10)")
    d5{"Is the room code found on the floor plan?"}
    s7("Keep the shelf details visible and display that<br/>the room cannot be identified on the map (FR-01-09)")
    s8("Display the library map with the room highlighted,<br/>keeping the shelf details visible (FR-01-03)")
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
    stop4@{ shape: fr-circ }
    stop5@{ shape: fr-circ }
    stop6@{ shape: fr-circ }
  end

  start --> r1 --> s1 --> d1
  d1 -->|"[No]"| s2 --> stop1
  d1 -->|"[Yes]"| d2
  d2 -->|"[No]"| s3 --> stop2
  d2 -->|"[Yes]"| s4 --> d3
  d3 -->|"[No]"| stop3
  d3 -->|"[Yes]"| r2 --> s5 --> d4
  d4 -->|"[No]"| s6 --> stop4
  d4 -->|"[Yes]"| d5
  d5 -->|"[No]"| s7 --> stop5
  d5 -->|"[Yes]"| s8 --> stop6
```

Reading notes:

- The diagram has six activity final nodes, one for each way the flow can end. In UML an activity
  may have several final nodes; the first one reached ends the activity.
- `d3` is the reader's own choice. `d3 [No]` is a success end: the reader has the shelf code and
  does not need the map.
- The map branch (`r2` to `s8`) uses FR-01-03, which W4 moved to Could. If it is cut, the flow ends
  after `s4` and `d3` to `d5` are removed.

## 2. Node trace

Every action cites one requirement. Every decision cites the requirement that decides it.

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Open a book's detail page and request its shelf location | FR-01-01 |
| s1 | Action | Retrieve the book's format and physical location data | FR-01-01 |
| d1 | Decision | Does the book have a physical copy? | FR-01-01, FR-01-06 |
| s2 | Action | Display that the book is available electronically and no physical shelf location applies | FR-01-06 |
| d2 | Decision | Are the floor, room and shelf codes complete and consistent? | FR-01-01, FR-01-07 |
| s3 | Action | Display that the shelf location is unavailable and direct the reader to library staff | FR-01-07 |
| s4 | Action | Display the floor, room and shelf code | FR-01-01 |
| d3 | Decision (Reader) | View the book's room on the map? | FR-01-03 |
| r2 | Action (Reader) | Request the library map for the book's room | FR-01-03 |
| s5 | Action | Retrieve the floor plan of the book's floor | FR-01-03 |
| d4 | Decision | Is the floor plan available and readable? | FR-01-10 |
| s6 | Action | Keep the shelf details visible and display that the map is unavailable | FR-01-10 |
| d5 | Decision | Is the room code found on the floor plan? | FR-01-09 |
| s7 | Action | Keep the shelf details visible and display that the room cannot be identified on the map | FR-01-09 |
| s8 | Action | Display the library map with the room highlighted, keeping the shelf details visible | FR-01-03 |

## 3. Branches and acceptance tests

One row per outgoing branch of every decision. DBIZ3 turns each row into at least one test.

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [No] | the book "Digital Marketing Basics" exists only as an online PDF | the reader asks for its shelf location | the page says the book is available electronically and no shelf location applies; no floor, room or shelf code is shown |
| d1 [Yes] → d2 [No] | a physical book has floor 2 and shelf S-12 but no room code | the reader asks for its shelf location | the page says the shelf location is unavailable and tells the reader to ask library staff |
| d2 [Yes] → d3 [No] | a physical book is on floor 2, room R-204, shelf S-12 | the reader asks for its shelf location and does not open the map | "Floor 2 · Room R-204 · Shelf S-12" is shown and nothing else happens |
| d3 [Yes] → d4 [No] | the book is on floor 2, room R-204, shelf S-12, and the floor 2 plan file is missing | the reader asks to see the room on the map | "Floor 2 · Room R-204 · Shelf S-12" stays visible and a message says the map is unavailable |
| d4 [Yes] → d5 [No] | the book is in room R-299, and the floor 2 plan has no room R-299 | the reader asks to see the room on the map | the shelf details stay visible and a message says the room cannot be identified on the map |
| d5 [Yes] | the book is in room R-204, and the floor 2 plan has room R-204 | the reader asks to see the room on the map | the floor 2 map opens with R-204 highlighted and the shelf details still visible |

## 4. Object states used

| Object | States in this diagram | Note |
|---|---|---|
| Book placement & library layout (EIF) | none written | Read only; the platform never writes to it (W0 Table 4) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Open a book's detail page and request its shelf location (r1) | Existing OPAC Book Detail (entry point, outside the product) → S-F01-01 |
| See the floor, room and shelf code (s4) | S-F01-01 |
| See that the book is electronic only (s2), or that the shelf location is unavailable (s3) | S-F01-01 (message state) |
| View the book's room on the map? (d3), Request the library map for the book's room (r2) | S-F01-01 ("View on map") → S-F01-02 |
| See the library map with the room highlighted (s8) | S-F01-02 (success state, shelf details kept visible) |
| See that the map is unavailable (s6), or that the room cannot be identified on the map (s7) | S-F01-02 (error state, shelf details kept visible) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | a book with several physical copies on different shelves: which shelf location is shown? | No (decided) | Decided 2026-11-04 (default adopted): Every copy's floor, room and shelf code is shown, one line per copy. |
| 2 | does "direct the reader to library staff" name a place, such as the information desk on each floor? | No (decided) | Decided 2026-11-04 (default adopted): A fixed message names the information desk on the ground floor. |
| 3 | FR-01-03 is Could after W4. If the release cuts it, is UC-01 still accepted with the shelf code only? | No (decided) | Decided 2026-11-04 (default adopted): Yes; if FR-01-03 is cut, the map branch is removed and `s4` ends the flow. The branch stays until the release scope is fixed. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-01 appears in the diagram | Pass (6 of 6 W1 rows whose source trace names UC-01) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
