# Sequence Diagram: SD-UC-12 Save physical books to a personal list for finding them later in the library, and remove them from the list

| Field | Value |
|---|---|
| SD ID | SD-UC-12 |
| Use case | UC-12 Save physical books to a personal list for finding them later in the library, and remove them from the list |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Reader database · Book database |
| Trigger | The reader asks for a saved-books action: save a physical book, or open the saved books list |
| Preconditions | The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). |
| FRs covered | FR-01-07, FR-03-06, FR-03-07, FR-03-08, FR-03-24, FR-03-25, FR-04-08 |
| Activity diagram | [AD-UC-12](../ACTIVITY%20DIAGRAM/AD-UC-12.md) |
| Redrawn from | `Reader API Saved List-2026-10-12-033031.png` |
| Version / status | v2.2 · Draft |

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
  participant RDB as Reader database<br/>(saved list)
  participant BDB as Book database<br/>(catalogue, placement,<br/>synced daily - FR-04-09)
  rect rgba(120, 160, 220, 0.12)
    Note over R,W: Reader's choice, one of two (AD-UC-12 d2)
    R->>W: Save: select Save on a physical book (FR-03-06)
    R->>W: View: open the saved books list (FR-03-07)
  end
  W->>B: Send the chosen action (FR-04-08)
  B->>B: Check the reader's session (FR-04-08)
  opt No valid session
    B-->>W: Deny the request (FR-04-08)
    W-->>R: Ask "Sign in to continue?" (FR-04-08)
    Note over R,B: ref Sign in (UC-11), see SD-UC-11 (FR-04-01). "Not now" stops here. After sign-in the action already chosen continues, the reader does not choose again (D1).
  end
  alt Requested action: save a physical book
    B->>RDB: Check whether the book is already saved (FR-03-24)
    RDB-->>B: Return the result (FR-03-24)
    alt Book already saved
      B-->>W: Return already saved (FR-03-24)
      W-->>R: Display that the book is already saved (FR-03-24)
    else Book not saved yet
      B->>RDB: Store the book in the reader's saved list (FR-03-06)
      RDB-->>B: Confirm (FR-03-06)
      B-->>W: Confirm (FR-03-06)
      W-->>R: Show the book as saved (FR-03-06)
    end
  else Requested action: view the saved list
    B->>RDB: Read saved books (FR-03-07)
    RDB-->>B: Return saved books (FR-03-07)
    alt List is empty
      B-->>W: Return an empty list (FR-03-25)
      W-->>R: Display that no books have been saved yet (FR-03-25)
    else List has books
      B->>BDB: Read the shelf location of each saved book (FR-03-07)
      BDB-->>B: Return shelf locations (FR-03-07)
      B-->>W: Return saved books with shelf locations (FR-03-07)
      W-->>R: Display saved books with shelf locations (FR-03-07)
      opt A shelf location is missing or inconsistent
        W-->>R: Show location unavailable and direct the reader to staff (FR-01-07)
      end
      rect rgba(120, 160, 220, 0.12)
        Note over R,B: Reader's choice: remove a saved book (AD-UC-12 d6)
        R->>W: Select Remove on a saved book (FR-03-08)
        W->>B: Remove the book from the saved list (FR-03-08)
        B->>RDB: Delete the book from the saved list (FR-03-08)
        RDB-->>B: Confirm (FR-03-08)
        B-->>W: Return the refreshed list (FR-03-08)
        W-->>R: Display the updated list (FR-03-08)
      end
    end
  end
```

## 2. Changes from the original diagram

- Added the session check, already saved (FR-03-24), empty list (FR-03-25) and missing shelf location (FR-01-07).
- Removing a book is a reader's choice, so it is a marked section instead of `opt` (Inputs check 5).
- v2.1 (23/11/2026): the reader chooses the action before the session check, so it continues by itself after sign-in (D1, AD-UC-12 v1.2).
- v2.2 (23/11/2026): the first step "Request a saved-books action" is removed, as in AD-UC-12 v1.3 (L8-21).
