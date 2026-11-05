# Activity Diagram: AD-UC-02 Browse interactive digital library map

| Field | Value |
|---|---|
| AD ID | AD-UC-02 |
| Use case | UC-02 Browse interactive digital library map |
| Feature | F-01 Book Location & Library Map |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader; flow "Shelf location & library map"; Library Internal System flow "Shelf placement, floors & rooms") · Use Case Diagram (UC-02) · Sequence: User Interface Flow (UC-01, UC-02) · W0 Table 3 (no screen to edit floor plans), Table 4 (Book placement & library layout, EIF) · W1 rows FR-01-02, FR-01-03, FR-01-09, FR-01-10, FR-01-11 |
| Trigger | The reader asks for the digital library map, from the menu or from a book's shelf location (UC-01) |
| Preconditions | No sign-in is needed (W0 Table 1). The digital floor plan exists and its room codes match the Library Internal System (FR-01-04). Floors and rooms have been synced (FR-04-09). |
| Success end state | The reader has seen the map of the library, switched floors and selected rooms as they wished, and chooses Finish. |
| Failure end state | The floor plan cannot be read: the reader sees a map-unavailable message, and any shelf details already shown stay visible. |
| FRs covered | FR-01-02, FR-01-03, FR-01-09, FR-01-10, FR-01-11 |
| Business rules applied | Rooms on the floor plan carry the same room code as the Library Internal System (FR-01-04). A plan that cannot be read gives a map-unavailable message, never an empty map (FR-01-10). Shelf details already shown are kept (FR-01-10). |
| Version / status | v1.2 · Draft |
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
    r1("Request the digital library map (FR-01-02)")
    d4{"What does the reader do next?"}
    r2("Request to view another floor (FR-01-02)")
    r3("Select a reading room on the map (FR-01-11)")
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Retrieve the synced floor and room data<br/>and the floor plan (FR-01-02)")
    d1{"Is the floor plan available and readable?"}
    s2("Display a map-unavailable message,<br/>keeping any shelf details already shown (FR-01-10)")
    d2{"Was the map opened for a book's room?"}
    d3{"Is the book's room code found on the floor plan?"}
    s3("Display the map with the book's room highlighted (FR-01-03)")
    s4("Display that the room cannot be<br/>identified on the map (FR-01-09)")
    m1{" "}
    s5("Display the map with the available<br/>floors and reading rooms (FR-01-02)")
    m2{" "}
    d5{"Is the selected floor's plan<br/>available and readable?"}
    s6("Display the selected floor's map<br/>and its reading rooms (FR-01-02)")
    s7("Display a map-unavailable message for that floor (FR-01-10)")
    s8("Highlight the room and display its<br/>room name, room code and floor (FR-01-11)")
    stop1@{ shape: fr-circ }
  end

  start --> r1 --> s1 --> d1
  d1 -->|"[No]"| s2 --> stop1
  d1 -->|"[Yes]"| d2
  d2 -->|"[No]"| m1
  d2 -->|"[Yes]"| d3
  d3 -->|"[Yes]"| s3 --> m2
  d3 -->|"[No]"| s4 --> m1
  m1 --> s5 --> m2
  m2 --> d4
  d4 -->|"[View another floor]"| r2 --> d5
  d5 -->|"[Yes]"| s6 --> m2
  d5 -->|"[No]"| s7 --> m2
  d4 -->|"[Select a room]"| r3 --> s8 --> m2
  d4 -->|"[Finish]"| stop2
```

Reading notes:

- `d2` separates the two ways in: a map opened for a book's room (link from UC-01) and a map opened
  on its own. Both end up on the same map view.
- `m2` is the merge every loop comes back through before the reader's choice `d4`. The reader can
  switch floors and select rooms as often as they like, then choose Finish.
- `m1` gathers "opened on its own" and "room not found" because both show the plain map (`s5`).

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Request the digital library map | FR-01-02 |
| s1 | Action | Retrieve the synced floor and room data and the floor plan | FR-01-02 |
| d1 | Decision | Is the floor plan available and readable? | FR-01-10 |
| s2 | Action | Display a map-unavailable message, keeping any shelf details already shown | FR-01-10 |
| d2 | Decision | Was the map opened for a book's room? | FR-01-03 |
| d3 | Decision | Is the book's room code found on the floor plan? | FR-01-09 |
| s3 | Action | Display the map with the book's room highlighted | FR-01-03 |
| s4 | Action | Display that the room cannot be identified on the map | FR-01-09 |
| s5 | Action | Display the map with the available floors and reading rooms | FR-01-02 |
| d4 | Decision (Reader) | What does the reader do next? | FR-01-02, FR-01-11 |
| r2 | Action (Reader) | Request to view another floor | FR-01-02 |
| d5 | Decision | Is the selected floor's plan available and readable? | FR-01-10 |
| s6 | Action | Display the selected floor's map and its reading rooms | FR-01-02 |
| s7 | Action | Display a map-unavailable message for that floor | FR-01-10 |
| r3 | Action (Reader) | Select a reading room on the map | FR-01-11 |
| s8 | Action | Highlight the room and display its room name, room code and floor | FR-01-11 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [No] | the floor plan files cannot be read | the reader opens the library map | a map-unavailable message is shown and no map is drawn |
| d1 [Yes] → d2 [No] | the floor plans are available | the reader opens the map from the menu | the map shows the floors and reading rooms, no room highlighted |
| d2 [Yes] → d3 [Yes] | the reader came from book shelf location Floor 2 · Room R-204, and R-204 is on the floor 2 plan | the map opens | the floor 2 map is shown with R-204 highlighted |
| d2 [Yes] → d3 [No] | the reader came from a book in room R-299, which is not on the floor 2 plan | the map opens | a message says the room cannot be identified, then the plain map is shown |
| d4 [View another floor] → d5 [Yes] | the map of floor 1 is shown and the floor 3 plan is readable | the reader chooses floor 3 | the floor 3 map and its reading rooms are shown |
| d4 [View another floor] → d5 [No] | the floor 4 plan file is damaged | the reader chooses floor 4 | a map-unavailable message for floor 4 is shown and the reader can choose again |
| d4 [Select a room] | the floor 2 map is shown | the reader selects room R-204 | R-204 is highlighted with its name "Reading Room A", code R-204 and floor 2 |
| d4 [Finish] | any map is shown | the reader leaves the map | the activity ends; nothing is saved |

## 4. Object states used

| Object | States in this diagram | Note |
|---|---|---|
| Book placement & library layout (EIF) | none written | Floors and rooms are read only (W0 Table 4) |

## 5. Screens touched

Filled in from the Screen List (Lesson 8).

| Reader action | Screen ID |
|---|---|
| Request the digital library map | S-F01-02 |
| Request to view another floor, Select a reading room on the map | S-F01-02 |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | which floor is shown first when the map is opened from the menu? | No (decided) | Decided 2026-11-04 (default adopted): The ground floor (lowest floor number). |
| 2 | when the selected floor's plan cannot be read (`d5 [No]`), does the previous floor's map stay on screen? | No (decided) | Decided 2026-11-04 (default adopted): Yes; the message is shown above the previous floor's map. |
| 3 | FR-01-03 is Could after W4. If it is cut, `d2`, `d3`, `s3` and `s4` are removed and the map always opens plain. | No (decided) | Decided 2026-11-04 (default adopted): Keep the branch until the release scope is fixed. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-02 appears in the diagram | Pass (5 of 5 W1 rows whose source trace names UC-02) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
