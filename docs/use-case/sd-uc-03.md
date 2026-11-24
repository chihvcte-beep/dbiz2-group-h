# Sequence Diagram: SD-UC-03 Filter books by access format (online, physical or both)

| Field | Value |
|---|---|
| SD ID | SD-UC-03 |
| Use case | UC-03 Filter books by access format (online, physical or both) |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Book database · Reader database |
| Trigger | The reader opens the access-format filter |
| Preconditions | No sign-in is needed (W0 Table 1). The catalogue, with the access format of each book, has been synced (FR-04-09). |
| FRs covered | FR-03-02, FR-03-12, FR-03-13, FR-03-23 |
| Activity diagram | [AD-UC-03](../activity/ad-uc-03.md) |
| Redrawn from | `User Interface Flow-2026-10-12-032159.png` |
| Version / status | v2.1 · Draft |

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
  participant BDB as Book database<br/>(catalogue, synced daily - FR-04-09)
  participant RDB as Reader database<br/>(online read log, reading history)
  Note over R,RDB: No sign-in required
  R->>W: Open the access-format filter (FR-03-12)
  W-->>R: Show the filter with no format selected, no results yet (FR-03-12)
  R->>W: Choose Online, Physical or Both (FR-03-12)
  W->>B: Query books by access format (FR-03-12)
  B->>BDB: Search the catalogue by access format (FR-03-12)
  BDB-->>B: Return matching books (FR-03-12)
  alt Matching books found
    B-->>W: Return the first 20 matching books (FR-03-12)
    W-->>R: Display the books with their access-format labels, 20 per page (FR-03-12)
  else No matching books
    B-->>W: Return no results (FR-03-23)
    W-->>R: Display no books found, reader may choose another format (FR-03-23)
  end
  rect rgba(120, 160, 220, 0.12)
    Note over R,B: Reader's choice, repeatable: open another page (AD-UC-03 d2)
    R->>W: Open another page of the results (FR-03-12)
    W->>B: Get that page (FR-03-12)
    B->>BDB: Read that page of 20 books (FR-03-12)
    BDB-->>B: Return the page (FR-03-12)
    B-->>W: Return the page (FR-03-12)
    W-->>R: Show that page of the results (FR-03-12)
  end
  Note over R,B: Choosing another access format repeats the query from page 1 (D14)
  rect rgba(120, 160, 220, 0.12)
    Note over R,B: Reader's choice, repeatable: open an online book (AD-UC-03 d2)
    R->>W: Open an online book from the results (FR-03-13)
    W->>B: Record that the book was opened (FR-03-13)
    B->>RDB: Record the book and time, without reader identity (FR-03-13)
    opt Reader signed in with a library card
      B->>RDB: Add the book to the reader's reading history (FR-03-02)
    end
    B-->>W: Return the link to the book on the current OPAC (FR-03-13)
    W-->>R: Hand the reader over to the online book on the OPAC (FR-03-13)
  end
  Note over R,B: ref Open a physical book: View book shelf location (UC-01), see SD-UC-01 (FR-01-01)
```

## 2. Changes from the original diagram

- Added the no-result case (FR-03-23) and opening an online book (FR-03-13, FR-03-02), as in AD-UC-03.
- The filter opens with no format selected (D19).
- v2.1 (23/11/2026): added paging, 20 books per page, and the return to page 1 when the format changes (FR-03-12; D9, D14, D33).
