# Sequence Diagram: SD-UC-09 Automatic personalised book recommendations

| Field | Value |
|---|---|
| SD ID | SD-UC-09 |
| Use case | UC-09 Automatic personalised book recommendations |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · AI Service · Reader database · Book database |
| Trigger | The reader opens the recommendations section |
| Preconditions | The reader may not be signed in yet: the flow checks the session and shows a sign-in prompt (FR-03-21). |
| FRs covered | FR-03-11, FR-03-19, FR-03-20, FR-03-21, FR-04-08 |
| Activity diagram | [AD-UC-09](../../activity_diagram/ad_uc_09.md) |
| Redrawn from | `Reader Interaction Flow-2026-10-12-031246.png` |
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
  participant AI as AI Service<br/>(inside Library Core System)
  participant RDB as Reader database<br/>(history, preferences, chatbot)
  participant BDB as Book database<br/>(catalogue, QR scan counts)
  R->>W: Open the recommendations section (FR-03-11)
  W->>B: Request personalised recommendations (FR-03-11)
  B->>B: Check the reader's session (FR-04-08)
  opt No valid session
    B-->>W: Deny the request (FR-03-21)
    W-->>R: Show that recommendations require a library card account (FR-03-21)
    Note over R,B: ref Sign in (UC-11), see SD-UC-11 (FR-04-01). "Not now" stops here. After sign-in the pending action continues (D1).
  end
  B->>RDB: Retrieve history, preferences and chatbot conversations (FR-03-11)
  RDB-->>B: Return the reader data (FR-03-11)
  alt No reader data
    B->>BDB: Read popular books by QR scan count (FR-03-19)
    BDB-->>B: Return popular books (FR-03-19)
    B-->>W: Return popular books and a preferences prompt (FR-03-19)
    W-->>R: Prompt the reader to set reading preferences (FR-03-19)
  else Reader data exists
    B->>AI: Send the reader context (FR-03-11)
    AI->>BDB: Find catalogue books matching the context (FR-03-11)
    BDB-->>AI: Return candidate books and metadata (FR-03-11)
    AI->>AI: Compute recommendation scores (FR-03-11)
    AI-->>B: Return ranked recommendations (FR-03-11)
    opt Fewer than three matching titles
      B->>BDB: Read trending books of the same subjects (FR-03-20)
      BDB-->>B: Return trending books (FR-03-20)
    end
    B-->>W: Return the recommended books (FR-03-11)
  end
  W-->>R: Display the recommended book list (FR-03-11)
  Note over R,B: ref Open a physical book (UC-01, SD-UC-01), open an online book on the OPAC, or set preferences (UC-07, SD-UC-07), then the list is rebuilt
```

## 2. Changes from the original diagram

- Split from the combined UC-07 + UC-09 image (Inputs check 4).
- Added the sign-in prompt (FR-03-21), popular books when there is no reader data (FR-03-19) and the top-up (FR-03-20).
- v2.1 (23/11/2026): a recommended online book opens on the OPAC (AD-UC-09 v1.3).
