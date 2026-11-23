# Sequence Diagram: SD-UC-01 View book shelf location

| Field | Value |
|---|---|
| SD ID | SD-UC-01 |
| Use case | UC-01 View book shelf location |
| Feature | F-01 Book Location & Library Map |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Book database |
| Trigger | The reader opens a book's detail page and asks for its shelf location |
| Preconditions | None for the reader: no sign-in is needed (W0 Table 1). The catalogue and shelf placement have been synced from the Library Internal System (FR-04-09). |
| FRs covered | FR-01-01, FR-01-03, FR-01-06, FR-01-07, FR-01-09, FR-01-10 |
| Activity diagram | [AD-UC-01](../../activity_diagram/ad_uc_01.md) |
| Redrawn from | `User Interface Flow-2026-10-12-031728.png` |
| Version / status | v2.1 · Draft |

## 1. Diagram

Blue sections are choices of the actor, grey sections run automatically, and `alt` / `opt` are system
conditions. Reading rules: [sequence_index.md](sequence_index.md#drawing-rules).

```mermaid
---
config:
  sequence:
    actorMargin: 110
---
sequenceDiagram
  autonumber
  actor R as Reader
  participant W as Web App<br/>(User Interface)
  participant B as Backend<br/>(API)
  participant BDB as Book database<br/>(catalogue, shelf placement,<br/>floors and rooms, synced daily - FR-04-09)
  Note over R,BDB: No sign-in required
  R->>W: Open a book's detail page and request its shelf location (FR-01-01)
  W->>B: Get the shelf location by book ID (FR-01-01)
  B->>BDB: Read the book's format, floor, room and shelf code (FR-01-01)
  BDB-->>B: Return the format and location data (FR-01-01)
  alt Book has no physical copy
    B-->>W: Return that the book is online only (FR-01-06)
    W-->>R: Display that no physical shelf location applies (FR-01-06)
  else Floor, room or shelf code missing or inconsistent
    B-->>W: Return that the location is unavailable (FR-01-07)
    W-->>R: Display location unavailable and direct the reader to staff (FR-01-07)
  else Codes complete and consistent
    B-->>W: Return floor, room and shelf code (FR-01-01)
    W-->>R: Display floor, room and shelf code (FR-01-01)
    Note over R,B: ref Reader's choice: save the book to my list (UC-12), see SD-UC-12 (FR-03-06)
    rect rgba(120, 160, 220, 0.12)
      Note over R,B: Reader's choice: view the room on the map (AD-UC-01 d3)
      R->>W: Request the library map for the book's room (FR-01-03)
      W->>B: Get the floor plan with the book's room (FR-01-03)
      B->>B: Load the floor plan drawing of the book's floor (FR-01-03)
      alt Floor plan unavailable or unreadable
        B-->>W: Return that the map is unavailable (FR-01-10)
        W-->>R: Keep shelf details and display map unavailable (FR-01-10)
      else Room code not on the floor plan
        B-->>W: Return that the room is not on the plan (FR-01-09)
        W-->>R: Keep shelf details and display room cannot be identified (FR-01-09)
      else Room found on the floor plan
        B-->>W: Return the floor plan and the room (FR-01-03)
        W-->>R: Display the map with the room highlighted, shelf details kept (FR-01-03)
      end
    end
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-01 + UC-02 image (Inputs check 4). The map browsing is now in SD-UC-02.
- The optional map link is a reader's choice, so it is a marked section instead of `opt` (Inputs check 5).
- The floor plan is loaded by the Backend, not read from the Book database: W0 Table 4 says the drawing is a fixed asset.
- Added the edge cases of AD-UC-01: FR-01-06, FR-01-07, FR-01-09, FR-01-10.
- v2.1 (23/11/2026): the call to UC-12 (save the book), as `c1` in AD-UC-01.
