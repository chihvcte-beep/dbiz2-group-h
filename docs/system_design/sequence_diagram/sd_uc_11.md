# Sequence Diagram: SD-UC-11 Register and sign in (library card with email OTP)

| Field | Value |
|---|---|
| SD ID | SD-UC-11 |
| Use case | UC-11 Register and sign in (library card with email OTP) |
| Feature | F-04 Platform, Access & Operations |
| Primary actor | Reader |
| Participants | Reader · Web App · Backend · Library Internal System |
| Trigger | The reader submits their library card number, directly or from the "Sign in (UC-11)" step of another use case |
| Preconditions | The reader holds a library card whose record in the Library Internal System has an email address. |
| FRs covered | FR-04-01, FR-04-04, FR-04-12, FR-04-16, FR-04-17, FR-04-19 |
| Activity diagram | [AD-UC-11](../../activity_diagram/ad_uc_11.md) |
| Redrawn from | `Library Sign-In OTP Pipeline-2026-10-12-035036.pdf` |
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
  participant LIS as Library Internal System<br/>(reader accounts)
  R->>W: Enter the library card number (FR-04-01)
  W->>B: Request an OTP for the library card (FR-04-01)
  B->>LIS: Look up the card number and email (FR-04-01)
  LIS-->>B: Return the card holder and email, or not found (FR-04-01)
  alt Card not found
    B-->>W: Reject the sign-in (FR-04-01)
    W-->>R: Show an error message (FR-04-01)
  else Card found
    B->>B: Generate a 6-digit OTP, 5 minutes, single use (FR-04-04)
    alt OTP email could not be sent
      B-->>W: Return that the code could not be sent (FR-04-16)
      W-->>R: Display that the code could not be sent (FR-04-16)
    else OTP email sent
      B-)R: Email the OTP to the email declared on the card (FR-04-04)
      B-->>W: Return that the OTP was sent (FR-04-04)
      W-->>R: Show the OTP entry with the full email address (FR-04-04)
      R->>W: Enter the OTP code (FR-04-01)
      W->>B: Verify the card number and OTP (FR-04-04)
      alt OTP correct, not expired, not used
        B->>B: Start a signed-in session (FR-04-01)
        B->>B: Write audit entry (actor, action, time) (FR-04-12)
        B-->>W: Return the signed-in session (FR-04-01)
        W-->>R: Show signed-in state and continue the pending action (FR-04-01)
      else OTP incorrect, fewer than 5 attempts
        B-->>W: Return incorrect code and attempts left (FR-04-17)
        W-->>R: Display that the code is incorrect, the reader may enter it again (FR-04-17)
        W-->>R: Display the number of attempts left (FR-04-19)
      else OTP incorrect, 5th attempt
        B->>B: Invalidate the OTP (FR-04-17)
        B-->>W: Reject the sign-in (FR-04-17)
        W-->>R: Show an error message (FR-04-17)
      else OTP expired or already used
        B-->>W: Reject the sign-in (FR-04-01)
        W-->>R: Show an error message (FR-04-01)
      end
    end
    rect rgba(120, 160, 220, 0.12)
      Note over R,B: Reader's choice at any time on the code screen (AD-UC-11 d6), or after a failed send or a rejected OTP (d5), then back to entering the code
      R->>W: Request a new OTP (FR-04-04)
      W->>B: Request a new OTP (FR-04-04)
      B->>B: Invalidate the previous OTP and generate a new one (FR-04-04)
      B-)R: Email the new OTP (FR-04-04)
    end
  end
```

## 2. Changes from the original diagram

- The image had no FR labels. Every step now cites one FR.
- Added a failed OTP email (FR-04-16), the 5-attempt limit (FR-04-17, FR-04-19) and a new OTP (FR-04-04).
- The full email is shown (D2). The pending action continues after sign-in (D1).
- v2.1 (23/11/2026): the incorrect-code message and the attempts left are two steps, as `s9` and `s13` in AD-UC-11 v1.3.
- v2.2 (23/11/2026): a new OTP can be requested at any time on the code screen (AD-UC-11 v1.4).
