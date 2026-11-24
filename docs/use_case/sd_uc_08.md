# Sequence Diagram: SD-UC-08 AI-based conversational book search

| Field | Value |
|---|---|
| SD ID | SD-UC-08 |
| Use case | UC-08 AI-based conversational book search |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · AI Service · Reader database · Book database |
| Trigger | The reader sends an inquiry message to the chatbot |
| Preconditions | The reader may not be signed in yet: the flow checks the session and prompts sign-in with a library card (FR-03-18). |
| FRs covered | FR-03-09, FR-03-10, FR-03-16, FR-03-17, FR-03-18, FR-04-08 |
| Activity diagram | [AD-UC-08](../activity/ad_uc_08.md) |
| Redrawn from | `AI Service Chatbot-2026-10-12-032513.png` |
| Version / status | v2.2 · Draft |

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
  participant RDB as Reader database<br/>(chatbot conversations)
  participant BDB as Book database<br/>(catalogue, synced daily - FR-04-09)
  R->>W: Send an inquiry message to the chatbot (FR-03-09)
  W->>B: Send the chat message (FR-03-09)
  B->>B: Check the reader's session (FR-04-08)
  opt No valid session
    B-->>W: Deny the request (FR-03-18)
    W-->>R: Prompt the reader to sign in with a library card (FR-03-18)
    Note over R,B: ref Sign in (UC-11), see SD-UC-11 (FR-04-01). "Not now" stops here. After sign-in the message already sent goes on by itself, the reader does not send it again (D1).
  end
  B->>RDB: Save the reader message in the conversation history (FR-03-10)
  B->>AI: Forward the message and reader context (FR-03-09)
  alt AI Service replies in time without error
    AI->>BDB: Search the catalogue for matching books (FR-03-09)
    BDB-->>AI: Return matching books (FR-03-09)
    AI-->>B: Return the composed reply (FR-03-09)
    B->>RDB: Save the reply in the conversation history (FR-03-10)
    alt Matching books found
      B-->>W: Return the reply with book results (FR-03-09)
      W-->>R: Display the reply with book result cards (FR-03-09)
    else No matching books
      B-->>W: Return the no-results reply (FR-03-16)
      W-->>R: Display no results and suggest other terms or subjects (FR-03-16)
    end
  else AI Service unresponsive, timed out or in error
    AI--xB: No reply, or an error (FR-03-17)
    B-->>W: Return that AI search is unavailable (FR-03-17)
    W-->>R: Display AI search unavailable and advise the format filter (FR-03-17)
    Note over B,RDB: The reader message stays saved. No reply is saved.
  end
  Note over R,B: ref Open a physical book (UC-01, SD-UC-01), open an online book on the OPAC, or use the format filter (UC-03, SD-UC-03)
```

## 2. Changes from the original diagram

- Added the sign-in prompt (FR-03-18), no results (FR-03-16) and AI failure (FR-03-17), as in AD-UC-08.
- Participant names are cleaned (the image showed "WebApp as Web App").
- v2.1 (23/11/2026): the note on sign-in now says that the message goes on by itself (D1, AD-UC-08 v1.3).
- v2.2 (23/11/2026): an online book card opens the book on the OPAC (AD-UC-08 v1.4).
