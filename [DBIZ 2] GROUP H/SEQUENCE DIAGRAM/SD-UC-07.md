# Sequence Diagram: SD-UC-07 Update and view personal reading history and preferences

| Field | Value |
|---|---|
| SD ID | SD-UC-07 |
| Use case | UC-07 Update and view personal reading history and preferences |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader; two parts start by themselves: a time event (daily loan sync finished) and an accept event (online book opened, from UC-03) |
| Participants | Reader · Web App · Backend · Reader database |
| Trigger | (a) The reader opens their reading history and preferences. (b) Time event: the daily loan records sync has finished (FR-04-10). (c) Accept event: a signed-in reader opened an online book from the filter results (AD-UC-03). |
| Preconditions | (a) The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). (b) Loan records of library card accounts are synced daily (FR-04-10). |
| FRs covered | FR-03-01, FR-03-02, FR-03-03, FR-03-04, FR-03-05, FR-03-22, FR-04-08 |
| Activity diagram | [AD-UC-07](../ACTIVITY%20DIAGRAM/AD-UC-07.md) |
| Redrawn from | `Reader Interaction Flow-2026-10-12-031246.png` |
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
  participant RDB as Reader database<br/>(history, preferences)
  R->>W: Open reading history and preferences (FR-03-01)
  W->>B: Get the reader's history and preferences (FR-03-01)
  B->>B: Check the reader's session (FR-04-08)
  opt No valid session
    B-->>W: Deny the request (FR-04-08)
    W-->>R: Ask "Sign in to continue?" (FR-04-08)
    Note over R,B: ref Sign in (UC-11), see SD-UC-11 (FR-04-01). "Not now" stops here. After sign-in the pending action continues (D1).
  end
  B->>RDB: Read history with reading status, and preferences (FR-03-01)
  RDB-->>B: Return the entries and preferences (FR-03-01)
  B-->>W: Return the entries and preferences (FR-03-01)
  W-->>R: Display the reading history with status (FR-03-01)
  rect rgba(120, 160, 220, 0.12)
    Note over R,B: Reader's choice, repeatable: update status and progress (AD-UC-07 d2)
    R->>W: Submit the reading status and progress of a book (FR-03-04)
    W->>B: Save status and progress (FR-03-04)
    B->>B: Check: Reading or Finished, progress 0 to 100 percent (FR-03-04)
    alt Update fails the check
      B-->>W: Reject, keeping the saved data (FR-03-22)
      W-->>R: Display an error message (FR-03-22)
    else Update passes the check
      B->>RDB: Save status and progress (FR-03-04)
      RDB-->>B: Confirm (FR-03-04)
      B-->>W: Return the updated history (FR-03-01)
      W-->>R: Display the updated reading history (FR-03-01)
    end
  end
  rect rgba(120, 160, 220, 0.12)
    Note over R,B: Reader's choice, repeatable: update preferences (AD-UC-07 d2)
    R->>W: Submit updated reading preferences (FR-03-05)
    W->>B: Save reading preferences (FR-03-05)
    B->>B: Validate the preferences (FR-03-05)
    alt Preferences fail the validation
      B-->>W: Reject, keeping the saved data (FR-03-22)
      W-->>R: Display an error message (FR-03-22)
    else Preferences pass the validation
      B->>RDB: Save the preferences to the reader's profile (FR-03-05)
      RDB-->>B: Confirm (FR-03-05)
      B-->>W: Return the updated preferences (FR-03-05)
      W-->>R: Display the updated preferences (FR-03-05)
    end
  end
  rect rgba(150, 150, 150, 0.14)
    Note over B,RDB: Automatic: daily loan records sync finished (FR-04-10)
    B->>B: Find new borrow records of library card accounts (FR-03-03)
    loop Each new borrow record
      B->>RDB: Add the borrowed book to that reader's history (FR-03-03)
    end
  end
  rect rgba(150, 150, 150, 0.14)
    Note over B,RDB: Automatic: a signed-in reader opened an online book (SD-UC-03)
    B->>RDB: Add the book to the reader's reading history (FR-03-02)
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-07 + UC-09 image (Inputs check 4). Recommendations are now in SD-UC-09.
- Viewing history and setting preferences are reader's choices, so they are no longer `alt` (Inputs check 5).
- The yellow note on automatic history entries is now two drawn flows. Added the session check and rejected updates (FR-03-22).
