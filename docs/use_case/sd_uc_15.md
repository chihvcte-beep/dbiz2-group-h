# Sequence Diagram: SD-UC-15 Sync data from the library internal system

| Field | Value |
|---|---|
| SD ID | SD-UC-15 |
| Use case | UC-15 Sync data from the library internal system |
| Feature | F-04 Platform, Access & Operations |
| Primary actor | None: started by time (daily sync time) |
| Participants | Backend · Library Internal System · Book database · Reader database |
| Trigger | Time event: the daily sync time is reached (02:00) |
| Preconditions | The connection to the Library Internal System is set up. The digital floor plan exists (FR-01-04). |
| FRs covered | FR-01-05, FR-04-09, FR-04-10, FR-04-11, FR-04-12 |
| Activity diagram | [AD-UC-15](../activity/ad_uc_15.md) |
| Redrawn from | New on 23/11/2026 (no original diagram; D48) |
| Version / status | v1.0 · Draft |

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
  participant B as Backend<br/>(scheduled job)
  participant LIS as Library Internal System<br/>(catalogue, placement, loans)
  participant BDB as Book database<br/>(catalogue, shelf placement,<br/>floors and rooms)
  participant RDB as Reader database<br/>(loan records)
  rect rgba(150, 150, 150, 0.14)
    Note over B,RDB: Automatic: the daily sync time is reached (02:00). No person takes part.
    loop Until the run succeeds or 3 retries are used (FR-04-11)
      B->>LIS: Request the catalogue, shelf codes, floors and rooms (FR-04-09)
      LIS-->>B: Return the data, or an error (FR-04-09)
      alt Data returned
        B->>BDB: Import the catalogue, shelf codes, floors and rooms (FR-04-09)
        B->>LIS: Request the loan records of library card accounts (FR-04-10)
        LIS-->>B: Return the loan records, or an error (FR-04-10)
        alt Loan records returned
          B->>RDB: Import the loan records (FR-04-10)
          B->>B: Report room codes that do not match the floor plan (FR-01-05)
          B->>B: Write audit entry for the sync run (FR-04-12)
        else Error
          B->>B: Keep the last successful data and log the error (FR-04-11)
        end
      else Error
        B->>B: Keep the last successful data and log the error (FR-04-11)
      end
    end
  end
  Note over B,RDB: After a successful run, QR codes for new physical books (SD-UC-10) and history entries from new loans (SD-UC-07) start by themselves
```

## 2. Changes from the original diagram

- New diagram for UC-15, which gives the daily sync its own use case (Inputs check 3, L8-20, D48).
- Nothing is written back to the Library Internal System (W0 Table 4).
