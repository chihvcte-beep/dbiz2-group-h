# Sequence Diagram: SD-UC-02 Browse interactive digital library map

| Field | Value |
|---|---|
| SD ID | SD-UC-02 |
| Use case | UC-02 Browse interactive digital library map |
| Feature | F-01 Book Location & Library Map |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Book database |
| Trigger | The reader asks for the digital library map, from the menu or from a book's shelf location (UC-01) |
| Preconditions | No sign-in is needed (W0 Table 1). The digital floor plan exists and its room codes match the Library Internal System (FR-01-04). Floors and rooms have been synced (FR-04-09). |
| FRs covered | FR-01-02, FR-01-03, FR-01-04, FR-01-09, FR-01-10, FR-01-11 |
| Activity diagram | [AD-UC-02](../ACTIVITY%20DIAGRAM/AD-UC-02.md) |
| Redrawn from | `User Interface Flow-2026-10-12-031728.png` |
| Version / status | v2.0 · Draft |

## 1. Diagram

Blue sections are choices of the actor, grey sections run automatically, and `alt` / `opt` are system
conditions. Reading rules: [sequence-index.md](sequence-index.md#drawing-rules).

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
  participant BDB as Book database<br/>(floors and rooms,<br/>synced daily - FR-04-09)
  Note over R,BDB: No sign-in required
  R->>W: Request the digital library map (FR-01-02)
  W->>B: Get floors, rooms and the floor plan (FR-01-02)
  B->>BDB: Read the synced floors and rooms (FR-01-02)
  BDB-->>B: Return floors and rooms (FR-01-02)
  B->>B: Load the floor plan with rooms tagged by room code (FR-01-04)
  alt Floor plan unavailable or unreadable
    B-->>W: Return that the map is unavailable (FR-01-10)
    W-->>R: Display map unavailable, keeping shelf details already shown (FR-01-10)
  else Map opened for a book's room, room found
    B-->>W: Return the map with the book's room (FR-01-03)
    W-->>R: Display the map with the book's room highlighted (FR-01-03)
  else Map opened for a book's room, room not on the plan
    B-->>W: Return the map and that the room is not on the plan (FR-01-09)
    W-->>R: Display the map and that the room cannot be identified (FR-01-09)
  else Map opened on its own
    B-->>W: Return the map with floors and rooms (FR-01-02)
    W-->>R: Display the available floors and reading rooms (FR-01-02)
  end
  rect rgba(120, 160, 220, 0.12)
    Note over R,B: Reader's choice, repeatable when a map is shown: view another floor (AD-UC-02 d4)
    R->>W: Request to view another floor (FR-01-02)
    W->>B: Get the selected floor (FR-01-02)
    B->>B: Load the selected floor's plan (FR-01-02)
    alt Selected floor's plan available
      B-->>W: Return the floor's map and rooms (FR-01-02)
      W-->>R: Display the floor's map and reading rooms (FR-01-02)
    else Plan unavailable or unreadable
      B-->>W: Return that the map is unavailable (FR-01-10)
      W-->>R: Display map unavailable for that floor (FR-01-10)
    end
  end
  rect rgba(120, 160, 220, 0.12)
    Note over R,B: Reader's choice, repeatable: select a room (AD-UC-02 d4)
    R->>W: Select a reading room on the map (FR-01-11)
    W-->>R: Highlight the room and show its name, code and floor (FR-01-11)
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-01 + UC-02 image (Inputs check 4).
- Added switching floors, selecting a room (FR-01-11) and the map errors of AD-UC-02.
- FR-01-04 now has its own step, because each message carries one FR.
