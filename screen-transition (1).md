# Screen Transition Diagram: LabDesk (worked example)

> Worked example for teaching. Not a student submission and not a real product.

## 1. Student

```mermaid
flowchart LR
  entry(["Opens LabDesk"])
  qr(["Scans lab door QR"])
  mail(["Link in email"])
  S00_01["S-F00-01<br>Sign in"]
  S01_01["S-F01-01<br>Slot picker"]
  S01_02["S-F01-02<br>Seat map"]
  S01_03["S-F01-03<br>My bookings"]
  S02_01["S-F02-01<br>Check-in result"]
  entry --> S00_01
  S00_01 -->|"signed in"| S01_01
  S01_01 -->|"picks a slot"| S01_02
  S01_02 -->|"back"| S01_01
  S01_02 -->|"[booking saved] View my bookings"| S01_03
  S01_03 -->|"Book another"| S01_01
  mail --> S01_03
  qr --> S02_01
  S02_01 -->|"View my bookings"| S01_03
```

Main task "book a seat": S-F01-01 → S-F01-02 → success state. Two screens from the start screen.

## 2. Lab Technician

```mermaid
flowchart LR
  entry(["Opens LabDesk"])
  S00_01["S-F00-01<br>Sign in"]
  S03_01["S-F03-01<br>Lab occupancy"]
  S03_02["S-F03-02<br>Seat maintenance"]
  entry --> S00_01
  S00_01 -->|"signed in as technician"| S03_01
  S03_01 -->|"Manage seats"| S03_02
  S03_02 -->|"back"| S03_01
```

## Checks

- Every screen in the Screen List appears: yes (7 of 7).
- Every screen reachable from an entry point: yes.
- No dead ends: yes.
- Usage-flow paths: every arrow of [usage-flow.md](usage-flow.md) has a path (table below).
- Sign in is shared; signed-out users who open an email or QR link see S-F00-01 first and then
  return to the screen they asked for (screen-level rule in S-F00-01).

## Usage-flow paths

| Actor | Usage-flow arrow | Path on this diagram |
|---|---|---|
| Student | UC-01 to UC-03 | S-F01-02 Seat map → S-F01-03 My bookings ("[booking saved] View my bookings") |
| Student | UC-03 to UC-04 | The student leaves LabDesk and walks to the lab; entry point "Scans lab door QR" → S-F02-01 |
| Student | UC-03 to UC-02 | Same screen: S-F01-03 My bookings, modal "Cancel booking?" |
| Lab Technician | UC-07 to UC-06 | S-F03-01 Lab occupancy → S-F03-02 Seat maintenance ("Manage seats") |
| Lab Technician | UC-06 to UC-07 | S-F03-02 Seat maintenance → S-F03-01 Lab occupancy ("back") |

LabDesk has 7 screens, so a single diagram would also work; it keeps one per actor because the two
actors share only the sign-in screen.
