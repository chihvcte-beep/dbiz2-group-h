# Sequence Diagram: SD-UC-05 View book reviews

| Field | Value |
|---|---|
| SD ID | SD-UC-05 |
| Use case | UC-05 View book reviews |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Book database · Reader database |
| Trigger | The reader asks to see the reviews of a book |
| Preconditions | None: no sign-in is needed to read reviews (W0 Table 1). |
| FRs covered | FR-02-02, FR-02-13, FR-02-15 |
| Activity diagram | [AD-UC-05](../activity/ad_uc_05.md) |
| Redrawn from | `User Review Interaction Flow-2026-10-12-032334.png` |
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
  participant BDB as Book database<br/>(catalogue)
  participant RDB as Reader database<br/>(reviews)
  Note over R,RDB: No sign-in required
  R->>W: Ask to see the reviews of a book (FR-02-02)
  W->>B: Get the reviews of the book (FR-02-02)
  B->>BDB: Find the book (FR-02-02)
  BDB-->>B: Return the book, or not found (FR-02-02)
  alt Book not found
    B-->>W: Return nothing to show (FR-02-15)
    W-->>R: Display that there are no reviews to show (FR-02-15)
  else Book found
    B->>RDB: Read the reviews, leaving out removed ones (FR-02-13)
    RDB-->>B: Return published reviews (FR-02-02)
    alt No reviews yet
      B-->>W: Return that the book has no reviews yet (FR-02-15)
      W-->>R: Show that there are no reviews yet and invite the first review (FR-02-15)
    else Reviews found
      B-->>W: Return the first 10 reviews and whether more remain (FR-02-02)
      W-->>R: Display the page of reviews (FR-02-02)
      rect rgba(120, 160, 220, 0.12)
        Note over R,B: Reader's choice while more reviews remain, repeatable (AD-UC-05 d4)
        R->>W: Ask for the next page of reviews (FR-02-02)
        W->>B: Get the next page (FR-02-02)
        B->>RDB: Read the next 10 published reviews (FR-02-02)
        RDB-->>B: Return the reviews (FR-02-02)
        B-->>W: Return the page and whether more remain (FR-02-02)
        W-->>R: Display the next page (FR-02-02)
      end
      Note over R,B: ref Report a review (UC-14), see SD-UC-14 (FR-02-09)
    end
    Note over R,B: ref Write, edit or delete a review (UC-04), see SD-UC-04 (FR-02-01)
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-05 + UC-04 image (Inputs check 4). Edit and delete are now in SD-UC-04.
- Added: book not found or no reviews (FR-02-15), removed reviews left out (FR-02-13), 10 reviews per page (D6).
- v2.1 (23/11/2026): a book with no reviews yet invites the first review, and the page calls UC-04 (AD-UC-05 v1.2, L8-17).
