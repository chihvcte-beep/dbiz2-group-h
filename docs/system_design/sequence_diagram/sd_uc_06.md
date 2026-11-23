# Sequence Diagram: SD-UC-06 Access book information and reviews via QR code (physical books; reviews via UC-04)

| Field | Value |
|---|---|
| SD ID | SD-UC-06 |
| Use case | UC-06 Access book information and reviews via QR code (physical books; reviews via UC-04) |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Book database · Reader database |
| Trigger | The reader scans the QR code on a physical book |
| Preconditions | The book has a QR code (FR-02-07) and a printed label (UC-10). No sign-in is needed to view the page. |
| FRs covered | FR-02-02, FR-02-05, FR-02-06, FR-02-16, FR-02-22 |
| Activity diagram | [AD-UC-06](../../activity_diagram/ad_uc_06.md) |
| Redrawn from | `Book Review API Interaction-2026-10-12-032039.png` |
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
  participant BDB as Book database<br/>(catalogue, QR codes)
  participant RDB as Reader database<br/>(reviews)
  Note over R,RDB: No sign-in required to view. Only physical books have a QR code (FR-02-07).
  R->>W: Scan the QR code on a physical book (FR-02-05)
  W->>B: Open the QR link (FR-02-05)
  B->>BDB: Find the book linked to the QR code (FR-02-05)
  BDB-->>B: Return the book, or not found (FR-02-05)
  alt QR code linked to no book
    B-->>W: Return book not found (FR-02-16)
    W-->>R: Display that the book cannot be found (FR-02-16)
    Note over R,W: The error offers the link «Về OPAC» to the OPAC main menu (D37)
  else QR code linked to a book
    par Count the scan
      B->>BDB: Increase the scan count by one (FR-02-06)
    and Load the page
      B->>RDB: Read the first 10 published reviews (FR-02-02)
      RDB-->>B: Return the reviews (FR-02-02)
    end
    B->>B: Set each reviewer shown: full name or «Bạn đọc ẩn danh» (FR-02-22)
    B-->>W: Return book information and reviews (FR-02-05)
    W-->>R: Show the information and review page (FR-02-05)
    rect rgba(120, 160, 220, 0.12)
      Note over R,B: Reader's choice while more reviews remain, repeatable (AD-UC-06 d2)
      R->>W: Ask for the next page of reviews (FR-02-02)
      W->>B: Get the next page (FR-02-02)
      B->>RDB: Read the next 10 published reviews (FR-02-02)
      RDB-->>B: Return the reviews (FR-02-02)
      B->>B: Set each reviewer shown: full name or «Bạn đọc ẩn danh» (FR-02-22)
      B-->>W: Return the page and whether more remain (FR-02-02)
      W-->>R: Show the next 10 reviews (FR-02-02)
    end
    Note over R,B: ref Write, edit or delete a review (UC-04), see SD-UC-04 (FR-02-01)
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-06 + UC-04 image (Inputs check 4). Writing a review is now in SD-UC-04.
- The old step with two FRs is now two steps, drawn in parallel as in the fork of AD-UC-06.
- Added the QR code linked to no book (FR-02-16) and the next page of reviews (D6).
- v2.1 (23/11/2026): added the reviewer name (FR-02-22) and the way out of the invalid-QR error (D37), as in AD-UC-06 v1.3.
