# Sequence Diagram: SD-UC-04 Write, edit and delete own book reviews

| Field | Value |
|---|---|
| SD ID | SD-UC-04 |
| Use case | UC-04 Write, edit and delete own book reviews |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Reader database |
| Trigger | The reader asks to write, edit or delete a review on a book |
| Preconditions | The book is in the synced catalogue. The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). |
| FRs covered | FR-02-01, FR-02-03, FR-02-04, FR-02-11, FR-02-12, FR-02-22, FR-04-08 |
| Activity diagram | [AD-UC-04](../ACTIVITY%20DIAGRAM/AD-UC-04.md) |
| Redrawn from | `User Review Interaction Flow-2026-10-12-032334.png` · `Book Review API Interaction-2026-10-12-032039.png` |
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
  participant RDB as Reader database<br/>(reviews)
  R->>W: Request a review action on a book (FR-04-08)
  rect rgba(120, 160, 220, 0.12)
    Note over R,W: Reader's choice, one of three (AD-UC-04 d2)
    R->>W: Write: choose to post under own name or anonymously (FR-02-22)
    R->>W: Write: submit a new review text (FR-02-01)
    R->>W: Edit: choose to show own name or post anonymously (FR-02-22)
    R->>W: Edit: submit an edited text of own review (FR-02-03)
    R->>W: Delete: choose own review to delete (FR-02-04)
  end
  W->>B: Send the chosen action (FR-04-08)
  B->>B: Check the reader's session (FR-04-08)
  opt No valid session
    B-->>W: Deny the request (FR-04-08)
    W-->>R: Ask "Sign in to continue?" (FR-04-08)
    Note over R,B: ref Sign in (UC-11), see SD-UC-11 (FR-04-01). "Not now" stops here. After sign-in the action already chosen continues, the reader does not choose or type again (D1).
  end
  alt Requested action: write
    B->>B: Check: not empty, max 2,000 characters, plain text (FR-02-01)
    alt Text fails the check
      B-->>W: Reject the action (FR-02-11)
      W-->>R: Show an error message (FR-02-11)
    else Text passes the check
      B->>RDB: Save the review against the book and reader (FR-02-01)
      RDB-->>B: Confirm (FR-02-01)
      B->>B: Set the reviewer shown: full name or «Bạn đọc ẩn danh» (FR-02-22)
      B-->>W: Return confirmation and updated review list (FR-02-12)
      W-->>R: Show confirmation and updated review list (FR-02-12)
    end
  else Requested action: edit
    B->>RDB: Read the review's owner (FR-02-03)
    RDB-->>B: Return the owner (FR-02-03)
    alt Not the reader's own review
      B-->>W: Reject the action (FR-02-11)
      W-->>R: Show an error message (FR-02-11)
    else Reader's own review
      B->>B: Check the edited text with the same rules (FR-02-03)
      alt Text fails the check
        B-->>W: Reject the action (FR-02-11)
        W-->>R: Show an error message (FR-02-11)
      else Text passes the check
        B->>RDB: Replace the text, keeping the same book (FR-02-03)
        RDB-->>B: Confirm (FR-02-03)
        B->>B: Set the reviewer shown: full name or «Bạn đọc ẩn danh» (FR-02-22)
        B-->>W: Return confirmation and updated review list (FR-02-12)
        W-->>R: Show confirmation and updated review list (FR-02-12)
      end
    end
  else Requested action: delete
    B-->>W: Confirm the session is valid (FR-04-08)
    W-->>R: Ask to confirm the deletion (FR-02-04)
    rect rgba(120, 160, 220, 0.12)
      Note over R,W: Reader's choice (AD-UC-04 d6). «Huỷ» stops here and nothing changes
      R->>W: Confirm the deletion (FR-02-04)
    end
    W->>B: Delete own review (FR-02-04)
    B->>RDB: Read the review's owner (FR-02-04)
    RDB-->>B: Return the owner (FR-02-04)
    alt Not the reader's own review
      B-->>W: Reject the action (FR-02-11)
      W-->>R: Show an error message (FR-02-11)
    else Reader's own review
      B->>RDB: Remove the review from public display (FR-02-04)
      RDB-->>B: Confirm (FR-02-04)
      B-->>W: Return confirmation and updated review list (FR-02-12)
      W-->>R: Show confirmation and updated review list (FR-02-12)
    end
  end
```

## 2. Changes from the original diagram

- Joins the write steps of Book Review API Interaction and the edit and delete steps of User Review Interaction Flow (Inputs check 4).
- Write, edit and delete are reader's choices, so they are marked sections instead of `opt` (Inputs check 5).
- Added the session check, the rejections (FR-02-11), the confirmation (FR-02-12) and the anonymous option (FR-02-22).
- v2.1 (23/11/2026): the reader chooses the action before the session check, so it continues by itself after sign-in (D1, AD-UC-04 v1.3).
- v2.1 (23/11/2026): the system then follows the requested action (`alt`, AD-UC-04 `d8`) and sets the name shown on the review (FR-02-22).
