# Sequence Diagram: SD-UC-13 Remove reviews that violate rules

| Field | Value |
|---|---|
| SD ID | SD-UC-13 |
| Use case | UC-13 Remove reviews that violate rules |
| Feature | F-02 Reviews & QR |
| Primary actor | On-site Staff |
| Participants | On-site Staff · Web App · Backend · Reader database · Library Internal System |
| Trigger | On-site Staff open the staff page to handle the reported reviews |
| Preconditions | Staff have an internal library account (FR-04-07). Readers have reported reviews through UC-14. |
| FRs covered | FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-07, FR-04-08, FR-04-12, FR-04-18, FR-04-21 |
| Activity diagram | [AD-UC-13](../activity/ad_uc_13.md) |
| Redrawn from | `User Review Reporting Flow-2026-10-12-035252.pdf` |
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
  actor S as On-site Staff
  participant W as Web App<br/>(Staff page)
  participant B as Backend<br/>(API)
  participant RDB as Reader database<br/>(reviews, reports)
  participant LIS as Library Internal System<br/>(staff accounts)
  S->>W: Open the staff page (FR-04-08)
  W->>B: Check the staff session and role (FR-04-08)
  opt No valid staff session or role
    B-->>W: Deny the request (FR-04-08)
    W-->>S: Show the staff sign-in (FR-04-08)
    loop Until sign-in succeeds or staff stop trying
      S->>W: Sign in with the internal library account (FR-04-07)
      W->>B: Submit the credentials (FR-04-07)
      B->>LIS: Verify the account and the staff role (FR-04-07)
      LIS-->>B: Return the verification result (FR-04-07)
      alt Valid account with the staff role
        B->>B: Start a staff session (FR-04-07)
        B->>B: Write audit entry (actor, action, time) (FR-04-12)
        B-->>W: Open the staff page (FR-04-07)
      else Wrong account or no staff role
        B-->>W: Reject the sign-in (FR-04-18)
        W-->>S: Show an error message (FR-04-18)
      end
    end
  end
  S->>W: Open the reported reviews (FR-02-14)
  W->>B: Get reported reviews (FR-02-14)
  B->>RDB: Read reported reviews (FR-02-14)
  RDB-->>B: Return reported reviews (FR-02-14)
  alt No reported reviews
    B-->>W: Return an empty list (FR-02-19)
    W-->>S: Display that no reported reviews are waiting (FR-02-19)
  else Reported reviews exist
    B-->>W: Return reported reviews (FR-02-14)
    W-->>S: Display the reported-reviews list (FR-02-14)
    loop Each reported review, until none is left or staff stop (AD-UC-13 d5)
      S->>W: Select a reported review (FR-02-10)
      rect rgba(120, 160, 220, 0.12)
        Note over S,B: Staff judgement: the review violates the rules (AD-UC-13 d3, D20)
        S->>W: Choose Remove on the review (FR-02-10)
        W-->>S: Ask to confirm the removal (FR-02-10)
        Note over S,B: Not confirming stops here and nothing changes
        S->>W: Confirm the removal (FR-02-10)
        W->>B: Remove the review (FR-02-10)
        B->>RDB: Remove the review from public display (FR-02-10)
        RDB-->>B: Confirm (FR-02-10)
        B->>B: Write audit entry (actor, action, time) (FR-04-12)
        B-->>W: Confirm (FR-02-10)
        W-->>S: Show review removed (FR-02-10)
      end
      rect rgba(120, 160, 220, 0.12)
        Note over S,B: Staff judgement: the review follows the rules (AD-UC-13 d3)
        S->>W: Dismiss the report (FR-02-20)
        W->>B: Dismiss the report (FR-02-20)
        B->>RDB: Keep the review public, take it off the reported list (FR-02-20)
        RDB-->>B: Confirm (FR-02-20)
        B-->>W: Confirm (FR-02-20)
        W-->>S: Show the updated reported-reviews list (FR-02-20)
      end
    end
  end
  rect rgba(120, 160, 220, 0.12)
    Note over S,B: Staff choice, available on every staff screen (D7)
    S->>W: Choose «Đăng xuất» (FR-04-21)
    W->>B: Close the staff session (FR-04-21)
    B-->>W: Confirm the session is closed (FR-04-21)
    W-->>S: Show the staff sign-in (FR-04-21)
  end
```

## 2. Changes from the original diagram

- Split from the combined UC-14 + UC-13 image (Inputs check 4). Reporting is now in SD-UC-14.
- Opening the reported list now cites FR-02-14 instead of FR-02-10 (Inputs check 7, AD-UC-13 Q4).
- Added staff sign-in with its audit entry (FR-04-07, FR-04-12, D30), the empty list (FR-02-19), dismissing a report (FR-02-20) and sign-out (FR-04-21).
- v2.1 (23/11/2026): staff handle one reported review after another (`loop`, AD-UC-13 d5).
