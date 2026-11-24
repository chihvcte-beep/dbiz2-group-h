# Sequence Diagram: SD-UC-14 Report a review that violates rules

| Field | Value |
|---|---|
| SD ID | SD-UC-14 |
| Use case | UC-14 Report a review that violates rules |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Reader database |
| Trigger | The reader selects Report on a review (usually from UC-05) |
| Preconditions | The review is on public display. The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). |
| FRs covered | FR-02-09, FR-02-21, FR-02-24, FR-04-08 |
| Activity diagram | [AD-UC-14](../activity/ad-uc-14.md) |
| Redrawn from | `User Review Reporting Flow-2026-10-12-035252.pdf` |
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
  participant RDB as Reader database<br/>(reviews, reports)
  R->>W: Select Report on a review (FR-02-09)
  W->>B: Send the request (FR-04-08)
  B->>B: Check the reader's session (FR-04-08)
  opt No valid session
    B-->>W: Deny the request (FR-04-08)
    W-->>R: Ask "Sign in to continue?" (FR-04-08)
    Note over R,B: ref Sign in (UC-11), see SD-UC-11 (FR-04-01). "Not now" stops here. After sign-in the pending action continues (D1).
  end
  B->>RDB: Read who wrote the review (FR-02-24)
  RDB-->>B: Return the author (FR-02-24)
  alt The reader wrote this review
    B-->>W: Reject the report (FR-02-24)
    W-->>R: Display that a reader cannot report their own review (FR-02-24)
  else Another reader's review
    B-->>W: Confirm the session is valid (FR-04-08)
    W-->>R: Ask to confirm the report (FR-02-09)
    Note over R,B: «Huỷ» stops here and nothing is saved
    R->>W: Submit the report for the selected review (FR-02-09)
    W->>B: Report the review (FR-02-09)
    B->>RDB: Check whether this reader already reported it (FR-02-21)
    RDB-->>B: Return the result (FR-02-21)
    alt Already reported by this reader
      B-->>W: Return already reported (FR-02-21)
      W-->>R: Display that the review has already been reported (FR-02-21)
    else Not reported yet
      B->>RDB: Save the report against the review (FR-02-09)
      RDB-->>B: Confirm (FR-02-09)
      B-->>W: Confirm (FR-02-09)
      W-->>R: Show report received (FR-02-09)
    end
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-14 + UC-13 image (Inputs check 4). Staff handling is now in SD-UC-13.
- Added the session check, the confirmation step and the duplicate report rule (FR-02-21).
- v2.1 (23/11/2026): a reader cannot report their own review, also when the report was requested before sign-in (FR-02-24, D39, AD-UC-14 v1.4).
